
* Run keycloark in standalone mode:

```sh
{$KEYCLOARK-HOME}/bin/standalone.bat "-Djboss.socket.binding.port-offset=1616"
```

By default, the keycloak server will run on port 8080 on top of wildfly server on port 9990. The offset setting will adjust both ports to new ones.