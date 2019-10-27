# Práctica: Integridad, firmas y autenticación
## Tarea 1: Firmas electrónicas 
En este primer apartado vamos a trabajar con las firmas electrónicas, para ello te pueden ayudar los siguientes enlaces:

*GPG*

**1. Manda un documento y la firma electrónica del mismo a un compañero. Verifica la firma que tu has recibido.**
Para crear la firma electrónica de un documento:
~~~
paloma@coatlicue:~$ gpg --output pruebaFirma.txt.sig --detach-sign pruebaFirma.txt 
~~~

Verificamos el fichero que hemos recibido:
~~~
paloma@coatlicue:~$ gpg --verify pruebaFirma_alejandro.txt.sig 
gpg: asumiendo que los datos firmados están en 'pruebaFirma_alejandro.txt'
gpg: Firmado el mar 15 oct 2019 12:28:43 CEST
gpg:                usando RSA clave EC7EEAB6F3986FD97F72A4409F229BC929C410C4
gpg: Firma correcta de "Alejandro Morales Gracia <ale95mogra@gmail.com>" [desconocido]
gpg: ATENCIÓN: ¡Esta clave no está certificada por una firma de confianza!
gpg:          No hay indicios de que la firma pertenezca al propietario.
Huellas dactilares de la clave primaria: EC7E EAB6 F398 6FD9 7F72  A440 9F22 9BC9 29C4 10C4
~~~


**2. ¿Qué significa el mensaje que aparece en el momento de verificar la firma?**
~~~
gpg: Firma correcta de "Pepe D <josedom24@gmail.com>" [desconocido]
gpg: ATENCIÓN: ¡Esta clave no está certificada por una firma de confianza!
gpg:          No hay indicios de que la firma pertenezca al propietario.
Huellas dactilares de la clave primaria: E8DD 5DA9 3B88 F08A DA1D  26BF 5141 3DDB 0C99 55FC
~~~

Significa que, aunque el fichero y el certificado concuerdan, no hay ninguna garantía de que el usuario de la firma sea de verdad esa persona.


**3. Vamos a crear un anillo de confianza entre los miembros de nuestra clase, para ello.**
- Tu clave pública debe estar en un servidor de claves

- Puedes seguir el esquema que se nos presenta en la siguiente página de Debian:

- Una vez que firmes una clave se la tendrás que devolver a su dueño, para que otra persona se la firme.

- Cuando tengas las tres firmas sube la clave al servidor de claves y rellena tus datos en la tabla Claves públicas PGP 2019-2020

- Asegurate que te vuelves a bajar las claves públicas de tus compañeros que tengan las tres firmas.

~~~
gpg --keyserver pgp.rediris.es --send-key FD52AA5481FD0E1518011D83952393CC31351D81
~~~

- Escribe tu fingerprint en un papel y dárselo a tu compañero, para que puede descargarse tu clave pública.
Para encontrar mi fingerprint:
~~~
paloma@coatlicue:~$ gpg --edit-key palomagarciacampon08@gmail.com
gpg (GnuPG) 2.2.12; Copyright (C) 2018 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Clave secreta disponible.

sec  rsa3072/952393CC31351D81
     creado: 2019-10-07  caduca: 2019-11-06  uso: SC  
     confianza: absoluta      validez: absoluta
ssb  rsa3072/D7F9FDBB7151CA51
     creado: 2019-10-07  caduca: 2019-11-06  uso: E   
[  absoluta ] (1). Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>

gpg> fpr
pub   rsa3072/952393CC31351D81 2019-10-07 Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>
 Huella clave primaria: FD52 AA54 81FD 0E15 1801  1D83 9523 93CC 3135 1D81
~~~


- Te debes bajar al menos tres claves públicas de compañeros. Firma estas claves.

Se descarga la clave:
~~~
paloma@coatlicue:~$ gpg --keyserver pgp.rediris.es --search-key A615 146E 82E2 72C8 99A3  4100 F405 106D BBAB FB72
gpg: data source: http://130.206.1.8:11371
(1)	Fernando Tirado <fernando.tb.95@gmail.com>
	  3072 bit RSA key F405106DBBABFB72, creado: 2019-10-07, caduca: 2019-11-06
Keys 1-1 of 1 for "A615 146E 82E2 72C8 99A3 4100 F405 106D BBAB FB72".  Introduzca número(s), O)tro, o F)in > 1
gpg: clave F405106DBBABFB72: "Fernando Tirado <fernando.tb.95@gmail.com>" sin cambios
gpg: Cantidad total procesada: 1
gpg:              sin cambios: 1
~~~

