# GIT STASH Y GIT REBASE

## GIT STASH

### COMANDOS BÁSICOS

Veamos con el `stash` como un contenedor donde podemos almacenar todos los cambios de manera temporal, para dejar el repositorio a como se encontraba en el último `commit` o en un determinado punto, para poder trabajar con otros cambios; posteriormente podemos regresar los cambios que teníamos en un principio y recuperar todo el trabajo.

El comando para ejecutar `stash`

> git stash

**NOTA:** Con el comando anterior, enviamos al `stash` todos los archivos, ***excepto aquellos a los que `git` no les da segumiento***.

Si deseamos conocer todos los trabajos en progreso que hay en todo el repositorio

> git stash list

`Stash` usa una denotación en los registros para especificar que hay cambios guardados de manera temporal y la rama en la que se encuentran, para diferenciarlos de los registros de un `commit` cuando se consulta el `log`; la denotación es `WIP` que significa: **Work In Progress**

Para recuperar los cambios de un `stash`

> git stash pop

### CONFLICTOS CON STASH

Los conflictos pueden producirse cuando se envian cambios de un archivo al `stash`, para posteriormente enviar un `commit` con nuevos cambios en ese mismo archivo en las mismas líneas y, finalmente se desea restaurar o recuperar los cambios del `stash`; de igual manera que el conflicto que se presenta en los `merge` entre dos ramas cuando se detentan modificaciones en las mismas líneas de un mismo archivo, podemos resolverlo a través del `merge` de forma manual, para así determinar los cambios que se quedarán en ese archivo. La consola nos mencionará qué archivos y en qué líneas se encuentran los conflictos, es recomendable abrir los archivos con conflictos con un editor o IDE que contenga plugin para realizar el `merge`, ya que eso nos facilitará el proceso del `merge`. El archivo con los conflictos, nos mostrará los mismos caracteres que nos muestra un archivo de conflicto en `merge`.

~~~
<<<<<<< Updated upstream
Los cambios que están en la rama principal
=======
Los cambios que están en el stash
>>>>>>> Stashed changes
~~~

Con esto tendriamos resuelto nuestro conflicto y podemos proceder a continuar trabajando.

Adicional, si revisamos el `log`, podemos observar que todavía se encuentra el `stash` en el registro de `git`, por lo que es recomendable eliminarlo, para ello, ejecutamos el comando 

> git stash list

Si solo existe un `stash`, podemos ejecutar el comando

> git stash drop

Con esto hemos eliminado el único `stash`

### MAS INFORMACIÓN SOBRE EL `STASH`

El comando `stash` toma los archivos que han sufrido cambios desde el último `commit` y los coloca en un área temporal.

Para enviar archivos al `stash`, podemos ejecutar cualquiera de los dos comandos:

> git stash

ó

> git stash save

Si deseamos agregar un mensaje al `stash`

> git stash save "`Tu mensaje`"

Podemos tener múltiples `stash`, y los podemos listar con el comando

> git stash list

Si deseamos obtener mas información detallada de los `stash`

> git stash list --stat

Si deseamos obtener mas información de la última entrada de `stash`

> git show stash

Si deseamos obtener mas información de un `stash` en particular

> git show `stash@{#}`

Para restaurar el primer `stash` de la lista

> git stash apply

Y si deseamos restaurar un `stash` en particular, ejecutamos el comando

> git stash apply `stash@{#}`

Para restaurar el primer `stash` de la lista y posteriormente eliminarlo

> git stash pop

Cuando se presentan conflictos al restaurar un `stash`, ese `stash` **NO** se elimina del registro, por lo que es conveniente que, después de solucionar el conflicto, eliminar ese `stash`

Para eliminar la primera entrada de la lista de `stash`

> git stash drop

Si deseamos eliminar un `stash` en particular

> git stash drop `stash@{#}`

Para eliminar todas las entradas del `stash`

> git stash clear

**NOTA:** Este comando borra directamente todas las entradas del `stash` **sin preguntar**, por lo que una vez ejecutado este comando, no hay manera de recuperarlas.

