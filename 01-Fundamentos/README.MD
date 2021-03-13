# INTRODUCCIÓN A GIT

## CONCEPTOS BÁSICOS Y COMANDOS DE AYUDA

Para entender cómo funciona `git` debemos comprender algunos conceptos básicos que se utilizan en el flujo de trabajo de `git`:

* ***Staged***: conocido como el *escenario*, que es el estado en el que se ponen los archivos que están listos para agregarlos a la línea del tiempo a través del `commit`.

* ***Commit***: Es el momento en el que se crea el registro histórico (snaptshot o fotografía) de los archivos agregados al `staged` (escenario) con todos los cambios que sucedieron en ese preciso momento.

* ***Status***: Lista de archivos que participaron o sufrieron cambios desde el último `commit` a la fecha.

* ***HEAD***: Se refiere al `commit` en el que está tu repositorio posicionado en cada momento. Por regla general `HEAD` suele coincidir con el último `commit` de la rama en la que estés, ya que habitualmente estás trabajando en lo último.

* ***Log***: Historial de `commit` realizados en el repositorio.

* ***Hash del commit***: es el número o identificador del `commit`, cada vez que se crea un `commit` nuevo se le asigna un *hash* nuevo. El *hash* lo podemos obtener a través del `log`.

Desde la terminal de `git`, introduciremos el primer comando para visualizar la versión de git con la que nos encontramos trabajando:

> git --version

El siguiente comando nos brinda ayuda para conocer la sintaxis de los comandos:

> git help

Si deseamos conocer mas a detalle un comando en particular:

> git help `comando`

**NOTA:** Cuando en la consola o termina se muestra mucha información por algún comando que fue ejecutado, al final suele mostrar dos puntos `:` esto significa que hay mas información que mostrar, para salir podemos presionar la tecla `q`, y si queremos seguir visualizando mas información presionamos la tecla `enter`.

## CONFIGURACIÓN INICIAL

Antes de empezar a trabajar con `git`, es importante especificar nuestra identidad (usuario y correo) en la configuración global, para ello, usamos los siguientes comandos:

> git config --global user.name "`Mi nombre`"

> git config --global user.email "`micorreo@correo.com`"

Para visualizar la configuración global implementada en `git` desde un editor de texto en la terminal, ejecutamos el comando:

> git config --global -e

Para visualizar en forma de lista toda la configuración **global** implementada en `git`, utilizamos el comando:

> git config --global -l

Para visualizar en forma de lista toda la configuración **completa** implementada en `git`, utilizamos el comando:

> git config -l

## COMANDOS BÁSICOS

Para inicializar un repositorio, en la terminal de `git`, debemos pocisionarnos en la carpeta donde inicializaremos dicho repositorio y ejecutamos el comando:

> git init

Esto nos creará una carpeta `.git`. Esta carpeta contiene toda la configuración de `git` de nuestro repositorio.

Si deseamos eliminar `git` de nuestro repositorio bastará únicamente con eliminar la carpeta `.git`.

Para visualizar los archivos de un repositorio que han sido agregados, modificados o eliminados ejecutamos el comando:

> git status

Este comando nos muestra una lista de archivos que han sufrido alguna modificación, señalando en colores rojo y verde aquellos:

* *rojo*: archivos que participaron en alguna modificación o que recibieron algún cambio desde el último `commit` a la fecha pero que no han sido agregados al escenario (staged).
* *verde*: son aquellos archivos modificados que fueron agregados al escenario (staged), y son estos archivos los que están listos para enviarlos al `commit`.

Para agregar todos los archivos y que `git` esté pendiente de los cambios que realizamos en ellos, ejecutamos el comando:

> git add .

Esto es indicarle a `git` que prepare nuestros archivos y lo mande al `staged` (o escenario).

Para tomar un snapshoot o fotografía del código y registrarlo en la línea del tiempo en `git`, ejecutamos el comando:

> git commit -m "`Tu mensaje`"

Con eso `git` crea un registro histórico de los cambios que sucedieron en los archivos que se encontraron en el `staged`.

Si realizamos cambios en uno o varios archivos y guardamos y cerramos o, inclusive si eliminamos accidentalmente varios archivos, podemos restaurar al último `commit` todos los archivos con el comando:

> git checkout -- .

Para visualizar toda la historia de los `commit` registrados en el repositorio, ejecutamos el comando:

> git log

Este comando nos enlista los `commit` desde el mas reciente hasta el mas antiguo. Con este comando podemos obtener el *hash*, que son los números que acompañan a la leyenda `commit`:

    commit 3185e1842db6636e59bebdbafb9d13b59446aeca
    Author: your name <your.email@domain.com>
    Date:   Wed Mar 10 18:22:18 2021 -0600

        Your message