Se firma:
~~~
paloma@coatlicue:~$ gpg --sign-key A615146E82E272C899A34100F405106DBBABFB72

pub  rsa3072/F405106DBBABFB72
     creado: 2019-10-07  caduca: 2019-11-06  uso: SC  
     confianza: desconocido   validez: desconocido
sub  rsa3072/1A3DEC0EAA18E3ED
     creado: 2019-10-07  caduca: 2019-11-06  uso: E   
[desconocida] (1). Fernando Tirado <fernando.tb.95@gmail.com>


pub  rsa3072/F405106DBBABFB72
     creado: 2019-10-07  caduca: 2019-11-06  uso: SC  
     confianza: desconocido   validez: desconocido
 Huella clave primaria: A615 146E 82E2 72C8 99A3  4100 F405 106D BBAB FB72

     Fernando Tirado <fernando.tb.95@gmail.com>

Esta clave expirará el 2019-11-06.
¿Está realmente seguro de querer firmar esta clave
con su clave: "Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>" (952393CC31351D81)?

¿Firmar de verdad? (s/N) s

paloma@coatlicue:~$ gpg --output Ftirado.asc --export A615146E82E272C899A34100F405106DBBABFB72
El fichero 'Ftirado.asc' ya existe. ¿Sobreescribir? (s/N) s
~~~

Se repite el procedimiento con otros dos compañeros:
~~~
paloma@coatlicue:~$ gpg --keyserver pgp.rediris.es --search-key EC7E EAB6 F398 6FD9 7F72  A440 9F22 9BC9 29C4 10C4
gpg: data source: http://130.206.1.8:11371
(1)	Alejandro Morales Gracia <ale95mogra@gmail.com>
	  3072 bit RSA key 9F229BC929C410C4, creado: 2019-10-14, caduca: 2021-10-13
Keys 1-1 of 1 for "EC7E EAB6 F398 6FD9 7F72 A440 9F22 9BC9 29C4 10C4".  Introduzca número(s), O)tro, o F)in > 1
gpg: clave 9F229BC929C410C4: "Alejandro Morales Gracia <ale95mogra@gmail.com>" sin cambios
gpg: Cantidad total procesada: 1
gpg:              sin cambios: 1

paloma@coatlicue:~$ gpg --sign-key EC7EEAB6F3986FD97F72A4409F229BC929C410C4
paloma@coatlicue:~$ gpg --output MoralGFirmada.asc --export EC7EEAB6F3986FD97F72A4409F229BC929C410C4
paloma@coatlicue:~$ scp MoralGFirmada.asc moralg@172.22.9.198:
~~~

~~~
paloma@coatlicue:~$ gpg --sign-key C7BAE0D4F7D76C1AFB523DB11ED42C7688EC344D
paloma@coatlicue:~$ gpg --output firmaPaloma.asc --export C7BAE0D4F7D76C1AFB523DB11ED42C7688EC344D
~~~


- Tu te debes asegurar que tu clave pública es firmada por al menos tres compañeros de la clase.
Añado la firma que me han enviado:
~~~
paloma@coatlicue:~$ gpg --import Palomatomatufirma.asc 
gpg: clave 952393CC31351D81: "Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>" 1 firma nueva
gpg: Cantidad total procesada: 1
gpg:         nuevas firmas: 1
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: nivel: 0  validez:   1  firmada:   1  confianza: 0-, 0q, 0n, 0m, 0f, 1u
gpg: nivel: 1  validez:   1  firmada:   0  confianza: 1-, 0q, 0n, 0m, 0f, 0u
gpg: siguiente comprobación de base de datos de confianza el: 2019-11-06
~~~

~~~
paloma@coatlicue:~$ gpg --import ClavePalomaFirmada.asc 
gpg: clave 952393CC31351D81: "Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>" 1 firma nueva
gpg: Cantidad total procesada: 1
gpg:         nuevas firmas: 1
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: nivel: 0  validez:   1  firmada:   2  confianza: 0-, 0q, 0n, 0m, 0f, 1u
gpg: nivel: 1  validez:   2  firmada:   0  confianza: 2-, 0q, 0n, 0m, 0f, 0u
gpg: siguiente comprobación de base de datos de confianza el: 2019-11-06
~~~

~~~
paloma@coatlicue:~$ gpg --import Descargas/clavePaloma.asc 
~~~



**4. Muestra las firmas que tiene tu clave pública.**
~~~
paloma@coatlicue:~$ gpg --list-sign
/home/paloma/.gnupg/pubring.kbx
-------------------------------
pub   rsa3072 2019-10-07 [SC] [caduca: 2019-11-06]
      FD52AA5481FD0E1518011D83952393CC31351D81
