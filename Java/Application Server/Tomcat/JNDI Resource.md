Tomcat provides a JNDI `InitialContext` to each web application running under it, compatible to those provided by Java EE applicaiton servers.

# Define a resource in Tomcat 
By configured in either:
## `context.xml` :
```xml
<Resource name="bean/MyBeanFactory" auth="Container"
          type="com.mycompany.MyBean"
          factory="org.apache.naming.factory.BeanFactory"/>
```

## `web.xml`
```xml
<resource-env-ref>
  <description>
    Object factory for MyBean instances.
  </description>
  <resource-env-ref-name>
    bean/MyBeanFactory
  </resource-env-ref-name>
  <resource-env-ref-type>
    com.mycompany.MyBean
  </resource-env-ref-type>
</resource-env-ref>
```

# Using the resource in the application:
All configured entries or resource is avalable in the `java:comp/env`  namespace of the JNDI. 

```java
Context initCtx = new InitialContext();
Context envCtx = (Context) initCtx.lookup("java:comp/env");
MyBean bean = (MyBean) envCtx.lookup("bean/MyBeanFactory");
```

# `GlobalNamingResources`
The `GlobalNamingResources` define the global resources for the Server.
```xml
<GlobalNamingResources>
  ...
</GlobalNamingResources>
```

These resources are not visible in the per-web-application context unless we link them with `ResourceLink` in the context.
```xml
<ResourceLink
    name="bean/MyBeanFactory"
    global="bean/MyBeanFactory"
    type="com.mycompany.MyBean"
/>
```

# Resource factories

## Standard resource factories
* Java bean resources
* UserDatabase resources
* JavaMail sessions
* JDBC data sources

## Custom resource factories
Custom resource factories must implement `javax.naming.spi.ObjectFactory` interface. You need to complile the class to a jar file and put it in `$CATALINA_HOME/lib`

``` java
package com.mycompany;

import java.util.Enumeration;
import java.util.Hashtable;
import javax.naming.Context;
import javax.naming.Name;
import javax.naming.NamingException;
import javax.naming.RefAddr;
import javax.naming.Reference;
import javax.naming.spi.ObjectFactory;

public class MyBeanFactory implements ObjectFactory {

  public Object getObjectInstance(
      Object obj, Name name2, Context nameCtx, Hashtable environment) throws NamingException {

      MyBean bean = new MyBean();

     // For Tomcat obj is always Reference
      Reference ref = (Reference) obj; 
      Enumeration addrs = ref.getAll();
      while (addrs.hasMoreElements()) {
          RefAddr addr = (RefAddr) addrs.nextElement();
          String name = addr.getType();
          String value = (String) addr.getContent();
          // Get parameters from the declaration
          if (name.equals("foo")) {
              bean.setFoo(value);
          }
          if (name.equals("bar")) {
            try {
                bean.setBar(Integer.parseInt(value));
            } catch (NumberFormatException e) {
                throw new NamingException("Invalid 'bar' value " + value);
            }
          }
      }

      return bean;
  }
}
```

In the declaration
```xml
<Resource name="bean/MyBeanFactory" auth="Container"
          type="com.mycompany.MyBean"
          factory="com.mycompany.MyBeanFactory"
          singleton="false"
          bar="23"/>
```

