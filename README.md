# Empty-example

### nginx config example

```
server {
  listen 80;
  server_name empty-example.loc;
  root /path-to/empty-example/dist;

  charset utf-8;

  client_max_body_size 4G;
  keepalive_timeout 10;

  location / {
    try_files $uri $uri/ /index.php?$args;
    index index.php index.html;
  }

  location ~ .php$ {
  include fastcgi_params;
  fastcgi_intercept_errors on;
  fastcgi_pass 127.0.0.1:9000;
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  fastcgi_index index.php;
  fastcgi_read_timeout 1m;
  fastcgi_buffers 16 16k;
  fastcgi_buffer_size 32k;
  }

  error_log /path-to/empty-example/project_error.log error;
}
```
