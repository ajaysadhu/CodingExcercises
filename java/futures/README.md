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
