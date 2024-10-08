---
title: Concurrency
parent: Java
---

# Concurrency
- <https://www.baeldung.com/java-stop-execution-after-certain-time>
- <https://gist.github.com/djspiewak/46b543800958cf61af6efa8e072bfd5c>
- <https://engineering.zalando.com/posts/2019/04/how-to-set-an-ideal-thread-pool-size.html>

## Keywords
- **volatile**
  - *are variables that are always read directly from main memory. When a new value is assigned to a volatile variable the value is always written immediately to main memory. This guarantees that the latest value of a volatile variable is always visible to other threads running on other CPUs*
  - *Other threads will read the value of the volatile from main memory every time, instead of from e.g. the CPU cache of the CPU the threads are running on.*
  - *Volatile variables are non-blocking. The writing of a value to a volatile variable is an atomic operation*
  - *However, a read-update-write sequence performed on a volatile variable is not atomic. Thus, this code may still lead to race conditions if performed by more than one thread: `private volatile int var = 0; ... var++;` When executed, the value of var is read into a CPU register or the local CPU cache, one is added, and then the value from the CPU register or CPU cache is written back to main memory.*
  - *In some cases you only have a single thread writing to a shared variable, and multiple threads reading the value of that variable. No race conditions can occur when only a single thread is updating a variable, no matter how many threads are reading it. Therefore, whenever you have only a single writer of a shared variable you can use a volatile variable.*
- **synchronized**

## JDK API

### java.lang
- **Thread**
  - *A thread is a thread of execution in a program. The Java Virtual Machine allows an application to have multiple threads of execution running concurrently.*
  - Methoden
    - `long	getId()`
    - `String	getName()`
    - `int getPriority()`
    - `Thread.UncaughtExceptionHandler getUncaughtExceptionHandler()`
    - `boolean isDaemon()`
      <br/>default: false
      ```
      t.setDaemon(true);
      t.start();
      ```
      *if the last non-daemon thread exits then [remaining daemon] thread[s] will be killed by the JVM*
    - `void	join()` (+2 Overloads)
    - `void	run()`
    - `void	start()`
      - *Causes this thread to begin execution; the Java Virtual Machine calls the run method of this thread.*
    - `static void yield()`
      - *A hint to the scheduler that the current thread is willing to yield its current use of a processor.*
    - `void interrupt()`
      - keine Garantie, funktioniert z. B. nicht bei infinite loops
      - *There's no guarantee that the execution is stopped after a certain time. The main reason is that not all blocking methods are interruptible. In fact, there are only a few well-defined methods that are interruptible. So, if a thread is interrupted, nothing else will happen until it reaches one of these interruptible methods.*
      - <https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#interrupt-->
        - *If this thread is blocked in an invocation of the wait(), wait(long), or wait(long, int) methods of the Object class, or of the join(), join(long), join(long, int), sleep(long), or sleep(long, int), methods of this class, then its interrupt status will be cleared and it will receive an InterruptedException.*
        - *If this thread is blocked in an I/O operation upon an InterruptibleChannel then the channel will be closed, the thread's interrupt status will be set, and the thread will receive a ClosedByInterruptException.*
        - *If this thread is blocked in a Selector then the thread's interrupt status will be set and it will return immediately from the selection operation, possibly with a non-zero value, just as if the selector's wakeup method were invoked.*
        - *If none of the previous conditions hold then this thread's interrupt status will be set.* 
    - `void stop(Throwable?)`
      - deprecated
      - *thread is forced to stop whatever it is doing abnormally and to throw a newly created ThreadDeath object as an exception.*
      - *stopping a thread means that it won't send any of the notifies (etc) that it should have sent. And that leaves other threads stuck waiting for things that won't ever happen. Even though you have (in a sense) broken the deadlock. This kind of thing is part of why Thread.stop() was deprecated ... in the 1990's*
      - <https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#stop-->
      - <https://www.baeldung.com/java-thread-stop> 
    - ...
  - <https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html>
- **ThreadLocal**
  - *allows us to store data that will be accessible only by a specific thread.*
  - *Simply put, we can think that ThreadLocal stores data inside of a map – with the thread as the key.*
  - <https://www.baeldung.com/java-threadlocal>

### java.util
- **Timer**
  - *A facility for threads to schedule tasks for future execution in a background thread.*
  - *Tasks may be scheduled for one-time execution, or for repeated execution at regular intervals.*
  - *Java 5.0 introduced the java.util.concurrent package and one of the concurrency utilities therein is the `ScheduledThreadPoolExecutor` which is a thread pool for repeatedly executing tasks at a given rate or delay. It is effectively a more versatile replacement for the `Timer`/`TimerTask` combination, as it allows multiple service threads, accepts various time units, and doesn't require subclassing `TimerTask` (just implement `Runnable`). Configuring `ScheduledThreadPoolExecutor` with one thread makes it equivalent to `Timer`.*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/Timer.html> 

