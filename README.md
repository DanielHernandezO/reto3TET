
# Configuracion reto 3
Para completarlo vamos a seguir paso a paso la configuracion de las maquinas.


## DB

para la base de datos se creo una imagen en docker hub usando mysql, la imagen se puede descargar usando el siguiente comando:

```sudo docker pull dahernando/mysql:v1.0```

esta imagen crea una imagen por defecto en la cual se crea una base de datos y las credenciales para conectarse. 

## NFS

Para configurar el NFS que se debe instalar, en la maquina nfs se instala el servidor usando el comando 
 - instalar el nfs server ```sudo apt-get update && sudo apt install nfs-kernel-server ```
 
 - Luego se crea la carpeta que se va a compartir usando (al final del comando se indica el path)
    ```sudo mkdir -p ```
 - Luego se asignan los permisos a la carpeta creada (al final del comando se indica el path)
    ```sudo chown nobody:nogroup ``` & ```sudo chmod 777```
-  Por ultimos e crea la configuracion en el archivo /etc/exports con la carpeta creada indicando que se va a compartir, para esto se sigue la siguiente estructura ```PATH IP:MASK(rw,no_subtree_check,no_root_squas)``` donde se debe remplazar PATH por el que se creo, IP por las IPs que estaran permitidas en para usar esa carpeta y la mascara de la IP.

En caso de querer montar la imagen usando el cliente se debe seguir los siguientes pasos:
- instalar el cliente ```sudo apt-get install nfs-common``` 
- Crear la carpeta donde se van a guardar los archivos ```sudo mkdir -p ```
- Montar la el server ```sudo mount SERVER_IP:PATH_SERVER PATH_LOCAL```

## Wordpress
para configurar el wordpress se debe correr usando ```sudo docker compose up -d``` el archivo docker-compose.yml en la carptea wordpress. **NOTA:** Llenar correctamente las variables de entorno de acuerdo a lo configurado en el NFS y la base de datos

## NGINX
Para configurar el NGNX se debe pedir la certificacion HTTPS y crear una carpeta llamada ssl dentro de nginx donde almacenara todas las keys de la certificacion, luego se debe actualizar el backend en nginx.conf con las IPs de los servidores y por ultimo se debe correr el archivo docker compose usando
```sudo docker compose up -d```