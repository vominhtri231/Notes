# Persistent data

Containers are designed to be immutable and ephemeral, which causing problem when dealing with persistent data like databases or unique data. 
To solve this, docker intruduces volumes and bind mount. 

## Volume 

A special location outside the container union file system (UFS) for saving persistent data so that the persistent data can outlive the container.

To use the volume, we could:

* Use the `VOLUME` command in `Dockerfile`
* Run container using `-v <volume-name>:<path>` (volume-name can be ommited, the name will be generated)

To create the volume, for greater customize posibility, using `docker volume create ...`

## Bind mount 

A link between the host's directory and the container's directory so they both point to the same directory.

```sh
# the host path must start with forward slash '/'
docker run -v <host-path>:<container-path> ...

# E.g
docker run -v /Users/abc:/user/abc ...
docker run -v //c/Users/abc:/user/abc ..
```
