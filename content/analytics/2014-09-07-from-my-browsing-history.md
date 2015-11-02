title: Analytics From my Browsing History
tags: docker, dotmarks, elasticsearch
date: 2014-09-07
slug: /2014/09/07/from-my-browsing-history

One of the problems I had while writing dotMarks was the fact that I could not get enough URLs for my testing. I did ask friends and family to send me over their exported list of bookmarks or the bookmarks from pocket&#8230; but [I needed more data][1], so, I look somewhere else: My browsing history.

Of course I couldn&#8217;t just get those links &#8220;**_and carry on_**&#8220;. I had to look at them, poke them and write an extension that allows me to analyse them.

Because, the idea was&#8230; what kind of high level information can Google (or anyone else) know from just looking at my browing history? and the result was as scary as you might imagine.

Bear in mind that Google knows much more than just my history&#8230; but that&#8217;s for another post. Let&#8217;s focus!

This extension basically gathers all your browing history (100 days max), sends it to dotmarks where some data-crunching happens and&#8230; then you see the results.

For example, it checks at what time you visit a link and creates this pretty graph:

[<img class="aligncenter size-medium wp-image-330" src="http://ivan.pedrazas.me/wp-content/uploads/2014/09/Screenshot-from-2014-09-07-111057-300x167.png" alt="Screenshot from 2014-09-07 11:10:57" width="300" height="167" />][2]

Which highlights something that everybody who knows me is aware of: I do not sleep much and&#8230; that I work very early in the morning, or very late at night.

I was very curious about finding out my most visited websites&#8230; nothing surprising here:

[<img class="aligncenter size-medium wp-image-328" src="http://ivan.pedrazas.me/wp-content/uploads/2014/09/Screenshot-from-2014-09-07-111147-300x207.png" alt="Screenshot from 2014-09-07 11:11:47" width="300" height="207" />][3]

That I do not procastinate as much as I thought is quiet clear (twitter reloads itself a lot, that&#8217;s why it ranks so high), but mostly I work on my localhost&#8230; and check how my Bitcoins are doing at [Megamine][4].

[<img class="aligncenter size-medium wp-image-333" src="http://ivan.pedrazas.me/wp-content/uploads/2014/09/theres-no-place-like-127-0-0-1-localhost-computer-print-poster-300x200.jpg" alt="theres-no-place-like-127-0-0-1-localhost-computer-print-poster" width="300" height="200" />][5]

Then, I started extracting keywords from my searches&#8230; and things got more interesting:

[<img class="aligncenter size-medium wp-image-329" src="http://ivan.pedrazas.me/wp-content/uploads/2014/09/Screenshot-from-2014-09-07-111126-300x209.png" alt="Screenshot from 2014-09-07 11:11:26" width="300" height="209" />][6]

Yes, I do search about superheroes a lot&#8230; things of having children addicted to Thor, Spiderman and such troop.

What is really interesting is how high rank generics like java, python or ubuntu. I was a bit puzzled at first, then I realised that those keywords are ways of filtering out unwanted results. No surprise then, I do work with ubuntu, java and python.

Still, top marks for the two technologies I&#8217;ve been working more with: ElasticSearch and Docker. ElasticSearch documentation is quite dry&#8230; Docker, because I&#8217;m trying to do a bit too much I guess.

[dotMarks][7] is a self hosted bookmarks service. The idea is that you will run your own dotMarks server. I&#8217;m working hard to make it as easy as possible to run it (thanks to Docker) but if you&#8217;re curious and want to see what your browsing history says about you, [download the extension][8] and give it a go.

What I need is advice  <img src="http://ivan.pedrazas.me/wp-includes/images/smilies/icon_smile.gif" alt=":)" class="wp-smiley" />If you run the extension and think of something else I can extract I&#8217;m all ears.

Currently I&#8217;m working on a simple amazon parser, but it&#8217;s still very early&#8230; anyway, if you want to give it a go, by all means try it out and if you can share your feedback [with me][9], I would really appreciate it.

&nbsp;

**Disclaimer**: [dotMarks][7] and all related to this project is OpenSource. I do have a working version [here][10], but as I said, the idea is that you will run your own service. Still, if you want to add your bookmarks, go ahead, and if you want to be able to find them later, use a tag that you can recognise later.

&nbsp;

 [1]: https://www.youtube.com/watch?v=Pj-qBUWOYfE
 [2]: http://ivan.pedrazas.me/wp-content/uploads/2014/09/Screenshot-from-2014-09-07-111057.png
 [3]: http://ivan.pedrazas.me/wp-content/uploads/2014/09/Screenshot-from-2014-09-07-111147.png
 [4]: http://megamine.com/
 [5]: http://ivan.pedrazas.me/wp-content/uploads/2014/09/theres-no-place-like-127-0-0-1-localhost-computer-print-poster.jpg
 [6]: http://ivan.pedrazas.me/wp-content/uploads/2014/09/Screenshot-from-2014-09-07-111126.png
 [7]: https://dotmarks.net
 [8]: https://github.com/ipedrazas/dotmarks-history
 [9]: https://twitter.com/ipedrazas
 [10]: https://dotmarks.net/app/#/dotmarks
