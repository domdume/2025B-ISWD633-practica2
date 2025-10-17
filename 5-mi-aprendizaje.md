
## Aprendizaje

Antes de realizar la práctica entendía el concepto de contenedor, pero no tenía una comprensión de cómo gestionarlos en la práctica. Desconocía cómo se debían configurar o cómo manejaban persistencia y configuraciones como contraseñas y diferentes datos sensibles. Después de completar los diferentes ejercicios, los principales aprendizajes que obtuve fue:
- Configuración dinámica mediante variables de entorno: En lugar de tener una imagen para cada configuración, se utiliza una imagen genérica (como mysql:8 o postgres) y se personaliza su arranque con variables de entorno. Esto es fundamental para la seguridad (al no "quemar" contraseñas en la imagen) y la flexibilidad.
- Aislamiento y comunicación controlada: Al principio, no era obvio por qué los contenedores no se veían entre sí. La práctica con WordPress y MySQL me enseñó que, por defecto, los contenedores están completamente aislados. Para que puedan comunicarse, deben ser conectados explícitamente a una red virtual personalizada (docker network create).
- Importancia de Logs: uando un contenedor fallaba y se detenía inmediatamente (como en el caso de MySQL sin la contraseña de root), mi primer instinto era no saber qué hacer. El uso de docker logs <nombre_contenedor> sirvió como herramienta de diagnóstico, ya que me mostraba el mensaje de error exacto que ocurría dentro del contenedor, permitiéndome entender y solucionar el problema.

## Errores
Durante la práctica para levantar un sitio de WordPress contectado a una base de datos MYSQL, me encontré con un error "Error establishing a database connection" en el navegador. Tras crear los contenedores mysql3 y worldpress3 y conectarlos a la misma red (net3), la aplicación de WordPress no lograba conectarse a la base de datos, a pesar de que ambos contenedores estaban en ejecución.La causa raíz fue que, si bien el contenedor de la base de datos se creó, nunca se le instruyó que creara la base de datos específica (wordpress) ni el usuario (wpuser) que la aplicación WordPress esperaba encontrar. Por lo tanto, WordPress intentaba iniciar sesión con credenciales que no existían.La solución fue eliminar los contenedores y recrear el contenedor de MySQL añadiendo las variables de entorno necesarias para que, durante su primer arranque, inicializara la base de datos y el usuario requeridos por WordPress.

```
C:\Windows\System32>docker run --name mysql3 -e MSQL_ROOT_PASSWORD=mysql -d mysql:8
Unable to find image 'mysql:8' locally
8: Pulling from library/mysql
69718387e824: Pull complete
f56ec30544fc: Pull complete
a49b4bec6f69: Pull complete
d3dc946e9b73: Pull complete
46d5b31c795a: Pull complete
7a99a8dca35c: Pull complete
8389b884d3d6: Pull complete
970f697f30e8: Pull complete
35a745903ff9: Pull complete
Digest: sha256:5367102acfefeaa47eb0eb57c8d4f8b96c8c14004859131eac9bbfaa62f81e34
Status: Downloaded newer image for mysql:8
b712ff041e11b031ca0c5e4d647476aefb50da527cb9a2970c2d630616f7d559

C:\Windows\System32>docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS             PORTS     NAMES
21dc8d77e6dc   nginx:alpine   "/docker-entrypoint.…"   About an hour ago   Up About an hour             ngnixRed

```
## Docker Secrets
Docker Secrets es la forma nativa y segura de gestionar datos confidenciales, como contraseñas, tokens o claves de API, en un entorno de contenedores orquestado con Docker Swarm. En lugar de exponer esta información sensible en variables de entorno o archivos de configuración, los "secretos" se almacenan de forma cifrada en el gestor del cluster (Swarm manager) y solo se entregan a los contenedores que han recibido permiso explícito para acceder a ellos. Una vez dentro del contenedor, el secreto se monta como un archivo en una ubicación de memoria temporal (/run/secrets), lo que evita que se escriba en el disco del contenedor y reduce drásticamente el riesgo de exposición.
