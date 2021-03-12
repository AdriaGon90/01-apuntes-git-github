# RAMAS

Pensemos que las `ramas` son como líneas de tiempo alternativas, sobre las cuales podemos realizar modificaciones sin afectar la rama principal.

Una rama es una línea de tiempo de `commits`.

En la sección de fundamentos, en las prácticas hemos trabajado con una rama llamada `master`, que es la rama principal y por defecto que se crean cuando inicializamos un repositorio.

Un concepto que va de la mano con las ramas es el `merge`, que es el proceso mediante el cual unimos cambios de una rama a otra.

Cuando queremos unir cambios de una rama a otra, `git` lo intentará realizar por nosotros, por lo que existen 3 posibles escenarios que pueden presentarse en el proceso del `merge`:

* Fast-foward: se dispara cuando `git` detecta que no hay cambios en la rama a la que se está realizando el `merge` y los cambios pueden ser integrados de forma, por decirlo así, transparente y cada uno de los `commtis` formará parte de la rama a la que se está realizando el `merge`.

* Uniones Automáticas: se dispara cuando `git` detecta que se realizaron cambios en la rama a la que se le está realizando el `merge`, pero no se modificaron las mismas líneas de los mismos archivos en ambas ramas, por lo que `git` puede realizar el `merge` sin problema alguno.

* Union manual: se dispara cuando `git` no puede realizar el `merge` ya sea porque se modificaron las mismas líneas de los mismos archivos en ambas ramas, cuando se resuelve este conflicto, `git` crea un nuevo `commit` llamado `merge commit`.

## COMANDOS PARA TRABAJAR CON RAMAS

Para crear una nueva rama, ejecutamos el comando:

> git branch `nombre-rama`

Para visiualizar las ramas, marcando en color verde la rama en la cual estamos en ese momento:

> git branch

Para realizar el cambio de rama:

> git checkout `nombre-rama`

*Nota:* Si revisamos el log con los cambios realizados en varias ramas, nos indicará la rama de cada commit que se realizó.

Para visualizar los cambios entre una rama y otra:

> git diff `nombre-rama-secundaria` `nombre-rama-principal`

Para crear una nueva rama y cambiarnos al mismo tiempo:

> git checkout -b `nombre-rama`

## COMANDOS PARA TRABAJAR CON UNIONES

### FAST-FOWARD

Para realizar las uniones de los cambios en las ramas, se debió realizar previamente el `commit`, posteriormente realizar el cambio de rama hacia la rama principal (o rama donde integraremos los cambios de la rama secundaria).

Para ello ejecutamos:

> git merge `nombre-rama-secundaria`

Para eliminar una rama:

> git branch -d `nombre-rama-a-eliminar`

### UNIONES AUTOMÁTICAS

Esta union se presenta cuando se realizaron `commits` en las dos ramas que posteriormente serán fusionadas, pero que no afectaron las mismas líneas de los mismos archivos, para ello, nos debemos posicionar en la rama donde integraremos los `commits`, que será nuestra rama principal, y la rama secundaria será la rama que vamos a fusionar con la rama principal, ejecutamos el comando:

> git merge `rama-secundaria`

Nos pedirá que ingresemos un mensaje, tecleamos la tecla `A` para editar y escribir, posteriormente tecleamos la tecla `ESC` para salir del modo editor, y finalmente tecleamos las teclas `:` (dos puntos), `w` (para guardar) y `q` (para salir) y pulsamos la tecla `ENTER`.

### UNIONES CON CONFLICTOS

Este conflicto se presenta cuando realizamos el merge de dos ramas, pero que han sido modificadas las mismas líneas de los mismos archivos en ambas ramas. En primera instancia, nos posicionamos en la rama principal que será donde integraremos los cambios de la otra rama (rama secundaria), ejecutamos:

> git merge `rama-secundaria`

Si existe conflictos, la consola nos lo indicará a través del siguiente mensaje:

