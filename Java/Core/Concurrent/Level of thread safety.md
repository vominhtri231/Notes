### When design a class for concurrent use, the class should document its level of thread safety:
1. Immutable   
Instant of this type appear to be a constant, like String, Long or BigDecimal, etc. No external synchronization is necessary.
2. Unconditional thread-safe  
Mutable but has internal synchronizations so no external synchronization needed. Eg: AmoticLong, ConcurrentHashMap, etc.
3. Conditional thread-safe  
Like Unconditional thread-safe, but some operations need synchronization.
   Eg: Collections returned by Collections.synchronized() required external lock on iterator operation. 
   The class should document both the operation, and the lock should be acquired.
4. Not thread-safe  
Must wrap the instances in synchronized block if concurrent uses is needed.
Eg: ArrayList, HasMap
5. Thread-hostile  
Unsafe for concurrent use even if be wrapped in synchronized block. Usually because of modifying data without synchronization. 
   This is mostly because non-relevant methods modified the static fields.  
=> Always internally synchronize static fields when modifying