### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:15-alpine3.21
# COMPLETAR
```
docker run -d -name postgresCont -e POSTGRES_USER=domeP -e POSTGRES_PASSWORD=admin postgres:15-alpine3.21
```
<img width="715" height="230" alt="image" src="https://github.com/user-attachments/assets/b48c3cbb-e5b5-4343-bd7f-41ebc08099c9" />

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
```
docker run -d --name pgAdmin -p 8080:80 -e PGADMIN_DEFAULT_EMAIL=admin@mail.com -e PGADMIN_DEFAULT_PASSWORD=admin dpage/pgadmin4
```
<img width="803" height="38" alt="image" src="https://github.com/user-attachments/assets/044a9a24-9bf6-4018-9915-a40665599529" />

# COMPLETAR

La figura presenta el esquema creado en donde los puertos son:
- a: 8080
- b: 80
- c: 5432

![Imagen](esquema-2-ejercicio.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
# COMPLETAR CON UNA CAPTURA DEL LOGIN
<img width="942" height="516" alt="image" src="https://github.com/user-attachments/assets/36843c54-fd11-4c06-95aa-dad7be1339de" />

Antes de ingresar al servidor se utiliza 
```
docker network create netPostgres
docker network connect netPostgres postgresCont
docker network connect netPostgres pgAdmin
```
<img width="950" height="477" alt="image" src="https://github.com/user-attachments/assets/25753568-c119-4ed0-b2f3-2e1ffa071a06" />

### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

<img width="940" height="465" alt="image" src="https://github.com/user-attachments/assets/16a3882d-cc67-422d-9400-cf8627812e83" />

Se ejecuta el siguiente Query para crear la tabla e insertar datos. 
```
CREATE DATABASE info;
CREATE TABLE personas (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(50)
);
INSERT INTO personas (nombre) VALUES ('Dome Cardenas');
INSERT INTO personas (nombre) VALUES ('Zoro Roronoa'); 
```

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
```
docker exec -it postgresCont psql -U domeP
```
<img width="373" height="82" alt="image" src="https://github.com/user-attachments/assets/c9faa156-1f40-4520-945e-10e8f4b43f90" />

# COMPLETAR
### Realizar un select *from personas
# AGREGAR UNA CAPTURA DE PANTALLA DEL RESULTADO
<img width="340" height="86" alt="image" src="https://github.com/user-attachments/assets/d455b2b0-3e47-4ea9-b9bf-005ae5711606" />
