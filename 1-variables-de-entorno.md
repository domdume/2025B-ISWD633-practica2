# Variables de Entorno
### ¿Qué son las variables de entorno?
# COMPLETAR
Una variable de entorno es un valor con un nombre que se almacena fuera de un programa y que influye en su comportamiento. 
### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

# COMPLETAR
```
docker run -d --name entornoV -e username=dome -e role=admin nginx:alpine
```
<img width="381" height="29" alt="image" src="https://github.com/user-attachments/assets/cb08e0a7-bc62-4620-bbf8-fbbac1daff82" />

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR
```
docker inspect entornoV
```
<img width="319" height="83" alt="image" src="https://github.com/user-attachments/assets/73497aae-1a2e-440c-b7e1-8242e60677e4" />

### Crear un contenedor con la imagen de mysql, mapear todos los puertos
# COMPLETAR
```
docker run -d --name mysqlContenedor -P mysql
```
### ¿El contenedor se está ejecutando?
# COMPLETAR

<img width="335" height="133" alt="image" src="https://github.com/user-attachments/assets/b05e7f79-e3ce-4ddf-bead-74c631f4edc4" />

### Identificar el problema
# COMPLETAR
La imagen oficial de MySQL requiere obligatoriamente que se establezca una contraseña para el usuario root al momento de la creación. Al no ser proporcionado, el contenedor se inició, pero detecta que falta la configuración de seguridad y se apaga para evitar dejar una base de datos vulnerable.

### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

### ¿Qué bases de datos existen en el contenedor creado?
# COMPLETAR
Primero se crea el contenedor, esta vez estableciendo la contraseña y variables de entorno necesarias. 
```
docker run -d --name mysqlContenedor -e MYSQL_ROOT_PASSWORD=bddome -p 3306:3306 mysql:latest
```
<img width="646" height="43" alt="image" src="https://github.com/user-attachments/assets/5ae071ee-8d04-406f-8811-f8660f33b6e8" />

Para listar las bases de datos existentes se utiliza exec

```
docker exec -it msqlContenedor bash
mysql -u root -p
```

<img width="467" height="332" alt="image" src="https://github.com/user-attachments/assets/9264cc1a-bfef-4208-ac10-924031b75869" />

Las bases existentes fueron 
1. information_schema
2. mysql
3. performance_schema
4. sys
