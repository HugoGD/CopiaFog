# Sprint 3

## Instalacion dominio LDAP

Utilizaremos “xarxa NAT” para que nuestra IP sea fijo independientemente de mi ubicacion.

![ipa](Imagenes/Sprint3/ipa.png)

La colocamos estática para corroborar que no cambiara.

![CapRed](Imagenes/Sprint3/confredç.png)

Comprobamos la IP para ver que realmente sigue todo igual

![IpaComprobacion](Imagenes/Sprint3/ipacomprobacion.png)

Le hacemos un ping a 8.8.8.8 para comprobar que tenemos acceso a internet.

![conectividad8.8.8.8](Imagenes/Sprint3/conectividad.png)

Comprobamos el hostname de nuestro equipo con el archivo ```/etc/hostname```

![etc/hostname](Imagenes/Sprint3/hostname.png)

Añadimos un host nuevo para el dominio en el archivo ```/etc/hosts``` y en caso de haber modificado el hostname lo cambiamos donde salía el antiguo

![etchosts](Imagenes/Sprint3/etchosts.png)

Después de este paso reiniciamos la máquina utilizando ```reboot``` para que se aplique todo correctamente.

Para comprobar que todo se a aplicado correctamente comprobamos que  sale el nuevo hostname.

![hugoubuntu](Imagenes/Sprint3/hugoubuntu.png)

Instalamos los paquetes **slapd** (Dominio) y el paquete **ldap-utils** (comandos para modificar el dominio).

![instalar_paquetes](Imagenes/Sprint3/instalarpaquetes.png)


Añadimos la contraseña.

![contra](Imagenes/Sprint3/contra.png)

Confirmamos la contraseña nuevamente.

![confcontra](Imagenes/Sprint3/confcontra.png)

Comprobamos con el comando ```slapcat``` que se nos han creado los objetos basicos.

![slapcat](Imagenes/Sprint3/slapcat.png)

Para crear el dominio básico (esquema) con el nombre de la organización y usuario admin tenemos 2 opciones, podemos ejecutar los archivos que nos hemos descargado del moodle o podremos utilizar el comando ```dpkg-reconfigure slapd```.

![dpkg](Imagenes/Sprint3/dpkg-reconfigur.png)

Colocaremos el nombre del dominio que tiene que ser el mismo que colocamos en ```etc/hosts```.

![nodomain](Imagenes/Sprint3/nodomain.png)

Colocamos el nombre  de la organización, puede ser diferente.

![slapdhugo](Imagenes/Sprint3/slapdhugo.png)

Nos pide configurar nuevamente la contraseña.

![contraseña](Imagenes/Sprint3/slapdcontra.png)

Repetimos nuevamente la contraseña.

![repcont](Imagenes/Sprint3/repcontr.png)

Le damos que si a las dos ultimas opciones que nos salen.


![si1](Imagenes/Sprint3/si1.png)

![si](Imagenes/Sprint3/si2.png)

Ahora si volvemos a hacer el comando ```slapcat``` veremos que los objetos saldrán modificados con lo que hemos colocado en la anterior configuración.

![slapcat](Imagenes/Sprint3/slapcattt.png)

Modificamos el archivo ```uo.ldif``` que nos hemos descargado y lo configuramos con el dominio que configuramos anteriormente.

![uoldif](Imagenes/Sprint3/uoldiff.png)

Ahora se hará lo mismo con el apartado de “grupos” en el archivo ```grup.ldif```, tambien modificamos en caso de que se haya cambiado el nombre de unidad organizativa al correspondiente y creamos el primer miembro del grupo en este caso “alu1” y en el apartado “cn=” le damos nombre al grupo que estamos creando en este caso alumnes.

![grupldif](Imagenes/Sprint3/grupldif.png)

Ahora hacemos lo mismo pero con el archivo de los usuarios ```usu.ldif```, en este caso únicamente modificamos el apartado del dominio, el resto es para crear el usuario y los parámetros del mismo.

![usu.ldif](Imagenes/Sprint3/usu.ldif.png)

**IMPORTANTE!** El nombre de todos los archivos que se acaba de modificar no es importante, lo que es importante es que su extensión siempre sea .ldif

Aqui subimos con el comando ```ldapadd -c -x -D “cn=admin,dc=gallardo,dc=com” -W -f (archivo)``` los archivos .ldif que hemos modificado en la configuracion