### java.util.concurrent
- <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html#package.description>
- **Future**
  - *represents a future result of an asynchronous computation*
  - <https://www.baeldung.com/java-future>
  - Task abbrechen
    ```java
    Consumer<Integer> sleep = millis -> {
      try { Thread.sleep(millis);
      } catch (Exception ex) {}
    };
    Runnable task = () -> {
      System.out.println(LocalTime.now() + ": 1");
      sleep.accept(2000);
      System.out.println(LocalTime.now() + ": 2");
      sleep.accept(20000);
      System.out.println(LocalTime.now() + ": 3");
      // mit infinite loop while(true); statt sleep() würde zwar "done" erreicht werden, aber "shutting down" nicht (async task lebt weiter)
    };
    
    Runtime.getRuntime().addShutdownHook(new Thread(() -> System.out.println("shutting down")));
    ExecutorService executor = Executors.newSingleThreadExecutor();
    Future<?> future = executor.submit(task);
    try {
      // blocks main thread
      future.get(3500, TimeUnit.MILLISECONDS);
    } catch (TimeoutException tex) {
      System.out.println(LocalTime.now() +  ": timed out");
      future.cancel(true);
    } finally {
      executor.shutdownNow();
    }
    System.out.println(LocalTime.now() + ": done");
    
    // 12:13:20.994605618: 1
    // 12:13:23.094122851: 2
    // 12:13:24.388485138: timed out
    // 12:13:24.389773458: done
    // shutting down
  ```

  ```java
  // non-blocking:
  ScheduledExecutorService executor = Executors.newScheduledThreadPool(2);
  Future future = executor.submit(new LongRunningTask());
  Runnable cancelTask = () -> future.cancel(true);
  executor.schedule(cancelTask, 3000, TimeUnit.MILLISECONDS);
  executor.shutdown();
  ```

- **CompletableFuture**
  - *enhances `Future` with chaining, manual completion, exception handling, ...*
  - *CompletableFuture executes these tasks in a thread obtained from the global ForkJoinPool.commonPool().* (manche Methoden akzeptieren einen anderen Executor als Argument)
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html> 
  - <https://www.baeldung.com/java-completablefuture>
  - <https://www.baeldung.com/java-executorservice-vs-completablefuture>
- **FutureTask**
  - implements Runnable, Future 
  - *A cancellable asynchronous computation*
  - *can be used to wrap a Callable or Runnable object. Because FutureTask implements Runnable, a FutureTask can be submitted to an Executor for execution.* 
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/FutureTask.html> 
- **Atomic-**
  - <https://www.baeldung.com/java-atomic-variables>
  - AtomicReference
  - AtomicInteger

#### Executors
- **Executor**
  - Interface
  - *An object that executes submitted Runnable tasks*
  - einzige Methode: `void execute(Runnable command)`
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html> 
- **ExecutorService**
  - Interface, extends Executor
  - *provides methods to manage termination and methods that can produce a `Future` for tracking progress of one or more asynchronous tasks*
  - *can be shut down, which will cause it to reject new tasks*
  - *extends base method `Executor.execute(Runnable)` by creating and returning a `Future` that can be used to cancel execution and/or wait for completion*
  - Methoden
    - `Future<?> submit(Runnable task)`
    - `void shutdown()`
      - *Initiates an orderly shutdown in which previously submitted tasks are executed, but no new tasks will be accepted.*
    - `List<Runnable>	shutdownNow()`
      - *Attempts to stop all actively executing tasks, halts the processing of waiting tasks, and returns a list of the tasks that were awaiting execution.*   
    - `boolean awaitTermination(long timeout, TimeUnit unit) throws InterruptedException`
      - *Blocks until all tasks have completed execution after a shutdown request, or the timeout occurs, or the current thread is interrupted, whichever happens first.* 
    - ...
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html>
  - <https://www.baeldung.com/java-executorservice-vs-completablefuture>
