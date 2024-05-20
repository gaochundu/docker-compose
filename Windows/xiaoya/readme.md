# 如何设置xiaoya的docker

> https://xiaoyaliu.notion.site/xiaoya-docker-69404af849504fa5bcf9f2dd5ecaa75f#8647f4096f494a9c89a9bb5295c37a18



要获得最新小雅的资讯请关注小雅的tg频道 https://t.me/xiaoyaliu

平时有什么使用上遇到的困难可以来这里找我或其他人帮助 https://t.me/PlutoPlayer





[小雅的分类](https://alist.xiaoya.pro/) Alist 是一个基于 Alist 搭建的阿里云盘聚合站，资源极为丰富，分类细致。同时提供 docker 镜像，可以快速搭建自己的镜像站。

# 1、安装

## 1.1、创建文件夹

```

mkdir /etc/xiaoya/mytoken.txt
mkdir /etc/xiaoya/myopentoken.txt
mkdir /etc/xiaoya/temp_transfer_folder_id.txt
```

> 文件对应的值查看 [官方文档](https://xiaoyaliu.notion.site/xiaoya-docker-69404af849504fa5bcf9f2dd5ecaa75f) 填写

## 1.2、拉取最新镜像

```

docker pull xiaoyaliu/alist:latest
```

## 1.3、创建

```

docker run -d -p 5678:80 -p 2345:2345 -p 2346:2346 -v /etc/xiaoya:/data --restart=always --name=xiaoya xiaoyaliu/alist:latest
```

# 2、配置 `Nginx`

## 2.1、生成证书

```

certbot certonly --dns-cloudflare --dns-cloudflare-credentials ~/.secrets/certbot/cloudflare.ini -d alist.ysbzcn.com --email 'email@ysbzcn.com'
```

## 2.2、将域名解析到服务器，利用 `Nginx` 代理请求 `127.0.0.1:5678`

```


upstream alist {
  server 127.0.0.1:5678;
}

#HTTP 重定向到 HTTPS

server {
    listen 80;
    listen [::]:80;
    server_name alist.ysbzcn.com;

    if ($host = alist.ysbzcn.com) {
        return 301 https://$host$request_uri;
    }
    return 404;
}

server {

    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name alist.ysbzcn.com; #你的域名，已经解析到服务器ip

  #HTTP 重定向到 HTTPS
    # if ($ssl_protocol = "") { return 301 https://$host$request_uri; }

  #判断 $host 如果不是设置好的域名，就返回403页面，可以禁止 IP 访问 Web。
    if ($host !~ (alist.ysbzcn.com)$){
      return 403;
   }

  # IP 访问跳转至域名，将域名替换成自己的。就是判断 $host 如果不是域名结尾的，就重定向至该域名。
  #   if ($host !~ (ysbzcn.com)$){
  #     rewrite ^ https://ysbzcn.com$request_uri?;
  #  }

  # IP 访问跳转至域名，将 IP 和域名替换成自己的。判断是 IP 的，就重定向。
  #   if ($host ~ 192.168.1.1){
  #   rewrite ^ https://www.yourdomain.com$request_uri?;
  #  }


  #证书位置
    ssl_certificate      /etc/letsencrypt/live/alist.ysbzcn.com/fullchain.pem; 
    ssl_certificate_key  /etc/letsencrypt/live/alist.ysbzcn.com/privkey.pem;

  #证书配置
    ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3;  #安全链接可选的加密协议
    ssl_ciphers TLS13-AES-256-GCM-SHA384:TLS13-CHACHA20-POLY1305-SHA256:TLS13-AES-128-GCM-SHA256:TLS13-AES-128-CCM-8-SHA256:TLS13-AES-128-CCM-SHA256:EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5;  #加密算法
    ssl_prefer_server_ciphers on;  #表示优先使用服务端加密套件。默认开启
    ssl_session_timeout 10m;  #缓存有效期
    ssl_session_cache builtin:1000 shared:SSL:10m;
    ssl_buffer_size 1400;
    add_header Strict-Transport-Security max-age=15768000;
    ssl_stapling on;
    ssl_stapling_verify on;

    client_max_body_size 525m;

  #Nginx 默认的 client_max_body_size 配置大小为 1m，可能会导致你在 Halo 后台上传文件被 Nginx 限制，
  #所以此示例配置文件加上了 client_max_body_size 1024m; 这行配置。当然，1024m 可根据你的需要自行修改

  #日志
    access_log   /var/log/nginx/nginx.alist.access.log;
    error_log    /var/log/nginx/nginx.alist.error.log;

  #反代设置开始#
  location / {
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header Range $http_range;
	  proxy_set_header If-Range $http_if_range;
    proxy_redirect off;
    proxy_pass http://alist;
    # the max size of file to upload
    client_max_body_size 20000m;
  }
  #反代设置结束#

}
```

## 2.3、验证并重载 `nginx` 配置

```
PLAINTEXT
nginx -t
PLAINTEXT
nginx -s reload
```

## 2.4、如何定时和网站同步数据

- 终端执行

```

crontab -e
```

- 添加一条记录

```

0 6 * * * docker restart xiaoya
```

就是每天凌晨6点自动重启 xiaoya docker 去同步数据，你把6改成13，那就是下午1点。

# 3、更新

## 3.1、停止并移除旧容器

```

docker stop xiaoya && docker rm xiaoya
```

## 3.2、拉取最新镜像

```

docker pull xiaoyaliu/alist:latest
```

## 3.3、重新安装

```

docker run -d -p 5678:80 -p 2345:2345 -p 2346:2346 -v /etc/xiaoya:/data --restart=always --name=xiaoya xiaoyaliu/alist:latest
```

# 4、设置

对照 [官方文档](https://xiaoyaliu.notion.site/xiaoya-docker-69404af849504fa5bcf9f2dd5ecaa75f) 进行设置。