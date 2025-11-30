
### 1. Create a private key and a self-signed certificate using OpenSSL

```

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048
-keyout /etc/nginx/ssl/nginx.key
-out /etc/nginx/ssl/nginx.crt

```
### 2. Make sure to type in :


"Common Name (e.g. server FQDN or YOUR name)" type: `localhost`


### 3. Configure Nginx to use these generated files.
You will need to modify your Nginx configuration file, typically located at `/etc/nginx/sites-available/default`

```

server {
        listen 80 default_server;
        listen 443 ssl;

        root /your/path/to/html;
        index index.html index.html;

        server_name your_domain.com;
        ssl_certificate /path/to/your/certificate.crt;
        ssl_certificate_key /path/to/your/private.key;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

Replace `/path/to/your/certificate.crt` and `/path/to/your/private.key` with the actual paths where you saved your generated certificate and private key.


## 4. Reload Nginx:
After making changes to the Nginx configuration, reload the Nginx service for the changes to take effect.

```
sudo nginx -s reload
```

