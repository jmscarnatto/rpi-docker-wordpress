www:
  image: arm32v7/wordpress
  container_name: sitename
  restart: always
  expose:
    - "80"
    - "443"
  volumes:
    - ./:/var/www/html:rw
  environment:
    - VIRTUAL_HOST=sub.domain.com, www.sub.domain.com
    - LETSENCRYPT_HOST=sub.domain.com, www.sub.domain.com
    - LETSENCRYPT_EMAIL=domain@gmail.com
    - WORDPRESS_DB_HOST=db
    - WORDPRESS_DB_USER=root
    - WORDPRESS_DB_PASSWORD=examplepass
    - WORDPRESS_DB_NAME=wordpress
  links:
    - db:db

db:
  image: hypriot/rpi-mysql
  container_name: db
  restart: always
  volumes:
    - /home/pi/www/databases/sitename:/var/lib/mysql
  environment:
    - MYSQL_ROOT_PASSWORD=examplepass
    - MYSQL_DATABASE=wordpress