### COMANDOS ADICIONALES

#### DIFERENTES FORMAS DE AGREGAR ARCHIVOS AL ESCENARIO

* Suponiendo que tenemos una serie de archivos donde hemos realizado cambios dentro de un repositorio en `git`, pero que no han sido agregados al escenario y deseamos agregarlos para que `git` pueda darles segumiento y realizar el `commit` correspondiente, tomando en cuenta que no queremos agregar todos, sino sólo unos archivos en específico.

    En primera instancia, debemos obtener el path y el nombre de los archivos que deseamos agregar al escenario, para ello, ejecutamos el comando `git status`, que nos mostrará una lista de los archivos que han sufrido cambios, copiamos el path con el nombre del archivo que deseamos agregar y lo agregamos al final del comando `git add`:

    > git add `path\filename.ext`

    Ejecutamos nuevamente el comando `git status` y nos mostrará la lista de los archivos que han sufrido cambios, pero adicional, nos señalará en color verde el/los archivo(s) que han sido agregados al escenario.

    Para enviar al `commit` estos archivos, ejecutamos el comando `git commit -m "Tu mensaje"`.

    Ejecutamos nuevamente el comando `git status` y no veremos archivos en el escenario (señalados en color verde).

* Suponiendo que ahora deseamos agregar al escenario (staged) y enviar al `commit` todos los archivos con una extensión en particular, para ello ejecutamos el comando 

    > git add *.`ext`

    Posteriormente procedemos a ejecutar el `commit`.

* Si deseamos agregar todos los archivos que se encuentren en una carpeta en particular, ejecutamos:

    > git add `folder/`

    Prodecemos a ejecutar el `commit`

* Si deseamos agregar todos los archivos excepto aquellos con extensión en particular, ejecutamos el comando

    > git add -A

    para agregar todos los archivos al `staged`, y quitamos del `staged` aquel o aquellos archivos con extensión en particular que deseamos omitir, con el comando:

    > git reset *.`ext`

    Procedemos a ejecutar el `commit`.

* Otras formas de agregar al `staged`

    * Para agregar todos los archivos con una extension `ext` en particular del TODO el repositorio
        > git add "*.`ext`"

    * Para agregar todos los archivos con una extension `ext` en particular del directorio actual

        > git add *.`ext`

    * Para agregar todos los archivos que se hayan modificado sin excepción

        > git add --all

        > git add .

        > git add -A

    * Para agregar una lista de archivos

        > git add `lista de archvivos ...`

    * Para agregar todos los archivos con una extensión `ext` en particular que se encuentran dentro de una carpeta `folder`

        > git add `folder/*.ext`

    * Para agregar todos los archivos que se encuentran dentro de una carpeta `folder` sin excepción

        > git add `folder/`

    * Si deseamos agregar todos los archivos al `staged` y hacer `commit` al mismo tiempo, ejecutamos el comando

        > git commit -am "`Tu mensaje`"

#### DIFERENTES FORMAS DE REVISAR EL `LOG` Y LOS CAMBIOS DEL ÚLTIMO `COMMIT`

Para revisar el `log` de la forma común, ejecutamos el comando

> git log

Una forma mas resumida de visualizar la información del `log`:

> git log --oneline

Otra forma de visualizar la misma información pero con gráficos de la línea de tiempo:

> git log --oneline --decorate --all --graph

#### ALIAS PARA COMANDOS

`Git` nos ofrece una larga lista de comandos que nos son sumamente útiles, pero muchos de ellos pueden ser demasiados largos al momento de teclearlos en la consola. Para ello, `git` nos ofrece una herramienta que nos permite crear *alias* para los comandos, permitiendonos invocar comandos largos con pocas letras.

Para crear un alias de un comando:

> git config --global alias.`nombre` "`comando con parámetros`"

Esto nos permite invocar el comando con el alias que le asignemos:

> git `nombre`

Por ejemplo, para crear el alias de nombre `lg` del comando `git log --oneline --decorate --all --graph`:

> git config --global alias.lg "log --oneline --decorate --all --graph

podemos invocarlo con:

> git lg

Otro comando útil sería `git status -s -b`, podemos crear un alias de nombre `s`:

> git config --global alias.s "status -s -b

podemos invocarlo con:

> git s

## CUESTIONARIO DE APRENDIZAJE DE COMANDOS BÁSICOS

1. Cuando utilizamos Git, ¿Todos los miembros del equipo tienen una copia del repositorio cental?

    - [x] A) Verdadero

    - [ ] B) Falso

2. ¿Un commit en Git, es como una fotografía del proyecto en ese momento?

    - [x] A) Verdadero

    - [ ] B) Falso

