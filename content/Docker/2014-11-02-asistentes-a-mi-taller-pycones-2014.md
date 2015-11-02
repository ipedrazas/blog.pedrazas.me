title: Asistentes a mi taller – PyCoNes 2014
date: 2014-11-02
slug: /2014/11/02/asistentes-a-mi-taller-pycones-2014/
tags: Docker, Spanish, pycones

Si aún no tienes claro si vas a venir a mi taller o no, [lee esto][1], y luego sigue <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

Parece que la conexión de internet no va a ser para tirar cohetes&#8230; nada que no hayamos sufrido todos alguna vez. Así que, para minimizar el impacto de una mala conexión hay dos opciones:

Usar una conexion ssh a una máquina virtual en la nube (AWS, [Digital Ocean][2], Linode&#8230; o vuestro proveedor de máquinas virtuales favorito). Con ésto conseguimos que el tráfico ocurra entre esa máquina y docker, limitando el tráfico desde la sala a un puñado de conexiones ssh.

Otra opción es usar vuestro ordenador y descargar antes las imágenes que se van a usar. Ésta opción es más agresiva con la red por que cuando hagamos un build habrá imágenes que no se cachearán y habrá que descargarlas&#8230; y petaremos la red.

Si váis a usar vuestro ordenador, es recomendable que os instaléis la versión 1.3 de docker y hagáis pull de las siguientes imágenes. En negrita están las 5 imágenes base para desarrollo python:

**docker pull ubuntu**

docker pull tpires/neo4j

**docker pull dockerfile/redis**

docker pull dockerfile/mongodb

docker pull ipedrazas/elasticsearch

docker pull poklet/cassandra

**docker pull python:2**

**docker pull python:3**

docker pull nornagon/postgres

docker pull clue/ttrss

**docker pull postgres**

docker pull ipedrazas/taiga-front

docker pull ipedrazas/taiga-back

docker pull php:5.6-apache

docker pull node:0.10-onbuild

La lista no es definitiva, pero cubre mucho camino. A los que no uséis Linux, tenéis que instalar Boot2Docker y si no recuerdo mal, la versión 1.3 ya permite montar volúmenes entre host y contenedor, así que no tendréis problemas para seguir el taller.

Si tenéis preguntas o queréis que hable de algún tema en concreto, mandadme un email, o dadme un toque por [twitter][3].

El taller está pensado para que la gente salga con una idea clara de lo que se puede hacer con Docker y por donde se puede empezar. Todo el material estará colgado en github.

Nos vemos el Sábado!

**Nota**: ya empezamos otra vez con las notitas?

**Nota 2**: No, el código de DO no es por que &#8220;espere forrarme&#8221;, ni mucho menos.  O sea, en serio??

**Nota 3**: a ver cuántos errores y tildes encuentra [Yamila][4]&#8230;

Nota 4: Gracias a [Álex][5] por corregirme 723 errores, lo menos <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

 [1]: http://ivan.pedrazas.me/?p=364
 [2]: https://www.digitalocean.com/?refcode=56ae0600c4bc
 [3]: https://twitter.com/ipedrazas
 [4]: https://twitter.com/yamila_moreno
 [5]: https://twitter.com/agonzalezro
