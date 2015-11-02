title: Vagrant, second round
date: 2013-06-18
slug: /2013/06/18/vagrant-second-round/
tags: Development, clinker, vagrant

A few developers have asked me if I could explain a little bit more about what makes [Vagrant][1] such an awesome tool and how different is to work with any of the other virtual machines solutions like VmWare.

[Vagrant][1] is made and brewed for developers by developers. The idea is to speed up and reduce friction as much as possible. It is not about building infrastructure, it&#8217;s about developing for that infrastructure.

Perhaps this is the take away lesson here: you don&#8217;t use Vagrant to replicate your production system, you use Vagrant to produce code to deploy to that production system.

In my case I used to have three environments: local dev, system test and production.

The problem with local dev is that it&#8217;s local&#8230; means only me (or whoever using my machine) can write code for it. When [Valgreens][2] joined **:blibb** we tried to build the system in his local machine but the task was painful and impossible (I work with ubuntu, he&#8217;s uses Mac, and trying to reproduce the whole thing was just not possible for me&#8230; using remote connections and yes, I accept my burden: we didn&#8217;t know enough).

**How Vagrant solved that problem?**

Well, we started by building a Vagrant box with what we needed: nginx, supervisor, mongodb, redis, php and zeroMQ. I configured the whole thing and re-package it. Move it to our web server and we install it from there. At that point both of us had the system ready to go. We cloned the git repo in the folder we had mapped in Vagrant and&#8230; that&#8217;s it, we had 2 systems running the latest code in 2 completely different architectures (if we can say that Mac and Linux are completely different&#8230;)

**How different is this to do the same with VmWare, for example?**

Well, Vagrant it&#8217;s not only the virtual machine or box, it&#8217;s all this little details, like that you can work in your own editor in your local system (but hey, it&#8217;s executed inside the vagrant box!).

Ok, let me say this again: you work in your local system with your editor and the code is saved and executed inside vagrant. No need for FTPs, no need for moving anything because Vagrant allows you to share any folder and remap it into the box as you want.

This is what the project folders look like:

<pre>blibb-project
        Vagrantfile
        blibb-api/</pre>

By default Vagrant maps the folder where you run Vagrant inside the box in /Vagrant and we configure nginx and gunicorn to create the virtualhost there.

The we had a couple of (handy) port mappings that allowed us to access MongoDB, gunicorn and the web server (localhost:27007, localhost:8001, localhost:8181)

That&#8217;s it, we wrote code locally, execute code inside vagrant, access the resources through localhost (no need to mess with the hosts files and fake ip/domains)&#8230; easy <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

Developing is hard and since we started using Vagrant our productivity has sky rocketed. In this sense, there&#8217;s another product that I will recommend always: [clinker][3], a Development Ecosystem.

I will be writing soon about Clinker and how it has helped me out to get more time and lower my stress levels, in fact, these two products have made developing quite a rewarding experience. Both of them aim to the same pain point: Forget about system administration. **Developers, develop!**

 [1]: http://www.vagrantup.com/
 [2]: http://twitter.com/valgreens
 [3]: http://clinkerhq.com/
