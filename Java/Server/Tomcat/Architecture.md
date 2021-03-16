![](https://programmer.help/images/blog/f154b23bacd998b37bb6e2581856c84e.jpg)

1. Server  
   Represent an instance of Tomcat, listens to a particular port (default is 8085) for signals.
```xml
<Server port="8005" shutdown="SHUTDOWN">
</Server>
```
2. Services  
   Tie one or more connections with an engine
```xml
<Service name="Catalina">
</Service>
```
3. Connector  
   Handle communications with client by listening on a port for client request then handing them over to Engine.  
   The connections could be HTTP connection, AJP connection or HTTPS connection, etc.
```xml
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```
4. Engine  
   Process request from the connector then hand the response back.
```xml
<Engine name="Catalina" defaultHost="localhost">
</Engine>
```
5. Host   
   Represents a virtual host, which is an association of a network name for a server.
```xml
<Host name="localhost" appBase="webapps"
      unpackWARs="true" autoDeploy="true">
</Host>
```
6. Context  
   Represents a web application in `appBase` folder.

```xml
<Context>
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
    <WatchedResource>${catalina.base}/conf/web.xml</WatchedResource>
</Context>
```