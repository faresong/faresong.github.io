---
key: openssl-self-signed-ecc
title: OpenSSL 快速生成自签署 ECC 证书
tags: TLS
---

```bash
openssl ecparam -name prime256v1 -out ec.pem
openssl req -x509 -sha256 -nodes -days 365 -newkey ec:ec.pem -keyout app.key -out app.crt
```

## 参考

<https://github.com/ljskr/ssl_tool>