## Create a Server profile

Unlike Glassfish or WildFly server, Open Liberty does not provide a default domain.

Locate to *<Open Liberty dif>/bin*, execute the following command to create a new server profile.

```
server create
Server defaultServer created.
```

Open *<Open Liberty dif>/usr/servers*, there is a new *defaultServer* folder created. In this folder, there are some files and folder are generated for your application deployment.



Open the *server.xml* file, it already included *javaee-8.0* feature. There are several templates allow you create a server profile quickly with essential features, more templates check *<Open Liberty dif>/templates/servers*.

Try to run the following command to create a **microProfile3** profile with the name *mp3* and the template *microProfile3*.

```
server create mp3 --template="microProfile3"
Server mp3 created.
```




## Start and Stop Open Liberty Server

In the *<Open Liberty dir>/bin* folder, execute the following command to start Open Liberty Server.

```
# server start
Starting server defaultServer.
Server defaultServer started.
```

By default, it will start the **defaultServer**. You can specify the server name to start a different server.

```
# server start mp3
Starting server mp3.
Server mp3 started.
```
