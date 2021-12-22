# Useful configs

## Http response

* add_header  
Set header for the response, eg: Content-Type, Cache-Control, etc

## Compression

### Compress

* gzip: whether gzip resource or not
* gzip_types: the resource type to gzip (application/html by default)
* gzip_min_length: minimal length to be zipped
* gzip_proxied: how to save the gzip files

```
  gzip on;
  gzip_types      text/plain application/xml;
  gzip_proxied    no-cache no-store private expired auth;
  gzip_min_length 1000;
```

### Serving

* gzip_static: serving gzip version of static content if possible

### Decompress

* gunzip: decompress resources or not