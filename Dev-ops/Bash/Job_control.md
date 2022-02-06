# Job control

## Signals

UNIX system communicate to the process by sending signals.  
These signals can be captured by the program (Eg: when you hit CTRL-C, the program can save instead of quit), except SIGKILL which will terminate the process immediately and could leave orphaned children processes.  
See more about those signals by: `man signal`.  

### Some signal can be sent using shortcut

| signal | description | terminal shortcut for sending |
| --- | --- | --- |
| SIGINT | Happy terminate the process | CTRL-C |
| SIGQUIT | Unhappy terminate the process | CTRL-\ |
| SIGTSTP | Suppend the process | CTRL-Z |

### To send an arbitrary signal

```sh
kill -<The-signal> <PID>
```

## Background processes

To run a command in background process, you could add a suffix `&` to it. However, it still use the the shell's STDOUT and can be annoying.

To list all jobs related to the terminal session, use the command `jobs`. You can later refer to the job by its index by `$<index>` instead of the `PID`. The `$!` could be used to refer to the latest job.

You could continue a stopped job in the foreground or in the background using `fg` and `bg`, respectively.
