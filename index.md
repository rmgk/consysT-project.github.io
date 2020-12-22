---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# layout: home
---

# What is ConSysT?

ConSysT is a distributed object-oriented language. Objects can be replicated with different levels of [consistency](https://en.wikipedia.org/wiki/Consistency_model).
 The type system ensures that consistency levels are mixed safely.

<div id="featureparent">
	<div class="feature">
		<h4>Multiple consistency levels</h4>
		<p>Each replicated object comes with its own consistency level.</p>
	</div>
	<div class="feature">
		<h4>Safe mixing of consistencies</h4>
		<p>The static type system ensures correct mixing of consistency levels.</p>
	</div>
	<div class="feature">
		<h4>Object-oriented programming</h4>
		<p>Consistency is fully integrated with object-oriented abstractions.</p>
	</div>
</div>

<!-- # What is consysT?

Many modern applications use some distribution of data -- sharing pictures with friends, contacting payment servers, or reading news.
In particular, replication of data is useful when scalability, failure tolerance, offline functionality or latency play a role.
For these reasons, data is replicated over devices in a local network, datacenter, or world-wide.

However, when data can be modified, data consistency is a challenge for the system and for developers.
Keeping data consistent all the time is costly as replicas have to coordinate continuously, but may be important to guarantee application correctness.
To counteract this Weak consistency models have been developed to reduce the coordination cost, but developers have to reason about temporarily inconsistent data or asynchronous change propagation.

To make things worse, developers often have to mix consistency models in the same application. -->

<!-- **consysT** is a language and middle ware for that purpose. It lets developers easily define data with different consistency models. It tracks the replicated data and its consistency models through the application and ensures that consistency models are mixed correctly. -->

### How does ConSysT look like?

```java
class Concert {
	Date date;
	//Define fields that reference other replicated objects.
	JRef<@Eventual ConcertHall> hall;
	JRef<@Eventual Band> band;
	//Fields can have different consistency levels.
	JRef<@Sequential Counter> soldTickets;

	//Define operations as Java methods...
	int getSoldTickets() {
		//... and execute them on replicated objects.
		return soldTickets.ref().value;
	}

	...
}
```

You define replicated objects just like normal Java classes. Operations on replicated data is defined as methods. Executing an operation is just as easy as calling a method.

# Overview

In **ConSysT**, the main abstraction are _replicated objects_ that are fully integrated into an _object-oriented_ language.
Replicated objects have a _consistency level_ specified by the developer.

<!-- Strong consistency levels ensure that application invariants always hold but come at the cost of availability.
Weak models, on the other hand, may have temporary inconsistencies but have a high availability. -->

<!-- Since applications usually work with various consistency levels, consysT uses a *static consistency type system* to ensure that developers *safely mix* data with different consistency levels.

Besides the language, consysT also provides the middleware for distributing replicated data. -->

<!-- **consysT** features easy replication of data using various consistency models and ensures that replicated data with different consistency models is mixed correctly. -->

### Distribution

Easily distribute your your data across your local network, datacenters or geo-replicated devices. _Replicated objects_ allow to distribute and perform operations on your data. As ConSysT is implemented as a language extension to Java, you can create replicated objects from already existing Java classes.

```java
class MyClass {
	void myMethod() { ... }
}

//Create a replicated object.
JRef<MyClass> obj1 = sys.replicate(MyClass.class);

//Perform a distributed operation.
obj1.ref().myMethod();
```

### Consistency

Method invocations on replicated objects are handled as operations on replicated data by the system. [Consistency models](http://jepsen.io/consistency) define how the system keeps replicas consistent. Developers can opt to use weak consistency models, like [Eventual Consistency](https://en.wikipedia.org/wiki/Eventual_consistency), to boost performance or use strong models, like [Sequential Consistency](https://en.wikipedia.org/wiki/Sequential_consistency), to reduce application complexity. In ConSysT, developers state their desired consistency model as a _consistency level_ attached to each replicated object.

```java
//Define consistency as part of the type.
JRef<@Eventual MyClass> obj1 = ...
```

### Safety

Applications generally use more than one consistency level. As consistency can be corrupted when consistency levels are mixed mindlessly, ConSysT adopts a special _consistency type system_.
The type system ensures that objects with strong levels are _not_ affected by weak  data. More precisely, ConSysT orders consistency levels in a lattice and checks that there is no _information-flow_ from weak to strong levels.

```java
JRef<@Eventual MyClass> obj1 = sys.replicate(MyClass.class);
JRef<@Sequential MyClass> obj2 = sys.replicate(MyClass.class);

if (obj1.ref().f == 42) {
	//Type error! Disallowed information-flow from obj1 to obj2.
	obj2.ref().f = 42;
}
```

<!-- # Example


We introduce how **consysT** works with an example.
Assume you have the following `Counter` class in Java.

```java
class Counter {
	int value;

	Counter(int value) {
		this.value = value;
	}

	void inc() {
		value = value + 1;
	}

	int get() {
		return value;
	}
}
``` -->

### Download

<div class="tryout">
<h5>Try it out</h5>
ConSysT is <a href="https://github.com/consysT-project/consyst-code"><strong>available</strong></a> as a language extension to Java.
<br>
Follow the <a href="install.html"><strong>installation instructions</strong></a> to get started.
</div>

# Academic Publications

-   Mirko Köhler, Nafise Eskandani, Pascal Weisenburger, Alessandro Margara, Guido Salvaneschi: [Rethinking Safe Consistency in Distributed Object-Oriented Programming](oopsla2020.pdf). Proc. ACM Program. Lang. 4, OOPSLA, Article 188 (November 2020), 30 pages. <https://doi.org/10.1145/3428256>

-   Mirko Köhler, Nafise Eskandani Masoule, Alessandro Margara, and Guido Salvaneschi. 2020. [ConSysT: Tunable, Safe Consistency Meets Object-Oriented Programming](ftfjp2020.pdf). In Proceedings of the 22th ACM SIGPLAN International Workshop on Formal Techniques for Java-Like Programs (FTfJP ’20), July 23, 2020, Virtual, USA. ACM, New York, NY, USA, 3 pages. <https://doi.org/10.1145/3427761.3428346>

-   Nafise Eskandani, Mirko Köhler, Alessandro Margara, Guido Salvaneschi:
    [Distributed object-oriented programming with multiple consistency levels in ConSysT](https://dl.acm.org/doi/10.1145/3359061.3362779). SPLASH (Companion Volume) 2019: 13-14

-   Alessandro Margara, Guido Salvaneschi: [Consistency Types for Safe and Efficient Distributed Programming](https://dl.acm.org/doi/10.1145/3103111.3104044). FTFJP 2017.

# Credits

ConSysT is a project developed at the Technical University of Darmstadt and at Politecnico di Milano.
