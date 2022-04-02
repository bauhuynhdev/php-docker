# Includes
```text
- Nginx: 1.20.2
- PHP: 7.4.x
- Composer: 2.2.9
- Node: 14.x
- Supervisor: 4.2.4
```
# Open ports
```text
- 80
- 443
- 9000
```
# Volumes
```text
- /app
- /etc/php.ini
- /etc/supervisord.conf
- /etc/supervisord.d/nginx.ini
- /etc/supervisord.d/php-fpm.ini
- /etc/nginx/nginx.conf
- /etc/php-fpm.d/www.conf
- /etc/nginx/conf.d/default.conf
```
# Virtual host
```apacheconf
server {
    listen 80;
    listen [::]:80;
    server_name 127.0.0.1;
    root /app;

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```