Si deseamos enviar al `stash` todos los archivos, excepto los que se encuentran en el `staged` (o escenario), ejecutamos el comando

> git stash save --keep-index

Si deseamos agregar al `stash` a todos los archivos, incluyendo a los que `git` **NO** les da seguimiento

git stash save --include-untracked

## GIT REBASE

Para comprender esta funcionalidad, pensemos en la siguiente situación; tenemos nuestra *rama principal* donde tenemos varios `commit`, adicional, tenemos una *rama secundaria*, donde también tenemos varios `commit`, que son posteriores a los `commit` de la *rama principal*, pero, con el tiempo, se crean nuevos `commit` en la *rama principal* que no existen en la *rama secundaria*, y que si o si necesitamos agregar a esta rama. Esta integración la podemos resolver a través del `rebase`.

Al ejecutar el comando `rebase`, internamente lo que está haciendo `git` es; mover los `commit` de la *rama secundaria* a un **área temporal**, posteriormente, mueve el puntero de esta rama hacia el último `commit` de la *rama principal*, y por último regresa los `commit` que se encuentran en el **área temporal** de la *rama secundaria*.

En pocas palabras, el `rebase` nos sirve para actualizar el punto donde creamos la rama (rama secundaria), obteniendo los cambios que han sucedido en la rama de la cual nos desprendimos (rama principal).

