# Laboratorio-sistemas-distribuidos
Laboratorio *sistemas distribuidos*

Escuela Superior de Informática.

https://github.com/rosasacedon/SacedonMartin

##  Miembros
* *Rosa María Sacedón Ortega*
* *Victor Martin Alonso*

## Manual de Usuario
Este manual de usuario pretende explicar la funcionalidad de los componentes de la práctica y su forma de ejecución.


### Pasos para ejecutar

1- En una terminal ejecutar lo siguiente:

    make run

Esto ejecutará todos los nodos de la práctica.

2- En otra terminal ejecutamos:

    icegridgui
    
2.1- Creamos una nueva conexión
 
2.2- Abrimos el archivo el archivo xml que contiene la aplicación.
    File -> Open -> *YoutubeDownloaderApp.xml*
    
2.3- Guardamos al registro con el botón (save to a registry)

2.4- Distribuimos la aplicación en el Live Deployment
    Tools -> Path distribution -> Apply path distribution

2.5- Ejecutamos los servidores con cierto orden.
    1) IceStorm
    2) Transfer / Downloader
    3) Orchestrators
    
3- Ejecutar el cliente

    ./run_client.sh
    
## Descripción de la práctica

El objetivo principal del proyecto es diseñar un sistema cliente-servidor que permita la descarga
de ficheros a partir de URIs. El ejemplo típico será la descarga de clips de audio de YouTube. La
implementación de este proyecto permitirá al alumno trabajar, mediante ZeroC Ice, los siguientes
aspectos:
	
	  Comunicación asíncrona
	  Manejo de canales de eventos
	  Despliegue de servidores de forma dinámica
	  Gestión de un grid

Arquitectura del proyecto

El sistema está formado por cinco tipos de componentes: downloaders, encargados de la descargade ficheros;  orchestrators, para la gestión de los  downloaders;  transfers, empleados para latransferencia de archivos; clientes, que solicitarán ficheros; y canales de eventos para mantener unestado coherente entre componentes. Con el objetivo de facilitar el desarrollo de la práctica, laarquitectura descrita se irá desarrollando a lo largo de distintas fases:

	  FASE 1: Introducción de los Actores
	  FASE 2: Descarga y sincronización de componentes
	  FASE 3: El sistema final

-FASE 3: El sistema final-

-PARTE 1: Implementación-

En la tercera fase el sistema se compondrá de un  cliente, tres  orchestrators,  una factoría de downloaders y una factoría de transfers. El cliente tendrá que mandar un URL en forma de string a uno de los orchestrators que, a su vez, redirigirá la petición a un downloader creado a tal efecto siempre que el fichero de audio no haya sido descargado previamente en el sistema. El downloader descargará el archivo y notificará que se ha descargado correctamente en un canal de eventos para que todos los orchestrators sepan que el fichero existe, mandando la información de ese fichero. Al terminar se destruirá.

El cliente podrá solicitar la lista de ficheros descargados a uno de los orchestrators.

Además, el cliente también tendrá la opción de pedir la transferencia de un archivo de audio. Harála petición a uno de los *orchestrators* que, a su vez, redirigirá la petición a un transfer creado a tal efecto siempre que el fichero de audio haya sido descargado previamente en el sistema. El transferle mandará directamente al cliente el archivo. Al terminar se destruirá.

Los orchestrators se anunciarán al resto de orchestrators en su creación, que se anunciarán a su vez al nuevo orchestrator para actualizar las listas de orchestrators existentes de cada objeto. Además, un nuevo orchestrator ha de ser consciente de los ficheros de audio que ya han sido descargados en el sistema.

Se puede observar el diagrama de secuencia de la fase 2 en la Figura 1.



