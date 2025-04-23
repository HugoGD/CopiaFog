# Sprint 4

## Raid's

**Que es un RAID:**
RAID (Redundant Array of Independent Disks) es una tecnología de almacenamiento que combina múltiples discos duros en una sola unidad lógica para mejorar el rendimiento y la redundancia.

**Tipos de RAID:**
- RAID 0: Distribución de datos sin redundancia.
- RAID 1: Espejado de discos para redundancia.
- RAID 5: Distribución de datos y paridad.
- RAID 6: Distribución de datos y doble paridad.
- RAID 10: Combinación de RAID 1 y RAID 0.

**Que funcion tienen todos los RAID:**
Todos los RAID tienen la función de mejorar el rendimiento, la redundancia y la disponibilidad de los datos.

**Que es un Volum?**
Un volumen es una unidad lógica de almacenamiento creada a partir de uno o más discos físicos.

## RAID 1

Hacemos un Update para actualizar los repositorios y descargar la última versión

![Sprint4](Imagenes/Sprint%204/Sp4.1.png)

Ahora instalamos el paquete que necesitaremos para poder comenzar a trabajar con los RAID

![Sprint4](Imagenes/Sprint%204/sp4.2.png)

Hacemos un ```fdisk -l``` para poder ver los discos 

![Sprint4](Imagenes/Sprint%204/sp4.3.png)

Entramos dentro del disco

![Sprint4](Imagenes/Sprint%204/sp4.4.png)

Cambiamos el sistema de fitxeros para poder hacerlo de ambos discos.

![Sprint4](Imagenes/Sprint%204/sp4.5.png)

![Sprint4](Imagenes/Sprint%204/sp4.6.png)

Ahora hacemos un ```fdisk -l``` para comprobar que salen de esta manera los discos que hemos cambiado.

![Sprint4](Imagenes/Sprint%204/sp4.7.png)

Creamos la carpeta donde se hara el raid y le entregamos todos los permisos.

![Sprint4](Imagenes/Sprint%204/sprint4.8.png)

![Sprint4](Imagenes/Sprint%204/sp4.9.png)

Ahora crearemos el RAID con el siguiente comando

```mdadm –create /dev/md0 –level=1 –raid-devices=2 /dev/sdb1 /dev/sdc1```

![Sprint4](Imagenes/Sprint%204/sp4.10.png)

Le cambiamos el formato para poder utilizarlo

![Sprint4](Imagenes/Sprint%204/sp4.11.png)

Para recibir información de raid utilizaremos ```mdadm –detail /dev/md0```

![Sprint4](Imagenes/Sprint%204/sp4.12.png)

Ahora haremos que el ```–detail –scan``` se vaya a una carpeta en un .txt que nosotros le indicaremos 

![Sprint4](Imagenes/Sprint%204/sp4.13.png)

Ahora haremos que el raid se monte automáticamente yendo al archivo ```/etc/mdadm.conf``` y añadimos la siguiente línea

![Sprint4](Imagenes/Sprint%204/sp4.14.png)

Y añadiremos también una línea en el archivo ```/etc/fstab```

![Sprint4](Imagenes/Sprint%204/sp4.15.png)

### **<span style="color:red">IMPORTANTE!</span>** 

Antes de hacer el reboot tendremos que poner las siguientes comandas

![Sprint4](Imagenes/Sprint%204/sp4.16.png)

Una vez se haya iniciado nuevamente la máquina para comprobar que todo ha funcionado correctamente haremos un detail ```mdadm –detail /dev/md0```

![Sprint4](Imagenes/Sprint%204/sp4.17.png)

Ahora para hacer las pruebas crearemos una carpeta y un archivo dentro

![Sprint4](Imagenes/Sprint%204/sp4.18.png)

Ahora haremos fallar uno de los discos para comprobar que pasa ```mdadm /dev/md0 -f /dev/sdb1```

![Sprint4](Imagenes/Sprint%204/sp4.19.png)

Tendría que salir asi en un detail

![Sprint4](Imagenes/Sprint%204/sp4.20.png)

