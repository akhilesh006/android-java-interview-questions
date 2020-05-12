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
      
