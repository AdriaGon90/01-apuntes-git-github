# PRIMEROS COMANDOS DE GIT

## INTRODUCCIÓN

Desde terminal de `git`, introduciremos el primer comando para visualizar la versión de git con la que nos encontramos trabajando:

> git --version

El siguiente comando nos brinda ayuda para conocer la sintaxis de los comandos:

> git help

Si deseamos conocer mas a detalle un comando en particular:

> git help `comando`

**NOTA:** Cuando en la consola o termina se muestra mucha información por algún comando que fue ejecutado, al final suele mostrar dos puntos `:` esto significa que hay mas información que mostrar, para salir podemos presionar la tecla `q`, y si queremos seguir visualizando mas información presionamos la tecla `enter`.

### CONFIGURACIÓN INICIAL

Antes de empezar a trabajar con `git`, es importante especificar nuestra identidad (usuario y correo) en la configuración global, para ello, usamos los siguientes comandos:

> git config --global user.name "Mi nombre"

> git config --global user.email "micorreo@correo.com"

Para visualizar la configuración global implementada en `git` desde un editor de texto en la terminal, ejecutamos el comando:

> git config --global -e

Para visualizar en forma de lista toda la configuración **global** implementada en `git`, utilizamos el comando:

> git config --global -l

Para visualizar en forma de lista toda la configuración **completa** implementada en `git`, utilizamos el comando:

> git config -l

### COMANDOS BÁSICOS

Para inicializar un repositorio, en la terminal de `git`, debemos pocisionarnos en la carpeta donde inicializaremos dicho repositorio y ejecutamos el comando:

> git init

Esto nos creará una carpeta `.git`. Esta carpeta contiene toda la configuración de `git` de nuestro repositorio.

Para visualizar los archivos de un repositorio que han sido agregados, modificados o eliminados ejecutamos el comando:

> git status

Este comando nos muestra una lista de archivos que han sufrido alguna modificación, señalando en colores rojo y verde aquellos:

* *rojo*: archivos que participaron en alguna modificación o que recibieron algún cambio desde el último `commit` a la fecha pero que no han sido agregados al escenario (stage).
* *verde*: son aquellos archivos modificados que fueron agregados al escenario (stage), y son estos archivos los que están listos para enviarlos al `commit`.

Para agregar todos los archivos y que `git` esté pendiente de los cambios que realizamos en ellos, ejecutamos el comando:

> git add .

Esto es indicarle a `git` que prepare nuestros archivos y lo mande al stage (o escenario).

Para tomar un snapshoot o fotografía del código y registrarlo en la línea del tiempo en `git`, ejecutamos el comando:

> git commit -m "Tu mensaje"

Con eso `git` crea un registro histórico de los cambios que sucedieron en los archivos que se encontraron en el stage.

Si realizamos cambios en un archivo y guardamos y cerramos o, inclusive si eliminamos accidentalmente, podemos restaurar al último `commit` ese archivo con el comando:

> git checkout -- .

Para visualizar toda la historia de los `commit` registrados en el repositorio, ejecutamos el comando:

> git log

Este comando nos enlista los `commit` desde el mas reciente hasta el mas antiguo.

## COMANDOS ADICIONALES

### DIFERENTES FORMAS DE AGREGAR ARCHIVOS AL ESCENARIO

* Suponiendo que tenemos una serie de archivos donde hemos realizado cambios dentro de un repositorio en `git`, pero que no han sido agregados al escenario y deseamos agregarlos para que `git` pueda darles segumiento y realizar el `commit` correspondiente, tomando en cuenta que no queremos agregar todos, sino sólo unos archivos en específico.

    En primera instancia, debemos obtener el path y el nombre de los archivos que deseamos agregar al escenario, para ello, ejecutamos el comando `git status`, que nos mostrará una lista de los archivos que han sufrido cambios, copiamos el path con el nombre del archivo que deseamos agregar y lo agregamos al final del comando `git add`:

    > git add `path\filename.ext`

    Ejecutamos nuevamente el comando `git status` y nos mostrará la lista de los archivos que han sufrido cambios, pero adicional, nos señalará en color verde el/los archivo(s) que han sido agregados al escenario.

    Para enviar al `commit` estos archivos, ejecutamos el comando `git commit -m "Tu mensaje"`.

    Ejecutamos nuevamente el comando `git status` y no veremos archivos en el escenario (señalados en color verde).

* Suponiendo que ahora deseamos agregar al escenario (stage) y enviar al `commit` todos los archivos con una extensión en particular, para ello ejecutamos el comando 

    > git add *.`ext`

    Posteriormente procedemos a ejecutar el `commit`.

* Si deseamos agregar todos los archivos que se encuentren en una carpeta en particular, ejecutamos:

    > git add `folder/`

    Prodecemos a ejecutar el `commit`

* Si deseamos agregar todos los archivos excepto aquellos con extensión en particular, ejecutamos el comando

    > git add -A

    para agregar todos los archivos al stage, y quitamos del stage aquel o aquellos archivos con extensión en particular que deseamos omitir, con el comando:

    > git reset *.`ext`

    Procedemos a ejecutar el `commit`.

* Otras formas de agregar al stage

    * Para agregar todos los archivos con una extension `ext` en particular del TODO el repositorio
        > git add "*.`ext`"

    * Para agregar todos los archivos con una extension `ext` en particular del directorio actual

        > git add *.`ext`

    * Para agregar todos los archivos que se hayan modificado sin excepción

        > git add --all

        > git add .

        > git add -A

    * Para agregar una lista de archivos

        > git add <`lista de archvivos`>

    * Para agregar todos los archivos con una extensión `ext` en particular que se encuentran dentro de una carpeta `folder`

        > git add `folder/*.ext`

    * Para agregar todos los archivos que se encuentran dentro de una carpeta `folder` sin excepción

        > git add `folder/`