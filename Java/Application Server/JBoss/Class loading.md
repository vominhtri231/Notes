# Class loading

JBoss's class loading is based on module that have have to define explicit dependencies for each module.

## JBoss deployment structure file

`jboss-deployment-structure.xml` is a file to control class loading, should be placed in top level deployment such as META-INF or WEB-INF.

It could:  

 * Prevent automatic dependencies
 * Add dependencies
 * Define additional modules
 * Add additional resource

 ```xml
 
<jboss-deployment-structure>
  <!-- Make sub deployments isolated by default, so they cannot see each others classes without a Class-Path entry -->
  <ear-subdeployments-isolated>true</ear-subdeployments-isolated>
  <!-- This corresponds to the top level deployment. For a war this is the war's module, for an ear -->
  <!-- This is the top level ear module, which contains all the classes in the EAR's lib folder     -->
  <deployment>
    <!-- Exclusions allow you to prevent the server from automatically adding some dependencies     -->
    <exclusions>
        <module name="org.javassist" />
    </exclusions>
    <!-- This allows you to define additional dependencies, it is the same as using the Dependencies: manifest attribute -->
    <dependencies>
      <module name="deployment.javassist.proxy" />
      <module name="deployment.myjavassist" />
    </dependencies>
    <!-- These add additional classes to the module. In this case it is the same as including the jar in the EAR's lib directory -->
    <resources>
      <resource-root path="my-library.jar" />
    </resources>
  </deployment>
  <sub-deployment name="myapp.war">
    <!-- This corresponds to the module for a web deployment -->
    <!-- it can use all the same tags as the <deployment> entry above -->
    <dependencies>
      <!-- Adds a dependency on a ejb jar. This could also be done with a Class-Path entry -->
      <module name="deployment.myear.ear.myejbjar.jar" />
    </dependencies>
  </sub-deployment>
  <!-- Now we are going to define two additional modules -->
  <!-- This one is a different version of javassist that we have packaged -->
  <module name="deployment.myjavassist" >
    <resources>
     <resource-root path="javassist.jar" >
       <!-- We want to use the servers version of javassist.util.proxy.* so we filter it out-->
       <filter>
         <exclude path="javassist/util/proxy" />
       </filter>
     </resource-root>
    </resources>
  </module>
  <!-- This is a module that re-exports the containers version of javassist.util.proxy -->
  <!-- This means that there is only one version of the Proxy classes defined          -->
  <module name="deployment.javassist.proxy" >
    <dependencies>
      <module name="org.javassist" >
        <imports>
          <include path="javassist/util/proxy" />
          <exclude path="/**" />
        </imports>
      </module>
    </dependencies>
  </module>
</jboss-deployment-structure>
 ```