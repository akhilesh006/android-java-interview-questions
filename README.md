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
