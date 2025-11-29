



```
sudo mkdir /etc/nginx/ssl

```


```

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt

```


```

"Common Name (e.g. server FQDN or YOUR name)"

```



```

server {
        listen 80 default_server;
        listen 443 ssl;

        root /your/path/to/html;
        index index.html index.html;

        server_name your_domain.com;
        ssl_certificate /etc/nginx/ssl/nginx.crt;
        ssl_certificate_key /etc/nginx/ssl/nginx.key;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
