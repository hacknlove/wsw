# Protocolo WSW

Diseño y documentación del protocolo WSW

![logo](../assets/logo.svg)

----

## Características:

* sitio = identidad
* interoperabilidad sin configuración
* versionable
* extensible

## sitio = identidad

**Tu sitio web de la WSW es tu identidad en la WSW, y tu proveedor de autentificación:**

Si necesitas loguearte en el sitio *ajeno.example.com*, por ejemplo para acceder a contenido privado, no necesitas crear o tener un usuario en el sitio *ajeno.example.com* sino que te identificas en *ajeno.example.com* como *propio.example.com*.  

**Los sitios de la WSW son mono-usuario en lo que respecta a la identidad y la autentificación dentro de la WSW.**

No hay nada que impida a un sitio de la WSW tener internamente multiples usuarios, pero dichos usuarios no tienen identidad en WSW. La identidad del sitio es única aunque sea una identidad colectiva.

Por ejemplo el sitio ficticio *lossieteenanitos.example.com* tiene 7 usuarios que pueden entrar a su panel de administración a crear contenido y firmarlo cada cual con su propio nombre. Pero dentro de la WSW, no existen ni *gruñón@lossieteenanitos.example.com* ni *dormilón@lossieteenanitos.example.com* ni *mudito@lossieteenanitos.example.com*. Solo existe *lossieteenanitos.example.com* 

## Interoperabilidad sin configuración

No sería escalable que cada sitio de la WSW tuviera que obtener a priori un api key, client id y secret de cada otro sitio de la WSW con el que va a interactuar.

Por ejemplo, el sitio *desconocido.example.com* quiere autentificarse en mi sitio *propio.example.com*. No tendría sentido que el protocolo exija que hayamos previamente configurado urls de redirección autorizadas, o secretos compartidos.

WSW tiene que funcionar entre cualesquiera dos sitios que implementen el protocolo, sin ninguna otra condición previa.

## Versionable
