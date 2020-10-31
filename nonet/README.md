# Nonet

Diseño y documentación de nonet, la aplicación de microbloging para la WSW

![logo](assets/logo.svg)

----

## Objetivos:

Ayudar a definir el protocolo WSW y a desarrollar la librería wswjs, mediante el descubrimiento de las necesidades que se derivan de las historias de usuario, los casos de uso y la UX.

## Framework

Se usará nextjs porque:

* es un framework fullstack
* utiliza react
* se despliega fácilmente

## Protocolo WSW

Absolutamente todo lo que tenga que ver con el protocolo WSW se hará a través de la librería wswjs.

Este no es un requisito técnico, sino estratégico.

## Características

* Dos interfaces, una privada (para el dueño del sitio), y otra pública (para los visitantes del sitio).
* Sistema de control de acceso al contenido, según la identidad de los visitantes
* Sistema de mensajería, y contacto.
* Publicaciones
* Hilos
* Reacciones
* Compartir
* Historias
* Muro principal
* Muros tematizados/contextuales
* Contenido remoto

### Interfaz privada

Se accede con usuario/contraseña.

Permite el acceso a opciones de publicación, y administración.

También habilita opciones de moderación en la interfaz pública.

### control de acceso

Se puede configurar que usuarios pueden ver una publicación.

La configuración consiste en una secuencia de reglas, que en su conjunto determinan si un usuario puede acceder o no a un sitio.

[Se empleará la librería wswjs](wswjs/control-de-acceso.md)

### Sistema de mensajería y contacto

En la interfaz privada hay un "chat" donde se reciben y envían mensajes de y a otros sitios.

En la interfaz pública de *propio.example.com* hay un formulario de contacto desde donde el sitio autentificado como *ajeno.example.com* puede enviar en nombre de *ajeno.example.com* un mensaje a

El dueño de *propio.example.com* y el dueño *ajeno.example.com* pueden chatear entre sí usando cada cual su interfaz privada.

En caso de que se de permiso a ello, los usuarios anónimos podrán enviar mensajes como *anonimo*. El formulario de contacto anónimo incluye un campo para introducir la forma de contacto para la respuesta.

### Publicaciones

Las publicaciones se crean desde la interfaz privada por el dueño del sitio

Las publicaciones tienen dos partes miniatura, y vista.

El tipo de publicación "enlace" muestra una vista previa de un enlace que no es de la WSW

#### Miniatura
La miniatura sirve para ser mostrado en los muros, y se compone de los siguientes campos:

**Obligatorios**
* title
* description
* type

**Opcionales**
* image
* video
* tags

**Automáticos**
* url
* site_name

Se puede obtener un json con la miniatura haciendo `{url}/preview`

#### Vista

La vista es lo que se muestra cuando se accede a la url.

No necesita seguir ningún estandar pues es solo para uso interno.

En nonet el view muestra la imagen/video a ancho completo, el texto sin recortar, y a continuación un muro contextual con las de las reacciones a la publicación.

La vista también contiene una sala de mensajería de la publicación, a modo de comentarios.


### Hilos

Un hilo es una secuencia de publicaciones.

El dueño del sitio crea un hilo, o añade otra publicación a un hilo, haciendo click en "continuar" desde la vista de la última publicación del hilo. (O desde la vista de cualquier publicación que no sea de ningún hilo)

Las miniaturas que formen parte de un hilo tendrán el campo thread que es una url que devuelve todas las publicaciones del hilo, y el campo position que indica qué posición ocupa la publicación actual en el hilo

### Reacciones

Una reacción es una publicación que está vinculada a otra, la cual puede estar en otro sitio.

La miniatura incluye el campo: `about` con una url a la publicación a la cual reacciona

La publicación a la que se reacciona puede contabilizar los tags de sus reacciones, y mostrar los tags más comunes con su cantidad.

De este modo, los "me gusta", "me encanta", etc. surgen de forma orgánica

Se puede reaccionar a un enlace que no es de la WSW.

### Compartir

El dueño del sitio *propio.example.com*, puede en el sitio *ajeno.example.com* click en el botón "compartir" de cualquier publicación, y la miniatura aparecerá en el muro de *propio.example.com*

En el momento de compartir, puede seleccionar en qué muros de *propio.example.com* quiere compartirlo

Para compartir una url que no es una publicación de la WSW, el dueño de *propio.example.com* tiene que ir a su sitio, y crear una publicación de tipo enlace.

### Historias

Las historias están de moda, y el objetivo de WSW es aportar toda la funcionalidad de las redes sociales, así que hay que añadir historias.

Una historia es una publicación efímera y limitada:

Una historia no admite hilos.
Su vista no tiene muro contextual ni sala de chat.


### Muro principal

El muro principal muestra cronológicamente todas las publicaciones que puede ver el visitante actual, excepto las que hayan sido excluídas del muro de forma explícita.

### Muros tematizados/contextuales

Los muros temátizados/contextuales muestran cronológicamente todas las publicaciones que cumplen los requisitos del muro.


### Contenido remoto

Un muro de la WSW puede mostrar en sus muros miniaturas de publicaciones de sitios remotos.

Bien porque:

1. El dueño haya compartido de forma explícita una publicación remota en el muro, bien porque
2. El dueño ha incluído en el muro una suscripción a un muro remoto, (con la posibilidad de añadir filtros por etiquetas etc)
3. Se trata del muro contextual a una publicación, y el contenido remoto son reacciones a la publicación

La sección historias también puede mostrar historias remotas, de sitios cuyas historias está siguiendo.

Tanto los muros como las historias admiten un parámetro para la recursividad del contenido remoto, que indica la distancia a la que puede estar un contenido.

Recursividad 0 indica que no se mostrarán el contenido de ningún sitio remoto
Recursividad 1 indica que se mostrará el contenido de los sitios a los que sitio actual sigue
Recursividad 2 indica que también se mostrará el contenido de los sitios a los que los sitios anteriores siguen
