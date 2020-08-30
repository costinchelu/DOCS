# Java Memory Leaks

With Java memory management being a complex domain, I do understand the
background of this anxiety. When your software does not perform the way
it should, the current state of root cause detection forces you to apply
different kinds of dark arts to really understand what is going on.
Often enough, the process involves a lot of guesswork. One of the
frequent guesses seems to often take the form of, “Gosh, I have a memory
leak”. In this post, I would like to give some examples of different
situations and suggest patterns that you can follow to verify whether or
not you actually are a victim of a memory leak.

I will walk you through four different patterns of memory usage,
explaining which of these are symptomatic to memory leaks and which ones
are not. Equipped with this information, you can reduce the amount of
guesswork the next time you are suspecting a leak.

For all the four examples below, we will look at heap consumption in the
JVM over time. You can access this information via a variety of
different solutions: JMX beans, garbage collection logs, Java monitoring
tools, profilers, APMs, and our very own [Plumbr](https://plumbr.eu/)
are all capable of plotting out memory consumption over time.

Healthy JVM
-----------

Our first example presents memory usage of a perfectly healthy JVM.
Seeing the following pattern...

![java memory usage
example](images/java-memory-usage-example.png)

...is a confirmation that the JVM at question is definitely **not**
leaking memory. The indicator giving me the confidence to claim it is in
the flat baseline trend in the double-sawtooth pattern where the memory
usage steadily increases and decreases in small increments and then
drops a lot suddenly.

If you are unfamiliar with the Garbage Collection internals, it might be confusing at first. Understanding the reasons, however, unlocks the door to understanding the basics of the Java garbage collection.

The reason for the double-sawtooth pattern is that the JVM needs to
allocate memory on the heap as new objects are created as a part of the
normal program execution. Most of these objects are short-lived and
quickly become garbage. These short-lived objects are collected by a
collector called “[Minor
GC](https://plumbr.eu/handbook/garbage-collection-in-java#minor-gc)” and
represent the small drops on the sawteeth.

Longer-living objects are kept in a different memory region and are
collected less frequently, as their expected lifetime is considered to
be longer. When this separate region in memory becomes too crowded, it
is also collected, and you will see a steeper drop in memory consumption
after the so-called [Major
GC](https://plumbr.eu/handbook/garbage-collection-in-java#major-gc-vs-full-gc)
finishes its work.

A memory leak in Java is a situation where objects that are no longer
needed for the application are referred from other objects, blocking the
garbage collector from removing the objects. Bearing in mind that
definition, we can see that the above JVM is definitely not suffering
from a memory leak. There is no growth trend in the long run, indicating
that all objects, in fact, can and will be garbage collected, allowing
us to claim that the application is leak-free.

So, all-in-all,**whenever the baseline trend after major GC events is
flat or declining, the application at hand does not contain a memory
leak**and the root cause for your performance issue is hidden somewhere
else.

Pay attention that when zooming into a shorter period of time, the
picture can be deceiving. For example, when the period does not contain
any major GC events collecting the old generation, you could be facing a
situation similar to the following where we are looking at just five
minutes of the very same JVM:

![java memory usage short
trend](images/java-memory-usage-short-trend.png)

There has been no major GC events collecting the old generation, thus
the picture would look scary enough to start suspecting a memory leak.
So whenever you are analyzing the behavior, you would need to make sure
the period you are monitoring contains major GC events in addition to
minor garbage collection events.

Memory Explosion at Startup
---------------------------

As a second example, let us look at the memory consumption chart that
exposes a different pattern:

![java memory usage quick growth at
startup](images/java-memory-usage-quick-growth-at-startup.png)

This situation occurs shortly after a JVM is started. The memory usage
grows rapidly, reaching the maximum allowed memory just seconds after
the JVM was started. The JVM usually dies quickly with an
[OutOfMemoryError](https://plumbr.eu/outofmemoryerror) being thrown.

In such a situation, the first suspect again should not be a memory
leak. In 99.99% of the cases, there is a situation where an XXL-sized
application is attempted to be squeezed into an S-sized Java heap space.

The solution for such case is just to make sure you have given enough
heap for the application to start. Increasing (or adding) the maximum
heap size via the *-Xmx*parameter is the first place to start solving
the problem in such situations.

Surge Allocation
----------------

The third example that we will analyze again presents a different heap
consumption pattern:

![java memory usage
spike](images/java-memory-usage-spike.png)

The above memory usage pattern corresponds to a spike in [allocation
rate](https://plumbr.eu/handbook/gc-tuning-in-practice/high-allocation-rate).
The JVM has been functioning normally for a while until a sudden surge
appears, after which the JVM might or might not throw an
[OutOfMemoryError](https://plumbr.eu/outofmemoryerror) and die,
depending on the way the application has been implemented.

This symptom often indicates a programming error resulting in too much
data being loaded via a specific user action. A typical example includes
searches loading millions of objects from storage into the JVM memory.
Again, we are not speaking about a memory leak, and solution for the
problem is as easy as limiting the number of objects actually loaded
into the memory via potentially dangerous operations.

Leaking Application
-------------------

The last pattern is finally one that corresponds to a leaking
application:

![java memory
leak](images/java-memory-leak.png)

A memory usage pattern above suggests the presence of a memory leak. The
key is in baseline growth – instead of the flat trendline seen in the
first example, the major GCs constantly free less and less memory
exposing a clear growth trend. This trend is dangerous and will
eventually lead to memory exhaustion and application crash via
[OutOfMemoryError](https://plumbr.eu/outofmemoryerror).

In such a situation you would need to collect information from within
the JVM to understand what is actually consuming the memory. There are
several tools available for the job. Being proud of my own craft, I can
definitely recommend our very own [Plumbr](https://plumbr.eu/) for the
job. Using Plumbr, you get full transparency to the most memory-hungry
data structures in your JVM during runtime with minimal impact to
runtime performance. Other solutions in the field include heap dump
analyzers (with [Eclipse MAT](http://eclipse.org/mat) being most widely
used one) or profilers to name a few.

Conclusions
-----------

I do believe that memory leaks are one of the most widely misunderstood
concepts among Java developers. Hopefully, this article will allow some
of our readers to skip the ghost-chasing process. After all, only one of
the symptoms above is actually correlated to leakage, so if I save
someone a week of troubleshooting, this article has fulfilled its
purpose.

[Link to article](https://dzone.com/articles/memory-leaks-fallacies-and-misconceptions?fromrel=true#)