Ahora quitaremos el disco que falla como se hace en maquinas fisicas, se hara con el comando ```mdadm /dev/md0 -r /dev/sdb1```

![Sprint4](Imagenes/Sprint%204/sp4.21.png)

Ahora para comprobar que podemos trabajar con un solo disco crearemos algo nuevamente

![sprint4](Imagenes/Sprint%204/sp4.21.png)

Ahora volveremos a añadir el disco utilizando ```mdadm /dev/md0 -a /dev/sdb1``` y rapidamente haremos un detail para ver como se esta copiando el contenido

![Sprint4](Imagenes/Sprint%204/sp4.23.png)

Si volvemos a hacer el detail tendría que salir el estado ACTIVE como de normal.

![Sprint4](Imagenes/Sprint%204/sp4.24.png)

Ahora comprobaremos lo mismo pero quitando el disco desde el VB con la máquina apagada

![Sprint4](Imagenes/Sprint%204/sp4.25.png)

Una vez la máquina se a encendido volveremos a hacer un detail a ver qué está pasando

![Sprint4](Imagenes/Sprint%204/sp4.26.png)

Y podemos comprobar que en la carpeta raid1 no hay nada

![Sprint4](Imagenes/Sprint%204/sp4.27.png)

Ahora pararemos el raid para poder montarlo con un solo disco, le haremos un update para que pueda volver a funcionar con normalidad y lo montaremos

![Sprint4](Imagenes/Sprint%204/sp4.28.png)

Comprobamos que funcione 

![Sprint4](Imagenes/Sprint%204/sp4.29.png)

![Sprint4](Imagenes/Sprint%204/sp4.30.png)

Ahora nuevamente creamos otro disco y lo añadimos a la maquina virtual

![Sprint4](Imagenes/Sprint%204/sp4.30.png)

Comprobamos que se sigue manteniendo el raid activo y se puede seguir trabajando

![Sprint4](Imagenes/Sprint%204/sp4.32.png)

Comprobamos como se llama el nuevo disco y lo particionamos como antes.

![Sprint4](Imagenes/Sprint%204/sp4.33.png)

![Sprint4](Imagenes/Sprint%204/sp4.34.png)

Ahora añadimos el disco al raid

![Sprint4](Imagenes/Sprint%204/sp4.35.png)

![Sprint4](Imagenes/Sprint%204/sp4.36.png)

Y comprobamos que podemos ver las cosas en la carpeta de **raid1**

![Sprint4](Imagenes/Sprint%204/sp4.37.png)

Ahora veremos si funciona correctamente después de hacer un reboot.

![Sprint4](Imagenes/Sprint%204/sp4.38.png)

Ahora desmontamos el raid y lo pararemos

![Sprint4](Imagenes/Sprint%204/sp4.39.png)

Eliminaremos el interior la carpeta de raid1

![Sprint4](Imagenes/Sprint%204/sp4.40.png)

Entraremos al fstab y comentaremos la línea del fstab para que no se monte nuevamente

![Sprint4](Imagenes/Sprint%204/sp4.41.png)

También borraremos las lineas del mdadm.conf

![Sprint4](Imagenes/Sprint%204/sp4.42.png)

Haremos un ```–stop```, ```--remove``` y un ```--superblock``` ya después un reboot para comprobar si se vuelve a montar el raid una vez reiniciada.

![Sprint4](Imagenes/Sprint%204/sp4.43.png)

## RAID 5

Para un raid 5 tendremos que añadir 4 discos duros en el virtual box.

![Sprint4](Imagenes/Sprint%204/raid5-1.png)

Hacemos un fdisk -l para poder ver los discos 

![Sprint4](Imagenes/Sprint%204/raid5-2.png)

![Sprint4](Imagenes/Sprint%204/raid5-3.png)

Tenemos que entrar dentro de cada disco para cambiar el sistema de fitxeros de cada uno de ellos.

![Sprint4](Imagenes/Sprint%204/raid5-4.png)

![Sprint4](Imagenes/Sprint%204/raid5-5.png)

Al no tener particion en los 2 discos nuevos tendremos que crearla en el disco “sdd” y “sde”.

