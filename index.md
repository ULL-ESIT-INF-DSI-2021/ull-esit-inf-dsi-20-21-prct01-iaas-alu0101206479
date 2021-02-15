# Informe
## Práctica 1 - Configuración de máquina virtual en el IaaS
### Desarrollo de Sistemas Informáticos
### ACOIDAN MESA HERNANDEZ - alu0101206479@ull.edu.es

#### Introducción

Esto es un informe para poder llevar a cabo la **práctica 1 de Desarrollo de Sistemas Informáticos**, hemos aprendido a modificar los **hosts** de una maquina para así poder ejecutar `SSH` sin tener que introducir la contraseña e incluso sin tener que introducir el usuario. A parte hemos configurado **git** en la maquina virtual del **IaaS** para vincular el **GitHub** con la máquina y para así poder también configurar el `prompt` de la terminal para que aparezca la rama actual y también se han hecho más cosas que se pueden observar posteriormente.

#### Objetivos

Los objetivos de esta práctica han sido configurar la maquina virtual en el IaaS, además de instalar y configurar todas las herramientas necesarias para comenzar a trabajar la asignatura (Node.js, por ejemplo).

#### Pasos a seguir
##### 1. Configurar el servicio VPN de la ULL
Para una persona poder conectarse al servicio IaaS desde fuera de la red universitaria, es necesario conectarse a la VPN de la ULL. Para ello, accederemos a la [documentacion de configuración de la VPN](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) de la ULL y descargaremos las introucciones correspondientes a nuestro sistema operativo, las seguiremos y nos conectaremos.

##### 2. Acceder al servicio IaaS de la ULL y obtenemos la IP
Una vez conectada la VPN deberemos acceder al [Servicio IaaS de la ULL](https://iaas.ull.es/ovirt-engine/sso/login.html) e introducir nuestras credenciales. A continuación encontraremos todas las máqinas virtuales que tenemos, seleccionaremos la que se llama *DSI*, y pulsaremos **Ejecutar** para iniciar la máquina.
Una vez iniciada la máquina virtual, en la parte derecha de la interfaz, donde se indica *Interfaces de red*, encontraremos la IP asignada a la interfaz de nuestra máquina.

##### 3. Acceder por ssh a la máquina y cambiar la contraseña
Posteriormente, copiaremos la IP de la máquina virtual para conectarnos a ella por `SSH` a través de nuestra máquina local, por lo que ejecutaremos el comando:

```bash
  ssh usuario@10.6.XXX.XXX
```

El nombre usuario es el mismo y en la IP pondremos la IP que hemos copiado. Ya hecho esto, introduciremos `yes` e intro ante la siguiente pregunta:

```bash
  The authenticity of host '10.6.XXX.XXX (10.6.XXX.XXX)' can't be established.
  ECDSA key fingerprint is SHA256:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX.
  Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Después, te pide que introduzcas la contraseña, la cual es `usuario` y una vez introducida el propio sistema te pedirá que cambies la contraseña. Para ello te hará introducir la contraseña actual (`usuario`) y posteriormente te hará introducir dos veces la nueva contraseña *(Es recomendable que la apuntes en algún lugar seguro para que no se te olvide)*.

Posteriormente se nos habrá cerrado la sesión por lo que nos conectaremos de nuevo a través de `ssh` e introduciremos como contraseña la nueva.

##### 4. Modificar el nombre del host de la máquina virtual
Para hacer esto modificaremos el fichero `/etc/hostname`, el cual contiene el nombre del host de la máquina (el cual sera `ubuntu`) y lo cambiaremos por el nombre que queramos, en mi caso ha sido `iaas-dsi`. Para hacer esto ejecutaremos los siguientes comandos:

```bash
  # Mostramos el nombre de la máquina
  usuario@ubuntu:~$ cat /etc/hostname
  ubuntu
  
  # Lo cambiamos editando el fichero
  usuario@ubuntu:~$ sudo vi /etc/hostname
  
  # Mostramos el nombre nuevamente para comprobar que se haya cambiado
  usuario@ubuntu:~$ cat /etc/hostname
  iaas-dsi
```

A parte de esto, tambien deberemos modificar ciertos parámetros en el fichero `/etc/hosts`:

```bash
  # Mostramos el contenido del fichero (las ip seguido de los nombres de los hosts)
  usuario@ubuntu:~$ cat /etc/hosts
  127.0.0.1	localhost
  127.0.1.1	ubuntu
  ...

  # Editamos el fichero para cambiar el nombre del host local (ubuntu) por el que habíamos puesto
  usuario@ubuntu:~$ sudo vi /etc/hosts

  # Mostramos el contenido del fichero nuevamente para comprobar que se haya cambiado
  usuario@ubuntu:~$ cat /etc/hosts
  127.0.0.1	localhost
  127.0.1.1	iaas-dsi
  ...
