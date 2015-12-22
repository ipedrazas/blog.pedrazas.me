title: Thoughts on Docker
date: 2014-06-18
slug: /2014/06/18/ditto-docker/

[<img class="aligncenter size-full wp-image-237" src="http://ivan.pedrazas.me/wp-content/uploads/2014/06/docker-logo.png" alt="docker logo" width="400" height="400" />][1]

&nbsp;

> <span style="font-style: italic; color: #574d4d;">Docker is an open-source project to easily create lightweight, portable, self-sufficient containers from any application</span>

<div id="wmd-preview-section-3" class="wmd-preview-section preview-content" style="color: #162029;">
  <h3 id="vagrant">
    Vagrant
  </h3>

  <p>
    It’s not a secret that <a href="http://www.vagrantup.com/" target="_blank">Vagrant</a> changed my life as a developer. I&#8217;m sure that if you know me, you will have heard me talking about how great vagrant is.
  </p>

  <p>
    Vagrant, in case that you don’t know, it’s a little tool that allows you to develop locally an execute your code inside a Virtual Machine. This, of course, gives you the advantage of not needing to setup your own machine (a painful activity that we all have been suffering in silence for years). In a nutshell, vagrant helps you to decouple your development environment from your workstation.
  </p>
</div>

<div id="wmd-preview-section-4" class="wmd-preview-section preview-content" style="color: #162029;">
  <h3 id="after-vagrant">
    After Vagrant
  </h3>

  <p>
    Now, we cannot say that there’s a new guy in the block, because <a href="https://www.docker.com" target="_blank">Docker</a> has been around for a while (ehem…) but we do can say that Docker is not only going to change my life but it’s about to change everyone’s life.
  </p>

  <p>
    <strong>Docker will change the way we run and distribute applications.</strong>
  </p>

  <p>
    I don’t think I’m the right person to explain what Docker is. I can tell you how it has changed the way I work, or to put it differently, to change the things I do, but if you really want to understand how Docker works, it&#8217;s better you look at the resources at the bottom of the page.
  </p>
</div>

<div id="wmd-preview-section-5" class="wmd-preview-section preview-content" style="color: #162029;">
  <div class="se-section-delimiter">
  </div>

  <h3 id="enter-docker">
    Enter Docker
  </h3>

  <p>
    Docker is a linux container that allows you to run an application with a simple &#8220;RUN&#8221; command. Yes, there are a few other parameter but the idea is that you can launch an app (that it&#8217;s self contained) with a single command.
  </p>

  <p>
    If you haven&#8217;t suffered the enlighting experience of trying to run a web application like WordPress, for example, you don&#8217;t know how complex things can turn very quickly. The ammount of software and things that have to be &#8220;in place&#8221; and configured properly is painful. How Docker can help you there? well, someone, for example me, will spend some time building a Docker image so people like you can just run it with a simple command.
  </p>

  <p>
    Docker will lower the sys admin barrier. People who doesn&#8217;t know much about how to set up a web server suddenly can run their own wordpress instance (which is the idea behind of all those VPS with &#8220;one-click install&#8221;).
  </p>

  <p>
    But there&#8217;s more, with Docker creating a cluster it’s easy. Ok, not trivial, but very feasible. Do you remember those complicated architectures you have seen in books? now you can build them in your laptop. I agree, a cluster under work load behaves very different than a cluster you could run in your workstation, but let’s face it, the fact that you can use docker to build a cluster of machines will help to speed up the future development of applications and solutions.
  </p>

  <p>
    So, what I have been doing with Docker that has changed the way I see things?
  </p>

  <p>
    well, I’m writing<a href="http://dotmarks.net"> a little tool </a>to manage bookmarks. The App has two provisioning tools. Vagrant (of course) and ansible scripts to deploy and configure the app in a VPS (like <a href="https://www.digitalocean.com/?refcode=56ae0600c4bc">Digital Ocean</a>, for example).
  </p>
</div>

