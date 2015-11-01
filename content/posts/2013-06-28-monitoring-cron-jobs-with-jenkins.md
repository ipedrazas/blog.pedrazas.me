---
title: Monitoring Cron Jobs with Jenkins
author: ipedrazas
layout: post
date: 2013-06-28
url: /2013/06/28/monitoring-cron-jobs-with-jenkins/
categories:
  - DevOps
tags:
  - jenkins
---
> &#8220;How do you monitor your cron jobs?&#8221;
> 
> &#8220;We just don&#8217;t&#8230;&#8221;

Monitoring is one of those things that yo should do: monitor EVERYTHING&#8230; or at least as much as you can.

One of the most slippery cases are our cron jobs. Many of them don&#8217;t report anything, many of them run without anyone knowing they&#8217;re there&#8230; And even worse, if they fail, they fail silently: as this cron job I disabled because it had been failing since 2008 (only 5 years or every day failures).

That was the last straw, after removing that entry from the crontab I went to my boss and we decided to tackle the problem. This client uses Nimbus but it seems that the Nimbus guy was not very happy on having loads of cron jobs added so I suggested using Jenkins.

In this case we decided to use Free Style Software Projects since they allow us to run the cron job manually

<pre>JENKINS_HOME=http://myserver.acme.org/path/to/jenkins/
0 * * * *     export JENKINS_HOME=$JENKINS_HOME; java -jar jenkins-core-*.jar "backup" backup.sh 2&gt;&1 &gt; /dev/null</pre>

You can find more info in the [Jenkins Wiki][1] but if you want to know more or have any doubts, just [ping me on Twitter][2] <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

 [1]: https://wiki.jenkins-ci.org/display/JENKINS/Monitoring+external+jobs
 [2]: https://twitter.com/ipedrazas