uid        [  absoluta ] Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>
sig 3        952393CC31351D81 2019-10-07  Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>
sig          F405106DBBABFB72 2019-10-22  Fernando Tirado <fernando.tb.95@gmail.com>
sig          9F229BC929C410C4 2019-10-22  Alejandro Morales Gracia <ale95mogra@gmail.com>
sig          1ED42C7688EC344D 2019-10-22  Juan Antonio Reifs Ramirez <initiategnat9@gmail.com>
sub   rsa3072 2019-10-07 [E] [caduca: 2019-11-06]
sig          952393CC31351D81 2019-10-07  Paloma R. Garcia Campon <palomagarciacampon08@gmail.com>
~~~


**5. Comprueba que ya puedes verificar sin “problemas” una firma recibida por una persona en la que confías.**

Se añade la clave del compañero actualizada:
~~~
paloma@coatlicue:~$ gpg --import ClaveAlejadroActualizada.asc 
gpg: clave 9F229BC929C410C4: "Alejandro Morales Gracia <ale95mogra@gmail.com>" 2 firmas nuevas
gpg: Cantidad total procesada: 1
gpg:         nuevas firmas: 2
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: nivel: 0  validez:   1  firmada:   3  confianza: 0-, 0q, 0n, 0m, 0f, 1u
gpg: nivel: 1  validez:   3  firmada:   0  confianza: 3-, 0q, 0n, 0m, 0f, 0u
gpg: siguiente comprobación de base de datos de confianza el: 2019-11-06
~~~

Y se verifica:
~~~
paloma@coatlicue:~$ gpg --verify paraPaloma.txt.sig 
gpg: asumiendo que los datos firmados están en 'paraPaloma.txt'
gpg: Firmado el mar 22 oct 2019 12:51:33 CEST
gpg:                usando RSA clave EC7EEAB6F3986FD97F72A4409F229BC929C410C4
gpg: Firma correcta de "Alejandro Morales Gracia <ale95mogra@gmail.com>" [total]
~~~


**6. Comprueba que puedes verificar sin “problemas” una firma recibida por una tercera problema en la que confía una persona en la que tu confías.**


## Tarea 2: Correo seguro con evolution/thunderbird

Ahora vamos a configurar nuestro cliente de correo electrónico para poder mandar correos cifrados, para ello:

1. Configura el cliente de correo evolution con tu cuenta de correo habitual
2. Añade a la cuenta las opciones de seguridad para poder enviar correos firmados con tu clave privada o cifrar los mensajes para otros destinatarios
3. Envía y recibe varios mensajes con tus compañeros y comprueba el funcionamiento adecuado de GPG


## Tarea 3: Integridad de ficheros

Vamos a descargarnos la ISO de debian, y posteriormente vamos a comprobar su integridad.

Puedes encontrar la ISO en la dirección: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/.

    Para validar el contenido de la imagen CD, solo asegúrese de usar la herramienta apropiada para sumas de verificación. Para cada versión publicada existen archivos de suma de comprobación con algoritmos fuertes (SHA256 y SHA512); debería usar las herramientas sha256sum o sha512sum para trabajar con ellos.
    Verifica que el contenido del hash que has utilizado no ha sido manipulado, usando la firma digital que encontrarás en el repositorio. Puedes encontrar una guía para realizarlo en este artículo: How to verify an authenticity of downloaded Debian ISO images

Tarea 4: Integridad y autenticidad (apt secure) (2 puntos)

Cuando nos instalamos un paquete en nuestra distribución linux tenemos que asegurarnos que ese paquete es legítimo. Para conseguir este objetivo se utiliza criptografía asimétrica, y en el caso de Debian a este sistema se llama apt secure. Esto lo debemos tener en cuenta al utilizar los repositorios oficiales. Cuando añadamos nuevos repositorios tendremos que añadir las firmas necesarias para confiar en que los paquetes son legítimos y no han sido modificados.

Busca información sobre apt secure y responde las siguientes preguntas:

    ¿Qué software utiliza apt secure para realizar la criptografía asimétrica?
    ¿Para que sirve el comando apt-key? ¿Qué muestra el comando apt-key list?
    En que fichero se guarda el anillo de claves que guarda la herramienta apt-key?
    ¿Qué contiene el archivo Release de un repositorio de paquetes?. ¿Y el archivo Release.gpg?. Puedes ver estos archivos en el repositorio http://ftp.debian.org/debian/dists/Debian10.1/. Estos archivos se descargan cuando hacemos un apt update.
    Explica el proceso por el cual el sistema nos asegura que los ficheros que estamos descargando son legítimos.
    añade de forma correcta el repositorio de virtualbox añadiendo la clave pública de virtualbox como se indica en la documentación.

