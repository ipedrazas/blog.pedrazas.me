---
title: The Art of Testing in the rain
author: ipedrazas
layout: post
date: 2014-09-22
url: /2014/09/22/the-art-of-testing-in-the-rain/
categories:
  - Development
tags:
  - cassandra
  - docker
  - testing
---
<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Testing is hard. We all know that. Testing distributed applications is just a nightmare. Like having Jason, Freddy Krugger and legions of zombies chasing you while you run barefoot, naked and of course, in the rain.</span></span>

<span style="color: #333333;">Why it&#8217;s so hard? Well, let&#8217;s look at it. We have </span>**<span style="color: #333333;">Unit Testing</span>**<span style="color: #333333;">, where we test that our code does what it has to do. Then, we have </span>**<span style="color: #333333;">Integration Test</span>**<span style="color: #333333;">, where we test that our code can connect and query other systems. Finally, we have </span>**<span style="color: #333333;">System Test</span>**<span style="color: #333333;">, where we want to test if our application works.</span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Questions you ask during <strong>Unit Testing</strong>:</span></span>

  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Does this method return this expected value?</span></span>
  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Does this method parse this XML properly?</span></span>
  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Does this method transform this object into this other one?</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Questions you ask during <strong>Integration Test</strong>:</span></span>

  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Can my application connect to the database?</span></span>
  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Does this method return any data?</span></span>
  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Does this API call return the Json objects as I expect?</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Finally, <strong>System Test</strong>:</span></span>

  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Can I log in?</span></span>
  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Can I sign up as a new user?</span></span>
  * <span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">When I delete this message, does it goes away?</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">And this last bit, this last bit it&#8217;s terribly hard because you have different systems and a frontend to deal with and not only that, you have to have a system that replicates production (and this is expensive and time consuming).</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">So, why testing is so hard? because there are many dependencies at many different layers that are very difficult to replicate (have I talked about firewalls? well, maybe I should)</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Unit Testing can be done as a pre-building task. Cheap, easy.</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Integration Test needs two system talking to each other: our code, and the system my code is connecting to. Not as cheap as it seems. Mocking up is a way of reducing the cost of running two (or more) systems. But don&#8217;t deceive yourself, when mocking you are unit testing.</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">System Test needs all the systems in place properly configured. Expensive.</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Take this, testing your application is not an extra life, it&#8217;s a sneak peak to the dangers that stalk ahead.</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">So, how much effort I should put on testing? as much as you can. Read it again: as much as you can. It depends. Let&#8217;s put it like this, the more effort you put in proper testing, the less effort you will have to put when deploying to production.</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Testing is hard, and with every release, with every problem we find in production we learn (like simulating dodgy firewalls), but you should take Testing like that: a learning exercise.</span></span>

<span style="color: #333333;"><span style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">I&#8217;m planning to write a series of posts about Integration and System Testing. So, if you&#8217;re interested, bear with me! </span></span>