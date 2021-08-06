# Hashbang - shebang 
Used to specify the program to run the script.


Eg:

```shell
#!usr/local/bin/python
...
```

So to execute the script, you just need `./a.py` instead of `python a.py`

Eg:

```shell
#!usr/bin/env python
```

This way the shell would try to find the program in PATH => make the script more portable
