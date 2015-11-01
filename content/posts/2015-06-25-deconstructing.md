---
title: Deconstructing
author: ipedrazas
layout: post
date: 2015-06-25
url: /2015/06/25/deconstructing/
categories:
  - DevOps
tags:
  - apache kafka
  - aws
  - docker
  - kinesis
  - mesos
---
[<img class="alignleft size-full wp-image-454" src="http://ivan.pedrazas.me/wp-content/uploads/2015/06/kafka_logo.png" alt="kafka_logo" width="75" height="117" />][1]If you haven&#8217;t heard about [Apache Kafka][2], or his little brother Amazon Kinesis, go and read about [why they are so great][3].

I was chatting with a friend last night and he told me &#8220;I get containers now. I needed some give it some thought, but I get them now&#8221;. If I had to describe him with one word I would use &#8220;smart&#8221; without any doubt&#8230; still he had to think about why containers are so great.

We carried on talking and after two more beers and few pork ribs I managed to make him understand why we are about to change we build applications. It&#8217;s not only because of containers (or systems like Mesos or Kubernetes), but because with containers, we have seen the light of deconstructing the monoliths into microservices.

But, there&#8217;s another key element on this Game of Thrones: The Log, systems like Apache kafka are going to help to change completely the landscape of what we build, and ship and run. Like with Microservices, the Log overlord brings a blessing in disguise: it&#8217;s not what it does, it&#8217;s what allows others to do.

It is not about its responsibility, it&#8217;s about delegating that responsibility in who really has it. Let&#8217;s look at what happens today. We have a system, that system gets some data, compute that data and stores that data in a database. Easy!

Then someone comes along and asks to get that same data and put it somewhere else, so our system now gets some data, compute that data and stores that data in two different places.

As we can see, this does not scale very well, so people get smart, and start doing things like database triggers and a whole bunch of things that are totally correct in itself, but over time, it creates a big mess of &#8220;dirty integrations&#8221;. These are the things that will break when we want to move our system. These are the future nightmares of our microservices journey.

Then, we have The LOG&#8230; a dumb system that guess what: it does not care about what do you do with that data. The Log Overlord will keep your data for a while, and it&#8217;s up to you, the consumers, to use it.

A bit like how the TV has been broadcasting for a few years&#8230; with a twist, because, as we do now, this TV system allows you to consume the programs when you want it.

Ok, so, basically, we have a place where we put all that data (for a while) and we have a bunch of people consuming that data? So what?

Well, not much, but as with microservices, what the LOG overlord provides is the ability of your consumers to consume the way they want (once per hour, once per day&#8230; in real time), and even more, the people who create the TV shows do not care about the broadcasting anymore.

Think about it. Microservices decouple your business logic. With microservices you can write very business specific services without having to worry about all the other business rules, use cases and (oh yes) those terrible exceptions.

Apache Kafka or Amazon Kinesis decouple your data. How you read that data is up to the readers and the writers have nothing to do with that. It&#8217;s like a writer writing a book, and people reading that book: when they want, how they want&#8230; as opposed to the writer writing and reading aloud to certain audience.

I&#8217;m not sure if the creators of Kafka chose that name because it&#8217;s a system that allows writers and readers to focus and enjoy what they want to do.

As I said, we are living very exciting times with a lot of change. Let me finish with a song&#8230; or my own version of a song by [Elvis Presley][4]:

<p style="text-align: center;">
  Treat me like a fool,<br /> Treat me mean and cruel,<br /> But <strong>LOG</strong> me.
</p>

<p style="text-align: center;">
  Wring my faithful heart,<br /> Tear it all apart,<br /> But <strong>LOG</strong> me.
</p>

<p style="text-align: center;">
  <a href="http://ivan.pedrazas.me/wp-content/uploads/2015/06/649ca9a3f3d4aba78095a28c26fba1fa.jpg"><img class="aligncenter size-medium wp-image-455" src="http://ivan.pedrazas.me/wp-content/uploads/2015/06/649ca9a3f3d4aba78095a28c26fba1fa-233x300.jpg" alt="649ca9a3f3d4aba78095a28c26fba1fa" width="233" height="300" /></a>
</p>

 [1]: http://ivan.pedrazas.me/wp-content/uploads/2015/06/kafka_logo.png
 [2]: http://kafka.apache.org/
 [3]: http://www.oreilly.com/pub/e/3098
 [4]: https://www.youtube.com/watch?v=f8PMqLHF1jU