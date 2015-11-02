title: 'Using Cassandra in AWS for Dev & Test'
date: 2015-03-12
slug: /2015/03/12/using-cassandra-in-aws-for-dev-test/
tags: Cassandra, DevOps

At [Adbrain][1], Cassandra is one of our core databases. I&#8217;m a big fan of not doing much by automating a lot. However, I couldn&#8217;t find an easy way, by easy I mean that it would take very little to implement and could work without me having to do any intervention.

As I&#8217;ve mentioned before, we create ephemeral clusters for our computational work force using Apache Spark, which helped us a lot to reduce the cost of our running infrastructure.

Yes, I&#8217;m a big fan of using infrastructure in an effective way. There&#8217;s no secret here, using the cloud gives you the flexibility to pay for what you use.

Our Dev & Test machines only run during working hours (you know, to pay for what you use only). However, with Cassandra we had to do an exception. Noticed the past tense? We use the ephemeral drives of our AWS instances (in raid0), and as many of you have know, disks do not survive if you stop the instances&#8230; which makes stopping & starting Cassandra nodes a pain.

The solution is pretty obvious, and yes, I&#8217;m banging my head against the wall for all the times I&#8217;ve wrongly said &#8220;Cassandra clusters cannot be stopped&#8221;.

We have a jenkins job that stop Dev & Test machines. The idea was to be able to put my Cassandra cluster nodes in that job as well (to keep things tidy). However, it&#8217;s possible but not ideal because you create some dependencies (and there&#8217;s nothing better than being independent)

This is what my job does:

<p style="padding-left: 30px;">
  <strong>Cassandra Stop Job</strong>
</p>

  1. Flush cassandra data.
      1. nodetool flush
  2. Stop cassandra service.
  3. Copy Data out. (you have two options)
      1. nodetool snapshot + tar + upload to S3
      2. tar /data/cassandra + upload S3
  4. Stop the instance.

<p style="padding-left: 30px;">
  <strong>Cassandra Start Job</strong>
</p>

  1. Start the instance.
  2. Create raid0.
  3. Copy data in.
  4. Start cassandra service.

That&#8217;s it, now my Cassandra clusters for Dev & Test only run for 50h a week, instead of 168h (24&#215;7).

If you use the m3.2xlarge instance type, you will pay per node $28 per week instead of $94.08. A saving of **$66.08** per node per week.

 [1]: http://www.adbrain.com/
