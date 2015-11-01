---
title: The Challenge
author: ipedrazas
layout: post
date: 2013-06-30
url: /2013/06/30/the-challenge-2/
categories:
  - children
  - security
tags:
  - raspberry pi
---
Recently me and my wife have been having some problems with Internet and Children. I know, there are hundreds of filters and ways of preventing children to access content that it not appropriate to their age&#8230; and none seems to work well.

You can enable [Safe Search][1] in Google and YouTube Safety Mode. Let me show you acouple of Image Searches by Mighty Google with the Safe Search On, I searched for &#8220;[Human Rights][2]&#8220;:

[<img class="aligncenter size-medium wp-image-165" alt="Google Search" src="http://ivan.pedrazas.me/wp-content/uploads/2013/06/Selection_021-300x140.png" width="300" height="140" />][3]

[<img class="aligncenter size-medium wp-image-164" alt="Google Search" src="http://ivan.pedrazas.me/wp-content/uploads/2013/06/Selection_020-300x151.png" width="300" height="151" />][4]

So, yes, almost all the images are &#8220;safe&#8221;&#8230; almost. Thing is, if you disable that safe search the results contain less blood.

Other options are using a proxy that filters out the dodgy content but not many people know how to install those things that have evolved into add-ons or extensions that filter out certain pages.

The issue with those solutions is that you rely on a company that gathers your browsing data (and your children&#8217;s browsing data) and all of them have long Terms and Conditions and what really worries me is that as a company, you need to make money. Since they give away their product, I&#8217;m afraid that the real product is the user&#8217;s data.

So, as parents we have some options. But it&#8217;s not what us as parents can do, but what our children are going to do. An example would be WoT, a great idea with a big problem: children don&#8217;t understand it. WoT

> &#8220;crowdsources ratings from a global community of millions of users, who rate and comment on websites based on their personal experiences&#8221;.

Wicked! Now when I search I see that little green/red icon next to the results&#8230; Do you think that children understand that? me neither.

Don&#8217;t get me wrong, I think it is a great idea and it is the way to go. They have options to &#8220;_Block sites that are unsuitable for children_&#8220;. So, in many ways it is better than using Mighty Google and its Safe Search.

[<img class="aligncenter size-medium wp-image-167" alt="WoT" src="http://ivan.pedrazas.me/wp-content/uploads/2013/06/Screenshot-from-2013-06-30-233411-300x267.png" width="300" height="267" />][5]

&nbsp;

Unfortunately WoT is not only focused on Children safety which is good and bad&#8230; but it is a great idea and I will be looking at them (and their API) more closely.

One of the best Add-ons for Firefox or Chrome is Web Filter by [CloudAcl][6]. It allows you Black List or White List websites. A parents/kids mode and it&#8217;s password protected&#8230; and they have a mobile version for your iPhone/iPad or your Android device.

[<img class="aligncenter size-medium wp-image-173" alt="CloudAcl" src="http://ivan.pedrazas.me/wp-content/uploads/2013/06/Selection_022-296x300.png" width="296" height="300" />][7]

Another option is to use a &#8220;Kid&#8217;s Safe Browser&#8221; like [KidZui][8]. Again, this is a great tool with the only issue of why do they need to gather and keep browsing history in their servers and not keep it in MY BROWSER!!! (the fact that they do that is a big red flag, since technically there&#8217;s no reason for taking my data somewhere else and by doing that your message is &#8220;I do it because that&#8217;s how I make money&#8221;. Again, me and my children are the product not the customer.

As it seems, the options out there are not as good as we might expect. Or they are not as efficient as we would like to or they are not specialised in children&#8217;s browing or they have a dodgy business model.

What **I would like** is to have an <span style="text-decoration: underline;">open source solution</span> that stops my children from seeing things that are not appropriate for them. I&#8217;d like to have also a tool that allows me easily to monitor what is going on when I&#8217;m not there browsing with them.

I&#8217;m not sure if there&#8217;s such thing, what I know is that I haven&#8217;t found it yet&#8230;  Since I like technology and specially [Raspberry Pis][9], I&#8217;m building a plug and play device that I call **SafeBerry Pi** and it&#8217;s basically the monitoring tool. Still very early stages but worry not, I will be writing about it as soon as I have something (stable) working, so, stay tunned!!

&nbsp;

 [1]: http://www.google.com/preferences
 [2]: https://www.google.co.uk/search?hl=en&authuser=0&site=imghp&tbm=isch&source=hp&biw=1920&bih=990&q=human+rights
 [3]: http://ivan.pedrazas.me/wp-content/uploads/2013/06/Selection_021.png
 [4]: http://ivan.pedrazas.me/wp-content/uploads/2013/06/Selection_020.png
 [5]: http://ivan.pedrazas.me/wp-content/uploads/2013/06/Screenshot-from-2013-06-30-233411.png
 [6]: http://www.cloudacl.com/
 [7]: http://ivan.pedrazas.me/wp-content/uploads/2013/06/Selection_022.png
 [8]: http://www.kidzui.com/
 [9]: www.raspberrypi.org