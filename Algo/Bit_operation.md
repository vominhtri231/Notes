# BIT operations

## XOR

XOR will removed the duplicated numbers, as `a^a = 0`.
Can be very useful to :

* check every item appear in even number / reduce even count

* swap number
  
  ```
  a = a ^ b
  b = a ^ b
  a = a ^ b
  ```

| a     | b   |
| ----- | --- |
| a ^ b | b   |
| a ^ b | a   |
| b     | a   |

## Check only 1 bit set

```
x & (x  - 1) == 0

//   x          = 1 0 ... 0
//   x - 1      = 0 1 ... 1
// x & (x  - 1) = 0 0 ... 0
```

## Get last set bit

```
x & (-x)


//    x       = 1010
//   -x       = 0110 (-x = ~x + 1)
// x & (-x)   = 0010
```