3. ¿Para qué sirve el comando `git init`?

    - [ ] A) Para configurar nuestro usuario y contraseña

    - [x] B) Para inicializar el repositorio
    
    - [ ] C) Para iniciar el seguimiento de los archivos

4. Localmente, ¿Dónde se encuentra la carpeta que permite controlar todo nuestro repositorio de git?

    - [ ] A) En la carpeta git

    - [ ] B) En la carpeta git-config

    - [x] C) En la carpeta .git

5. Si queremos eliminar git de nuestro repositorio, ¿qué debemos hacer?

    - [x] A) Borrar la carpeta .git

    - [ ] B) Ejecutar el comando git destroy

    - [ ] C) Copial el folder a otro directorio

6. ¿Qué es el `staged` o el escenario?

    - [ ] A) Un lugar donde se muestra toda la información del commit

    - [ ] B) El lugar donde podemos ver todos los archivos de nuestro repositorio

    - [x] C) Es un lugar donde podemos confirmar los archivos y carpetas que conformarán el commit

7. El comando `git s`, ¿Es propio de Git?

    - [ ] A) Verdadero

    - [x] B) Falso

# ACCIONES AVANZADAS EN `GIT`

## DIFERENCIAS ENTRE COMMITS Y RESTAURACIÓN DE ARCHIVOS

Cuando realizamos cambios en uno o varios archivos y deseamos visualizar las diferencias de los cambios con respecto al último `commit`, ejecutamos el comando

> git diff

Este comando nos mostrará las diferencias de cambios de archivos que no están en el `staged`.

Si agregamos uno o varios archivos al `staged`, al ejecutar el comando `diff` no nos mostrará las diferencias de esos archivos; para visualizar la diferencia de cambios de los archivos agregados al `staged` ejecutamos el comando:

> git diff --staged

Si deseamos quitar uno o varios archivos del `staged`,  ejecutamos el comando:

> git reset HEAD `path/filename.ext`

Si deseamos restaurar los cambios que hemos realizado en todos los archivos, ejecutamos el comando

> git checkout -- .

Si deseamos resturar los cambios efectuados en un archivo en específico al último `commit`, ejecutamos el comando:

> git checkout -- `path/file.ext`

Si deseamos restaurar un archivo en específico de un `commit` en particular:

> git checkout `hash` `path/filename.ext`

## ACTUALIZAR MENSAJE DEL `COMMIT` Y REVERTIR `COMMIT`

Si deseamos cambiar el mensaje del último `commit` ejecutado, tecleamos el comando:

> git commit --amend -m "`Tu mensaje`"

Si se nos presenta la situación en la que olvidamos agregar cambios a uno o varios archivos (o incluso omitirlos) al último `commit` y estos cambios deben estar ligados a ese `commit`, podemos realizar lo siguiente:

1. Ejecutamos el comando para deshacer el último `commit`:

    > git reset --soft HEAD^

2. Realizamos las modificaciones que nos faltan, incluso ya sea que agregemos nuevos archivos, eliminemos u omitamos algunos.

3. Ejecutamos el comando:

    > git commit -am "`Tu mensaje`"

*NOTA*: si vamos a agregar todos los cambios al `staged` ejecutamos el comando anterior, pero si agregaremos ciertos archivos, agregamos con el comando `add` y posteriormente `commit`.

Para agregar un mensaje en el `commit` de múltiples líneas realizamos lo siguiente:

1. Ejecutamos el comando

    > git commit

2. Esto nos abrirá un editor de texto en la consola, pulsamos la tecla `A` para editar

3. Escribimos el mensaje que deseamos, para agregar una nueva línea pulsamos la tecla `ENTER`.

4. Cuando hayamos terminado de escribir el mensaje, pulsamos la tecla `ESC` para salir del editor.

5. Pulsamos la tecla dos puntos `:` posteriormente las teclas `W` para escribir y `Q` para salir y finalmente pulsamos la tecla `ENTER`.

## VIAJANDO EN EL TIEMPO EN EL REPOSITORIO

### VIAJES EN EL TIEMPO, RESETS Y REFLOG

`Git` nos permite regresar a un punto en el tiempo para realizar cambios en un `commit` determinado. Para ello:

1. Ejecutamos el comando 

    > git log --oneline --decorate --all --graph

2. Obtenemos el *hash* del `commit` al que deseamos regresar

