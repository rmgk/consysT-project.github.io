---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# layout: home
---

**consysT** is a *statically-typed* language for programming with replicated data using various *consistency models*.
Consistency model specifications allow to boost performance where possible or to increase consistency where needed.
The static type system ensures *safe mixing* of replicated data with different consistency levels.
The language features are integrated into *object-oriented programming* and are easily used in existing Java programs.


# Features

<!--
| Distribution           | Consistency                   | Correctness |
|:------------------------|:------------------------------|:----------------------|
|   hmm        | good swedish fish | nice  |
-->

* **Distribution.** Easily distribute your your data. Use *replicated objects* from already defined Java classes and distribute them across devices.
```java
JRef<String> string1 = sys.replicate(MyClass.class);
```

* **Consistency.** Boost performance or increase consistency by simply stating your desired replication strategy as a *consistency level*.
```java
JRef<@Weak String> string1 = ...
```

* **Correctness.** The special *consistency type system* ensures that consistency guarantees can not be corrupted.
```java
JRef<@Weak String> string1 = sys.replicate("Hello World!");
JRef<@Strong String> string2 = string1; //type error!
```


# Try it out

[**consys** is available on GitHub](https://github.com/consyst-project/consyst-code). Follow the [installation instructions](install.md) to get started.


# What is consysT?

Many modern applications use some distribution of data -- sharing pictures with friends, contacting payment servers, or reading news.
In particular, replication of data is useful when scalability, failure tolerance, offline functionality or latency play a role.
For these reasons, data is replicated over devices in a local network, datacenter, or world-wide.

However, when data can be modified, data consistency is a challenge for the system and for developers.
Keeping data consistent all the time is costly as replicas have to coordinate continuously, but may be important to guarantee application correctness.
To counteract this Weak consistency models have been developed to reduce the coordination cost, but developers have to reason about temporarily inconsistent data or asynchronous change propagation.

To make things worse, developers often have to mix consistency models in the same application.

**consysT** is a language and middle ware for that purpose. It lets developers easily define data with different consistency models. It tracks the replicated data and its consistency models through the application and ensures that consistency models are mixed correctly.


# How to use consysT?

**consysT** is implemented as a language extension to Java.
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
```



<!--
ust create a new *replicated object* and consys manages the rest.

, you can define the [*consistency model*](https://jepsen.io/consistency) which defines how changes of your replicated data are propageted. For example, it may suffice to not immediately propagate changes and allow concurrent updates in order to gain performance. consys lets you define your desired consistency model separately for each object as part of a consistency type.

that ensures correct mixing objects with with different consistency models. Incompatible consistency models can not be mixed in a way that would corrupt consistency guarantees, while still allowing mixing where it is sensible.
-->
