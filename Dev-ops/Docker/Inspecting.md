# Inspecting

Inspecting a docker object via `inspect` command, E.g:

```sh
docker container inspect <container>
docker image inspect <container> 
```

For formating the result (E.g. for filtering it), you can use `--format` for formatting using Go template.

```sh
# For getting ip address of the container
docker container inspect --format "{{ .NetworkSettings.IPAddress }}" <container>
```
