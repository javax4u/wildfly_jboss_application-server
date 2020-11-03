## Q A. I want to change log level in wildfly, by default its printing only INFO level.

Answer you should change LOG level in standalone.xml

#### subsystem>profile>logging:8.0
  
 **object diagram**
![object diagram](image/logger-20201028223112.png)


**xml screenshot**

![xml screenshot](image/camel_screenshot.png)

##### Before changing the LOG level
	14:45:06,424 INFO  [org.jboss.as.mail.extension] (MSC service thread 1-1) WFLYMAIL0002: Unbound mail session [java:jboss/mail/Default]
	14:45:06,433 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-8) WFLYUT0008: Undertow HTTP listener default suspending
	14:45:06,429 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-7) WFLYUT0008: Undertow HTTPS listener https suspending
	14:45:06,445 INFO  [org.jboss.as.connector.deployers.jdbc] (MSC service thread 1-5) WFLYJCA0019: Stopped Driver service with driver-name = h2

##### After changing the LOG level
	18:47:18,868 DEBUG [org.apache.activemq.artemis.core.server.impl.QueueImpl] (Thread-2 (ActiveMQ-server-org.apache.activemq.artemis.core.server.impl.ActiveMQServerImpl$6@36bbc347)) Scanning for expires on jms.queue.DLQ done
	18:47:48,876 DEBUG [org.apache.activemq.artemis.core.server.impl.QueueImpl] (Thread-4 (ActiveMQ-server-org.apache.activemq.artemis.core.server.impl.ActiveMQServerImpl$6@36bbc347)) Scanning for expires on jms.queue.DLQ
	18:47:48,876 DEBUG [org.apache.activemq.artemis.core.server.impl.QueueImpl] (Thread-4 (ActiveMQ-server-org.apache.activemq.artemis.core.server.impl.ActiveMQServerImpl$6@36bbc347)) Scanning for expires on jms.queue.DLQ done

## Q B. I want to know how many realms are there how to configure them ?

**Flow Diagram**

![Realm Diagram](image/realm.png)

## Q A. How to disable default web-app in wildfly ?

comment out below tag to disable welcome-content.

```html
 <!-- <location name="/" handler="welcome-content"/>-->
  
```
To replace this page simply deploy your own war with / as its context path.
To disable it, remove the "welcome-content" handler for location / in the undertow subsystem.

## Q A. How to enable exploded app deployment ?

Search for subsystem > deployment-scanner tag in file once found, the add **auto-deploy-exploded="true"** parameter into it.

	<!-- Adding auto-deploy-exploded=true parameter to enable auto deployment of exploded war,jar or ear files -->
	<!-- <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" runtime-failure-causes-rollback="${jboss.deployment.scanner.rollback.on.failure:false}"/>-->
	<deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" auto-deploy-exploded="true" runtime-failure-causes-rollback="${jboss.deployment.scanner.rollback.on.failure:false}"/>
		 

## Q A. How to deploy your app in root context (/) ?

Add jboss-web.xml file beside web.xml file with below content.
```xml
	<jboss-web>
	   <context-root>/</context-root>
	</jboss-web>
```

![deployment](image/deployment.png)	
![jboss-web.xml](image/jboss-web_xml.png)	 

## Q A. How to deploy your app in root context (/) ?

```xml
	<!-- commenting below lines to bind it with machine name -->
	<!-- <inet-address value="${jboss.bind.address:127.0.0.1}"/> -->
	<inet-address value="${jboss.bind.address:0.0.0.0}"/>
```

**Before binding to 0.0.0.0**
![bind_address_127_0_0_1.png](image/bind_address_127_0_0_1.png)

**After binding to 0.0.0.0**

![bind_address_0_0_0_0.png](image/bind_address_0_0_0_0.png)

#### Reference
 
[Onine graph editor link](https://mermaid-js.github.io/mermaid-live-editor)

[Mermaid diagram code file ](diagram_mermaid_code.txt)
	

