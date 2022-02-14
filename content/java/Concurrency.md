---
title: Concurrency
parent: Java
---

# Concurrency

## JDK

### java.util
- **Timer**
  - *A facility for threads to schedule tasks for future execution in a background thread.*
  - *Tasks may be scheduled for one-time execution, or for repeated execution at regular intervals.*
  - *Java 5.0 introduced the java.util.concurrent package and one of the concurrency utilities therein is the ScheduledThreadPoolExecutor which is a thread pool for repeatedly executing tasks at a given rate or delay. It is effectively a more versatile replacement for the Timer/TimerTask combination, as it allows multiple service threads, accepts various time units, and doesn't require subclassing TimerTask (just implement Runnable). Configuring ScheduledThreadPoolExecutor with one thread makes it equivalent to Timer.*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/Timer.html> 

### java.util.concurrent
- **Executor**
  - Interface
  - *An object that executes submitted Runnable tasks*
  - Methoden
    - `void execute(Runnable command)`
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html> 
- **ExecutorService**
  - Interface, extends Executor
  - *provides methods to manage termination and methods that can produce a `Future` for tracking progress of one or more asynchronous tasks*
  - *can be shut down, which will cause it to reject new tasks*
  - *extends base method Executor.execute(Runnable) by creating and returning a `Future` that can be used to cancel execution and/or wait for completion*
  - Methoden
    - `Future<?> submit(Runnable task)`
    - `void shutdown()`
    - `boolean awaitTermination(long timeout, TimeUnit unit)`
    - ...
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html>
- **ScheduledExecutorService**
  - Interface, extends ExecutorService
  - *can schedule commands to run after a given delay, or to execute periodically*
  - Methoden
    - `<V> ScheduledFuture<V>	schedule(Callable<V> callable, long delay, TimeUnit unit)`
    - `ScheduledFuture<?>	schedule(Runnable command, long delay, TimeUnit unit)`
    - `ScheduledFuture<?>	scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)`
    - `ScheduledFuture<?>	scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)`
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledExecutorService.html>
- **ThreadPoolExecutor**
  - *executes each submitted task using one of possibly several pooled threads, normally configured using `Executors` factory methods.*
  - *To be useful across a wide range of contexts, this class provides many adjustable parameters and extensibility hooks*
  - *However, programmers are urged to use the more convenient Executors factory methods (...), that preconfigure settings for the most common usage scenarios. Otherwise, use the following guide when manually configuring and tuning this class:*
  - Es folgen Hinweise zu den Themen: *Core and maximum pool sizes, On-demand construction, Creating new threads, Keep-alive times, Queuing, Rejected tasks, Hook methods, Queue maintenance, Finalization*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html> 
- **ScheduledThreadPoolExecutor**
  - extends ThreadPoolExecutor implements ScheduledExecutorService 
  - *A ThreadPoolExecutor that can additionally schedule commands to run after a given delay, or to execute periodically.*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ScheduledThreadPoolExecutor.html>
- **Executors**
  - *Factory and utility methods for Executor, ExecutorService, ScheduledExecutorService, ThreadFactory, and Callable classes defined in this package*
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