3. Ejecutamos el comando:

    > git reset --soft `hash`

    ó
    
    > git reset --mixed `hash`

    Esto nos regresará a un `commit` en específico, pero los cambios realizados en los `commit` superiores no se perderán, simplemente que los archivos cambiados ya no estarán en el `staged`.

    Si queremos definir este `commit` en el que nos posicionamos sea el nuevo `HEAD`, descartando todos los cambios que sucedieron en los `commit` superiores, ejecutamos el comando:

    > git reset --hard `hash`

    *NOTA IMPORTANTE*: este comando nos borrará todos los cambios que sucedieron de este `commit` para arriba.

    Si deseamos regresar a un `commit` que se encontraba despues del `commit` del que regresamos, debemos obtener el *hash* del `commit` al que deseamos regresar, ya que no lo visualizaremos en el `log`, para ello ejecutamos el comando:

    > git reflog

    y ejecutar el comando `--hard`

### CAMBIAR EL NOMBRE Y ELIMINAR ARCHIVOS MEDIANTE `GIT`

Si bien el cambio de nombre o eliminación de archivos se puede realizar mediante la interfaz del explorador de archivos, pero hacerlo mediante `git` tenemos la ventaja de mantener toda la historia de cambios que ese archivo a tenido en el repositorio.

Para cambiar nombre de archivo mediante la consola de `git`, usamos el siguiente comando:

> git mv `path/finename.ext` `path/newfilename.ext`

Inmediatamente en el `status` podemos visualizar que el archivo afectado se encuentra en el `staged` pero con la inicial `R` de *renombred*, y con eso podemos ejecutar el `commit` para registrar ese nuevo cambio.

Para eliminar un archivo utilizando la consola de `git` ejecutamos el comando:

> git rm path/`filename.ext`

Inmediatamente en el `status`, podemos visualizar que el archivo afectado se encuentra en el `staged` pero con la inicial `D` de *deleted*, y con eso podemos ejecutar el `commit` para registrar en la historia ese nuevo cambio.

### CAMBIAR EL NOMBRE Y ELIMINAR ARCHIVOS FUERA DE `GIT` (DESDE EL EXPLORADOR DE ARCHVOS)

Al realizar cambio de nombre desde el explorador de archivos, `git` lo interpreta como una eliminación y creación (con el nuevo nombre) de un nuevo archivo, por lo que al ejecutar el `status`, ese archivo ya no estará en el `staged` ya que tendrá dos estados, eliminación y creación, por lo que se tienen que ejecutar los siguientes comandos:

> git add -u

> git add -A

Y posteriormente realizar el `commit`.

Para el caso de la elimiación (desde el explorador de archivos, por supuesto), `git` reconoce la acción realizada, pero el archivo dejará de estar en el `staged`, por lo que tendremos que agregarlo y realizar el `commit`.

### IGNORAR ARCHIVOS

Para indicarle a `git` el o los archivos que deseamos que ignore (que no queremos versionar), se debe crear un archivo llamado `.gitignore` (se recomienda que se cree en la raíz del repositorio, ya que ponerlo en un directorio en particular, implica que ese archivo abrá que crearlo en cada directorio en particular), en cada línea de ese archivo se declara una expresión de los archivos a ignorar. Por ejemplo, si deseamos igorar un archivo en particular:

* path/filename.ext

Si deseamos ignorar archivos con una extensión en particular:

* *.ext

Si deseamos ignorar un directorio (implica ignorar todos los archivos que se encuentran dentro de él)

* directory/

### TAREA PRÁCTICA #1

Siga las instrucciones indicadas.

1. Cree una carpeta junto a a los demás ejercicios del proyecto llamada `demo-05-tarea`

2. Dentro de esa carpeta, inicialice el proyecto de git

3. Dentro del repositorio cree un archivo llamado `README.md`, ingrese el siguiente contenido:

        # Información
        Este es el resultado de mi esfuerzo aprendiendo GIT

4. 

* Agregue el `README.md` al `staged` o escenario
* Realice el primer commit con el mensaje `Creación del readme`

5. 

* Cree una carpeta dentro del proyecto llamada `logs`
* Dentro de la carpeta logs, cree un archivo llamado `hoy.log`
* Crear otro archivo llamado `historia.log`

6. Agregue únicamente el archivo `hoy.log` al `staged`

7. Realice el segundo commit con el archivo `hoy.log`, y en el mensaje coloque "Creamos el archivo hoy.log"

8. 

* Vamos a crear ahora el archivo `.gitignore`
* Ignoremos completamente el archivo `historia.log`

9. 

* Agregue al `staged` el archivo `.gitignore`
* Realice un commit unicamente con el archivo .gitignore

10. 

* Borre la carpeta LOGS
* Borre el archivo .gitignore
* El único archivo que debe de quedar, es el README.md

11. Reconstruir todo lo borrado con un único comando. (El archivo historia.log debe de aparecer)

12. ¿Por qué el archivo historia.log no apareció? Debe de ser capaz de analizar el por qué
