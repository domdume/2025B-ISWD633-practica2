## Esquema para el ejercicio
![Imagen](esquema-4-ejercicio.PNG)

### Crear la red
# COMPLETAR
```
docker network create net3
docker network ls
```
<img width="500" height="150" alt="image" src="https://github.com/user-attachments/assets/43cd238b-4f07-48bd-a7c1-0c47f072ce6f" />

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
# COMPLETAR

```
docker run -d --name mysql3 --network net3 -e MYSQL_ROOT_PASSWORD=wordpress -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wordpress mysql:8
```

<img width="500" height="150" alt="image" src="https://github.com/user-attachments/assets/1b491102-17c7-4304-86a9-30fb70bfe7ff" />


### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
# COMPLETAR
```
docker run -d --name worldpress3 --network net3 -p 9300:80 -e WORDPRESS_DB_HOST=mysql3 -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wordpress wordpress
```

De acuerdo con el trabajo realizado, en el esquema del ejercicio el puerto a es **9300**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
# COLOCAR UNA CAPTURA DE LA CONFIGURACIÓN

<img width="923" height="446" alt="image" src="https://github.com/user-attachments/assets/af6911f6-aa28-46db-8003-e39596ab4d5e" />

<img width="841" height="515" alt="image" src="https://github.com/user-attachments/assets/66f5e806-d65f-4d32-81c4-aaa483c61e78" />

Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
# COLOCAR UNA CAPTURA DEL SITO EN DONDE SEA VISIBLE LA PUBLICACIÓN.

<img width="937" height="524" alt="image" src="https://github.com/user-attachments/assets/a5514de8-1f3f-462e-ac1f-543174667961" />

### Eliminar el contenedor wordpress
# COMPLETAR
```
docker stop wordlpress3
docker rm worldpress3
```
<img width="500" height="120" alt="image" src="https://github.com/user-attachments/assets/8de951d9-ef29-4eb1-8eb9-7a72155fa6c2" />

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

```
docker run -d --name worldpress3 --network net3 -p 9300:80 -e WORDPRESS_DB_HOST=mysql3 -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wordpress wordpress
```

### ¿Qué ha sucedido, qué puede observar?
# COMPLETAR

Aunque el contenedor haya sido eliminado, el contenido de wordpress sigue configurado, esto se debe a que la base de datos guardaba la información del anterior contenedor. 

<img width="941" height="520" alt="image" src="https://github.com/user-attachments/assets/01fd9549-3856-41a4-ad1f-ecfe09be7cd8" />