- **ScheduledExecutorService**
  - Interface, extends ExecutorService
  - *can schedule commands to run after a given delay, or to execute periodically*
  - Methoden
    - `<V> ScheduledFuture<V>	schedule(Callable<V> callable, long delay, TimeUnit unit)`
      - *Creates and executes a ScheduledFuture that becomes enabled after the given delay.* 
    - `ScheduledFuture<?>	schedule(Runnable command, long delay, TimeUnit unit)`
      - *Creates and executes a one-shot action that becomes enabled after the given delay.* 
    - `ScheduledFuture<?>	scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)`
      - *Creates and executes a periodic action that becomes enabled first after the given initial delay, and subsequently with the given period; that is executions will commence after `initialDelay` then `initialDelay+period`, then `initialDelay + 2 * period`, and so on.*
      - *<mark>If any execution of the task encounters an exception, subsequent executions are suppressed</mark>. Otherwise, the task will only terminate via cancellation or termination of the executor.*
      - *<mark>If any execution of this task takes longer than its period, then subsequent executions may start late, but will not concurrently execute.</mark>* 
    - `ScheduledFuture<?>	scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)`
      - *Creates and executes a periodic action that becomes enabled first after the given initial delay, and subsequently with the given delay between the termination of one execution and the commencement of the next.*
      - *<mark>If any execution of the task encounters an exception, subsequent executions are suppressed</mark>. Otherwise, the task will only terminate via cancellation or termination of the executor.* 
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledExecutorService.html>
  - *(...) This is done by re-adding the periodic task to the queue only after it's execution. The task itself is not present in the queue during it's execution and will never be present in it multiple times.* (<https://stackoverflow.com/a/53529273>) => Wenn die execution time länger ist als delay/period, sammeln sich KEINE verzögerten Tasks in der internen Queue an
- **AbstractExecutorService**
  - *Provides default implementations of `ExecutorService` execution methods* 
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/AbstractExecutorService.html>
- **ThreadPoolExecutor**
  - extends AbstractExecutorService 
  - *executes each submitted task using one of possibly several pooled threads, normally configured using `Executors` factory methods.*
  - *To be useful across a wide range of contexts, this class provides many adjustable parameters and extensibility hooks*
  - *However, <mark>programmers are urged to use the more convenient `Executors` factory methods</mark> (...), that preconfigure settings for the most common usage scenarios. Otherwise, use the following guide when manually configuring and tuning this class:*
  - Es folgen Hinweise zu den Themen: *Core and maximum pool sizes, On-demand construction, Creating new threads, Keep-alive times, Queuing, Rejected tasks, Hook methods, Queue maintenance, Finalization*
  - Methoden
    - `void	setCorePoolSize(int corePoolSize)`
    - `void	setMaximumPoolSize(int maximumPoolSize)`
    - ... 
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html> 
- **ScheduledThreadPoolExecutor**
  - extends ThreadPoolExecutor implements ScheduledExecutorService 
  - *A ThreadPoolExecutor that can additionally schedule commands to run after a given delay, or to execute periodically.*
  - Methoden
    - `void setContinueExistingPeriodicTasksAfterShutdownPolicy(boolean value)`
      - *Sets the policy on whether to continue executing existing periodic tasks even when this executor has been shutdown.* 
    - `void setExecuteExistingDelayedTasksAfterShutdownPolicy(boolean value)`
      - *Sets the policy on whether to execute existing delayed tasks even when this executor has been shutdown.*
    - `BlockingQueue<Runnable> getQueue()`
    - ... 
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledThreadPoolExecutor.html>
- **Executors**
  - *Factory and utility methods for `Executor`, `ExecutorService`, `ScheduledExecutorService`, `ThreadFactory`, and `Callable` classes defined in this package*
  - Methoden
    - `static ExecutorService newCachedThreadPool()`
      - *Creates a thread pool that creates new threads as needed, but will reuse previously constructed threads when they are available.*
      - *These pools will typically improve the performance of programs that execute many short-lived asynchronous tasks.*
      - *Calls to execute will reuse previously constructed threads if available. If no existing thread is available, a new thread will be created and added to the pool.*
      - *Threads that have not been used for sixty seconds are terminated and removed from the cache. Thus, a pool that remains idle for long enough will not consume any resources.*
      - *Note that pools with similar properties but different details (for example, timeout parameters) may be created using ThreadPoolExecutor constructors.*
    - `static ExecutorService newFixedThreadPool(int nThreads)`
      - *Creates a thread pool that reuses a fixed number of threads operating off a shared unbounded queue.*
      - *At any point, at most nThreads threads will be active processing tasks.*
      - *If additional tasks are submitted when all threads are active, they will wait in the queue until a thread is available.*
      - *If any thread terminates due to a failure during execution prior to shutdown, a new one will take its place if needed to execute subsequent tasks.*
      - *The threads in the pool will exist until it is explicitly shutdown.* 
    - `static ScheduledExecutorService newScheduledThreadPool(int corePoolSize)`
    - `static ExecutorService newSingleThreadExecutor()`
    - `static ScheduledExecutorService newSingleThreadScheduledExecutor()`
    - `static ExecutorService newWorkStealingPool()`
    - ... 
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html> 
- **ForkJoinPool**
  - extends AbstractExecutorService
  - *An `ExecutorService` for running `ForkJoinTasks`*
  - *These classes employ a work-stealing scheduler that attains high throughput for tasks conforming to restrictions that often hold in computation-intensive parallel processing.*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinPool.html> 


#### Synchronizers
- **CountDownLatch**
- **CyclicBarrier**
  - *allows a set of threads to wait for each other to reach a common execution point, also called a barrier*
  - <https://www.baeldung.com/java-cyclic-barrier>
- **Phaser**
  - *a barrier on which the dynamic number of threads need to wait before continuing execution*
  - *very similar construct to the CountDownLatch that allows us to coordinate execution of threads. In comparison to the CountDownLatch, it has some additional functionality.*
  - *In the CountDownLatch that number cannot be configured dynamically and needs to be supplied when we're creating the instance.*
  - <https://www.baeldung.com/java-phaser>
- **Exchanger**
  - *works as a common point for two threads in Java to exchange objects between them.*
  - *The class provides only a single overloaded method exchange(T t). When invoked exchange waits for the other thread in the pair to call it as well.*
  - <https://www.baeldung.com/java-exchanger>
- **Semaphore**
  - *can use semaphores to limit the number of concurrent threads accessing a specific resource.*
  - <https://www.baeldung.com/java-semaphore>
- **ReentrantLock**
  - <https://www.geeksforgeeks.org/reentrant-lock-java/>
    - *allows threads to enter into the lock on a resource more than once. When the thread first enters into the lock, a hold count is set to one. Before unlocking the thread can re-enter into lock again and every time hold count is incremented by one. For every unlocks request, hold count is decremented by one and when hold count is 0, the resource is unlocked.*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html>
    - *same basic behavior and semantics as the implicit monitor lock accessed using synchronized methods and statements, but with extended capabilities*
    - *accepts an optional fairness parameter. When set true, under contention, locks favor granting access to the longest-waiting thread*


#### Queues
- **Queue**
  - Interface
- **BlockingQueue**
  - Interface, extends Queue
  - <https://www.baeldung.com/java-blocking-queue>
- **BlockingDeque**
  - Interface, extends BlockingQueue
- **SynchronousQueue**
  - Class, implements BlockingQueue
  - *we should think about it as an exchange point for a <mark>single element</mark> between two threads, in which one thread is handing off an element, and another thread is taking that element.*
  - <https://www.baeldung.com/java-synchronous-queue>
- **PriorityBlockingQueue**
- **DelayQueue**


#### Concurrent Collections
- **CopyOnWriteArrayList**
- **ConcurrentHashMap**


#### Reactive Streams
- <http://www.reactive-streams.org/>
  - *an initiative to provide a standard for asynchronous stream processing with non-blocking back pressure*
  - *The interfaces available in JDK >= 9 java.util.concurrent.Flow, are 1:1 semantically equivalent to their respective Reactive Streams counterparts.*
- java.util.concurrent.Flow
  - interface Flow.Subscriber<T>
    - onSubscribe(Subscription)
    - onNext(T item)
    - onComplete()
    - onError(Throwable)
  - interface Flow.Publisher
    - subscribe(Subscriber)
  - interface Flow.Processor<T, R>
  - Subscription
    - request(long)
    - cancel()
- <https://www.lightbend.com/blog/reactive-streams-java>
  - *Now if you take two subsequent stages and treat them as a producer and a consumer of data, the producer can either be slower or faster than the consumer. While it’s fine when the producer is the slower party, the situation gets complicated when the consumer is the slower one. The reason is that the consumer can then be flooded with data, which it has to handle more or less gracefully.*
  - *The simplest way to deal with too much data is simply to drop anything that cannot be handled - this is a common behavior e.g. in the world of networking hardware. But what if we don’t want to discard anything? Then <mark>backpressure</mark> comes to the rescue.*
  - *the idea of backpressure boils down to bounding the amount of data being transmitted between the stages of the pipeline, so that no stage gets flooded. And since the reactive approach is about not blocking unless really necessary, the backpressure implementation in a reactive stream must be non-blocking as well.*
- <https://dzone.com/articles/what-are-reactive-streams-in-java>
- <https://www.baeldung.com/java-9-reactive-streams>
- -> Java/Libs/Async/Reactive


#### Structured Concurrency
- **StructuredTaskScope**
  - Java 21+
  - <https://docs.oracle.com/en/java/javase/21/docs/api///java.base/java/util/concurrent/StructuredTaskScope.html>
