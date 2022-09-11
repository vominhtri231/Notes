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
* `<<<` : using string as input stream

```sh
readarray -t a_array <<< "a sample string"
```

* `|` : use the last program result as the input for the next program

```sh
ls -l | tail -n1
```

**NOTE:** Redirection (`<`, `>>`, `>`, `2>`) is execute before the main command is run.

E.g: `sudo echo "hello word" > hello.txt`. If the `hello.txt` file require special permission, the command sudo here will take no effect since the `hello.txt` will be open first. The echo command is also not execute at all.
