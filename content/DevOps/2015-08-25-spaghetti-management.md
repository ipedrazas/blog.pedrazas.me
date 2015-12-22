title: Spaghetti management
date: 2015-08-25
slug: /2015/08/25/spaghetti-management/
tags: DevOps, Docker, kubernetes, microservices

During a job interview they started asking questions about microservices and the discussion that we had made me think that it would be good to write a bit about it.

Microservices are great because:

  * They are small, that&#8217;s why the appended &#8220;_Micro_&#8220;
  * They are independent one each other (deployment, runtime, configuration, downtime, scaling&#8230;)

Great! so, where&#8217;s the catch&#8230; because there&#8217;s always a catch. Think about it. You can split your API in multiple microservices. Great, now, the application is loosely coupled to a bunch of services.

If you replace services by libraries, the name that comes to your mind is? DEPENDENCIES!

The catch with microservices is that dependencies are not implicit in your API or APP the way they used to be (think jars, gems or python libs).

Bear in mind as well that IDE&#8217;s and compilers are very good (in general) at finding when dependencies are broken&#8230; which is not the case if you have a bunch of loosely couple services.

Who&#8217;s responsible for managing all those dependencies now? because excuse me, but I need a way to bundle services together. Or, to be more precise, to bundle versions of services together.

To me the hardest problem is not a design problem, the hardest problem is managing dependencies at version level.

At [Import.io][1] we started moving towards this architecture and the way we solved it was not using service discovery but using the old idea of having a contract where you specify a bunch of versions that you know they play nicely together.

I always differentiate Runtime, Configuration and Context. In our case, Runtime was a container running a microservice. Configuration was another container (a data container) where the relationship between versions was explicitly defined, like a manifest.

The advantage of using a data container to bind a bunch of versions is that you have traceability. You know always how the application was configured, because it is true, with microservices we have gained a lot of flexibility but we have lost certain control. Using a container helps me to regain that control.

Why do I do this? because I can leverage my continuous integration pipeline to test my services and how they interact with each other according to specific versions. Because now, my microservice bundles are in git and not in some obscure key of zookeeper or consul. Even more, when the time to migrate to [Kubernetes][2] arrives, I can use my data container as my pod blueprint.

Because one thing is my architecture and another different thing is my runtime and my operations.

Remember&#8230;

> **It&#8217;s not about power, it&#8217;s about responsibility**

 [1]: https://import.io/ "Import.io"
 [2]: http://kubernetes.io/
