# Master theorem

Master theorem describe runtime analysis for divide and conquer algorithm

```
T(n) = aT(n/b) + f(n)
```

 In that `T(n)` is the problem runtime, which can be break in to `a` tasks, each would have the size `n/2` and  the time to create the subproblem is`f(n)`

 Master theorem runtime can be analyzed using recursive tree, for example:

* `T(n) = 3T(n/4)+ O(n^2)` 

![](.\images\2025-06-22-15-30-29-image.png)

* `T(n) = T(n/3) + T(2n/3) + O(n)`

![](.\images\2025-06-22-15-36-44-image.png)
