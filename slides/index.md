- title : Lord of Chaos - Becoming a Chaos Engineer
- description : Lord of Chaos - Becoming a Chaos Engineer
- author : Nikolai Norman Andersen
- theme : night
- transition : default

***

# Lord of chaos

## Becoming a Chaos Engineer

***

### What is Chaos Engineering

> Chaos Engineering is the discipline of experimenting on a distributed system
in order to build confidence in the system’s capability
to withstand turbulent conditions in production.

<!-- And why is this so important now? -->

***

#### Microservices gives us more

- Network communication
- Moving parts
- Configuration
- Possible failures
- Concepts to understad <!-- Like Service discovery and Circuit breakers -->

<!-- Our software systems are becoming more complex and more distributed. Microservices has become a household word, and many greenfield projects starts with small services from scratch. While it gives a lot opportunities, especially when it comes to scaling, polyglot solutions and maintenance, it also gives us a new set of problems: More network communication and more moving parts. We have a lot more configuration and we need to gracefully handle failures. Most likely we need service discovery and we are probably using a circuit breaker or two. This is getting complicated, but we get it working. -->

***

### Even Google goes down!

![Google Compute Engine Incident](images/googlecomputeincident.png)

<!-- So how can we solve it? Well, you should  -->

***

<!-- But how do we trust that all our failure handling will work as expected? How can we be sure that our autoscaling works? -->

### Embrace Chaos

<!-- We use unit tests to make sure our logic is sound, integration tests to test how our modules and systems work together and smoke tests to test more realistic scenarios when our solution is deployed to a environment with similarities to production. However we all know there are bugs or situations that will only occur in production, either because of the data or because of the load. Chaos Testing is a response to all of this. By injecting failures in a controlled experiment we can see how our system handles them. And we do it the only place where it matters: In production! And before you jump out of your chair to yell “Testing in production!? That’s crazy!”, let me tell you a bit more about Chaos Testing in practice: Chaos Testing, or Chaos Engineering, is not about fucking yourself over. It’s about finding weaknesses before they manifest, and to automate the process so you can, at any time - and after any change - be certain that your infrastructure and system can handle failures. -->

***

### Netflix

The Simian Army

<!-- is a suite of tools for keeping your cloud operating in top form. Chaos Monkey, the first member, is a resiliency tool that helps ensure that your applications can tolerate random instance failures -->

***

### Azure Search

??

***

### NoOps == NoWorries

?

***

Our software systems are becoming more complex and more distributed. How do we have confidence in the resilience and redundancy of the systems we put in production? Chaos Engineering is the practice of introducing failures into your system in controlled experiments to learn how your system reacts. In this talk we will look into how to establish the steady state behavior of a system and how to start experimenting to discover if the system can handle spikes in traffic, failures and timeouts.

***

<Show some examples of Netflix, Microsoft and Jet using Chaos Engineering>

This means we have to be aware of the steady state of our distributed system. We need to be able to track metrics that can help us monitor changes in the system, and to after some time determine what the normal state of our system is. This should hopefully already be in place from day one in any distributed system, not for controlled experiments that we are going to do through Chaos Engineering, but to monitor real world failures.

Our hypothesis will be that even as we inject failures, this normal steady state should continue. If it’s taken into account that our system should deliver slower on some areas if a hard drive dies or a service stops, that’s ok. We’ll just add that as part of our hypothesis.

“If service X dies on server Y, the system should still be able to handle N requests per second until service X has been moved and restarted on server Z.”. Most people most likely have a hypothesis like this about their system already, wouldn’t it be awesome to be able to prove it?

It might be hard to choose where to start, but you should start with real world events that are most likely to happen. One service going offline because of a bug in your code might be more likely than Google Cloud Platform going down globally (But yes, that happened for 18 minutes 11. April 2016: https://status.cloud.google.com/incident/compute/16007?post-mortem). So prioritise your test-cases!

Starting to experiment on your own services is probably the easiest. You can start by just shutting down the application gracefully, monitor and see that everything goes ok. Next kill it hard, does your fallbacks still work? When it comes back online, does it take up where it left and is introduced correctly into your distributed system?

Check your metrics, you already know your systems steady state, and should be able to see if this caused any harm. If everything is ok, make sure you write a short script that does exactly what you just did. Put it to run at random times each day. Congratulations!!! You can now put the title Chaos Engineer on your CV and tell your friends to call you Lord of Chaos!

“But I don’t want to put it to run at random, it might run during a critical period, or when load is at its highest!” — if your thinking this, then you don’t really trust your system to handle failures. These are the exact failures we are looking for so that we can make sure they are handled correctly. Just as we want tests for our code to trust our codebase, we want tests for our failure handling so that we can trust the mechanics we’ve put in place to protect our business from the indefinite failure of hard drives, operating systems or even people!

By combining monitoring and automated experiments (Sounds much more sellable to the IT director of your company than automated failure injections!) we can extend our tests by automatically producing detailed reports of each failure — providing data that can be used for future planning and as a basis for future tests.

With the public cloud, we have an even easier time doing Chaos Tests. All the big providers — Google, Azure, AWS, Digital Ocean — all provide huge APIs that lets us inject failures into services and infrastructure. They also give us logs and metrics for our experiments. It has never been easier to do Chaos Engineering!

— Jepsen tests

<Demo showing results of Chaos Tests in a distributed system running in the public cloud. If there is a time, we run a small experiment live as well>