![comandotolargo](Imagenes/Sprint3/comandotolargo.png)

Ahora si hacemos un slapcat saldra toda la configuracion nueva subida

![conffinal](Imagenes/Sprint3/configuracionfinal.png)






## Gestion del dominio

Comprobamos que tenemos completamente vacía la base de datos antes de comenzar con la práctica usando ```slapcat```.

![slapcat](Imagenes/Sprint3/slapcat2.png)

Importamos la nueva base de datos del nuevo documento .ldif con el comando ```ldapadd -x -D “cn=admin,dc=gallardo,dc=com” -W -f dades.ldif```.

![ldapadd](Imagenes/Sprint3/ldapadd.png)

Haremos la prueba para eliminar uno de los usuarios que tenemos dentro utilizare un documento para eliminarlo, una vez el documento este creado utilizare el comando ```ldapmodify -x -D “cn=admin,dc=gallardo,dc=com” -W -f uo.ldif```.

![ldapmodify](Imagenes/Sprint3/ldapmodify.png)

Me gusta utilizar más este método ya que te dice al 100% si se ha eliminado en el mismo comando, con el otro comando no te dice absolutamente nada y tienes que ir a comprobarlo. Pero tambien se podria utilizar ```ldapdelete -x -D “cn=admin,dc=gallardo,dc=com” -W “uid=trigden,ou=People,dc=gallardo,dc=com``` para eliminar. 

Si queremos modificar o añadir algun apartado de algun usuario que tengamos tendremos que utilizar el mismo comando de ```ldapmodify``` pero tendremos que cambiar el archivo de texto.

![archivodetextomodify](Imagenes/Sprint3/archivodetextomodify.png)

Ahora para ejecutar la modificacion tendremos que poner el comando con sudo en la terminal ```ldapmodify -x -D "cn=admin,dc=gallardo,dc=com" -W -f nombre_del_archivo```.

![ejecucion](Imagenes/Sprint3/ejecucion.png)

Ahora podremo eliminar tambien este mismo atributo que hemos añadido cambiando la parte final de "add" a "delete"

![eliminacion](Imagenes/Sprint3/eliminacion.png)

![eliminacion2](Imagenes/Sprint3/eliminacion2.png)

## Entornos Graficos

Empezamos buscando apache directoy en google que es lo que utilizare como entorno grafico.

![apache1](Imagenes/Sprint3/apache1.png)

Instalamos el paquete default-jre para que nos deje ejecutar el archivo.

![apache](Imagenes/Sprint3/apache2.png)

Ahora podremos ejecutar lo que hemos instalado de google

![apache](Imagenes/Sprint3/apache3.png)

Vamos a poner una nueva conexion en LDAP Apache Directory

![apache](Imagenes/Sprint3/apache4.png)

Configuramos los apartados que nos pida

![apache](Imagenes/Sprint3/apache5.png)

![apache](Imagenes/Sprint3/apache6.png)

Una vez acabamos la configuracion que nos pide podremos ver como ya estamos dentro de nuestra conexion LDAP.

![apache](Imagenes/Sprint3/apache7.png)

Podemos comprobar que si abrimos los desplegables saldran los usuarios que tenemos nosotros ya creados etc...

![apache](Imagenes/Sprint3/apache8.png)

Vamos a crear un nuevo usuario para poder comprobar que funciona todo coorectamente asi que le daremos click derecho a la barra de la izquierda y seleccionaremos New Entry

![apache](Imagenes/Sprint3/apache9.png)

Añadimos un nuevo usuario

![apache](Imagenes/Sprint3/apache10.png)

Comenzamos a llenar la configuracion del usuario

![apache](Imagenes/Sprint3/rectificado.png)

![apache](Imagenes/Sprint3/apache12.png)
## Unir equipos al dominio

### Comprobaciones Previas:

Tenemos que comprobar que están en la misma red tanto cliente como servidor ya que sino todo lo que hagamos no servirá de absolutamente nada.

Hacemos un “ip a” para comprobar la IP de la maquina cliente y comprobamos que este en el mismo rango que el servidor.

**IP CLIENTE**

![ipclient](Imagenes/Sprint3/IP%20CLIENTE.png)

**IP SERVIDOR**

![ipserver](Imagenes/Sprint3/ip%20server.png)

