### Intro
JNDI stands for Java Naming and Directory Interface. It allows application to look up services in an abstract, resource-dependent way.

### Architecture
![](https://docs.oracle.com/javase/tutorial/figures/jndi/jndiarch.gif)

Consists of an API and a service provider interface (SPI).
SPI allows naming and directory services to be plugged in, then the Java application using the JNDI APi to access the services.

### Available naming/directory services

* Lightweight Directory Access Protocol (LDAP)
* Common Object Request Broker Architecture (CORBA) Common Object Services (COS) name service
* Java Remote Method Invocation (RMI) Registry
* Domain Name Service (DNS)