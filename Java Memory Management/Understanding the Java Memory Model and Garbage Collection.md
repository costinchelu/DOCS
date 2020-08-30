

### Are you cavalier with your data allocations? Don't worry, Java has a built-in recycling plant. It has strange places like (the Garden of) Eden. All of this is convenient and nicely explained. It also makes clear to C++ programmers why Java is never used in critical, real-time systems such as aerospace ;-)

In this article we will try to understand the Java memory model and how
garbage collection works. In this article I have used JDK8 Oracle Hot
Spot 64 bit JVM. First let me depict the different memory areas
available for Java processes.

![JVM Memory
Allocations](images/jvm-memory-allocations1.png)

Once we launch the JVM, the operating system allocates memory for the
process. Here, the JVM itself is a process, and the memory allocated to
that process includes the Heap, Meta Space, JIT code cache, thread
stacks, and shared libraries. We call this native memory. “***Native
Memory***” is the memory provided to the process by the operating
system. How much memory the operating system allocates to the Java
process depends on the operating system, processor, and the JRE. Let me
explain the different memory blocks available for the JVM.

**Heap Memory:** JVM uses this memory to store objects. This memory is
in turn split into two different areas called the “***Young Generation
Space***” and “***Tenured Space***“.

**Young Generation:** The Young Generation or the New Space is divided
into two portions called “***Eden Space***” and “***Survivor Space**"*.

**Eden Space:**When we create an object, the memory will be allocated
from the Eden Space.

**Survivor Space:** This contains the objects that have survived from
the Young garbage collection or Minor garbage collection. We have two
equally divided survivor spaces called S0 and S1.

**Tenured Space:** The objects which reach to max tenured threshold
during the minor GC or young GC, will be moved to “***Tenured Space***”
or “**Old Generation Space**“.

When we discuss the garbage collection process we will come to know how
the above memory locations will be used.

**Meta Space:** This memory is out of heap memory and part of the native
memory. As per the document by default the meta space doesn’t have an
upper limit. In earlier versions of Java we called this “***Perm Gen
Space**".* This space is used to store the class definitions loaded by
class loaders. This is designed to grow in order to avoid 0ut of memory
errors. However, if it grows more than the available physical memory,
then the operating system will use virtual memory. This will have an
adverse effect on application performance, as swapping the data from
virtual memory to physical memory and vice versa is a costly operation.
We have JVM options to limit the Meta Space used by the JVM. In that
case, we may get out of memory errors.

**Code Cache:** JVM has an interpreter to interpret the byte code and
convert it into hardware dependent machine code. As part of JVM
optimization, the Just In Time (JIT) compiler has been introduced. The
frequently accessed code blocks will be compiled to native code by the
JIT and stored it in code cache. The JIT compiled code will not be
interpreted.

Now let us discuss the garbage collection process. The JVM uses a
separate demon thread to do garbage collection. As we said above when
the application creates the object the JVM try to get the  required
memory from the eden space. The JVM performs GC as minor GC and major
GC. Let us understand the minor GC.

[![Minor Garbage
Collection](images/minor-garbage-collection.png)

Initially the survivor space and the tenured space is empty. When the
JVM is not able to get the memory from the eden space it initiates minor
GC. During minor GC, the objects which are not reachable are marked to
be collected. The JVM selects one of the survivor spaces as “To Space”.
It might be S0/S1. Let us say the JVM selected S0 as the “To Space”. The
JVM copies the reachable objects to “To Space”, S0, and increments the
reachable object's age by 1. The objects which are not fit into the
survivor space will be moved to the tenured space.* *This process is
called “***premature promotion”**. For this image's purpose I have made
 the “To Space” bigger than the allocated space. Remember the survivor
space won’t grow.*

![Minor Garbage
Collection](images/minor-garbage-collection-2.png)

In the above diagram, the objects marked with a red color indicates that
they are non-reachable. All the reachable objects are GC roots. The
garbage collector won’t remove the GC roots. The garbage collector
removes the non-reachable objects and empties the eden space.

For the second minor GC, the garbage collector marks the non-reachable
objects from “eden space” and the “To survivor space (S0)”, copies the
GC roots to the other survivor space S1, and the reachable object's age
will be incremented.

![Minor Garbage
Collection](images/minor-garbage-collection-3.png)

In the above diagram, the objects marked with red are eligible for GC,
and the other objects will be copied from the eden and survivor spaces
to the other survivor space, S1, and the objects age incrementally.

![Minor Garbage
Collection](images/minor-garbage-collection-3.png)

The above process repeats for each minor GC. When objects reach the max
age threshold, then those objects are copied to the tenured space.

![Minor Garbage
Collection](images/minor-garbage-collection-5.png)

There is a JVM level option called “***MaxTenuringThreshold***” to
specify the object age threshold to promote the object to tenured space.
By default the value is 15.

So it is clear that minor GC reclaims the memory from the “***Young
Generation Space**"*. Minor GC is a “**s*****top the world***” process.
Some times the application pause is negligible. The minor GC will be
performed with single thread or multi-thread, based on the GC collector
applied.

If minor GC triggers several times, eventually the “***Tenured Space***”
will be filled up and will require more garbage collection. During this
time the JVM triggers a “***major GC***” event. Some times we call this
full GC. But, as part of full GC, the JVM reclaims the memory from “Meta
Space”. If there are no objects in the heap, then the loaded classes
will be removed from the meta space.

Now let us see what possibilities make the JVM trigger major GC.

-   If the developer calls `System.gc()`, or
     `Runtime.getRunTime().gc()` suggests the JVM to initiate GC.
-   If the JVM decides there is not enough tenured space.
-   During minor GC, if the JVM is not able to reclaim enough memory
    from the eden or survivor spaces, then a major GC may be triggered. 
-   If we set a “MaxMetaspaceSize” option for the JVM and there is not
    enough space to load new classes, then the JVM triggers a major GC.
