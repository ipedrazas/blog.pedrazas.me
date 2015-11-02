title: Distance to Mesos
date: 2015-06-16
slug: /2015/06/16/distance-to-mesos/
tags: DevOps, Mesos, devops, docker, mesos

I&#8217;ve been wanting to write this for a while but it seems that it&#8217;s never the right time, so tonight, I&#8217;m biting the bullet and not going to bed until I write it all.

I&#8217;ve notice that lately people don&#8217;t talk about Docker so much. Nothing to complain about, really, but what happens is that people has shifted to talk about <span id=":1u0.1" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Kubernetes</span> and [<span id=":1u0.2" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>][1]&#8230; Sigh.

One of the questions I&#8217;ve asked more frequently is &#8220;How to move to <span id=":1u0.3" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>&#8230; and is it worth it?&#8221;

There&#8217;s no straight answer to that question really. I don&#8217;t like to say &#8220;it depends&#8221; because it seems that you&#8217;re trying to run away, but in this case it really does.

It&#8217;s a bit like asking &#8220;how to go to the London Eye&#8221;, first thing I need to find out is to know where you&#8217;re travelling from because it is not the same to come from Liverpool than from Liverpool street&#8230; Distance is important because I can assume that if you come from Liverpool you will arrive to London <span id=":1u0.4" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Euston</span> (but I might be wrong, and you might be travelling by car instead of train&#8230;).

Anyway, it doesn&#8217;t matter where you come from, I&#8217;m sure you will manage to find the way to the London Eye, and if not&#8230;  just ask. There&#8217;s plenty of people happy to help.

With <span id=":1u0.5" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> you have a similar problem, you see? it&#8217;s not the same to come from a <span id=":1u0.6" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">multi</span>-monolithic architecture with more silos than the <acronym title="Ministry of Defense">MOD</acronym>, than to have a very lean service based architecture with containers and service discovery already in place.

So, are containers important? strictly speaking: No, however, by using containers you can leverage some very cool functionality that systems like <span id=":1u0.7" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> have.

Service Discovery, anyone? let&#8217;s put it like this, it does not matter how you build software, using SD should be part of it. Period.

There are 3 big blocks in any application:

  * <span id=":1u0.8" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Runtime</span>: this is what we run. From a web application to a queue worker, it doesn&#8217;t really matter. It&#8217;s that thing that (when it works) does its job.
  * Configuration: this is what the thing that runs need to run (the way we want). It can be credentials, external resources, addresses, whatever that makes our <span id=":1u0.9" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">runtime</span> to be flexible.
  * Context: this is usually forgotten (until it&#8217;s too late) and it&#8217;s where your <span id=":1u0.10" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">runtime</span> runs and all those bits and pieces that you need to be run it there. Firewall rules, Security groups, etc.

These blocks do not depend on what you run: Java, python, <span id=":1u0.11" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">javascript</span>&#8230; or where you run it: Amazon, Azure&#8230; they are 3 blocks that every software development has to define&#8230; what about in <span id=":1u0.12" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>?

Well, <span id=":1u0.13" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>, as a software, will need these 3 blocks: we have the <span id=":1u0.14" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">runtime</span>, <span id=":1u0.15" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">mesos</span>, marathon, <span id=":1u0.16" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">cronos</span>&#8230; the different configuration files these young lads use, and where do we run <span id=":1u0.17" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>: our <span id=":1u0.18" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">datacenter</span>, <span id=":1u0.19" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">AWS</span>, Google&#8230;

The interesting thing is that inside <span id=":1u0.20" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> those 3 blocks are somehow diluted.

To begin with, Context is <span id=":1u0.21" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>&#8230; To the point that once you have <span id=":1u0.22" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> you don&#8217;t have environments anymore. Your application have different <span id=":1u0.23" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">datasources</span> (Dev, Test, Prod) and different priorities, but it&#8217;s unlikely that you will have a <span id=":1u0.24" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> cluster per environment (and if you do, there&#8217;s something very fundamental that you didn&#8217;t get right).

What makes <span id=":1u0.25" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> very attractive is that &#8220;he knows&#8221; so you don&#8217;t have to. But to be able to do that your applications have to be built in a way that it&#8217;s safe for <span id=":1u0.26" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> to move around (here it&#8217;s where containers and service discovery can be very handy).

As I said before, people keep asking me about <span id=":1u0.27" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> and my answers always point towards the same place: maybe <span id=":1u0.28" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span> is not for you, but moving to containers and using service discovery will make your applications to work better and look, once you&#8217;re there, you&#8217;re not that far from <span id=":1u0.29" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>.

In summary, you should not aim to use Service Discovery and containers as a <span id=":1u0.30" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">pre</span>-condition to <span id=":1u0.31" class="J-JK9eJ-PJVNOc" tabindex="-1" data-g-spell-status="2">Mesos</span>, you should do it because it will make your life (and the life of people dealing with your systems) better.

Not everybody is Google, but everybody should aim to run applications like Google does.

 [1]: http://mesos.apache.org/
