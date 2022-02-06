# Communicate with remote machines

## ssh

The secure shell (ssh) is the main command for communicate with remote machines.

```sh
ssh <user-name>@<ip-or-URL>

ssh foo@server ls # execute command in the server and return it to the terminal
```

## SSH keys

### Generate ssh keys

The command for generate SSH keys is `ssh-keygen`.  
The keys will be stored in `~/.ssh` folder.  
You could specify the algorithm used to generate it (-t), how many derivation round (-a), file name (-f).

### Copy ssh keys to server

SSH will look into `~/.ssh/authorized_keys` to determine which client should let in.

```sh
cat <publish-key> | ssh foobar@remote 'cat >> ~/.ssh/authorized_keys'

ssh-copy-id -i <publish-key> foobar@remote #standard way to copy the ssh key
```

## Copy file over SSH

```sh
cat local-file | ssh remote_server tee server-file

scp path/to/local_file remote_host:path/to/remote_file
```

## SSH configuration

The config for SSH is saved in `~/.ssh/config`, and can be used by ssh, scp, rsync, mosh, etc.

```config
Host vm
    User foobar
    HostName 172.16.174.141
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
    LocalForward 9999 localhost:8888

# Configs can also take wildcards
Host *.edu
    User foobaz
```
