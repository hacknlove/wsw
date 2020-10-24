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
* Sistema de permisos, de modo que el contenido que la interfaz pública muestra a un visitante dependa de la identidad del usuario (incluído el caso no haberse identificado)
* Sistema de mensajería, (público para que el visitante pueda escribir al sitio, privado para que el dueño pueda chatear con cualquier sitio de la WSW)