En mi caso la IP se duplica, cosa que no iba a funcionar, para solucionarlo la he puesto de manera manual en el cliente.

![interficie](Imagenes/Sprint3/interficie.png)

Una vez las tengamos correctas comprobamos con un PING de cliente -> servidor y de servidor -> cliente para ver que si tenemos conectividad

**CLIENTE -> SERVIDOR**

![ping](Imagenes/Sprint3/ping%20CS.png)

**SERVIDOR -> CLIENTE**

![ping2](Imagenes/Sprint3/ping%20SC.png)

Tendremos que instalar estos 3 paquetes (libnss-ldap | libpam-ldap | nscd)

En primer paso haremos un ```apt update``` para actualizar repositorios, después utilizaremos el comando ```apt install libnss-ldap libpam-ldap nscd```

![descargacap](Imagenes/Sprint3/descargacap.png)

Comenzará un asistente para instalar los paquetes que acabamos de mencionar, tendremos que darle al ESC ignorando la configuración inicial y colocaremos el comando ```dpkg-reconfigure ldap-auth-config``` para comenzar con la instalación desde 0 ya que haciendolo asi nos saldran mas opciones que de manera default.

![dpkgreconf](Imagenes/Sprint3/dpkgconfigure.png)

Le damos a que si ya que queremos reconfigurarlo todo desde cero 

![si3](Imagenes/Sprint3/si3.png)

En este primer paso tendremos que corregir lo que sale predeterminado ```ldapi:///``` y tendremos que colocar lo siguiente ```ldap://IP_Server```.

![ipldap](Imagenes/Sprint3/IPnuevaaqui.png)

Cambiamos las opciones del dominio y colocamos en el servidor

![confdominio](Imagenes/Sprint3/confodominio.png)

Escogemos la version nº3

![version](Imagenes/Sprint3/version.png)

Le damos a que SI a las dos siguientes opciones

![si4](Imagenes/Sprint3/si4.png)

![si5](Imagenes/Sprint3/si5.png)

Colocamos mas configuraciones que ya se hizo previamente en el dominio del servidor del usuario con privilegios

![authconf](Imagenes/Sprint3/authconf.png)

Elegimos el sistema de encriptación MD5

![md5](Imagenes/Sprint3/md5.png)

Modificamos este archivo para que cuando vaya a buscar un archivo no pase por los archivos ya que esta en el servidor.

**ANTES:**

![antes](Imagenes/Sprint3/ante.png)

**DESPUES:**

![despues](Imagenes/Sprint3/despues.png)




## Servidor SAMBA

### Introduccion SAMBA

**¿Qué es SAMBA?**

Samba es una implementación libre del protocolo de archivos compartidos de Microsoft Windows (SMB/CIFS) para sistemas Unix y Linux. Permite que los sistemas Unix y Linux actúen como servidores de archivos e impresoras en redes mixtas, facilitando la interoperabilidad entre sistemas operativos diferentes. Con Samba, los usuarios pueden compartir archivos, impresoras y otros recursos en una red de manera transparente, como si estuvieran utilizando un servidor Windows.

### Instalacion y configuracion Server

Para comenzar con la instalación de samba instalaremos el paquete principal “samba” con el comando ```apt install samba```

![aptinstallsamba](Imagenes/Sprint3/aptinstallsamba.png)

Para iniciar con la prueba de que el servidor vaya a funcionar correctamente para compartir una carpeta tendremos que crear la carpeta en este caso “proves”, cambiaremos los permisos de esa carpeta con ```chmod -R 777 proves``` y le cambiaremos el propietario con ```chown nobody:nogroup```, también en el interior crearemos un archivo de texto llamado hola.

![permisos](Imagenes/Sprint3/permisos.png)

Uno de los archivos a tener en cuenta que de momento no tocaremos pero se tiene que saber es el archivo ```smb.conf``` situado en la carpeta ```/etc/samba/smb.conf```, en este caso lo único que añadiremos es un nuevo repositorio compartido.

![smn.conf](Imagenes/Sprint3/smb.conf.png)

**¿Que se puede hacer con smb.conf?**

El archivo ```smb.conf``` es la configuración principal de Samba, y controla cómo se comporta el servidor SMB. Se encuentra normalmente en ```/etc/samba/smb.conf``` (en Linux) y permite definir qué carpetas se comparten, qué permisos tienen los usuarios, la autenticación y otras opciones avanzadas.

