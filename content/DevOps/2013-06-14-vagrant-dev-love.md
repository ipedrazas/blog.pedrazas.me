title: Vagrant, dev love
date: 2013-06-14
slug: /2013/06/14/vagrant-dev-love/
tags: DevOps, ansible, vagrant

So, imagine I would say that with this two commands:

 `So, imagine I would say that with this two commands:

`

You have a Virtual machine with Ubuntu ready to play with.

Now, imagine that you configure that machine with the different software that you need. Smart people call that action to provision your machines. Just imagine. Because you have plenty of space, you save that virtual box somewhere in your dev server.

(in case you wonder where that virtual machine, or box, has been stored, it&#8217;s here, look:

`~/.vagrant.d/boxes/precise64/virtualbox/`

happy, now?)

Now, imagine this Science Fiction scene: a new starter arrives and it takes longer to set up his email and domain user than the dev machine. I know&#8230; sounds ridiculous.

Well, that&#8217;s Vagrant.

I use Vagrant with [Ansible][1] (we&#8217;ll talk about this in another post) to re-create a Dev environment. Last time we checked out, it took 4 minutes and 23 seconds to create, provision and deploy the code in Vagrant installing and configuring:

  * <span style="line-height: 15px;">Nginx</span>
  * php-fpm
  * python: gunicorn, supervisor, virtualenv
  * mongodb
  * redis

Thing is, I much rather prefer spending time setting up my sublime text than my python environment&#8230; unfortunately, I do have yet-another script that installs & configures my sublime.

Quote of the week:

> Automate Everything!

 [1]: http://www.ansibleworks.com/docs/playbooks2.html
