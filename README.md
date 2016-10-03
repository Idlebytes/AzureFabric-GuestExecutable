# AzureFabric-GuestExecutable


This is a Simple HelloWorld Java Spring application written using Spring boot which listens on port 8080 when invoked using command "java -jar HelloWorld.war"

The source code can be found in https://github.com/Idlebytes/SampleJavaMVC.git repository, the branch name is "springboot".

Here we will build the application with embedded JVM container instead of separate external hosting of JVM containers like Apache Tomcat, since there is no external environment dependencies, and can be easily invoked with a single command in dynamic cloud environments.

The application is built and tested in local and once it starts by invoking the java command, it listens successfully at http://localhost:8080/ 

We will now host the same application in Microsoft Azure service fabric cluster. (it runs anywhere in local Service Fabric Explorer - 1 node, Azure service Fabric cluster - unsecured and secured with no difference to end user)

Note: It will fail when running in local Service Fabric Explorer - 5 node, since all these nodes run in same local laptop, and once the first instance uses port 8080, the subsequent instances will fail due to non-availability of port 8080.

Documentation:

The detail documentation of project structure for Azure Service fabric is available in https://azure.microsoft.com/en-us/documentation/articles/service-fabric-deploy-existing-app/

The Azure fabric uses underlying Java installed on the individual Azure Fabric nodes. In case this is a new installation setup, go ahead and install Java on the individual nodes. (Individual nodes can be connected using RDP by accessing Load balancer IP and corresponding inbound NAT ports). Once Java is installed, note down the path of java executable (In our case, it is "C:\Program Files (x86)\Java\jre1.8.0_101\bin\java.exe")

For Java, we need to specify the application launch command "launchConfig.cmd" with full Java path, and placed under the scripts subdirectory. The Service Manifest specifies the code entry point, and we will invoke this launch command in the entry point.

Note:

The service fabric explorer can be monitored for the application health status using below URLs:

http://localhost:19080/Explorer - Service Fabric Explorer
http://{fabrictest.southindia.cloudapp.azure.com}:19080/Explorer - http endpoint for both unsecured and secured service fabric cluster. For secured cluster, we need to configure client certificate for authentication.
http://{fabrictest.southindia.cloudapp.azure.com}:19000/Explorer - Deployment endpoint for secure service fabric cluster using visual studio.

