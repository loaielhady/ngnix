# Customizing Access Log Format


## Steps:



### Step 1 :  Pick cutomizing the log format


```
log_format custom_format '$remote_addr - $remote_user [$time_local] '
                         '"$request" $status $body_bytes_sent '
                         '"$http_referer" "$http_user_agent" '
                         '"Request Time: $request_time"';
```



### Step 2 : Define where path do you want to save your new access log file

```
	access_log /home/loai/Desktop/custom_access.log custom_format;
```

### Step 3 :

#### cutomizing erorr log with one of this level : 

`warn` `info` `emerg` `erorr`

```

error_log /Your/Path/custom_error.log warn;
```








