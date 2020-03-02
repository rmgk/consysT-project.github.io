---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# layout: home
---

# What is ConSysT?

ConSysT is an distributed object-oriented language. Objects can be replicated with different levels of [consistency](https://en.wikipedia.org/wiki/Consistency_model).
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

# Overview

In **ConSysT**, the main abstraction are _replicated objects_ that are fully integrated into an _object-oriented_ language.
Replicated objects have a _consistency level_ specified by the developer.



<!-- Strong consistency levels ensure that application invariants always hold but come at the cost of availability.
Weak models, on the other hand, may have temporary inconsistencies but have a high availability. -->

<!-- Since applications usually work with various consistency levels, consysT uses a *static consistency type system* to ensure that developers *safely mix* data with different consistency levels.

Besides the language, consysT also provides the middleware for distributing replicated data. -->

<!-- **consysT** features easy replication of data using various consistency models and ensures that replicated data with different consistency models is mixed correctly. -->

### Distribution

Easily distribute your your data across geo-replicated devices, datacenters, or in a local network. _Replicated objects_ allow to distribute and perform operations on your data. As consysT is implemented as a language extension to Java, you can use already existing Java classes and replicate them with ease.

```java
//Create a replicated object.
JRef<MyClass> obj1 = sys.replicate(MyClass.class);

//Perform a distributed operation.
obj1.ref().myMethod();
```

### Consistency

Boost performance or increase consistency by simply stating your desired replication strategy as a _consistency level_. Just define the consistency level, e.g., Weak, when you create a replicated object and the consysT middleware manages the rest.

```java
//Define consistency as part of the type.
JRef<@Weak MyClass> obj1 = ...
```

### Correctness

The special _consistency type system_ ensures that consistency guarantees can not be corrupted. The type system ensures that objects that are Strong are affected by objects that are Weak. This type system does not only check explicit data-flow but also implicit information-flow.

```java
JRef<@Weak MyClass> obj1 = sys.replicate(MyClass.class);
JRef<@Strong MyClass> obj2 = sys.replicate(MyClass.class);

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


# Academic Publications



<!--
ust create a new *replicated object* and consys manages the rest.

, you can define the [*consistency model*](https://jepsen.io/consistency) which defines how changes of your replicated data are propageted. For example, it may suffice to not immediately propagate changes and allow concurrent updates in order to gain performance. consys lets you define your desired consistency model separately for each object as part of a consistency type.

that ensures correct mixing objects with with different consistency models. Incompatible consistency models can not be mixed in a way that would corrupt consistency guarantees, while still allowing mixing where it is sensible.
-->
<div class="tryout">
<h5>Try it out</h5>
consysT is implemented as a language extension to Java and <a href="https://github.com/consysT-project/consyst-code"><strong>available on GitHub</strong></a>.
<br>
Follow the <a href="install.html"><strong>installation instructions</strong></a> to get started.
</div>