Ahora reiniciamos los dos servicios para que se apliquen correctamente los cambios

![systemctlrestart](Imagenes/Sprint3/systemctlrestart.png)

Ahora crearemos usuarios para que puedan acceder al servidor samba pero que no sean logeables en el equipo. Crearemos también el usuario Roig y Groc para poder hacer pruebas añadiendoles al grupo colors.

![useradd](Imagenes/Sprint3/useradd.png)

También crearemos el grup “colors” y añadiremos a Roig y Groc

![grupo](Imagenes/Sprint3/colors.png)

Hacemos la comprobación para que se corrobore que está todo creado correctamente.

![tail-5](Imagenes/Sprint3/tail-5.png)

Ahora le añadimos una contraseña a los usuarios en samba para poder usarlos. De esta manera los añadimos al servicio de SAMBA

![smb1](Imagenes/Sprint3/smb1.png)

### Instalación y pruebas cliente

Para empezar a trabajar con el ciente instalamos el paquete "smbclient" con el comando ```apt install smbclient```

![smb2](Imagenes/Sprint3/smb2.png)

Para poder conectarse abrimos una pestaña de archivos -> Otras ubicaciones y añadimos “smb://IP/Repositorio”

![smb3](Imagenes/Sprint3/smb4.png)

![smb5](Imagenes/Sprint3/smb5.png)

Al conectarnos como anonimo no nos tendria que dejar escribir, vamos a hacer la comprobacion.

![smb6](Imagenes/Sprint3/smb6.png)

No nos ha dejado así que haremos otra prueba cambiando los parámetros del servidor

![smb7](Imagenes/Sprint3/smb7.png)

Reiniciamos los servicios para que se apliquen los cambios.

![smb8](Imagenes/Sprint3/smb8.png)

Ahora si nos dejara crear carpetas en el interior de la carpeta de samba desde el cliente.

![smb9](Imagenes/Sprint3/smb9.png)

Comprobamos desde el servidor que se vea el interior de la carpeta samba actualizado

![smb10](Imagenes/Sprint3/smb10.png)

Ahora haremos la misma prueba pero entrando con un usuario

![smb11](Imagenes/Sprint3/smb11.png)

Comprobamos que tiene permisos como indicamos en los parámetros de smb.conf

![smb12](Imagenes/Sprint3/smb12.png)

Y comprobamos quién es el propietario de la carpeta desde el servidor.

![smb13](Imagenes/Sprint3/smb13.png)

Ahora haremos la misma comprobación desde uno de los usuarios que no tiene permisos.

![smb14](Imagenes/Sprint3/smb14.png)

Comprobamos que no se puede crear una carpeta porque no tiene permisos.

![smb15](Imagenes/Sprint3/smb15.png)

Ahora haremos la misma comprobación con el usuario Roig y en teoría no nos tendría que dejar ni entrar.

![smb16](Imagenes/Sprint3/smb16.png)

Ahora nos devolvera al apartado de usuario porque no funcionara

![smb17](Imagenes/Sprint3/smb17.png)


## Servidor NFS

**¿Que es NFS?**
NFS (Network File System) es un protocolo de sistema de archivos distribuido que permite a los dispositivos compartir archivos y directorios a través de una red, como si estuvieran en el mismo sistema. Fue desarrollado por Sun Microsystems en los años 80 y es ampliamente utilizado en entornos UNIX y Linux.

**¿En que es diferente de SAMBA?**
Samba y NFS tienen un propósito similar (compartir archivos en red), pero difieren en su funcionamiento y compatibilidad:

![tabla](Imagenes/Sprint3/comparativa.png)

### Instalación parte servidor

Hacemos un apt update para que se actualicen todos los directorios para instalar los programas con la ultima version:

![update](Imagenes/Sprint3/update.png)

Instalamos el paquete del NFS:

![NFS](Imagenes/Sprint3/NFS.png)

Comprobamos el status del nfs para comprobar que se a instalado correctamente con el comando ```systemctl status nfs-server```

![status](Imagenes/Sprint3/status.png)

Una vez hecho esto el servidor ya está preparado para utilizar el servicio nfs

### Instalación parte cliente ubuntu

Hacemos un update para actualizar los repositorios nuevamente

