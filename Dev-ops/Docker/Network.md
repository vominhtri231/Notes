# Network

By default a container will be connected to the `bridge` network, which is created out-of-the-box and connect to the host firewall. There is also `host` network that skip all the virtual networking and connect to the host network. This can be risky but would improve the performance and can help get around some software problems. You could also create your own networks.

When user running a container using the `-p <host-port>:<container-port>` parameter, docker would create a port on the host machine, then forwarding all trafics from the host's port to the container's port by NAT. You could checking the container port by using the command `docker container port <container>`.

Containers inside the same network could connect to each other so that would be better for containers of the same application to connect to the same network. E.g. The database and the web of the same application can be in the same network, so that the web app can connect to the database without exposing it.

Docker allows containers to connect to each other using their name as host name. This would make the connection more reliable since IP Address of a container may change. This is called docker DNS. The default `bridge` network does not have this feature but manually created ones do.
You can also set the host name via `--alias` option when connect container to a network or `--network-alias` when starting a container. Multiple containers can have the same alias in a network, making the DNS sort of a load balancing.

```sh
docker network ls
docker network inspect

# You could create using different driver (`bridge` driver is used by default), setting the subset, etc.
docker network create

# Run a container and connect it to predefined network
docker container run --network <network-name>

# Plug and unplug the container - a container can connect to multiple or no networks
docker network connect <network> <container>
docker network disconnect <network> <container>
```