~~~
Auto-merging <file-name.ext> y <Tags/file-name.ext>
CONFLICT (content): Merge conflict in <file-name.ext>
Automatic merge failed; fix conflicts and then commit the result.
~~~

Cuando realizamos el merge y nos muestra ese mensaje de conflicto, debemos buscar y abrir el archivo que presenta esos conflictos, y veremos en las líneas donde se presenta ese conflicto marcadas de la siguiente forma:

~~~
<<<<<<< HEAD
Los cambios que están en la rama principal
=======
Los cambios que están en la rama secundaria
>>>>>>> rama-secundaria
~~~

Si deseamos realizar el merge en ese mismo archivo, debemos borrar `<<<<<<< HEAD`, `=======` y `>>>>>>> rama-secundaria` e integrar los contenidos que se deseamos; y finalmente debemos realizar el `commit` con esos nuevos cambios.

**Nota:** Para resolver este tipo de conflictos, es recomendable realizarlos con la ayuda de algún plugin de los editores de código o IDEs (como Webstorm, Intellij IDEA, PyCharm, Atom, VS Code, etc.) ya que nos permiten realizar los merge de forma manual a través de una interfaz gráfica, ya que en proyectos grandes, puede ser laborioso y confuso resolverlos de la manera explicada arriba.

# TAGS

Los tags o etiquetas no son mas que una referencia a un `commit` específico en el tiempo.

Normalmente los `tag` son utilizados para marcar versiones o releases de nuestros aplicativos o programas.

El comando para crear un `tag`:

> git tag `tag-name`

Para visualizar los nombres de los `tag` creados

> git tag

Si deseamos cambiar el nombre de algún `tag`, debemos borrarlo y crearlo nuevamente; para eliminar un `tag`:

> git tag -d `tag-name`

Existe otra forma de crear `tag`, que ya es una forma un poco más explícita con anotaciones y mensajes, que es lo mas recomendado al momento de crearlos.

Para crear `tag` con anotaciones y mensajes:

> git tag -a `anotacion` -m "`Tu mensaje`"

Si deseamos marcar con un tag un `commit` específico, obtenemos el `hash` del `commit`:

> git tag -a `anotacion` `hash` -m "`Tu mensaje`"

Para visualizar la información de un `tag` en específico:

> git show `tag-name`

# CUESTIONARIO DE APRENDIZAJE

1. ¿Una rama se puede definir como una linea del tiempo de commits?

    - [x] A) Verdadero

    - [ ] B) Falso

2. ¿El `master` es un rama?

    - [x] A) Verdadero

    - [ ] B) Falso

3. ¿Todas las ramas pueden unirse al master?

    - [x] A) Verdadero

    - [ ] B) Falso

4. ¿El merge, es la unión de dos ramas?

    - [x] A) Verdadero

    - [ ] B) Falso

5. Cuando aparece la palabra `Fast Forward` después de un merge, ¿Qué significa?

    - [ ] A) Todo se realizó correctamente en el merge

    - [ ] B) Tenemos que mover el puntero del HEAD porque ya no se encuentra actualizado

    - [x] C) Unió sin problemas ya que no existían commits en la rama a la cual unimos los cambios

6. En un merge, ¿Git siempre intentará resolver los merge de forma automática?

    - [x] A) Verdadero

    - [ ] B) Falso

7. ¿Qué significa el siguiente mensaje en consola?

    ~~~
    ?? Historia.md
    ~~~

    - [ ] A) Se desconoce el tipo de archivo Historia.md

    - [x] B) El archivo Historia.md, actualmente no se le está dando seguimiento en el repositorio

    - [ ] C) El archivo Historia.md es de otra rama y no hemos realizado un merge

8. ¿Cómo creamos una nueva rama?

    - [ ] A) git checkout

    - [ ] B) git checkout -b

    - [x] C) git branch rama

    - [ ] D) git branch -ab nombre-rama