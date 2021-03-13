# GITHUB

## CONCEPTOS BÁSICOS

`Git` y `GitHub` son dos cosas completamente diferentes. `GitHub` es una plataforma donde podemos realizar un respaldo de nuestro repositorio, convirtiéndolo así en un **`repositorio remoto`**. La idea de esto es que interactuemos con ese servidor para asegurarnos de que nuestro proyecto esté a salvo, porque puede que nuestro equipo físico (computadora) o algún componente de este falle o se dañe en algún momento (o incluso si perdemos este equipo); inclusive nos permite trabajar el proyecto de forma colaborativa con otros miembros del equipo.

`GitHub` es una plataforma de desarrollo colaborativo de software para alojar proyectos.

Otro concepto que utilizamos cuando trabajamos con repositorios remotos es el **`push`**, que consiste en integrar los cambios del **`repositorio local`** al **`repositorio remoto`**.

Para que los miembros del equipo puedan obtener los últimos o nuevos cambios del **`repositorio remoto`** en sus **`repositorios locales`**, deben ejecutar el comando **`pull`**. Este comando consiste en actualizar o mantener actualizado el **`repositorio local`** con respecto al **`servidor remoto`**.

Cuando estamos en nuestro **`repositorio local`** y queremos agregar lo que se conoce como un **`origen remoto`**, se utiliza el siguiente comando:

> git remote add origin `url`

Detallaremos algunas palabras que conforman este comando

* add: simplemente que queremos agregar un nuevo remote, ya que podemos tener varios remotes en un mismo repositorio.

* origin: es el nombre que queremos darle a ese repositorio, por lo que si deseamos agregar otro repositorio, podemos asignarle otro nombre, origin es un estándar.

* url: es la url donde estará alojado el repositorio.

Si deseamos revisar los remotos o las fuentas remotas que tenemos agregadas a este repositorio, ejecutamos el siguiente comando:

> git remote -v

Para subir nuestro **`repositorio local`** al **`origen remoto`**, usamos el comando:

> git push -u origin master

Detallaremos cada palabra que conforman este comando:

* origin: es el nombre del repositorio, así como master es un estándar para las ramas, origin lo es para nombres del remote.

* master: es el nombre de la rama a la que deseamos enviar al repositorio.

* -u: nos ayuda a que la próxima vez que deseemos hacer un push no necesitamos especificar la rama, ya que de este modo, se está estableciendo la rama master por defecto para integrar los cambios.

Si en nuestro **`repositorio local`** tenemos `tag`, pero no se reflejan en el **`repositorio remoto`**, ejecutamos el comando:

> git push --tag

Si en el **`repositorio remoto`** tenemos cambios nuevos que no existen en nuestro **`repositorio local`**, debemos descargar esos cambios, para ello, ejecutamos el comando:

> git pull

Esto se recomienda realizar cada vez que vamos a trabajar nuevos cambios en nuestro **`repositorio local`** y antes de integrarlos al **`repositorio remoto`**, para así evitar posibles conflictos y trabajar con las versiones mas recientes del repositorio.

Si en nuestro **`repositorio local`** tenemos cambios nuevos que deseamos integrar al **`repositorio remoto`**, ejecutamos el comando:

> git push

Cuando necesitamos copiar todo el **`repositorio remoto`** para comenzar a trabajar en otra computadora, o si deseamos compartirle el repositorio a otro compañero de trabajo, lo que debemos realizar es una copia del repositorio utilizando el `clone`, para ello, debemos copiar la *url* que nos genera el repositorio remoto desde el servidor y ejecutar el comando:

> git clone `url` `nombre-carpeta`

El `nombre-carpeta` será la carpeta donde se descargará todo el repositorio, si esa carpeta no existe la creará. En `nombre-carpeta` es opcional, por lo que si ejecutamos el comando sin especificar el nombre, creará una carpeta con el nombre del repositorio.

### GIT FECH VS GIT PULL

Ambos comandos descargan cambios desde el **`repositorio remoto`** al **`repositorio local`**, pero con la gran diferencia que `pull`:

> git pull

Intentará realizar el `merge` de manera automática en nuestro **`repositorio local`** con los nuevos cambios, pero en caso de existir un conflicto, entramos en un estado de conflicto en `git`, por lo que tendrémos que atender esos conflictos del mismo modo que lo resolvimos en el `merge` entre ramas. El comando `fetch`:

> git fetch

Solo descarga los cambios pero no realiza el `merge`, esto nos sirve para revisar las diferencias que podemos encontrar entre el **`repositorio remoto`** y el **`repositorio local`** a través del comando `diff`, y finalmente, si deseamos aceptar los cambios, debemos realizar el merge con el comando:

> git merge

## FORMAS DE COLABORACIÓN

