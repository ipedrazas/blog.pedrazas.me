---
title: Local Taiga with Docker
author: ipedrazas
layout: post
date: 2014-10-08
url: /2014/10/08/local-taiga-with-docker/
categories:
  - Docker
tags:
  - docker
  - taiga
---
Recently [Taiga.io][1] was announced. As they describe themselves:

> Free. Open Source. Powerful. **Taiga** is a project management platform for startups and agile developers & designers who want a simple, **beautiful** tool that makes work truly enjoyable.

It didn&#8217;t take me too long to realise that it would be a nice preparation to dockerize taiga for my next &#8220;50 Shades of Docker&#8221; workshop at the Spanish PyCon.

I have to reckon that it&#8217;s been more challenging than expected. I would blame the developers, of course  <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />but truth is that turning taiga into a docker container is quiet simple (specially since they provide all the scripts to build a taiga platform in one single host).

Unfortunately for me, I like distributing things&#8230; so I decided to run one single process per container, so I would have several containers.

The scripts installed Redis and RabbitMQ which are not in use (just yet), so teh final version has 3 containers:

  * Postgres
  * <del>RabbitMQ</del>
  * <del>Redis</del>
  * Taiga-back
  * Taiga-front

Another problem I found is that the front-end is not distributable. It means, you have to build it&#8230; so, I created another container that does the build.

If you want to run taiga in your local machine, you can do so by using this script:

<pre>sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
sudo sh -c "echo deb https://get.docker.io/ubuntu docker main &gt; /etc/apt/sources.list.d/docker.list"
sudo apt-get update -y
sudo apt-get install -y lxc-docker

sudo mkdir -p /data/postgresql

sudo docker run -d --name postgres    -p 5432:5432  -v /data/postgresql:/var/lib/postgresql/data postgres
sudo docker run -d --name taiga-back  -p 8001:8001  --link postgres:postgres ipedrazas/taiga-back
sudo docker run -d --name taiga-front -p 80:80 -p 8000:8000 --link taiga-back:taiga-back ipedrazas/taiga-front


sudo docker run -it --link postgres:postgres --rm postgres sh -c "su postgres --command 'createuser -h "'$POSTGRES_PORT_5432_TCP_ADDR'" -p "'$POSTGRES_PORT_5432_TCP_PORT'" -d -r -s taiga'"
sudo docker run -it --link postgres:postgres --rm postgres sh -c "su postgres --command 'createdb -h "'$POSTGRES_PORT_5432_TCP_ADDR'" -p "'$POSTGRES_PORT_5432_TCP_PORT'" -O taiga taiga'";
sudo docker run -it --rm --link postgres:postgres ipedrazas/taiga-back bash regenerate.sh
</pre>

If, like me, you want to run it in AWS or Digital Ocean, you will need first to create a DNS and build Taiga using that host (yes, the api url is hardcoded&#8230; so, you have to build it using your hostname).

Having said that, I want to congratulate the whole Taiag team for the product and the support they have been giving (not only to me, but to many others). **Well done, guys!**

All the code is in my [Github Repo][2], in case that anyone wants to play with it. If you have any doubts, [just ask][3] <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

 [1]: https://taiga.io/
 [2]: https://github.com/ipedrazas/taiga-docker
 [3]: https://twitter.com/ipedrazas