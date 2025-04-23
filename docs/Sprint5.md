# Sprint 5

## Monitorización y rendimiento

Podemos monitorizar y ver el rendimeinto de nuestro ordenador por herramientas graficas como por ejemplo Monitor del Sistema

![Sprint5](Imagenes/Sprint5/1.png)

![Sprint5](Imagenes/Sprint5/2.png)

![Sprint5](Imagenes/Sprint5/3.png)

Tambien tenemos un apartado importante que son los Log’s.

¿Que es un Log?

Un log es un archivo que registra eventos que ocurren en un sistema operativo o software. Estos registros son útiles para diagnosticar problemas, realizar auditorías y monitorear el rendimiento del sistema.

En Ubuntu tenemos mucha cantidad de Log’s y se encuentran en ```/var/log```

![Sprint5](Imagenes/Sprint5/4.png)

Podemos ver la configuración de estos logs en el documento ```/etc/logrotate.conf```

![Sprint5](Imagenes/Sprint5/5.png)

También está el ```/etc/logrotate.d``` que sirve para personalizar en especifico una a una de las configuraciones de los logs.

![Sprint5](Imagenes/Sprint5/6.png)

En el archivo ```/etc/rsyslog.d/50-default.conf``` servirá para indicar los logs que queremos que se guarden y donde queremos que se guarden.

![Sprint5](Imagenes/Sprint5/7.png)

Haremos las pruebas teniendo 2 terminales abiertas, una teniendo un tail de syslog para ver lo que pasa en todo momento.

![Sprint5](Imagenes/Sprint5/8.png)

Y en otra terminal iremos haciendo las pruebas como por ejemplo de mail

![Sprint5](Imagenes/Sprint5/9.png)

Podemos comprobar que sale en el tail

![Sprint5](Imagenes/Sprint5/10.png)

Y comprobamos que tambien se han hecho en el documento de la configuración

![Sprint5](Imagenes/Sprint5/11.png)

Editamos la configuracion de esta manera y volvemos a hacer la misma prueba.

![Sprint5](Imagenes/Sprint5/12.png)

Ahora volvems a hacer la misma prueba de la misma manera y comprobamos que solo nos sale esa alerta. 

![Sprint5](Imagenes/Sprint5/13.png)

Ahora hacemos un nuevo log en 50-default.conf para dividir los que mas nos interesan en un archivo nuevo.

![Sprint5](Imagenes/Sprint5/14.png)

Reiniciamos el servicio

![Sprint5](Imagenes/Sprint5/15.png)

Le hacemos la prueba poniendo una de las terminales con el tail de syslog para comprobar que salta el error, y en la otra terminal hacemos un logger para que salte un error critico.

![Sprint5](Imagenes/Sprint5/16.png)

Y comprobamos que vaya al archivo que le hemos indicado.

![Sprint5](Imagenes/Sprint5/17.png)

Para que nos salgan en el tail de syslog esta clase de errores tenemos que modificar esta linea del 50-default.conf y dejarla unicamente con “ * ”

![Sprint5](Imagenes/Sprint5/18.png)

Tenemos también comandos para ver los avisos que han saltado en el servicio por ejemplo para ver los críticos. Utilizaremos “journalctl”

![Sprint5](Imagenes/Sprint5/19.png)

Journalctl tambien puede filtrar alertas de los usuarios, podemos de un usuario en concreto utilizando el “UID” del usuario

![Sprint5](Imagenes/Sprint5/20.png)

O para ver usuarios en general se hara con –user

![Sprint5](Imagenes/Sprint5/21.png)

journalctl entre fechas:

#### 1. Filtrar entre dos fechas específicas

```journalctl --since "2025-03-10 12:00:00" --until "2025-03-12 18:30:00"```

![Sprint5](Imagenes/Sprint5/25.png)

#### 2. Filtrar desde una fecha en adelante

```journalctl --since "2025-03-10"```

![Sprint5](Imagenes/Sprint5/22.png)

#### 3. Filtrar hasta una fecha específica

```journalctl --until "2025-03-12"```

