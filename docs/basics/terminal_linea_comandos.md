# Terminal y Linea de Comandos

Los objetivos del curso es aprender a conocer y usar la terminal en nuestro dia a dia.

- Qué es la terminal
- Por qué usar la terminal
- Cómo usar la terminal
- Cómo aprovechar la terminal al máximo

## Qué es la terminal y por qué la usarías

Es un programa que recibe ordenes y las ejecuta de forma que la maquina entienda.

- Es mas eficiente
- Ayuda a la automatizacion de tareas

## Comandos

Los comandos tienen en comun la forma de ejecucion:

- Nombre del programa
- Parámetros: Informacion adicional
- Modificadores: Altera lo que el programa va a hacer

```
command_name -flag_1 -flag_2 arg_1 arg_2
```

### Ejemplos de comandos

- `date`: Mostrar la fecha
- `echo`: Imprimir mensaje
- `man`: Mostrar manual `man date`

## Utilidades de CLI

- Comodines
- Combinaciones de teclas
- Sustitución de comandos

### Ejemplos

- Si ponemos un comando y presionamos `tab` se autocompleta o se muestra los que comienzan con las letras que pusimos
- Flecha arriba despliega el comando anterior
- `CTRL + R` para busqueda de comandos previamente escritos
- El comando `history` permite ver el historial de comandos ejecutados
- `!<NUMERO>` ejecuta el comando correspontiente al numero en el historial

## Identificacion de Archivos

- Nombre
- Ubicacion: `/directorio/subdirectorio/archivo`

### Comandos relacionados

Se debe tener en cuenta que los parametros pueden ser concatenados para realizar multiples acciones a la vez.

- `ls`: Listar archivos dentro del directorio actual
    - `ls -x`: Ordena los archivos por extensión
    - `ls -t`: Ordena los archivos por fecha de modificación
    - `ls -l`: Muestra toda la información: usuario, grupo, permisos, tamaño, fecha y hora de creación
    - `ls -lh`: Muestra la misma información que ls -l pero con las unidades de tamaño en KB, MB
    - `ls -R`: Muestra el contenido de todos los subdirectorios de forma recursiva
    - `ls -S`: Ordena los resultados por tamaño de archivo
    - `ls -a`: Ver archivos ocultos
- `pwd` (Print Working Directory): Se usa para mostrar el directorio actual en el que nos encontramos trabajando.
- `cd <PATH>`: Se utiliza para cambiar de directorio.
    - `cd -`: Ultimo directorio visitado
    - `cd ~`: Ir al HOME del usuario logeado
- `mkdir <PATH>`: Crear una carpeta
- `cp <FILE> <NEW_PATH>`: Copiar un archivo hacia un directorio
- `rm <PATH>`: Remover archivos o carpeta
- `mv <PATH> <NEW_PATH>`: Mover archivos o carpeta
- `..`: Puntero al directorio anterior
- `.`: Puntero al directorio Actual
- `rmdir <PATH>`: Remover directorios

## Archivos de texto

Tipos de Archivo

- Binarios
    - Programas ejecutables
    - Archivos de datos
- Texto
    - Contenido legible por humanos

### Utilidades interactivas

Son programas que procesan texto en tiempo real

- VIM
    - `i`: Entrar modo de insercion
    - `Esc`: Salir de modo edicion
    - `:w`: Guardar
    - `:q`: Salir
- Nano
    - `CTRL + X`: Salir y Guardar

## Utilidades batch

Son programas que procesan texto y emiten el resultado

- `cat`: Mostrar contenido de un archivo
- `head`: Ver solo las primeras lineas del archivo
    - `head -n 5 archivo.txt`
- `tail`: Ver solo las ultimas lineas del archivo

### Opciones Avanzadas

- `grep`: Búsqueda por expresiones regulares
    - `grep -i "palabra-clave$" file.txt`: Podemos verificar si la línea incluye una palabra clave al final
    - `grep "^palabra-clave" file.txt`: Al Comienzo
- `awk`: Tratamiento de texto delimitado
- `sed`: Tratamiento de flujos de caracteres, Solo debemos indicarle que queremos realizar una sustitución (`s/`), la palabra que vamos a cambiar (NOMBRE_USUARIO), la nueva palabra que vamos a incluir (Ana) y cerrar con el símbolo /.
    - `sed ‘s/NOMBRE_USUARIO/Ana/; s/PUNTOS_USUARIO/35/’ archivo-saludo.txt`

## Comunicación entre procesos

Flujo Estandar

- Entrada
- Salida
- Error

### Procesamiento de datos

- `ls > archivo`: Esto borra el contenido de archivo.
- `ls >> archivo`: Esto agrega contenido sin afectar el existente.

Los Pipes (`|`) toman la salida de un proceso y pasarla directamente como entrada al siguiente.

- `ls -l | more`
- `cat archivo.txt | wc -l`

## Cómo lanzar nuevos procesos

Ejecucion en primer plano, solo puede haber un proceso en la ventana.

