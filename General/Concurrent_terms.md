# Concurrent terms

* Race condition: the situation when 2 or more thread write a share data and the final result depends on which thread run precisely when.
* Mutual exclusion: when one thread using a share resource, other threads will be excluded from using it.
* Critical regions: part of the program where shared resource is accessed.
* Synchronization mechanism
* Liveness failures: the program permanently unable to make forward progress.  
  Some forms of liveness failures: Death-lock, starvation, live-lock, etc
* Safety failures: the program run incorrectly