<div id="wmd-preview-section-6" class="wmd-preview-section preview-content" style="color: #162029;">
  <h3 id="dotmarks">
    .dotMarks
  </h3>

  <p>
    The whole idea of this app is to self-host your bookmarks. Yes, I know, nobody seems to use bookmarks nowadays but that&#8217;s a different story. The idea is that you run it in your machine… and because of that you can see how Docker can make my life much easier: It’s like giving people an executable that they can run. Everything is self-contained and pre-configured. It’s perfect, it&#8217;s Awesome!
  </p>

  <h3 id="dotmarks">
    What about me?
  </h3>

  <p>
    By default I run 3 docker containers in my machine. One with the <a href="https://github.com/crosbymichael/dockerui" target="_blank">Dockerui</a> (A web interface for Docker), <a href="https://registry.hub.docker.com/u/ipedrazas/elasticsearch/">One with ElasticSearch</a> and one with MongoDB. I still use Vagrant to develop and run .dotMarks, but once it&#8217;s ready, I can tell you, it will run in its own docker container.
  </p>

  <div id="attachment_240" style="width: 310px" class="wp-caption aligncenter">
    <a href="http://ivan.pedrazas.me/wp-content/uploads/2014/06/Screenshot-from-2014-06-19-004257.png"><img class="aligncenter size-medium wp-image-267" src="http://ivan.pedrazas.me/wp-content/uploads/2014/06/Screenshot-from-2014-06-19-004257-300x97.png" alt="Screenshot from 2014-06-19 00:42:57" width="300" height="97" /></a>

    <p class="wp-caption-text">
      Marvel plugin for ElaasticSearch showing the state of my system
    </p>
  </div>
</div>

<div id="wmd-preview-section-7" class="wmd-preview-section preview-content">
  <h3 id="where-do-we-go-from-here" style="color: #162029;">
    Where do we go from here
  </h3>

  <p style="color: #162029;">
    Good question. As I see it, there are three areas that are not under the Docker Radar but I think that once the right people understand the potential it will go through as a freight train:
  </p>

  <ul style="color: #162029;">
    <li>
      <strong>Education:</strong> From the newbies that they need a (safe) playground to land, to the more experienced guy who wants to understand complex architectures, Docker has a huge potential in (self) education.
    </li>
    <li>
      <strong>Application Distribution:</strong> WebApps are awesome, but distributing them is quite a pain… in fact, not many people do that because let&#8217;s face it, it&#8217;s hard. It’s not only shipping the code, it&#8217;s configuring the servers, and running the whole lot and… it’s complicated. Docker will bring a standard way of distributing applications. From wordpress to the latest trendy idea someone pushes to Github&#8230; I&#8217;m sure developers will start including Dockerfiles to their repos once they understand the wonders of linux containers
    </li>
    <li>
      <strong>Support and Quality Control:</strong> Suddenly, testing applications in the real architecture locally is suddenly possible. Do you have customers with your system installed in-house. Replicating their environtment is a matter of linking images in a Dockerfile.
    </li>
  </ul>

  <p style="color: #162029;">
    But don&#8217;t get too carried away, Docker has its amaizing Use Cases but it&#8217;s not for everyone. Yes, developers and SysAdmins love it&#8230; time will say if it will become mainstream.
  </p>

  <p style="color: #162029;">
    Want to know more? look at these resources:
  </p>

  <ul>
    <li>
      <a href="http://www.youtube.com/watch?v=pts6F00GFuU" target="_blank">Docker at Spotify</a>
    </li>
    <li>
      <a href="http://en.wikipedia.org/wiki/Docker_(software)" target="_blank">Docker entry in Wikipedia</a>
    </li>
    <li>
      <a href="https://www.youtube.com/watch?v=ZzQfxoMFH0U" target="_blank">What it&#8217;s Docker</a>
    </li>
    <li>
      <a href="http://www.slideshare.net/fasgoncalves/hypervisor-versus-linux-containers">Future of Aplication Delivery</a>
    </li>
  </ul>
</div>

 [1]: http://ivan.pedrazas.me/wp-content/uploads/2014/06/docker-logo.png
