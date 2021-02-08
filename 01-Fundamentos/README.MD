# PRIMEROS COMANDOS DE GIT

Desde terminal de git, introduciremos el primer comando para visualizar la versión de git con la que nos encontramos trabajando:

    git --version

El siguiente comando nos brinda ayuda para conocer la sintaxis de los comandos:

    git help

Si deseamos conocer mas a detalle un comando en particular:

    git help <comando>

**NOTA:** Cuando en la consola o termina se muestra mucha información por algún comando que fue ejecutado, al final suele mostrar dos puntos `:` esto significa que hay mas información que mostrar, para salir podemos presionar la tecla `q`, y si queremos seguir visualizando mas información presionamos la tecla `enter`.

## CONFIGURACIÓN INICIAL

Antes de empezar a trabajar con `git`, es importante especificar nuestra identidad (usuario y correo) en la configuración global, para ello, usamos los siguientes comandos:

    git config --global user.name "Mi nombre"
    git config --global user.email "micorreo@correo.com"

Para visualizar la configuración global implementada en `git`, ejecutamos el comando:

    git config --global -e

## CREAR REPOSITORIO

Para inicializar un repositorio, en la terminal de `git`, debemos pocisionarnos en la carpeta donde inicializaremos dicho repositorio y ejecutamos el comando:

    git init

Esto nos creará una carpeta `.git`. Esta carpeta contiene toda la configuración de `git` de nuestro repositorio.

## COMANDOS BÁSICOS

Para visualizar los archivos de un repositorio que han sido agregados, modificados o eliminados ejecutamos el comando:

    git status

Para agregar todos los archivos y que `git` esté pendiente de los cambios que realizamos en ellos, ejecutamos el comando:

    git add .

Para tomar un snapshoot o fotografía del código y registrarlo en la línea del tiempo en `git`, ejecutamos el comando:

    git commit -m "Tu mensaje"

Si realizamos cambios en un archivo y guardamos y cerramos accidentalmente, podemos restaurar al último `commit` ese archivo con el comando:

    git checkout -- .