![Sprint4](Imagenes/Sprint%204/raid5-6.png)

![Sprint4](Imagenes/Sprint%204/raid5-7.png)

![Sprint4](Imagenes/Sprint%204/raid5-8.png)

![Sprint4](Imagenes/Sprint%204/raid5-9.png)

Ahora hacemos un “fdisk -l” para comprobar que salen de esta manera los discos que hemos cambiado y verificar que lo hemos hecho adecuadamente.

![Sprint4](Imagenes/Sprint%204/raid5-10.png)

![Sprint4](Imagenes/Sprint%204/raid5-11.png)

Creamos la carpeta donde se formará el raid y le entregamos todos los permisos para poderla utilizar al completo.

![Sprint4](Imagenes/Sprint%204/raid5-12.png)

Ahora crearemos el “RAID” con el siguiente comando

```mdadm –create /dev/md0 –level=5 –raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1```

![Sprint4](Imagenes/Sprint%204/raid5-13.png)

Le cambiamos el formato para poder utilizarlo

![Sprint4](Imagenes/Sprint%204/raid5-14.png)

Para recibir información de raid utilizaremos ```mdadm –detail /dev/md0```

![Sprint4](Imagenes/Sprint%204/raid5-15.png)

Ahora haremos que el ```–detail –scan``` se vaya a una carpeta en un .txt que nosotros le indicaremos 

![Sprint4](Imagenes/Sprint%204/raid5-16.png)

Haremos que el raid se monte automáticamente yendo al archivo ```/etc/mdadm.conf``` y añadimos la siguiente línea

![Sprint4](Imagenes/Sprint%204/raid5-17.png)

Y añadiremos también una línea en el archivo /etc/fstab

![Sprint4](Imagenes/Sprint%204/raid5-18.png)

### **<span style="color:red; font-size: 1.5em;">IMPORTANTE!</span>** 

Antes de hacer el reboot tendremos que poner las siguientes comandas

![Sprint4](Imagenes/Sprint%204/raid5-19.png)

Una vez se haya iniciado nuevamente la máquina para comprobar que todo ha funcionado correctamente haremos un detail ```mdadm –detail /dev/md0```

![Sprint4](Imagenes/Sprint%204/raid5-20.png)

Ahora para hacer las pruebas crearemos una carpeta y un archivo dentro

![Sprint4](Imagenes/Sprint%204/raid5-21.png)

Ahora haremos fallar uno de los discos para comprobar que pasa ```mdadm /dev/md0 -f /dev/sdb1```

![Sprint4](Imagenes/Sprint%204/raid522.png)

Hacemos un detail y comprobamos que uno de los discos sale fallando.

![Sprint4](Imagenes/Sprint%204/raid5-23.png)

Ahora quitaremos el disco que falla como se hace en maquinas fisicas, se hara con el comando ```mdadm /dev/md0 -r /dev/sdb1```

![Sprint4](Imagenes/Sprint%204/raid5-24.png)

Haciendo un detail tendria que salir que el disco esta en el stado “removed”

![Sprint4](Imagenes/Sprint%204/raid5-25.png)

Ahora para comprobar que podemos trabajar con un disco menos crearemos algo nuevamente

![Sprint4](Imagenes/Sprint%204/raid5-26.png)

Ahora quitaremos otro de los discos para comprobar que pasa con el raid.

![Sprint4](Imagenes/Sprint%204/raid5-27.png)

![Sprint4](Imagenes/Sprint%204/28.png)

![Sprint4](Imagenes/Sprint%204/29.png)

![Sprint4](Imagenes/Sprint%204/30.png)

Ahora comprobaremos si funciona 

![Sprint4](Imagenes/Sprint%204/31.png)

Sigue funcionando, por lo que saldremos de la maquina y quitaremos los discos de la misma para comprobar que pasa.

![Sprint4](Imagenes/Sprint%204/32.png)

Una vez la máquina se a encendido volveremos a hacer un detail a ver qué está pasando

![Sprint4](Imagenes/Sprint%204/33.png)

Y podemos confirmar que ya no funciona

![Sprint4](Imagenes/Sprint%204/34.png)

