# Stream of program

Every program usually would have 2 primary streams:
* a input stream (By default is the keycloak) 
* a output stream (By default is the monitor)

## Rewired the stream (change the input and output stream)

* `<` : specify the input stream
* `>` : specify the output stream
* `2>` : specify the error stream

```shell
echo "hello world" > hello.txt
```

* `>>` : specify the output stream, but will append the stream only
* `|` : use the last program result as the input for the next program

```shell
ls -l | tail -n1
```