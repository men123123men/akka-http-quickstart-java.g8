Backend Actor logic
-------------------

In this example, the backend uses only one basic actor. In a real system, we would have many actors interacting
with each other and perhaps multiple data stores and microservices.

An interesting side-note to add here is: using actors in applications like this adds value
by just providing functions that returns Futures.
In fact, if your logic is stateless and simple request/reply style, you may not need to back it with an Actor.
Actors do shine however when you need to keep some form of state and allow various requests to access something in
(or *through*) an Actor. The other stellar feature of actors, which futures would not handle, is scaling-out onto a
cluster very easily, by using [Cluster Sharding](https://doc.akka.io/docs/akka/current/java/cluster-sharding.html)
or other [location-transparent](https://doc.akka.io/docs/akka/current/java/general/remoting.html) techniques.

However, the focus of this tutorial is on how to interact with an Actor backend from within Akka HTTP -- not on
the actor itself, so we'll keep it very simple.
 
The sample code in the `UserRegistryActor` is straightforward. It keeps registered users in a `Set`. Once it receives
messages it matches them to the defined cases to determine which action to take:

@@snip [UserRegistryActor.java]($g8src$/java/$package$/UserRegistryActor.java)

If you feel you need to brush up on your Akka Actor knowledge, the [Getting Started Guide]
((http://doc.akka.io/docs/akka/current/java/guide/index.html)) reviews actor concepts in
the context of a simple Internet of Things (IoT) example.
