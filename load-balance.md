# Load balance overview ![01 cara-setting-load-balancing-dengan-nginx_diagram-load-balancing](https://github.com/user-attachments/assets/25d572d1-b8a4-435a-a3ae-6b3cb33e9104)


* #### Load balancing across multiple application instances is a commonly used technique for optimizing resource utilization, maximizing throughput, reducing latency

## Load balance algorithm: 
| Algorithm |Behavior |
| :----------- | :------: |
| `weight`     | directing higher or lower number of incoming requests to specific backend servers |
| `round-robin` |Default — rotates through all backends equally  |
| `least_conn`  |Sends traffic to the backend with the fewest active connections|
| `ip_hash`    | Server routing is determined by hashing the client's IP address|

## Basic configuration:

### 1. Edit  
```
sudo nano /etc/nginx/sites-available/default
```

```
upstream backend_app {
	server 127.0.0.1:7001;
  server 127.0.0.1:7002; 
}
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

## Demo two local backend servers

* ### Create server A & B

1. server_a.js
```
const http = require('http');
http.createServer((req, res) => {
  res.end('This signal from server A');
}).listen(7001);

```

2. server_b.js

```
const http = require('http');
http.createServer((req, res) => {
  res.end('This signal from server B');
}).listen(7002);
```
* ### Run two servers
```
node server_a.js &
node server_b.js &
```
* ### Reload Nginx
```
sudo systemctl reload nginx
```
✅ you've done 


* ### Using `weight`
 to influence the load balancing algorithms, directing a proportionally higher or lower number of incoming requests to specific backend servers
 
```
upstream backend_app {
    
	server 127.0.0.1:7001 weight=3;
  server 127.0.0.1:7002 weight=1; 
}

```








* ### Using `least_conn`
```
upstream backend_app {
    least_conn;
	server 127.0.0.1:7001;
  server 127.0.0.1:7002; 
}

```

* ### Using `Ip_hash`
```
upstream backend_app {
    ip_hash;
	server 127.0.0.1:7001;
  server 127.0.0.1:7002; 
}

```



