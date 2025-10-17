# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 
![Imagen](redes.PNG)
- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de loopback y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create <nombre red> -d bridge
```

<img width="500" height="100" alt="image" src="https://github.com/user-attachments/assets/fe7473c1-36d7-4203-8acb-488bd85944f3" />

### Crear un contenedor vinculado a una red

```
docker run -d --name <nombre contenedor> --network <nombre red> <nombre imagen>
```

<img width="500" height="120" alt="image" src="https://github.com/user-attachments/assets/ba46f708-57cb-4a0e-a5bd-444a10ab792e" />

### Para saber a qué red está conectado un contenedor

```
docker inspect <nombre contenedor>
```
<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/fd02985e-907d-4a06-90c9-3740dbad505f" />

ó
```
docker network inspect <nombre red> 
```


### Vincular contenedor a una red
```
docker network connect <nombre red> <nombre contenedor>
```
<img width="500" height="98" alt="image" src="https://github.com/user-attachments/assets/eeb0abb2-eca0-4443-b655-0c68b8e3b763" />

### Para desvincular un contenedor de una red
```
docker network disconnect <nombre red> <nombre contenedor>
```
```
docker network disconnect redPrueba ngnixRed
```
<img width="500" height="50" alt="image" src="https://github.com/user-attachments/assets/ad01eda1-1c68-4bcd-b5f6-8f2ebb24f980" />

### Para listar las redes existentes
```
docker network ls
```

<img width="500" height="200" alt="image" src="https://github.com/user-attachments/assets/81b950e9-102f-4575-a6d6-f1e0eb2f54bb" />

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine

![Imagen](esquema-ejercicio-redes.PNG)

# COLOCAR UNA CAPTURA DE LAS REDES EXISTENTES CREADAS

# COLOCAR UNA(S) CAPTURAS(S) DE LOS CONTENEDORES CREADOS EN DONDE SE EVIDENCIE A QUÉ RED ESTÁN VINCULADOS

### Para eliminar las redes creadas
```
docker network rm <nombre de la red>
```
<img width="400" height="90" alt="image" src="https://github.com/user-attachments/assets/c85cd3f7-b6ef-42f4-a33f-cb19cd8e697c" />


