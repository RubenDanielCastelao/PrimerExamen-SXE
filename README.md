# EXAMEN DOCKER XSE

---

### Crear archivo de docker-compose

Usando el IDE que se quiera, en este caso PHPStorm
(siendo otra opción Visual Studio), creamos un nuevo proyecto
en el que crearemos un archivo .yml

En mi caso examenxse.yml.

### Configuración del Docker Compose

Dentro del docker-compose, crearemos 2 containers:

#### Prestashop:

Primero declararemos el container de prestashop, 
este es la configuración:

```
prestashop:
container_name: prestashop
image: prestashop/prestashop:latest
restart: unless-stopped
depends_on:
- mysql
ports:
- 8080:8080
environment:
DB_SERVER: some-mysql
DB_NAME: prestashop
DB_USER: root
DB_PASSWD: admin
PS_INSTALL_AUTO: 1
PS_DOMAIN: localhost:8080
networks:
- prestashop_network
```

Siendo:

 - container_name: El nombre del contenedor
 - image: La imagen de prestashop que usaremos
 - restart: Cuando se reiniciara el container
 - depends_on: La base de datos que usaremos
 - ports: El puerto en el que se hosteara el servicio de prestashop
 - enviroment: Son propiedades varias de prestashop, usuario, contraseña, etc....
 - networks: La network usada para conectar prestashop con su db

#### Mysql

Ahora declararemos el container mysql que sera usado por prestashop,
este es la configuración:

```
  mysql:
    container_name: some-mysql
    image: mysql:5.7
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: admin
      MYSQL_DATABASE: prestashop
    networks:
      - prestashop_network
```