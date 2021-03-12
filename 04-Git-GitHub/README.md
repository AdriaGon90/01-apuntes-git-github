# CONCEPTOS BÁSICOS

`Git` y `GitHub` son dos cosas completamente diferentes. `GitHub` es una plataforma donde podemos realizar un respaldo de nuestro repositorio, convirtiéndolo así en un **`repositorio remoto`**. La idea de esto es que interactuemos con ese servidor para asegurarnos de que nuestro proyecto esté a salvo, porque puede que nuestro equipo físico (computadora) o algún componente de este falle o se dañe en algún momento (o incluso si perdemos este equipo); inclusive nos permite trabajar el proyecto de forma colaborativa con otros miembros del equipo.

`GitHub` es una plataforma de desarrollo colaborativo de software para alojar proyectos.

Otro concepto que utilizamos cuando trabajamos con repositorios remotos es el **`push`**, que consiste en integrar los cambios del **`repositorio local`** al **`repositorio remoto`**.

Para que los miembros del equipo puedan obtener los últimos o nuevos cambios del **`repositorio remoto`** en sus **`repositorios locales`**, deben ejecutar el comando **`pull`**. Este comando consiste en actualizar o mantener actualizado el **`repositorio local`** con respecto al **`servidor remoto`**.

Cuando estamos en nuestro **`repositorio local`** y queremos agregar lo que se conoce como un **`origen remoto`**, se utiliza el siguiente comando:

> git remote add origin `url`

Detallaremos algunas palabras que conforman este comando

* add: simplemente que queremos agregar un nuevo remote, ya que podemos tener varios remotes en un mismo repositorio.

* origin: es el nombre que queremos darle a ese repositorio, por lo que si deseamos agregar otro repositorio, podemos asignarle otro nombre, origin es un estándar.

* url: es la url donde está alojado el repositorio.

Si deseamos revisar los remotos o las fuentas remotas que tenemos agregadas a este repositorio, ejecutamos el siguiente comando:

> git remote -v

Para subir nuestro **`repositorio local`** al **`origen remoto`**, usamos el comando:

> git push -u origin master

Detallaremos cada palabra que conforman este comando:

* origin: es el nombre del repositorio, así como master es un estándar para las ramas, origin lo es para nombres del remote.

* master: es el nombre de la rama a la que deseamos enviar al repositorio.

* -u: nos ayuda a que la próxima vez que deseemos hacer un push no necesitamos especificar la rama, ya que de este modo, se está estableciendo la rama master por defecto para integrar los cambios.