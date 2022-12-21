# Adminer

- Cree una carpeta Adminer
- Cree  el documento.yml


version: '3.1'

services:

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

  db:
    image: mysql:5.6
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
- Desde el terminal fui a la carpeta Adminer
- Utilece el comando docker compose up -d en el terminal
- Luego lo abri en el navegador
- El interior del yml lo saque de aqui https://hub.docker.com/_/adminer

# Apache

- Cree una carpeta Apache
- Elimine todos los contenedores e imagenes que ya tenia porque daba error
- Cree  el documento.yml
version: '3.1'
services:
  apache:
    image: httpd:latest
    ports:
    - '8080:80'
    volumes:
    - ./:/var/www/html

- Desde el terminal fui a la carpeta Apache
- El interior del yml lo saque de aqui https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Simple-Apache-docker-compose-example-with-Dockers-   httpd-image
- Cambie la ruta del volumen
- Utilece el comando docker compose up -d en el terminal
- Luego lo abri en el navegador

# Guestbook

- Cree una carpeta Guestbook
- Cree  el documento.yml
version: '3.1'
services:
  app:
    container_name: guestbook
    image: iesgn/guestbook
    restart: always
    ports:
      - 80:5000
  db:
    container_name: redis
    image: redis
    restart: always
- Desde el terminal fui a la carpeta Guestbook
- Utilece el comando docker compose up -d en el terminal
- Luego lo abri en el navegador
- El interior del yml lo saque de aqui https://josedom24.github.io/curso_docker_2022/sesion4/guestbook.html

# Mediawiki

- Cree una carpeta Mediawiki
- Cree  el documento.yml
#MediaWiki with MariaDB
#Access via "http://localhost:8080"
#(or "http://$(docker-machine ip):8080" if using docker-machine)
version: '3'
services:
  mediawiki:
    image: mediawiki
    restart: always
    ports:
      - 8080:80
    links:
      - database
    volumes:
      - images:/var/www/html/images
      - ./LocalSettings.php:/var/www/html/LocalSettings.php
      #After initial setup, download LocalSettings.php to the same directory as
      #this yaml and uncomment the following line and use compose to restart
      #the mediawiki service
         
  #This key also defines the name of the database host used during setup instead of the default "localhost"
  database:
    image: mariadb
    restart: always
    environment:
      # @see https://phabricator.wikimedia.org/source/mediawiki/browse/master/includes/DefaultSettings.php
      MYSQL_DATABASE: my_wiki
      MYSQL_USER: wikiuser
      MYSQL_PASSWORD: example
      MYSQL_RANDOM_ROOT_PASSWORD: 'yes'
    volumes:
      - db:/var/lib/mysql

volumes:
  images:
  db:
- Desde el terminal fui a la carpeta Mediawiki
- Utilece el comando docker compose up -d en el terminal
- Luego lo abri en el navegador
- Meti los datos 
- Le di continuar a todo
- Descargue el documento LocalSettings.php
- Guarde el documento LocalSettings en la carpeta 
- Me meti en el documento yml y descomente la linea - ./LocalSettings.php:/var/www/html/LocalSettings.php
- Utilece el comando docker compose up -d en el terminal de nuevo
- Volvia abrir el navegador
- El interior del yml lo saque de aqui https://hub.docker.com/_/mediawiki

# Wordpress

- Cree una carpeta Wordpress
- Cree  el documento.yml
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
- Desde el terminal fui a la carpeta Wordpress
- Utilece el comando docker compose up -d en el terminal
- Luego lo abri en el navegador
- El interior del yml lo saque de aqui https://hub.docker.com/_/wordpress