Tarea 5: Autentificación: ejemplo SSH (2 puntos)

Vamos a estudiar como la criptografía nos ayuda a cifrar las comunicaciones que hacemos utilizando el protocolo ssh, y cómo nos puede servir también para conseguir que un cliente se autentifique contra el servidor. Responde las siguientes cuestiones:

    Explica los pasos que se producen entre el cliente y el servidor para que el protocolo cifre la información que se transmite? ¿Para qué se utiliza la criptografía simétrica? ¿Y la asimétrica?
    Explica los dos métodos principales de autentificación: por contraseña y utilizando un par de claves públicas y privadas.
    En el cliente para uqe sirve el contenido que se guarda en el fichero ~/.ssh/know_hosts?

    ¿Qué significa este mensaje que aparece la primera vez que nos conectamos a un servidor?

     $ ssh debian@172.22.200.74
     The authenticity of host '172.22.200.74 (172.22.200.74)' can't be established.
     ECDSA key fingerprint is SHA256:7ZoNZPCbQTnDso1meVSNoKszn38ZwUI4i6saebbfL4M.
     Are you sure you want to continue connecting (yes/no)? 

    En ocasiones cuando estamos trabajando en el cloud, y reutilizamos una ip flotante nos aparece este mensaje:

     $ ssh debian@172.22.200.74
     @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
     @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
     @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
     IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
     Someone could be eavesdropping on you right now (man-in-the-middle attack)!
     It is also possible that a host key has just been changed.
     The fingerprint for the ECDSA key sent by the remote host is
     SHA256:W05RrybmcnJxD3fbwJOgSNNWATkVftsQl7EzfeKJgNc.
     Please contact your system administrator.
     Add correct host key in /home/jose/.ssh/known_hosts to get rid of this message.
     Offending ECDSA key in /home/jose/.ssh/known_hosts:103
       remove with:
       ssh-keygen -f "/home/jose/.ssh/known_hosts" -R "172.22.200.74"
     ECDSA host key for 172.22.200.74 has changed and you have requested strict checking.

    ¿Qué guardamos y para qué sirve el fichero en el servidor ~/.ssh/authorized_keys?

3 puntos)

En este primer apartado vamos a trabajar con las firmas electrónicas, para ello te pueden ayudar los siguientes enlaces:

    Intercambiar claves
    Firmado de claves (Debian)
    Manual de creación y mantenimiento de clave GPG

GPG

    Manda un documento y la firma electrónica del mismo a un compañero. Verifica la firma que tu has recibido.

    ¿Qué significa el mensaje que aparece en el momento de verificar la firma?

     gpg: Firma correcta de "Pepe D <josedom24@gmail.com>" [desconocido]
     gpg: ATENCIÓN: ¡Esta clave no está certificada por una firma de confianza!
     gpg:          No hay indicios de que la firma pertenezca al propietario.
     Huellas dactilares de la clave primaria: E8DD 5DA9 3B88 F08A DA1D  26BF 5141 3DDB 0C99 55FC

    Vamos a crear un anillo de confianza entre los miembros de nuestra clase, para ello.
        Tu clave pública debe estar en un servidor de claves
        Escribe tu fingerprint en un papel y dárselo a tu compañero, para que puede descargarse tu clave pública.
        Te debes bajar al menos tres claves públicas de compañeros. Firma estas claves.
        Tu te debes asegurar que tu clave pública es firmada por al menos tres compañeros de la clase.
        Puedes seguir el esquema que se nos presenta en la siguiente página de Debian:
        Una vez que firmes una clave se la tendrás que devolver a su dueño, para que otra persona se la firme.
        Cuando tengas las tres firmas sube la clave al servidor de claves y rellena tus datos en la tabla Claves públicas PGP 2019-2020
        Asegurate que te vuelves a bajar las claves públicas de tus compañeros que tengan las tres firmas.
    Muestra las firmas que tiene tu clave pública.
    Comprueba que ya puedes verificar sin “problemas” una firma recibida por una persona en la que confías.
    Comprueba que puedes verificar sin “problemas” una firma recibida por una tercera problema en la que confía una persona en la que tu confías.

Tarea 2: Correo seguro con evolution/thunderbird (2 puntos)