![Sprint5](Imagenes/Sprint5/23.png)

#### 4. Filtrar usando tiempos relativos

```journalctl --since "1 day ago"```

![Sprint5](Imagenes/Sprint5/24.png)

## Auditorias

**¿Que es Lynis?**

Lynis es un escáner de seguridad de código abierto que se usa para:
Evaluar la seguridad del sistema.


Detectar configuraciones débiles o incorrectas.


Recomendar mejoras para proteger mejor un servidor o equipo Linux.


Fue diseñado para administradores de sistemas, auditores y profesionales de seguridad.

Instalamos Lynis ejecutando el siguiente comando

![Sprint5](Imagenes/Sprint5/38.png)

Y con un simple comando como es ```lynis audit system``` podriamos tener toda la informacion de la maquina.

![Sprint5](Imagenes/Sprint5/39.png)

Podemos ver diferentes parametros del sistema

![Sprint5](Imagenes/Sprint5/40.png)

![Sprint5](Imagenes/Sprint5/41.png)

![Sprint5](Imagenes/Sprint5/42.png)

![Sprint5](Imagenes/Sprint5/43.png)

![Sprint5](Imagenes/Sprint5/44.png)

![Sprint5](Imagenes/Sprint5/45.png)

Tambien hay opciones para hacerlo de manera mas estructurada y que no nos salga toda la informacion directamente, sino que podemos filtrar por categorias con el comadando. ```lynis audit system --tests-from-category "kernel"```, de esta manera nos saldra unicamente la informacion necesaria del equipo y la categoria que nosotros hemos especificado

![Sprint5](Imagenes/Sprint5/46.png)

![Sprint5](Imagenes/Sprint5/47.png)

![Sprint5](Imagenes/Sprint5/48.png)


## Servidor de actualizaciones

**¿Que es?**

Un servidor de actualizaciones es un sistema que gestiona y distribuye actualizaciones de software a otros equipos en una red.

**¿Para qué sirve?**

Sirve para centralizar la gestión de actualizaciones, asegurando que todos los equipos de la red reciban las actualizaciones necesarias de manera eficiente y oportuna, mejorando la seguridad y el rendimiento del sistema.

Instalaremos el paquete Apache2 para poder comenzar con el servidor.

![Sprint5](Imagenes/Sprint5/26.png)

También descargamos el paquete apt-mirror

![Sprint5](Imagenes/Sprint5/27.png)

Abriremos el archivo ```/etc/apt/mirror.list``` para indicar el repositorio que se tendran que bajar los clientes, comentaremos todas las lineas para que no se descarguen los GB innecesarios que no queremos ahora mismo y añadiremos nuestra propia linea con lo que queremos que se descargue

![Sprint5](Imagenes/Sprint5/28.png)

Para descargar el repositorio en nuestro equipo colocamos la comanda ```apt-mirror```

![Sprint5](Imagenes/Sprint5/29.png)

Creamos un soft-link y comprobamos el interior de la carpeta indicada.

![Sprint5](Imagenes/Sprint5/30.png)

En el cliente modificamos este archivo para que coga el repositorio del servidor 

![Sprint5](Imagenes/Sprint5/31.png)

Ejecutamos el sigueinte comando

![Sprint5](Imagenes/Sprint5/32.png)

![Sprint5](Imagenes/Sprint5/33.png)

Creamos un soft link entre donde hemos añadido el repositorio de chrome al servidor apache que hemos instalado.

![Sprint5](Imagenes/Sprint5/34.png)

Ahora en el CLIENTE

Firmamos con google chrome

![Sprint5](Imagenes/Sprint5/35.png)

Añadimos el repositorio de Google Chrome pero esta vez desde nuestro servidor.
En el directorio ```/etc/apt/``` editamos el fichero ```sources.list``` y añadimos el servidor y el paquete.

![Sprint5](Imagenes/Sprint5/36.png)

Ahora al hacer un apt update deberia salirnos el servidor con el repositorio de Google Chrome.

![Sprint5](Imagenes/Sprint5/37.png)