`Git Hub` nos ofrece, a través de sus herramientas, una forma de trabajo colaborativa, donde los diferentes integrantes de un proyecto, pueden realizar e integrar cambios a los repositorios de una manera ordenada, organizada y segura, con la finalidad de presentar los mínimos conflictos posibles (los conflictos siempre van a estar presentes, la questión aquí es, ¿cómo hacemos frente a ellos?). Habíamos comentado en los puntos anteriores, que si uno o varios integrantes desean tener el proyecto en sus equipos personales, deben realizar un `clone` en sus dispositivos, realizar los cambios y subirlos a través del `push`; pero ¿qué sucedería si, uno de esos colaboradores sube un cambio erróneo que afecta gravemente al proyecto?, todos los demás integrantes descargan el cambio en sus **`repositorios locales`** y el error estará presente en todos **`repositorios locales`** y en el **`repositorio remoto`**, evidentemente que git nos ayuda revertir los cambios o corregirlos a través de comandos, pero es un tiempo que se tiene que inventir en la solución del problema. Otra situación es, si deseamos colaborar en un proyecto al cual no tenemos acceso, solo podemos clonarlo y trabajarlo localmente pero no podemos integrarlos al remoto, por lo que tendremos que levantar una solicitud con los cambios para que sean integrados al remoto.

La forma en que `GitHub` nos recomienda trabajar es a través del `fork`, que consiste en que cada colaborador realizará una copia del **`repositorio remoto del dueño`**, conocido como **`repositorio central`** o **`upstream`**, desde su cuenta, (existen otras herramientas que te permiten colaborar de esta forma, como GitLab, BitBucket, entre otras), para así cada colaborador tenga su copia en su cuenta de `GitHub`, y desde ella  realizar el `clone`, de esta manera pueden realizar cambios y subirlos al **`repositorio remoto personal`**, probar y validar para descartar posibles errores (como en la situación que les planteé al principio), y solicitar integrar los cambios al **`upstream`** ó **`repositorio central`** a través de un `pull request`.

### FORK

El `fork` es una copia o un `clone` del **`repositorio remoto central`** (**`upstream`**), el cual obtuvimos desde la cuenta del dueño, en nuestro **`repositorio personal`**.

El **`repositorio remoto del dueño`** se conoce como el **`upstream`**, y el **`repositorio remoto personal`** se conoce como el `fork`.

Para realizar el `fork`, debemos ingresar al repositorio en la cuenta del dueño en `GitHub`, pero con nuestra sesión personal iniciada; en la parte superior derecha, hay una serie de botones, uno de ellos se llama `Fork`. Al darle clic a ese botón realizará el `clone` hacia tu **`servidor remoto`**, lo que quiere decir que, si ingresas a tu cuenta personal, en la sección de repositorios, verás que tienes el repositorio de cliente al cual realizaste el `fork`. Posteriormente, puedes realizar el `clone` hacia tu dispositivo personal para tenerlo localmente.

### PULL REQUEST

Es una solicitud que realizamos al **`dueño del upstream`** para integrar los cambios que tenemos en nuestro **`fork`**.

Para solicitar o levantar un `pull request`, después de realizar el `push` al **`fork`**, en la ventana principal del repositorio en `GitHub`, hay un botón que se llama *New Pull Request*, al presionarlo, nos mostrará una pantalla donde podemos visualizar los cambios que se enviarán e integrarán para que se integren en el **`upstream`**. Cuando estemos seguros de los cambios a enviar, presionamos el botón *Create pull request*, nos solicitará un mensaje, este mensaje debe ser coherente con los cambios que se están enviando, finalmente presionamos el botón *Create pull request*. Ahora, queda esperar la aprobación/rechazo de parte del dueño del **`upstream`**. En cualquiera de los casos, notificará al colaborador que realizó la solicitud, por correo la acción que el dueño del **`upstream`** haya realizado.

### ACTUALIZANDO EL FORK

Este proceso consiste en mantener actualizado el **`fork`** respecto a los cambios que se van integrando en el **`upstream`**. Para ello, debemos realizar un `pull` del **`upstream`** en el **`repositorio local`**, por lo que tenemos que agregar, inicialmente, un nuevo `remote` que apunte al **`upstream`**, para ello ejecutamos el comando:

> git remote add upstream `url-repositorio-central`

**NOTA:** Este comando solo lo ejecutamos una vez, que será la primera vez que descarguemos cambios.

Posteriormente realizamos un `fetch` o un `pull` para descargar los cambios y así actualizar el `repositorio local`.

> git fetch upstream `rama`

ó

> git pull upstream `rama`

Si ejecutamos el `pull` nos pedirá un mensaje de ese `commit` que generará, podemos cambiarlo o dejar el que viene por defecto. Para salir del editor, presionamos la tecla `ESC`, tecleamos dos puntos **:**, luego `W` para guardar, `Q` para salir y finalmente presionamos `INTRO`.

Finalmente, debemos integrar esos nuevos cambios al **`fork`**, para ello, realizamos el `push`.