* Concurrent collections are concurrent implementation of standard collections like Map, List or Set.   
Eg: `ConcurrentMap`  
* They handle synchronization internally and lock them only slow the program down => well suit with state-dependent modify methods.  
Eg: `Map.putIfAbsent(key, value)`;
* They differ from synchronize collection which lock from object level => have better performance.

#### Examples: 
1. `BlockingQueue` has method take, which remove the first item from the queue and return, will wait if the queue is empty. 
   That make it great for producer-consumer queue.
2. `CopyOnWriteArrayList` would create a new underlying array list everytime it get modified, 
   which really suitable for high-read-frequency usages.
3. `ConcurrentMap`.