Ahora vamos a configurar nuestro cliente de correo electrónico para poder mandar correos cifrados, para ello:

    Configura el cliente de correo evolution con tu cuenta de correo habitual
    Añade a la cuenta las opciones de seguridad para poder enviar correos firmados con tu clave privada o cifrar los mensajes para otros destinatarios
    Envía y recibe varios mensajes con tus compañeros y comprueba el funcionamiento adecuado de GPG

Tarea 3: Integridad de ficheros (1 punto)

Vamos a descargarnos la ISO de debian, y posteriormente vamos a comprobar su integridad.

Puedes encontrar la ISO en la dirección: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/.

    Para validar el contenido de la imagen CD, solo asegúrese de usar la herramienta apropiada para sumas de verificación. Para cada versión publicada existen archivos de suma de comprobación con algoritmos fuertes (SHA256 y SHA512); debería usar las herramientas sha256sum o sha512sum para trabajar con ellos.
    Verifica que el contenido del hash que has utilizado no ha sido manipulado, usando la firma digital que encontrarás en el repositorio. Puedes encontrar una guía para realizarlo en este artículo: How to verify an authenticity of downloaded Debian ISO images

Tarea 4: Integridad y autenticidad (apt secure) (2 puntos)

Cuando nos instalamos un paquete en nuestra distribución linux tenemos que asegurarnos que ese paquete es legítimo. Para conseguir este objetivo se utiliza criptografía asimétrica, y en el caso de Debian a este sistema se llama apt secure. Esto lo debemos tener en cuenta al utilizar los repositorios oficiales. Cuando añadamos nuevos repositorios tendremos que añadir las firmas necesarias para confiar en que los paquetes son legítimos y no han sido modificados.

Busca información sobre apt secure y responde las siguientes preguntas:

    ¿Qué software utiliza apt secure para realizar la criptografía asimétrica?
    ¿Para que sirve el comando apt-key? ¿Qué muestra el comando apt-key list?
    En que fichero se guarda el anillo de claves que guarda la herramienta apt-key?
    ¿Qué contiene el archivo Release de un repositorio de paquetes?. ¿Y el archivo Release.gpg?. Puedes ver estos archivos en el repositorio http://ftp.debian.org/debian/dists/Debian10.1/. Estos archivos se descargan cuando hacemos un apt update.
    Explica el proceso por el cual el sistema nos asegura que los ficheros que estamos descargando son legítimos.
    añade de forma correcta el repositorio de virtualbox añadiendo la clave pública de virtualbox como se indica en la documentación.

Tarea 5: Autentificación: ejemplo SSH (2 puntos)

Vamos a estudiar como la criptografía nos ayuda a cifrar las comunicaciones que hacemos utilizando el protocolo ssh, y cómo nos puede servir también para conseguir que un cliente se autentifique contra el servidor. Responde las siguientes cuestiones:

    Explica los pasos que se producen entre el cliente y el servidor para que el protocolo cifre la información que se transmite? ¿Para qué se utiliza la criptografía simétrica? ¿Y la asimétrica?
    Explica los dos métodos principales de autentificación: por contraseña y utilizando un par de claves públicas y privadas.
    En el cliente para uqe sirve el contenido que se guarda en el fichero ~/.ssh/know_hosts?

    ¿Qué significa este mensaje que aparece la primera vez que nos conectamos a un servidor?

     $ ssh debian@172.22.200.74
     The authenticity of host '172.22.200.74 (172.22.200.74)' can't be established.
     ECDSA key fingerprint is SHA256:7ZoNZPCbQTnDso1meVSNoKszn38ZwUI4i6saebbfL4M.
     Are you sure you want to continue connecting (yes/no)? 

    En ocasiones cuando estamos trabajando en el cloud, y reutilizamos una ip flotante nos aparece este mensaje:

     $ ssh debian@172.22.200.74
     @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
     @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
     @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
     IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
     Someone could be eavesdropping on you right now (man-in-the-middle attack)!
     It is also possible that a host key has just been changed.
     The fingerprint for the ECDSA key sent by the remote host is
     SHA256:W05RrybmcnJxD3fbwJOgSNNWATkVftsQl7EzfeKJgNc.
     Please contact your system administrator.
     Add correct host key in /home/jose/.ssh/known_hosts to get rid of this message.
     Offending ECDSA key in /home/jose/.ssh/known_hosts:103
       remove with:
       ssh-keygen -f "/home/jose/.ssh/known_hosts" -R "172.22.200.74"
     ECDSA host key for 172.22.200.74 has changed and you have requested strict checking.

    ¿Qué guardamos y para qué sirve el fichero en el servidor ~/.ssh/authorized_keys?

