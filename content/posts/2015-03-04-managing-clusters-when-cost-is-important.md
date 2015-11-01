---
title: Managing Clusters
author: ipedrazas
layout: post
date: 2015-03-04
url: /2015/03/04/managing-clusters-when-cost-is-important/
categories:
  - DevOps
---
If you have a more than one cluster you know why Cluster Managers are so important: because managing clusters can be a nightmare. A cluster is a special kind of beast. Not only you have to be aware of the usual suspects: Disk space, logs, alerts, etc. But you have to be aware of other things: Master, Slaves, and what do they do together.

There are plenty of solutions out there that try to solve this problem. In fact, depending on your problem, you should chose one solution or another.

For example, [Apache Mesos][1] that abstracts machine resources like CPU, memory or storage, or [Yarn][2] (from the Hadoop family) that allows you to schedule your MapReduce jobs.

At Adbrain I&#8217;ve built a little tool that does a bit of both. By any means it&#8217;s anything like Mesos or Yarn but a super-hyper striped out version of the core ideas behind these two wonderful systems.

I&#8217;ve called it &#8220;_CheckPoint_&#8221; because I&#8217;ve designed it following the Hollywood Principle: &#8220;**_Don&#8217;t call me, I&#8217;ll call you_**&#8220;. One of the most annoying things I&#8217;ve found when provisioning machines using code is all that polling. Don&#8217;t get me wrong, it works, but if Javascript has showed us something is that callbacks are (awesome) way better to deal with than threads and sleeps (or waits). CheckPoint works the other way around. For example, it creates and provisions the Apache Spark master, once it&#8217;s up and running, that machine sends a request to Checkpoint and it creates and provision the workers. The whole cluster creation is asyncronous and it decoupled of what the other resources do.

So, CheckPoint started like yet-another-provisioning tool, but it ended up being much more than that. CheckPoint was the tool that allowed us to start working differently in what I call &#8220;_Agile Clusters_&#8220;.

The foundation of Agile Clusters are 3 simple elements:

  1. Creation and provisioning of Ephemeral clusters.
  2. Ephemeral logging and monitoring.
  3. Destruction of idle resources.

The 1st point it&#8217;s easy, you need a way of building your machines. There are many solutions like Puppet, Ansible, Salt or Chef. CheckPoint uses Chef because that&#8217;s what we use at Adbrain, but it&#8217;s more of a burden than an advantage.

The 2nd point is quiet tricky. Ephemeral infrastructure is great, but when the machine go away, so goes the data, and the logs, and everything you didn&#8217;t take out first. The other itchy point is monitoring. Yes, there are plenty solutions are there, but not that many that can deal with ephemeral infrastructure. CheckPoint uses [InfluxDB][3] and [grafana][4], in particular the &#8220;[_Scripted Dashboards_][5]&#8221;

The 3rd point is a blessing in disguise. CheckPoint provides a REST API so, developers can see infrastructure as one step more in their workflow execution where they can create and destroy resources but if for any reason your application or a developer forgets about a cluster&#8230; CheckPoint does not an it will destroy that resource unless it&#8217;s used.

[<img class="alignright size-medium wp-image-389" src="http://ivan.pedrazas.me/wp-content/uploads/2015/03/452b76319f298454e6f8ef6c3f6ce11a-230x300.png" alt="CheckPoint" width="230" height="300" />][6]There&#8217;s something that has made a huge impact in how we work: Accessible Information.

I&#8217;ve been working in Knowledge Management almost all my life and I know how important is to have access to the right data at the right time.

That&#8217;s why when I was building CheckPoint I was very conscious of who was going to use it and what it might be helpful to know at that time.

For example, the fact of displaying CPU, RAM and Price when selecting your instances has been incredibly useful to improve our cluster efficiency and cost.

But we not only managed to reduce the infrastructure cost by 30%, we achieved something that until now was a big unknown: &#8220;How much it costs to run every big data job&#8221;, because neither Mesos nor Yarn worry about cost, their job is not juggling with cost, it&#8217;s solving another problem, quite a hard one, but to me being able to quantify how much it cost to run a job is critical, because it&#8217;s not about in this world of Cloud services it&#8217;s not about if it&#8217;s possible or not, it&#8217;s about if economically makes sense or not.

&nbsp;

 [1]: http://mesos.apache.org/
 [2]: http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html
 [3]: http://influxdb.com/
 [4]: http://grafana.org/
 [5]: http://grafana.org/docs/features/scripted_dashboards/
 [6]: http://ivan.pedrazas.me/wp-content/uploads/2015/03/452b76319f298454e6f8ef6c3f6ce11a.png