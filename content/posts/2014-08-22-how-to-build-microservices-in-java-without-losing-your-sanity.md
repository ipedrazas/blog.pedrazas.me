---
title: How to build (and run) Microservices in Java without losing your Sanity
author: ipedrazas
layout: post
date: 2014-08-22
url: /2014/08/22/how-to-build-microservices-in-java-without-losing-your-sanity/
categories:
  - Development
  - Docker
  - Java
---
If you haven&#8217;t heard about Microservices, [go here][1] and read about them!

For a long time I&#8217;ve writen all my microservices using Python because Java had a massive overhead (called a Servlet Container).

I&#8217;m not sure how I stumbled upon DropWizard, but it has done something that I thought impossible: My Ops side has loved Java back.

What do I want?

I want to be able to define a simple REST service and publish it with as little dependencies as possible.

Yes, I can write a JAX-RS class and run:

<pre>-&gt;%mvn jetty:run
</pre>

And my servlet container will expose my REST service&#8230; but let&#8217;s face it, deploying services like this will not take us too far. Like, are you planning to run a Jetty/Tomcat service per MicroService you want to expose??? Yes, this is where my Ops side of me was cringing big time.

True, I could bundle services and&#8230; and little by little we will find ourselves walking away from our beloved Microservices because of &#8220;Operations is complicated&#8221;. Operations is hard, we all know that, but a good architecture has to provide enough tools to satisfy our design goals without compromise our operations.

Solution? I&#8217;m sure It won&#8217;t surprise any of my followers: it&#8217;s to use **Docker and&#8230; DropWizard**!!!

How, you don&#8217;t know [DropWizard][2]? run to their website and sort that out: NOW! DropWizard does a lot of things, one of them is awesome: It allows you to write a JAX-RS class and run it from your command line. I mean, it creates a fat jar file that you can then run:

<pre>java -jar my_microservice-0.0.1-SNAPSHOT.jar server my_microservice_conf.yml
</pre>

And&#8230; it will expose your rest service in the port 8080 (and it comes with an admin freebie in port 8081 <&#8211; my ops side of me is very happy about this).

Now&#8230; what happens if you build a Docker image that runs that instruction? That you have an easy way to run/test/distribute your microservice.

<pre>sudo docker run -d -p 9094:8080 7887:8081 ipedrazas/m_dotmarks:latest
</pre>

Note that all my microservices are exposed using the default ports: 8080 and 8081 and then I re-map them when running them in Docker. Why? because it gives me more flexibility and I don&#8217;t have to worry about Ops while doing Dev (yes, developers do not decide how to run the service).

As always, I strongly recommend to run nginx as a gateway to your dockerized services. In this case our two ports 8080 and 8081 will be remmaped to 9094 (that nginx will expose using a url like api.dotmarks.net/dotmarks) and 7887 that will be used internally only.

These holidays I&#8217;ve been rewriting my [dotMarks][3] app originally in python in Java using DropWizard and I will be releasing the code once it works.

Stay tunned!

 [1]: http://martinfowler.com/articles/microservices.html
 [2]: https://dropwizard.github.io
 [3]: https://dotmarks.net/