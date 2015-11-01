---
title: Docker in the Enterprise
author: ipedrazas
layout: post
date: 2015-04-01
url: /2015/04/01/docker-in-the-enterprise/
categories:
  - DevOps
  - Docker
tags:
  - devops
  - docker
  - mesos
---
One of the top questions that people ask me about Docker is by far &#8220;**_Do you think the Enterprise will use Docker?_**&#8221;

My answer has been the same since the very beginning: **Absolutely!**

It doesn&#8217;t mean it will happen soon, but it will happen. There&#8217;s just a few layers of middle management and hundreds of scared sysadmins in between, but it will happen.

I&#8217;ve migrated a few legacy enterprise applications to Docker and to me, there&#8217;s a big difference between startups using Docker and classic enterprise companies using Docker. To begin with, big enterprise companies are project and program based instead of product based. Middle management, red tape and a very low speed in general. In the technical aspects there are big differences also. Let me give you a couple of examples:

  * Firewalls.
  * Legacy applications.

Have you heard about Mesos? Docker Swarm? the ability to move containers around? well, let me tell you something, in the enterprise we have firewall rules. Firewall rules are dependant on the application but bound to the host. This means that you cannot move containers around if you cannot update firewall rules at the same time.

Solutions like Weave are perfect for this problem. Right now, I&#8217;m not sure how Docker is going to solve the networking aspect, so, I will not say that Docker will do it natively. Still, you get the point.

Another scary issue is &#8220;Legacy Applications&#8221;. Let&#8217;s face it, technical debt is bad, forgotten technical debt is pure evil. Moving these kind of applications into containers is sometimes harder than rewriting them from scratch. Issues that I&#8217;ve found while migrating legacy applications to containers can be split in two main groups:

  * Configuration issues like 
      * hard coded url and/or domains: quite typical to see hardcoded jdbc connections. You can get around it using internal DNSs or if in case of major trouble, a reverse proxy.
      * Hard coded IPs: If you&#8217;re lucky, again, Weave can give you a bit of air here.
      * Embedded credentials: hardcoding credentials is bad, but including these credentials inside of your binaries is terrible. Bad news is that it happens more often than you think. Yes, they used properties files, and yes, they put that file inside a jar, inside a war, inside an EAR&#8230; Hey, enterprise all the way down!
  * Context Issues: 
      * The system needs to run in a specific host with a specific configuration like specific IPs (ugh), specific URLs (easy), specific OS (this one was very painful)

Good news is that you have the tools to work around all these issues, and yes, you get much better on fixing them (with time, experience and tears). I don&#8217;t think that we will be seeing a &#8220;Wizard&#8221; to migrate your apps to Docker just yet but we will get there.