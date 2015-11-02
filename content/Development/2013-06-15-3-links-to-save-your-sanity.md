title: 3 links to save your sanity
date: 2013-06-15
slug: /2013/06/15/3-links-to-save-your-sanity/
tags: Development, DevOps, Python, deploy, python

During the last two years I&#8217;ve been deploying python code to production quiet often and because my memory is quite terrible and I know that when something goes wrong, I need to have everything there: IN-MY-FACE, I added from the beginning three links to my release process.

Imagine we want to deploy :blibb to our server. I will run my fabric script and once it&#8217;s finished Boom! deploy finished <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

This script will create the following directory:

 `/data/blibb/releases/2013.6.15-22.59.12`

Let&#8217;s assume the last deploy was done 2 days before:

 `/data/blibb/releases/2013.6.13-11.23.22<br />
/data/blibb/releases/2013.6.15-22.59.12`

Now, there&#8217;s something I do&#8230; &#8220;just in case&#8221;, I create 3 symbolic links as follows:

 ``During the last two years I&#8217;ve been deploying python code to production quiet often and because my memory is quite terrible and I know that when something goes wrong, I need to have everything there: IN-MY-FACE, I added from the beginning three links to my release process.

Imagine we want to deploy :blibb to our server. I will run my fabric script and once it&#8217;s finished Boom! deploy finished <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

This script will create the following directory:

 `/data/blibb/releases/2013.6.15-22.59.12`

Let&#8217;s assume the last deploy was done 2 days before:

 `/data/blibb/releases/2013.6.13-11.23.22<br />
/data/blibb/releases/2013.6.15-22.59.12`

Now, there&#8217;s something I do&#8230; &#8220;just in case&#8221;, I create 3 symbolic links as follows:

``

So, my nginx points to current, so if something goes wrong, I can always swap back to the previous release that, alas, it&#8217;s just there. With these 3 links I know exactly where I am and where I was before the release, and yes, things go wrong, and my rollback is as simple as changing a couple of links (I do something else, but the update of the links is what makes the process extremely fast).

In case that you wonder, this is how the links are left after a rollback:

 ```During the last two years I&#8217;ve been deploying python code to production quiet often and because my memory is quite terrible and I know that when something goes wrong, I need to have everything there: IN-MY-FACE, I added from the beginning three links to my release process.

Imagine we want to deploy :blibb to our server. I will run my fabric script and once it&#8217;s finished Boom! deploy finished <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

This script will create the following directory:

 `/data/blibb/releases/2013.6.15-22.59.12`

Let&#8217;s assume the last deploy was done 2 days before:

 `/data/blibb/releases/2013.6.13-11.23.22<br />
/data/blibb/releases/2013.6.15-22.59.12`

Now, there&#8217;s something I do&#8230; &#8220;just in case&#8221;, I create 3 symbolic links as follows:

 ``During the last two years I&#8217;ve been deploying python code to production quiet often and because my memory is quite terrible and I know that when something goes wrong, I need to have everything there: IN-MY-FACE, I added from the beginning three links to my release process.

Imagine we want to deploy :blibb to our server. I will run my fabric script and once it&#8217;s finished Boom! deploy finished <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />

This script will create the following directory:

 `/data/blibb/releases/2013.6.15-22.59.12`

Let&#8217;s assume the last deploy was done 2 days before:

 `/data/blibb/releases/2013.6.13-11.23.22<br />
/data/blibb/releases/2013.6.15-22.59.12`

Now, there&#8217;s something I do&#8230; &#8220;just in case&#8221;, I create 3 symbolic links as follows:

``

So, my nginx points to current, so if something goes wrong, I can always swap back to the previous release that, alas, it&#8217;s just there. With these 3 links I know exactly where I am and where I was before the release, and yes, things go wrong, and my rollback is as simple as changing a couple of links (I do something else, but the update of the links is what makes the process extremely fast).

In case that you wonder, this is how the links are left after a rollback:

```
