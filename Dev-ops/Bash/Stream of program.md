# Stream of program

Every program usually would have 2 primary streams:

* a input stream (By default is the keyboard)
* a output stream (By default is the monitor)

## Rewired the stream (change the input and output stream)

* `<` : specify the input stream
* `>` : specify the output stream
* `2>` : specify the error stream

```sh
echo "hello world" > hello.txt
```

* `>>` : specify the output stream, but will append the stream only
* `|` : use the last program result as the input for the next program

```sh
ls -l | tail -n1
```