El `rebase` se ejecuta en la rama secundaria, ya que en ella tenemos que integrar los cambios` que sucedieron posteriormente en la rama principal.

Para realizar el `rebase`, ejecutamos:

> git rebase `rama-principal`

Si todo se realizó correctamente, veremos un mensaje similar al siguiente:

~~~
Successfully rebased and updated refs/heads/rama-secundaria.
~~~

Finalmente se puede proceder a continuar trabajando como se desea, incluso se puede realizar el `merge` entre las dos ramas.

Existe otro `rebase` que se conoce como `rebase interactivo`, que básicamente lo que hace es agarrar los `commit` hasta la posición que le indiquemos y llevarlos al **área temporal** en ese mismo orden y posteriormente regresarlos igual como fueron ingresados al **área temporal** como fueron ejecutados.

Podemos plantearnos interrogantes acerca de para qué nos sirve esta funcionalidad; aunque existen muchas, te voy a mencionar 4 de los usos mas comunes que tiene el `rebase interactivo`:

1. Ordenar `commit`
2. Corregir mensajes de los `commit`
3. Unir `commit`
4. Separar `commit`

Existen diferntes `rebase interactivos`, de los cuales mencionaré aalguno de ellos a continuación y posteriormente los detallaremos:

* Rebase - Squash
* Rebase - Reword
* Rebase - Edit

### REBASE - SQUASH

Squash hace referencia a cuando dos cosas chocan y se unen, por lo que significa que podemos unir dos o mas `commit`, lo realizamos de la siguiente manera:

Estando en la rama donde deseamos realizar el `rebase`, debemos verificar la posición en la que se encuentran los `commit` (a través del `log`) con los que haremos esta acción, esta posición se especifica despúes del símbolo virgulilla `~` del comando, ejemplo, si deseamos unir el antepenúltimo y penúltimo `commit` debemos seleccionar los 3 primeros `commit`, por lo que despúes del símbolo virgulilla `~` especificamos el número 3:

> git rebase -i HEAD~`posición-commit`

**NOTA:** La posición del `commit`, es la posición en la que se encuentra el `commit` que vamos a seleccionar, contando a partir del último `commit` para abajo de la línea de tiempo de `git` (lo podemos visualizar a través del `log`), ya que por ejemplo, si queremos deshacer el `commit` de la posición 3 (contando desde el último `commit`) debemos escribir el número 3.

Al darle `Intro` al comando anterior, nos mostrará en consola un texto bastante extraño, pero ubicaremos las dos partes que nos interesan:

1. La primera parte nos muestra una lista de los `commit` seleccionados, estos `commit` los obtiene a través del número especificado en la posición del `commit`, por lo que si especificamos el número 3, nos devolverá desde el último `commit` dos commit anteriores a este, anteponiendo en cada uno, la palabra *pick*.

    ~~~
    pick 158ba9e Mensaje del antepenúltimo commit
    pick f4523dd Mensaje del penúltimo commit
    pick 8c45e67 Mensaje del último commit
    ~~~
    
    **NOTA:** Esa lista nos muestra los commit seleccionados de forma *ascendiente*.

2. La segunda parte es un menú, lo identificamos ubicando la palabra *Commands:*, en ella se enlistan las opciones que podemos utilizar en el `rebase`.

    ~~~
    # Commands:
    # p, pick = use commit
    # r, reward = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    ...
    ~~~

Pulsamos la tecla `A` para editar y en la primera parte, donde está el listado de `commit`, borramos la palabra *pick* del `commit` que deseamos unir con el anterior y en su lugar escribimos la letra `s` ó la palabra `squash`, por ejemplo, si deseamos unir el antepenúltimo y penúltimo `commit` escribimos la letra `s` en penúltimo `commit`.
    
    pick 158ba9e Mensaje del antepenúltimo commit
    s f4523dd Mensaje del penúltimo commit
    pick 8c45e67 Mensaje del último commit
    
Para salir y grabar los cambios, pulsamos la tecla `ESC` para salir del modo editor, dos puntos `:`, luego la tecla `W` para escribir y `Q` para salir y finalmente `INTRO`. Esto nos mostrará otro texto, pero básicamente ahí nos está solicitando que agreguemos un `commit` con la combinanción de los dos `commit`, por lo que introduciremos un nuevo mensaje para el nuevo `commit`, eliminando los mensajes de los `commit` que se fusionarán. Para editar y salir es el mismo procedimiento que el proceso anterior. Al finalizar veremos un mensaje similar al siguiente:

    [detached HEAD 75d7f34] Tu nuevo mensaje de commit
    Date: Wed Mar 10 19:01:58 2021 -0600
    1 file changed, 5 insertions(+)
    create mode 100644 path/filename.ext
    Successfully rebased and updated refs/heads/rama-actual.
    
### REBASE - REWORD

Este `rebase interactivo`, nos permite cambiar el mensaje de un `commit` en particular. Para ello, seguimos el mismo procedimiento del proceso anterior, ejecutando el comando:

> git rebase -i HEAD~`posición-commit`

**NOTA:** La posición del `commit` recordemos que es la posición en la que se encuentra el `commit` que vamos a seleccionar, contando a partir del último `commit` para abajo de la línea de tiempo de `git` (lo podemos visualizar a través del `log`), ya que por ejemplo, si queremos deshacer el `commit` de la posición 4 (contando desde el último `commit`) debemos escribir el número 4.

Al presionar la tecla `INTRO` nos mostrará el texto que mencionada en el punto anterior, y realizaremos el mismo procedimiento, con la única diferencia que, en vez de escribir la letra `s` ó la palabra `squash`, escríbiremos la letra `r` ó la palabra `reword` al `commit` al que le deseamos cambiar el mensaje. Continuamos exactamente el mismo procedimiento para guardar y salir del editor, lo que nos llevará posteriormente a una nueva ventana donde procederemos a cambiar el mensaje del `commit`, realizamos los mismos pasos para editar, salir del modo editor, guardar y cerrar. Si todo salió bien mostrará un mensaje similar al siguiente:

    [detached HEAD 19a5c44] Tu nuevo mensaje del commit
    Date: Mon Mar 8 18:32:37 2021 -0600
    1 file changed, 1 insertion(+), 1 deletion(-)
    Successfully rebased and updated refs/heads/rama-actual.

### REBASE - EDIT

Este `rebase interactivo` es un poco mas complicado y a la vez confuso, por lo que hay que tener mucho cuidado al momento de ejecutarlo. Este `rebase` nos permite deshacer un `commit` (cualquiera de la línea del tiempo de `git`), ya sea para separarlo en varios `commit` o simplemente integrar nuevos cambios y hacer un nuevo `commit`.

Si deseamos separar en varios `commit` un `commit` de la línea del tiempo de `git`, realizamos lo siguiente:

1. Ejecutamos el comando:
    
    > git rebase -i HEAD~`posición-commit`

    **NOTA:** La posición del `commit` recordemos que es la posición en la que se encuentra el `commit` que vamos a seleccionar, contando a partir del último `commit` para abajo de la línea de tiempo de `git` (lo podemos visualizar a través del `log`), ya que por ejemplo, si queremos deshacer el `commit` de la posición 6 (contando desde el último `commit`) debemos escribir el número 6.

2. Esto nos abriá la misma ventana con el texto que expuse en los puntos anteriores, realizamos los mismos pasos para editar el `commit` que deseamos, por lo que la palabra *pick* de ese `commit` la eliminamos y escribimos en su lugar la letra `e` o la palabra `edit`, guardamos y cerramos y nos llevará nuevamente a la consola, pero nos arrojará un mensaje con lo siguente:

    ~~~
    Stopped at d17b4ab...  Mensaje actual del commit
    You can amend the commit now, with

        git commit --amend

    Once you are satisfied with your changes, run

        git rebase --continue
    ~~~

    Básicamente nos indica que al finalizar de realizar los cambios que deseamos debemos ejecutar al final el comando:

    > git rebase --continue

3. Quitamos los archivos del `staged` de ese `commit`, con el comando:

    > git reset HEAD^

4. Procedemos a realizar los cambios que deseamos, agregamos al `staged` y ejecutamos los `commit`, cuando finalicemos, ejecutamos el comando:

    > git rebase --continue

5. Si todo se ejecutó correctamente, mostrará un mensaje similar al siguiente:

        Successfully rebased and updated refs/heads/rama-actual.

**NOTA:** Este `rebase interactivo` nos puede ayudar a cambiar de rama una serie de `commit` a partir de uno cuando se nos presenta el tema de haber integrado cambios en una rama equivocada, para ello, realizamos lo siguiente:

* Ejecutamos el comando

    > git rebase -i HEAD~`posición-commit`

* Cambiamos la palabra *pick* por la letra *e* o palabra *edit*, guaramos y cerramos.

* Ejecutamos el comando `git reset HEAD^` para quitar del `staged` los archivos de ese `commit`, ejecutamos `git checkout -b rama-nueva` para crear la rama (en caso que no exista) y nos cambia a ella directamente llevando los archivos que estaban en el `staged`; procedemos a integrar los cambios a esa rama (`staged` y `commit`), regresamos a la *rama principal*, realizamos el `merge`, y finalmente, ejecutamos el comando:

    > git rebase --abort

## EXÁMEN DE APRENDIZAJE

1. ¿Para qué sirve el stash?

    - [ ] A) Para fusionar los cambios inmediatamente con la rama master

    - [x] B) Sirve para colocar el trabajo actual, en un espacio temporal para posteriormente retomarlo

    - [ ] C) Sirve para guardar los cambios de la rama, y regresar al master para continuar los cambios desde el último `commit`.

2. ¿Qué significa **WIP** cuando realizamos un `git stash`?

    - [ ] A) Work Inside Progress

    - [x] B) Work In Progress

    - [ ] C) Wait In Process

    - [ ] D) Work In Process

3. ¿Cómo puedo ver todos los trabajos pendientes en el `stash`?

    - [x] A) git stash list

    - [ ] B) git stash -o

    - [ ] C) git stash all

    - [ ] D) git stash

4. ¿Cómo puedo recuperar el trabajo del `stash`?

    - [x] A) git stash pop

    - [ ] B) git stash recover

    - [ ] C) git stash

    - [ ] D) git stash drop

5. Cuando recuperamos un trabajo del `stash`, ¿Es posible caer en conflictos?

    - [x] A) Verdadero

    - [ ] B) Falso

6. ¿El git rebase, nos puede servir para actualizar el punto de separación de una rama?

    - [x] A) Verdadero

    - [ ] B) Falso

7. ¿Qué puede hacer un rebase interactivo?

    - [ ] A) Puede unir dos o más commit en un único commit

    - [ ] B) Puede re-ordenar commit

    - [ ] C) Corregir mensajes de commit

    - [ ] D) Para separar commit

    - [x] E) Todas las anteriores