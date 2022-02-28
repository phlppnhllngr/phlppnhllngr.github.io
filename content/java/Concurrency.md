---
title: Concurrency
parent: Java
---

# Concurrency

## JDK

### java.lang.Thread
- *A thread is a thread of execution in a program. The Java Virtual Machine allows an application to have multiple threads of execution running concurrently.*
- Methoden
  - `long	getId()`
  - `String	getName()`
  - `int getPriority()`
  - `Thread.UncaughtExceptionHandler getUncaughtExceptionHandler()`
  - `boolean isDaemon()`
  - `void	join()` (+2 Overloads)
  - `void	run()`
  - `void	start()`
    - *Causes this thread to begin execution; the Java Virtual Machine calls the run method of this thread.*
  - `static void yield()`
    - *A hint to the scheduler that the current thread is willing to yield its current use of a processor.*
  - ...
- <https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html>

### java.util
- **Timer**
  - *A facility for threads to schedule tasks for future execution in a background thread.*
  - *Tasks may be scheduled for one-time execution, or for repeated execution at regular intervals.*
  - *Java 5.0 introduced the java.util.concurrent package and one of the concurrency utilities therein is the `ScheduledThreadPoolExecutor` which is a thread pool for repeatedly executing tasks at a given rate or delay. It is effectively a more versatile replacement for the `Timer`/`TimerTask` combination, as it allows multiple service threads, accepts various time units, and doesn't require subclassing `TimerTask` (just implement `Runnable`). Configuring `ScheduledThreadPoolExecutor` with one thread makes it equivalent to `Timer`.*
  - <https://docs.oracle.com/javase/8/docs/api/java/util/Timer.html> 

### java.util.concurrent
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
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinPool.html> 
- **CompletableFuture**
  - <https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html> 
  - <https://www.baeldung.com/java-completablefuture> 