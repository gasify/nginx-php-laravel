# Introduction
This image is to dockerizing Laravel application in an easy way, build the Laravel app with nginx & PHP FPM in a single container. Just copy your Laravel project files and set some environment up, and voila your app is ready to use. But you can use this image to do another PHP project instead of using Laravel as your main framework.

# Version
| Tag | Nginx Version | PHP Version | Composer Version | Alpine Version |
| --- | --- | --- | --- | --- |
| latest | 1.22.1 | 8.1.14 | 2.5.1 | 3.17.1 |
| 8.1 | 1.22.1 | 8.1.14 | 2.5.1 | 3.17.1 |

# Build image from source
To build this image from Dockerfile, you could clone the repository and build it with your own customization. This repository is entirely open-source.
```bash
git clone https://github.com/galeka99/nginx-php-laravel
```
```bash
cd nginx-php-laravel
```

# Pull from Docker Hub
You could also pull this image from Docker Hub by execute this command:
```bash
docker pull galeka/nginx-php-laravel
```

# Run the container
To run this image, you can use 2 different methods. First using `docker run` command, or using a `docker compose`, choose wisely.

Using `docker run`:
```bash
sudo docker run -d galeka/nginx-php-laravel:latest
```
or using a `docker compose` instead:
  
**FILE: `Dockerfile`**
```Dockerfile
FROM galeka/nginx-php-laravel:latest

WORKDIR /var/www/html
COPY . /var/www/html
```
  
**FILE: `docker-compose.yml`**
```yaml
version: '3.7'

services:
    laravel:
        build:
            context: .
            dockerfile: Dockerfile
        container_name: laravel
        restart: unless-stopped
        working_dir: /var/www/html
        environment:
            - APP_NAME=Laravel
            - APP_ENV=production
            - APP_DEBUG=false
            - DB_CONNECTION=mysql
            - DB_HOST=172.17.0.1
            - DB_PORT=3306
            - DB_DATABASE=laravel
            - DB_USERNAME=root
            - DB_PASSWORD=root
        ports:
            - 8080:80
```

# Notes
- Default directory: `/var/www/html`
- Nginx root directory: `/var/www/html/public`
- Nginx default config: `/etc/nginx/nginx.conf`
- Nginx default host: `/etc/nginx/modules/nginx-laravel.conf`
- PHP default config: `/etc/php81/php.ini`
- PHP FPM default config: `/etc/php81/php-fpm.conf`