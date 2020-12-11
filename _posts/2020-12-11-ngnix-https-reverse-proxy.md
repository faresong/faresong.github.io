---
key: ngnix-https-reverse-proxy
title: Ngnix 使用 HTTPS 反向代理(转发) HTTP 协议
tags: TLS
---

自签证书生成参考 [OpenSSL 快速生成自签署 ECC 证书](/2020/12/11/openssl-self-signed-ecc.html)

nginx.conf 示例

```conf
worker_processes  1;

events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    gzip  on;
	
	# 监听 3002 端口，转发至本地地址 3001 端口
	server {
		listen 3002 ssl;
		server_name 192.168.0.174;		# 主机名
		ssl_certificate app.crt;		# 证书路径
		ssl_certificate_key app.key;		# 私钥路径
		location / {
			proxy_pass http://127.0.0.1:3001;
		}
		
	}

    # 默认示例
    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

