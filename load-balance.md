```
upstream backend_app {
	server 127.0.0.1:7001 weight=2;
  server 127.0.0.1:7002; 
}
```



```
server {
	listen 80;
	server_name localhost;

	root /var/www/html;

	index index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {

	    proxy_pass http://backend_app;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		try_files $uri $uri/ =404;
	}
}
```
