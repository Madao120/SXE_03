### 1. Descarga la imagen de Alpine sin arrancarla y comprueba que la tienes. Fija la versión: no uses latest. Escoge una versión, de las disponibles en docker hub.

La forma de realizar esto es con:
docker pull alpine:3.24.2

![imagen alpine:3.34.2](/capturas/1.png)

### 2. Crea un contenedor sin nombre y sin arrancarlo. ¿En qué estado queda? ¿Qué nombre le ha puesto Docker?
![imagen de contenedor creado](/capturas/2.png)
Como se ve en la imagen, responderemos a las preguntas.
Estado: Created
Nombre: "eager_brattain"

### 3. Crea y arranca dam_alp1 con una shell. ¿Qué opciones necesitas para poder escribir dentro?
Para crear y arrancar usamos docker run.<br>
Según los requisitos del ejercicio, usaremos:
--name para asignarle dam_alp1.
-it para interactuar directamente con una shell.

(Me di cuenta al final de que este paso no hacía falta)Y al final introduciremos <b> /bin/sh</b> que es el intérprete de comandos de alpine.

![imagen contenedor dam_alp1](/capturas/3.png)


### 4. Desde dentro, mira qué IP tiene y si puede hacer ping a google.com.
Para mirar la ip haremos <b>ip a</b> o <b>ip addr</b>
Para hacer ping a google bastará con hacer <b>ping google.com</b>
![imagen contenedor dam_alp1_funcionando](/capturas/4.png)

### 5. Deja dam_alp1 funcionando sin pararlo y crea dam_alp2 igual. Con los dos en marcha, haz ping de uno a otro: por IP y por nombre. Explica cada resultado.
###### Aclaración: 
###### Salí del contenedor principal, dam_alp1
Por lo que para volver a entrar haremos: **docker start -ai dam_alp1**
-a para hacer "attach", entrando al proceso principal. 
-i para "interactive".

Mostraremos como comprobamos la ip y haremos ping entre ellos.

#### Por ip
![img con ping ip](/capturas/5.1.png)
Vemos que funciona correctamente.

#### Por nombre de contenedor
![img con ping nombre](/capturas/5.2.png)
Esta vez no funciona, ya que los contenedores se pueden conectar por ip, pero el nombre de los contenedores no tiene que ver con su network, por lo que no se conocen entre ellos por el nombre, solo por la ip.

### Tampoco funciona con Hostnames
![img con ping nombre](/capturas/5.2(con_hostnames).png)

### 6. Con los dos en marcha, averigua cuánta memoria consumen. ¿Hay un comando de Docker para eso?
SI que hay un comando de Docker para ver cuanta memoria consumen ls docker activos.
Es **docker stats**

Pero no solo mira memoria, si no que también mira el nombre, porcentaje de CPU, límite de memoria, etc.
![img comprobar memoria dockers activos](/capturas/6.png)

Memoria usada por cada contenedor:
dam_alp1 = 520KiB
dam_alp2 = 524KiB

### 7. Sal con exit. ¿Qué les ha pasado? Repite el comando anterior: ¿qué ves ahora y por qué?
![docker stats sin contenedores activos](/capturas/7.png)
Ahora no se ven datos al hacer **docker stats**, esto debido a que **NO hay ningun contenedor activo**, ya que dentro de estos contenedores hicimos exit.

Esto último se puede hacer con otra comprobación, usando docker ps observaremos los docker activos, y con docker ps -a TODOS, aunque estén parados.

![docker stats sin contenedores activos](/capturas/7.1(no%20necesario).png)
Aquí observamos que los contenedores no están activos pero siguen existiendo.


### 8. ¿Cuánto disco has ocupado? Distingue imágenes de contenedores.
#### Aclaración: Para este paso borré los contenedores e imágenes que tenía antes de empezar el ejercicio.
Para comprobar esto, debemos de hacer **docker system df**
![docker system df comprobante de discos](/capturas/8.png)

Aquí veremos que tenemos 1 imagen, la de alpine:3.34.2 <br>
Y 3 contenedores, que son los dos dam_alp (1 y 2) a demás del contenedor de alpine que creamos sin nombre en el ejercicio 2.

Espacio de disco Imágenes:      8.422 MB <br>
Espacio de disco Contenedores:  274B




