# Way Forward for Java Futures
### Implementing as Non-Blocking code

For Void Return Types: CompletableFuture.runAsync
For Other Return Types: CompletableFuture.supplyAsync

CompletableFuture.completedFuture sends the actual value in argument.

### Handling Async Callback
```
Transforming Futures
Instead of waiting for it to complete. thenApply will run only after futureOrder is completed.

CompletableFuture<String> futureString = futureOrder.thenApply(order -> order.toString());

.thenCompose will flatten nested futures.
CompletableFuture<Order> flatttenedFutureOrder = futureOrder.thenCompose(order-> CompletedFuture(order));

Instead of thenCompose and thenApply there are other ways 
    - thenRun    : Executes a Runnable once the future Completes
    - thenAccept : Executes a Consumer once future Completes
    - thenCombine: Combines results of two futures using a Bi Function
```

### Executors
Futures are executed in a separate thread or thread pool. Managed by Executor or Executor Service.
Executor Service is an implementation of an Executor, leave default to faster ones.

If no Executor is provided, default is used.
Again there could be Contention if all non-blocking code uses same default Executor.
Better to isolate blocking operations to their owb Executor.

```
// Creates new threads if all threads blocked
ExecutorService executor = Executors.newCachedThreadPool();

// Maintains specific active threads
// May use multiple queues to reduce contention 
ExecutorService executor = Executors.newWorkStealingPool(10);

// Fixed no of threads
ExecutorService executor = Executors.newFixedThreadPool(10);
```

Wrap Up:
- Blocking Calls
- Futures
- Transforming Futures
- Executors