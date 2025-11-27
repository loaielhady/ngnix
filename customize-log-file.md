



```
error_log /home/loai/Desktop/custom_error.log warn;
````

```
	access_log /home/loai/Desktop/custom_access.log custom_format;
```

```
log_format custom_format '$remote_addr - $remote_user [$time_local] '
                              '"$request" $status $body_bytes_sent '
    			      '"$http_referer" "$http_user_agent" '
   '"Request Time: $request_time"';
	```