![updateclient](Imagenes/Sprint3/updateclt.png)

Instalamos el nfs-common y rpcbind con el comando ```apt install nfs-common rpcbind```

![paquetes](Imagenes/Sprint3/paquetes.png)

### Instalación parte cliente windows

Para la parte de Windows abrimos el panel de control

![part1windows](Imagenes/Sprint3/part1windows.png)

Le damos a la opcion de **Programes y caracteristiques**

![part2windows](Imagenes/Sprint3/part2windows.png)

Y en la parte de la izquierda le damos a la opción de “Activa o desactiva les caractéristiques de windows”, en esta opción buscamos la opción de Servicio NFS y activamos ambas opciones expandiendo la carpeta.

![part3windwos](Imagenes/Sprint3/part3windows.png)

### Compartición carpeta al server y pruebas 

Creamos la carpeta que vayamos a compartir

![compartida](Imagenes/Sprint3/compartida1.png)

Le quitamos de ningún grupo a la carpeta y le añadimos permisos a todos los usuarios

![compartida2](Imagenes/Sprint3/compartida2.png)

Para compartir la carpeta tendremos que ir al documento ```/etc/exports``` y añadir la siguiente linea:

![compartida3](Imagenes/Sprint3/compartida3.png)

Para que funcione correctamente reiniciamos el servicio:

![compartida4](Imagenes/Sprint3/compartida4.png)

Ahora creamos un fichero de texto dentro de la carpeta para comprobar que se ve en los clientes y verdaderamente se ha compartido.

![compartida5](Imagenes/Sprint3/compartida5.png)

![compartida6](Imagenes/Sprint3/compartida6.png)

Para comprobar los permisos del cliente Windows probamos a crear algo.

![compartida7](Imagenes/Sprint3/compartida7.png)

Ahora vamos al servidor para comprobar que se a creado correctamente y miramos el usuario.

![compartida8](Imagenes/Sprint3/compartida8.png)

Creamos una carpeta en /mnt llamada nfs que es donde montaremos el punto de montaje con ```mkdir nfs```.

Creamos un punto de montaje de la carpeta compartida en el cliente de ubuntu.

![Compartida9](Imagenes/Sprint3/compartida9.png)

Creamos y comprobamos el interior de la carpeta para ver que realmente si que funciona

![Compartida10](Imagenes/Sprint3/compartida10.png)

Lo comprobamos desde el servidor

![Compartida11](Imagenes/Sprint3/compartida11.png)

## Perfil Movil (Ubuntu LDAP)

**¿Que es un Perfil Movil?**

Un perfil móvil es un tipo de perfil de usuario que se almacena en un servidor central y se carga en cualquier equipo al que el usuario inicie sesión. Esto permite que los usuarios tengan un entorno de trabajo consistente y sus configuraciones personales disponibles en cualquier equipo de la red.

Creamos en la raiz ```/``` la carpeta perfils con ```mkdir perfils```

![pfmovil1](Imagenes/Sprint3/pfmovil1.png)

Al ser una carpeta compartida para tener los perfiles en cualquier ordenador tendremos que modificar ```/etc/exports``` para compartirla.

![pfmovil2](Imagenes/Sprint3/pfmovil2.png)

Reiniciamos el servicio nuevamente para que funcione correctamente 

![pfmovil3](Imagenes/Sprint3/pfmovil3.png)

Cuando vayamos a crear el nuevo usuario dentro del servidor tendremos que modificar el Home Directory para que su home este compartida en todos los pc’s

![pfmovil4](Imagenes/Sprint3/pfmovil4.png)

Creamos el nuevo usuario

![pfmovil5](Imagenes/Sprint3/pfmovil5.png)

En la carpeta de clientes creamos la carpeta de perils

![pfmovil6](Imagenes/Sprint3/pfmovil6.png)

Para que no se pierdan los mount crearemos una compartición en el archivo “/etc/fstab” del cliente ubuntu para mantener siempre los usuarios.

![pfmovil7](Imagenes/Sprint3/pfmovil7.png)

Ahora reiniciamos la máquina y comprobamos que podamos acceder con el usuario alu2

![pfmovil8](Imagenes/Sprint3/pfmovil8.png)

![pfmovil](Imagenes/Sprint3/perfilmovil9.png)

![pfmovil](Imagenes/Sprint3/pfmovil9.png)