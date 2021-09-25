# File Persistence.xml

`persistence.xml` (placed in `/resource/META-INF/`)is the central configuration file for JPA. It is used to define one or more persistence units with these configs:

1. Name and description of persistence unit
2. Transaction type, you could choose between manage the transaction by yourself (RESOURCE_LOCAL) or by application server's JTA implementation (JTA) ([source](http://tomee.apache.org/jpa-concepts.html))
3. The classes managed by persistence unit
4. Persistence provider
5. Data sources. Dependence on the transaction type, it could be `jta-data-source` or `non-jta-data-source`
6. Entity validation: There are 3 validation modes: AUTO, CALLBACK (thrown exception if no bean validation implementation is available) and NONE
7. Mode of 2nd level cache, which should be used to cache entity that often read by rarely change.
   There are 4 modes: ALL, NONE(default), ENABLE_SELECTED (only cache entities with `@Cacheable`) and DISABLE_SELECTED (only not cache entities with `@Cacheable(false)`)
8. Configuration parameters

```xml
<persistence>
    <persistence-unit name="persistenceUnitName" transaction-type="RESOURCE_LOCAL">
        <description>The description</description>
        
        <!-- The global JNDI name of the data source to be used by the JavaEE container -->
        <jta-data-source>jdbc/MyOrderDB</jta-data-source>
        
       <!-- The persistence provider -->
        <provider>org.eclipse.persistence.jpa.PersistenceProvider</provider>
        
        <!-- Define 2nd level cache mode -->
        <shared-cache-mode>ENABLE_SELECTIVE</shared-cache-mode>
        
        <!-- Define validation mode -->
        <validation-mode>CALLBACK</validation-mode>
        
        <!-- Jar file contains entity classes -->
        <jar-file>MyOrderApp.jar</jar-file>
        
        <!-- List of entity classes -->
        <class>com.widgets.CustomerOrder</class>
        <class>com.widgets.Customer</class>
        
        <!-- Define your properties here -->
        <properties>
            <!-- The lock time -->
            <property name="javax.persistence.lock.timeout" value="100"/>
            <property name="javax.persistence.query.timeout" value="100"/>
            
            <!-- Java SE might not have a data source, you could define the login information for the provider-->
            <property name="javax.persistence.jdbc.driver" value="org.postgresql.Driver" />
            <property name="javax.persistence.jdbc.url" value="jdbc:postgresql://localhost:5432/xyz" />
            <property name="javax.persistence.jdbc.user" value="postgres" />
            <property name="javax.persistence.jdbc.password" value="postgres" />
            
            <!-- How database is generate, it could be none (default), create, drop and drop and create -->
            <!-- USE VERSION-BASED DATABASE MIGRATION TOOL INSTEAD -->
            <property name="javax.persistence.schema-generation.database.action" value="drop-and-create" />
            <property name="javax.persistence.schema-generation.create-script-source" value="create-db.sql" />
            <property name="javax.persistence.schema-generation.drop-script-source" value="drop-db.sql" />
            <property name="javax.persistence.sql-load-script-source" value="data.sql" />
        </properties>
    </persistence-unit>
</persistence>
```
