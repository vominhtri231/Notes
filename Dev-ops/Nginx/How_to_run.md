# How to run

To control nginx, we use the command `nginx -s signal`, where the signal could be:

* stop: fast shutdown
* quit: graceful shutdown
* reload : reload configurations
* reopen : reopening the log files

The command should be executed under the same user that start nginx.
