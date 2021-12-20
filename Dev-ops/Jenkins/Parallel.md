# Run in parallel

```groovy
parallel
    firstBranch: {
        // do something
    }, 
    secondBranch: {
        // do something else
    },
    failFast: true
```

Parameter is a map of:

* brand name to the job closure and 
* `failFast` to boolean indicate whether the step be terminate if one branch fail
