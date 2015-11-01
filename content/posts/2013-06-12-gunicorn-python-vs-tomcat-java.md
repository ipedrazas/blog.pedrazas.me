---
title: (Gunicorn + Python) vs (Tomcat + Java)
author: ipedrazas
layout: post
date: 2013-06-12
url: /2013/06/12/gunicorn-python-vs-tomcat-java/
categories:
  - Python
tags:
  - dev
  - gunicorn
  - java
  - python
  - tomcat
---
Writing an app it&#8217;s one thing, deploying an app it&#8217;s a very different matter. Last night we were discussing about the differences between deploying Java apps and deploying python apps. I must admit that I never put my head to look at how python apps were deployed, so this morning I decided to take a look and&#8230; yes, deploying a java app in Tomcat is still easier than deploying a python app with gunicorn (let the troll wars begin!). True, to deploy an app with gunicorn you just need this:

`gunicorn --log-level=debug -c gunicorn.conf hello:app`

or if just &#8220;gunicorn hello:app&#8221; which is great, it couldn&#8217;t be more simple!

But&#8230; Imagine this scenario: we create 2 apps, one in Java, one in python, let&#8217;s say, using Flask (I could have said Django&#8230; but let&#8217;s keep it simple).

Now I have my BIG FAT SERVER where I have my tomcat instance and my gunicorn instance running.

  * To deploy the java app I need to create a war file and upload it using the admin page&#8230; et voila, we have java app deployed.
  * To deploy the python app I need to ssh to that server, scp the python app files over, and run that line from above.

Fair enough, it&#8217;s not that different and gunicorn kicks ass, but let&#8217;s be honest here, even if we had to ssh and copy over the war file&#8230; just by putting it in the right directory it will self-deploy. Don&#8217;t get me wrong, I do love python and when I can, I much rather use python-gunicorn than any of their java cousins, but we have to be fair with the fat jvm relatives, haven&#8217;t we?

This time, Java wins!