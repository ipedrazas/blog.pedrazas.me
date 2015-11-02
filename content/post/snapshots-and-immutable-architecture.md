+++
Categories = ["Architecture"]
Description = ""
Tags = ["kubernetes", "immutable", "Architecture"]
date = "2015-11-02T00:40:31Z"
title = "Snapshot Architecture"
draft = true
+++

Immutable is good. Immutable is good because it doesn't change, and things that don't change are good because if it works once, it has to work always... or that's the theory.

If you use any of those fancy new functional programming languages, you're using immutable data types. They are great. Do you know why? because they do not change. Things that change are hard. Managing things that change is complicated. Managing many things that chnage very quickly is a nightmare.

Have you heard of immutable infrastructure? infrastructure is hard, so, by making infrastructure immutable you reduce the pain of managing things that change. It has been recently that we achieved the fact of deploying __always__ the same application regardless of where it runs.

Kubernetes helps a bit with managing immutable infrastructure, but infrastructure is not our mission. It is important, but it is just another piece. I do not know anyone with the only purpouse of running machines by the sole sake of running them. It's the applications we're interested on!

Do we have immutable applications? kind of. Containers are helping. Do we have immutable infrastructure? indeed we have, and yes, containers are helping... So, where is the trouble?

It has taken me a while to understand this, but I think I'm starting to understand where the rabbit hole is (and where it takes).

If infrastructure is our data type, the architecture is the functional programming language. It's great to have immutability all the way down making sure our data, applications or machines do not change, but there's a missing piece still. If we don't start re-architecting solutions based on those principles, the principles will not stand.

Like those people making fun of microservices: you go from a big horrible monolithic application to a bunch of horrible services scatered all over the place. Comment might be fair in some contexts, but in my experience it's not about services or monoliths, it's about adopting a half baked approach.

Microservices are great, but they are hard to manage because the internal dependencies now are external. We give away control. We trust... the others.

Trouble is that if we understand an application as a set of loosely coupled microservices (all of them running in containers, hence immutable services), we have to accept that now that state, that mutability we have tried to get rid of, is present as the hardest of all forms: distributed evolution.

We have traded the cohesion of our applications for flexibility. And it is good. But we have still to embrace a truly immutable architecture. We have to understand that our applications are immutable. The services do not change. The services are replaced by other services that superseed the old ones.

It's not deploying new versions of an application anymore, it's deploying new services every time. Services that replace services.

Let me tell you 2 words: Backwards compatible. Probably the heaviest stone in our world of design and compute. Think about it. What I'm saying is that we're in a position to let all the baggage go. Every time you start, you start afresh. It doesn't matter your previous sins, you're clean.

Stop thinking of your code like something that it's alive. Think of your code as a cake or toy factory. It produces things that do not change. You can change the machinery of that factory, you can improve the making of products, but the toy you did two years ago... that toy will not be touched once has left the factory.

I know, you could go all crazy and start shouting __"Stop refactoring!!", "Stop fixing bugs!"__but truth is that you're not doing it to improve something that it's there, you're doing it to make something better.
