# Learning Java & Android in one go...

## Contents
- Java: :coffee:
   - [Beginner](#beginner_coffee)
   - [Expert](#expert-coffee)
   - [Best practices](#best-practices-coffee)
- Android: :iphone:
   - [Beginner](#beginner-iphone)
   - [Expert](#expert-iphone)
   - [Best practices](#best-practices-iphone)

# Java
### Beginner :coffee:
- Java Memory Areas: All memory area created by JVM memory managers:
   - Heap: Dynamic memory area and Shared among all threads of an application. When full, We get java.lang.OutOfMemoryError.
      - Young Generation Area:
         - Eden Space: Newely created Objects goes in Eden Space.
         - Survivor Space( Two survivor space s0 & s1): When Eden space is filled, Miner GC is performed and all servivour object moved into serviver space. 
      - Old/Tenured Generation Area: The remaining objects moved into Old generation which are surviver after many cycle of miner GC. Major GC is performed when Old generation is full.
   - Permanent Generation(PermGen): It is not part of Heap Memory area. It contains Application's metadeat i.e. classes and methods's description for JVM.
      - Method Area/ Class Area: Shared among all threads of an application. Also called PremGen before Java 8, It contains classes structure, constant pool, static method, static variable, constant, method codes and constructor.
   - Memory Pool: String pool comes under memory pool area. It can belogs to heap or PermGen area depending upon Memory Manager impplementation.
   - Runtime Constant Pool: It contains class specific runtime constant of a class and static method, comes under method area.
   - Stack: Static memory area and constant area, Generated for each thread, When full, We get StackOverflowError, It keeps method reference, local variables of method including argument variable and reference to local object created inside method.
   - Caching(Byte, Character, Integer, Short, Long): Will Discuss it later.
   - Program Counter Register: It is gererated for each thread and it stores current instruction executed by thread.
   - Native Method Stack: Shared among all threads, Same as stack, but used for native method which are outside of Java.
    
   - Creation of PermGen 2006( https://blogs.oracle.com/jonthecollector/presenting-the-permanent-generation )
   - Removal of PermGen 2014(https://blogs.oracle.com/poonam/about-g1-garbage-collector,-permanent-generation-and-metaspace)
   - [Changes done in Memory Model of JVM](http://openjdk.java.net/jeps/122): After Java 8 : PermGen kicked-off and MetaSpace kicked-in
      - Class meta-data, interned Strings and class static variables will be moved from the permanent generation to either the Java heap or native memory.
      - Java8 implementation move Class meta-data in native heap called MetaSpace and move interned Strings and class statics to the Java heap.
      - By default metaspace is unlimited and GC happens after 16 MB. its limit is specified with MaxMetaspaceSize. GC internally maintains what we call as the high-water-mark for the metaspace at which collections for the Metaspace are invoked, and it gets initialized with the value specified with MetaspaceSize. The HWM value is lowered or raised depending upon the free space after a GC.

   - The value of MaxMetaspaceFreeRatio determines how much maximum free space should be available after a GC. If the committed space available after a GC is more than MaxMetaspaceFreeRatio value, then the HWM is lowered.
   - The code for the permanent generation in the Hotspot JVM will be removed.

   - Each Thread contains:
      - Stack, 
      - Program Counter(PC) register
      - Native Statck
   - Shared Things among all thread:
      - Heap
      - PermGen/ Class Area/ Method Area
   - Each Object contains:
      - Monitor
      - Wait Set
      
   - Escape Analysis (EA) : It is a tool that the JIT compiler used to check the scope of the newly created object and decide weather the object will be placed in a heap or stack.
   - There are three type of escape states objects:
      - NoEscape – When the object is not visible outside of the current method or thread.
      - ArgEscape – When the object is passed to a method by argument and is not visible outside of the current method or other threads.
      - GlobalEscape – When the object is visible by outside of the method or the thread, e.g when a object is returned from a method or is declared static. 
    
   - If the object is NoEscape, It will not be kept in Heap area, Instead it will reside in Stack area.
   - If the object is NoEscape or ArgEscape, JIT compiler can revove the locking and synchronization technique to make it fast. e.g. If a StringBufer is declare inside a method body It will be called NoExcape object, and JIT compile will remove locking and syncronization check on its object.   
    
- HashMap vs LinkedHashMap
    - [Difference between HashMap LinkedHashMap and TreeMap](https://stackoverflow.com/questions/2889777/difference-between-hashmap-linkedhashmap-and-treemap)
- ConcurrentHashMap:
    - [Difference HashMap ConcurrentHashMap](https://www.geeksforgeeks.org/difference-hashmap-concurrenthashmap/)

### Intermidiate :coffee:
- Threading[http://tutorials.jenkov.com/java-concurrency/index.html]
    - [Semaphore](https://www.geeksforgeeks.org/java-util-concurrent-semaphore-class-java/)
    Semaphore sem = new Semaphore(5, true); creating a Semaphore object with number of permits 5 and fairness true.
    A semaphore maintains a set of permits. Each acquire() blocks if necessary until a permit is available, and then takes it. Each release() adds a permit, potentially releasing a blocking acquirer. However, no actual permit objects are used; the Semaphore just keeps a count of the number available and acts accordingly.
    - void acquire() - This method acquires a permit, if one is available and returns immediately, reducing the number of available permits by one.
    - void acquire(int permits) - This method acquires the given number of permits, if they are available, and returns immediately, reducing the number of available permits by the given amount.
    - void release() - This method releases a permit, increasing the number of available permits by one. 
    - void release(int permits) - This method releases the given number of permits, increasing the number of available permits by that amount.

    - [volatile](http://tutorials.jenkov.com/java-concurrency/volatile.html)
    - When is use of volatile is not always enough?
    - volatile int a = a++ + 2; // a++ is not a atomic statement. 
    Imagine if Thread 1 reads a shared counter variable with the value 0 into its CPU cache, increment it to 1 and not write the changed value back into main memory. Thread 2 could then read the same counter variable from main memory where the value of the variable is still 0, into its own CPU cache. Thread 2 could then also increment the counter to 1, and also not write it back to main memory. Thread 1 and Thread 2 are now practically out of sync. The real value of the shared counter variable should have been 2, but each of the threads has the value 1 for the variable in their CPU caches, and in main memory the value is still 0.
    - When is use of volatile enough?
    If two threads are both reading and writing to a shared variable, then using the volatile keyword for that is not enough. You need to use a synchronized in that case to guarantee that the reading and writing of the variable is atomic. Reading or writing a volatile variable does not block threads reading or writing. For this to happen you must use the synchronized keyword around critical sections.
    - As an alternative to a synchronized block you could also use one of the many atomic data types found in the java.util.concurrent package. For instance, the AtomicLong or AtomicReference or one of the others.

    - [How to work with wait(), notify() and notifyAll() in Java?](https://howtodoinjava.com/java/multi-threading/wait-notify-and-notifyall-methods/)
    - wait(0) - If timeout is zero, however, then real time is not taken into consideration and the thread simply waits until notified. wait(0) is same as wait().
    - Thread.yield(), Thread.sleep(0), Object.wait(0,1) and LockSupport.parkNanos(1) They all wait a sort period of time, but how much that is varies a surprising amount and between platforms.
    - Object.wait(long timeout, int nanos) causes current thread to wait until either another thread invokes the notify() method or the notifyAll() method for this object, or a specified amount of time has elapsed.
    - In particular, wait(0, 0) means the same thing as wait(0) and wait(0) is same as wait();
    
    - Java Wrapper Class Caching technique: It is used to improve perforamnce and save memory. It only works on autoboxing.
      - Byte : private static ByteCache inner class : Range -127 to +127
      - Short : private static ShortCache inner class : Range -127 to +127
      - Long : private static LongCache inner class : Range -127 to +127
      - Integer : private static IntegerCache inner class : Range -127 to +127
      - Character : private static CharacterCache inner class : Range 0 to +127
      
    - We can be modified this range only for Integer by using a VM argument -XX:AutoBoxCacheMax=size

```java
   Integer x = 10; //autoboxing
   Integer y = Integer.valueOf(10); //inside story
   Integer z = new Integer(100);
   System.out.println(x == y); // true
   System.out.println(x == z); // false
   System.out.println(y == z); // false
   
   Integer x1 = 128; //autoboxing
   Integer x2 = 128; //autoboxing
   System.out.println(x1 == x2); // false   

// Integer's valueOf API
   public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
   }

```

### Expert :coffee:
- Singleton Design pattern
    - [Double checked locking on singleton in java](http://javarevisited.blogspot.in/2014/05/double-checked-locking-on-singleton-in-java.html)
    - [When to use a singleton and when to use a static class](https://softwareengineering.stackexchange.com/questions/235527/when-to-use-a-singleton-and-when-to-use-a-static-class)
- Executers: 
    - [Executor framework understanding the basics](https://android.jlelse.eu/executor-framework-understanding-the-basics-43d575e72310)
    - [AsyncTasks threads pools executors android](https://academy.realm.io/posts/360andev-stacy-devino-async-tasks-threads-pools-executors-android/)
- Callable vs Runnable: 
    - [The difference between the runnable and callable interfaces in java](https://stackoverflow.com/questions/141284/the-difference-between-the-runnable-and-callable-interfaces-in-java)
    - [Java runnable callable](http://www.baeldung.com/java-runnable-callable)
    - [Difference between callable and runnable java](http://www.java67.com/2013/01/difference-between-callable-and-runnable-java.html)
- Immutable class:
    - [Immutable object with ArrayList member variable why can this variable be chang](https://stackoverflow.com/questions/6137224/immutable-object-with-arraylist-member-variable-why-can-this-variable-be-chang)

# Android
### Beginner :iphone:
- Fragment addToBackstack vs not add to backStack
    - [Difference between add replace and addToBackStack](https://stackoverflow.com/questions/18634207/difference-between-add-replace-and-addtobackstack)
    - [What is the purpose of null in addToBackStack(null)](https://www.codeproject.com/Questions/818401/What-is-the-purpose-of-null-in-addToBackStack-null)
    - [Fragment lifecycle during fragment transaction](https://androidlearnersite.wordpress.com/2017/02/27/fragment-lifecycle-during-fragment-transaction)

### Expert :iphone:
- Design pattern | MVC, MVP & MVVM:
    - [MVC MVP MVVP android app development](https://www.simform.com/mvc-mvp-mvvm-android-app-development/)
    - [Shared User Id](https://groups.google.com/forum/#!topic/android-security-discuss/eLPuV6uLQw8)
      SharedUserId is used to share the data,processes etc between two or more applications. It is defined in AndroidManifest.xml like
      ```xml
      <manifest
          xmlns:android="http://schemas.android.com/apk/res/android"
          android:sharedUserId="android.uid.shared"
          android:sharedUserLabel="@string/sharedUserLabel"
      ...>
      ```
      [Uses]https://stackoverflow.com/questions/9783765/what-is-shareduserid-in-android-and-how-is-it-used
      - SharedUserId is deprecated in API level 29, Android Q --> Android 10.
      

### Common Tips & Tricks for Competitive Programming.
#### Big-O: Time Complexity Order
O(1) < O(log n) < O(\sqrt{n}) < n < n log n < n<sup>2</sup> < n<sup>3</sup> ... < 2<sup>n</sup> < 3<sup>n</sup> ... < n! < n<sup>n</sup>

- [how-to-create-a-memory-leak-in-java](https://stackoverflow.com/questions/6470651/how-to-create-a-memory-leak-in-java)
