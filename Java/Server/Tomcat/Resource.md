## `Resource`
We could define a resource in Tomcat by :
```xml
<Resource name="bean/MyBeanFactory" auth="Container"
          type="com.mycompany.MyBean"
          factory="org.apache.naming.factory.BeanFactory"
          bar="23"/>
```
To use the resource:
```java
Context initCtx = new InitialContext();
Context envCtx = (Context) initCtx.lookup("java:comp/env");
MyBean bean = (MyBean) envCtx.lookup("bean/MyBeanFactory");
```

We could have JavaBean Resources, UserDatabase Resources, JavaMail Resources, JDBC Data Source Resources or Custom Resources.


## `GlobalNamingResources`
The `GlobalNamingResources` define the global resources for the Server.
```xml
<GlobalNamingResources>
  ...
</GlobalNamingResources>
```

These resources is not visible in the per-web-application context unless we link them with `ResourceLink` in the context.
```xml
<ResourceLink
    name="bean/MyBeanFactory"
    global="bean/MyBeanFactory"
    type="com.mycompany.MyBean"
/>
```