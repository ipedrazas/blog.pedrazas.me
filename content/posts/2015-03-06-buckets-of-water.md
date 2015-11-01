---
title: Buckets of Water
author: ipedrazas
layout: post
date: 2015-03-06
url: /2015/03/06/buckets-of-water/
categories:
  - Cassandra
  - DevOps
---
I&#8217;m sure you&#8217;ve been here before: you have a problem, you try to explain it to non-technical people and&#8230; you fail to send a clear message across .

Communication is a two way road. It&#8217;s not just you sending a message, it&#8217;s the other part receiving it and understanding it. We&#8217;re good at sending and receiving, it&#8217;s in the understanding bit that we all struggle more than we would like to.

Finding good similes and analogies is hard. It&#8217;s something that sales people excel to, but it seems that technical people, we struggle a bit more.

Anyway, I had a little problem with one of our Cassandra clusters: it was overflowing data and nodes refused to join the ring&#8230; Solution? Scale up!

The process was simple but when the non-technical people started asking what was going on I had to find a way of illustrating the situation&#8230; and I did, using buckets of water. This is what I said:

&#8220;Imagine we have buckets of water and we pour water on them in a regular basis. When we see that the water levels are getting to high we add more buckets and little by little move water around until all the buckets have enough space to get more water&#8221;

This is what it usually happens when you add more Cassandra nodes to a ring.

&#8220;Well, trouble is that we&#8217;re not sure why, we cannot add more buckets. What would you do if you cannot add more buckets?&#8221; I asked.

&#8220;Can we use bigger buckets?&#8221;

&#8220;That&#8217;s pretty much what I have done! do you want to work with us?&#8221; Laughs and nods.

&#8220;I had to replace every single bucket by a bigger one. But there&#8217;s a catch, the bucket has to be the same, which is fine, because I can expand the bucket&#8230; because they are elastic&#8221;.

Here the guy asked a few questions about elasticity regarding to how AWS works and blimey, he understood that too!

&#8220;So, what we do is to bring a bucket where we pour all the water, expand our empty bucket and put the water back, and we have to do that for every single bucket&#8221;.

Upgrading all the nodes with Chef is pretty simple, so, it was a matter of just moving data (or water) around and launching a few commands (to re-create the raid0).

Today I&#8217;ve heard a conversation between two sales guy about buckets of water and then, then it&#8217;s when I realised how important is to send our message across as clear as water (pun intended).