---
title: Online vs Offline
author: ipedrazas
layout: post
date: 2013-04-10
url: /2013/04/10/online-vs-offline/
categories:
  - Development
  - Javascript
---
While building the HTML5 wrapper for the mini apps in :blibb I hit one of the hardest problems I&#8217;ve seen with mobile: Offline support.

Offline is tough. In fact, in mobile, the ABC of [this video][1] is turned into &#8220;Assume Bad Connectivity&#8221; and no matter what you&#8217;re building today, it has to work on mobile. Don&#8217;t get it wrong, I&#8217;m not saying make it mobile, I&#8217;m saying it has to work on mobile&#8230; and here is where I hit my wall: Offline.

There are different approaches, but basically the idea is that if you&#8217;re offline you use the web database (any of the many available now) and save your temporary data there until you get back online and you sync your data back.

That idea didn&#8217;t work out with me. It makes thing too complicated. having this approach means having to implement two set of APIs, one for local and one for remote, and chances of messing up are quiet high:

<pre lang="javascript">if (online){
          getOnlineData();
          saveOnlineData();
          updateOnluneData();
          deleteOnlineData();
     }else{
          getOfflineData();
          saveOfflineData();
          updateOffluneData();
          deleteOfflineData();          
     }</pre>

Will not help you much because you ever know when you are going to lose your connectivity. For us it worked much better this approach: you use always the local storage by default. Assume being offline always and sync whenever you have connection. Why? because it makes things easier and because it makes much more sense: your users don&#8217;t care about your server&#8230; nor your app, they care about their data.

<pre lang="javascript">getOfflineData();
    saveOfflineData();
    updateOffluneData();
    deleteOfflineData(); 

    if (online){
          sync();
     }</pre>

This approach makes development of the mini app much easier: you code against the local APIs and implement a Sync method that will sync changes in your server.

 [1]: http://www.youtube.com/watch?v=y-AXTx4PcKI