# nginx-simple-loadbalancer

docker-compose.yaml
```yaml
version: "3"
services:
  nginx:
    image: nginx:1.15-alpine  
    volumes:
      - ./conf:/etc/nginx/conf.d
    ports:
      - 8585:8585
```

conf/default.conf
```text
upstream bankservers {
    server 172.17.0.1:6565;
    server 172.17.0.1:7575;
}
 
server {
 
    listen 8585 http2;
 
    location / {
       grpc_pass grpc://bankservers;
    }
   
}

```
