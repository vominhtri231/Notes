## Remarks
* The `web.xm`( placed in `/WEB-INF/web.xml`) is the Web Application Deployment Description of your application, used to define certain web components such as servlets, fileter, listeners, etc
* It's optional to have `web.xml` because we could config via JavaEE annotations. ([source](https://docs.oracle.com/cd/E24329_01/web.1211/e21049/web_xml.htm#WBAPP502))
## Some well known configurations:
### 1. Servlet
```xml
  <servlet>
    <servlet-name>HelloWorld</servlet-name>
    <servlet-class>tri.test.HelloServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>HelloWorld</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping> 
```
The equivalent annotation:

``` java
@WebServlet(
    name = "HelloWorld",
    urlPatterns = {"/hello"}
)
public class HelloServlet extends HttpServlet {} 
```
### 2. Filter
```xml
<filter>  
<filter-name>FilterA</filter-name>  
<filter-class>tri.test.FilterA</filter-class>  
</filter>  
   
<filter-mapping>  
<filter-name>FilterA</filter-name>  
<url-pattern>/url1/*</url-pattern>  
</filter-mapping>  
```
The equivalent annotation:

```java
@WebFilter(filterName="FilterA", urlPatterns="/url1/*")
public class FilterA implements Filter {}
```
### 3. Listener
```xml
<listener>
  <listener-class>tri.test.ListenerA</listener-class>
</listener>
```
The equivalent annotation:

```java
@WebListener
public class ListenerA implements ServletContextListener {}
```