- `ps` o `ps ax`: Identifica los procesos
- `top`: Tiempo real de los procesos
- `kill -9`: Interrumpir tareas pasando el numero del proceso (9 inmediatamente)
- `killall`: Interrumpe procesos pasando el nombre del archivo ejecutable.

### Opciones

- `&`: Al final de un comando, lo envia al 2do plano
- `CTRL + Z`: Enviar a segundo plano procesos que deban permanecer ejecutandose
- `fg`: Volverlo a traer a primer plano

## Administración de accesos

Podemos usar el siguiente comando para ver los permisos sobre un archivo o directorio

`ls -l` cada archivo/directorio tendra algo similar a `(-rwxrwxrwx)` lo cual nos indicara que permisos posee.

Estos permisos se dividen en 3 tipos de usuarios

- Propietario (Owner)
- Grupo
- Otros

| Permisos | |Owner|Group|Other|
|----------|-|-----|-----|-----|
|-rwxrwxrwx|-| rwx | rwx | rwx |
|dr-xrw--wx|d| r-x | rw- | -wx |

### Permisos

- `r`: Lectura
- `w`: Escritura
- `x`: Ejecucion

### Comandos

- `chmod`: Cambiar individualmente los permisos
- `chown`: Cambia el propietario
- `chgrp`: Cambia el grupo

#### Ejemplo

`chmod +x`: A todos los usuarios darle permisos de ejecucion

## Manejo de paquetes

Cómo ampliar las capacidades del sistema

### Paquetes Binarios

- `apt`: Debian
    - `apt install lynx`: Instalar Lynx
    - `apt update`
    - `apt upgrade`
- `zypper`: Suse
- `rpm`: Universal

### Paquetes de lenguajes

- `pip`: Python
- `composer`: PHP
- `npm`: NodeJS

### Otros

- `conda`
- `homebrew`

## Herramientas avanzadas

### Compresión de archivos

- `gzip <FILENAME>`: Comprimir archivos
- `gzip -d <COMPRESSED_FILE>`: Descomprimir

### Combinación de archivos

- `tar cf <OUTPUT>.tar <PATH>/*`: Combinar todo dentro de una carpeta
- `tar xf`: Desagrupar archivos
- `tar tf`: Ver el contenido de un archivo tar
- `tar czf`: Combinar archivos y comprimir con gzip

### Búsqueda de archivos

- `locate`: Busqueda en el sistema de archivos con el nombre
    - `locate hello.php`: Si no se encuentra posiblemente la DB esta desactualizada, se debe actualizar con sudo updatedb
- `whereis <BIN_FILE>`: Archivos binarios
- `find`: Busqueda dentro de un arbol con criterios
    - `find . -user esteban -type f -mtime +7`: Busqueda del directorio actual con usuario esteban solo archivos hace mas de 7 dias

### Interacción vía HTTP

- `curl`: Devuelve archivos crudos, respuesta http
    - `curl http://google.com`
- `wget`: Realiza Descargas
    - `wget http://google.com/archivo.txt`


### Envío de correo
Para poder enviar correos desde la terminal necesitamos contar con algunas utilidades en nuestra computadora.

La primera de ellas es postfix, un servidor de correo que se encargará de las tareas de comunicación con los servidores de destino.

En esta lectura asumiré que estás trabajando con alguna versión de Ubuntu, si no es así, los comandos podrían variar ligeramente.

Abre una terminal y asegúrate de tener tu sistema de paquetes al día usando el comando sudo apt update.

A continuación instala postfix utilizando el comando: `sudo DEBIAN_PRIORITY=low apt install postfix`.

Te encontrarás con una pantalla donde debes Seleccionas “Sitio de Internet” y darle “Aceptar”. Aceptar y pasarás a una pantalla donde ingresar tu dirección de correo electrónico.

Con eso finalizará el asistente para la configuración de postfix y la instalación habrá finalizado.

Instala las utilidades de correo con el comando:

```
sudo apt install mailutils
```

Y ahora sí, tienes todo lo que necesitas para enviar correos desde la terminal.

Puedes probarlo usando el comando:

```
echo “Hola Mundo!” | mail -s “Testing” TU_EMAIL
```

Revisa tu correo (no olvides revisar la bandeja de no deseados!) y ya podrás enviarle un saludo a todos tus conocidos sin pasar por Gmail, Outlook ni nada parecido.

#### Variables de entorno

- `$PATH`: Se almacenan todas las rutas de los comandos ejecutables

- Asignacion: `export VAR=VALOR`

## Automatización de tareas

### Scripting bash

Archivos ejecutables con extension `.sh`

```
#!/bin/bash

echo "Hola Automatizacion"
```

#### Ejecucion

- `./archivo.sh`
- `sh archivo.sh`

En el .bashrc se puede concatenar un archivo de estos sh `/pth/archivo`

### Programación de tareas

- `at`
    - `at now +2 minutes`
- `cron`

### Crontab

Con el comando `crontab -e` podemos abrir y editar el archivo

`* * * * * /path/to/the/script`

El significado de los asteriscos y el orden que tiene para la ejecucion son los siguientes

- Minuto
- Hora
- Dia del Mes
- Mes del Año
- Dia de la Semana
