# Spring Boot – How to change Tomcat port

In Spring Boot, to change the embedded Tomcat initialized port (8080), update `server.port` properties.

**Update via a properties file.**

`/src/main/resources/application.properties`  
`server.port=8888`

**Or update via a yaml file.**

`/src/main/resources/application.yml`  
`server:  `   
`  port: 8888`

**Or update via code, this overrides properties and yaml settings.**

```java
CustomContainer.java

package com.mkyong;

import org.springframework.boot.context.embedded.ConfigurableEmbeddedServletContainer;
import org.springframework.boot.context.embedded.EmbeddedServletContainerCustomizer;
import org.springframework.stereotype.Component;

@Component
public class CustomContainer implements EmbeddedServletContainerCustomizer {

    @Override
    public void customize(ConfigurableEmbeddedServletContainer container) {

        container.setPort(8888);

    }

}
```

**Or update the port by passing the system properties directly.**

`Terminal`  
`java -jar -Dserver.port=8888 spring-boot-example-1.0.jar`