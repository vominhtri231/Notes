# Request processing

## Server selection

```conf
  server {
    listen      80;
    server_name example.org www.example.org;
    ...
  }

  server {
    listen      192.168.1.2:80;
    server_name example.net www.example.net;
    ...
  }
```

Nginx will first select the server that process the request base on the address/port, then by the `Host` header of the request again the `server_name`.  

If there are no matching `Host`, the default server that match address/port (set explicitly by `default_server` or the first one)

## Location selection

```conf
  location / {
    index  index.html index.php;
  }

  location ~* \.(gif|jpg|png)$ {
    ...
  }

  location ~ \.php$ {
    ...
  }
```

 Nginx will chose the **most specific** prefix location.
