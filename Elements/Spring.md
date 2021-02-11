## Basic idea of IoC pattern. Benefits.

Spring IoC is the mechanism to achieve loose-coupling between Objects dependencies. 

To achieve loose coupling and dynamic binding of the objects at runtime, objects dependencies are injected by other assembler objects.  

Spring IoC container injects dependencies into an object and make it ready for our use.  
Spring IoC container classes are part of `org.springframework.beans` and `org.springframework.context` packages.  
Spring IoC container provides us different ways to decouple the object dependencies.

## What is Spring configuration file? How does it look like?

Annotating a class with the `@Configuration` indicates that the class can be used by the Spring IoC container as a source of bean definitions. 

The `@Bean` annotation tells Spring that a method annotated with `@Bean` will return an object that should be registered as a bean in the Spring application context. 

The simplest possible `@Configuration` class would be as follows:

```java
import org.springframework.context.annotation.*;

@Configuration
public class HelloWorldConfig {

   @Bean 
   public HelloWorld helloWorld() {
      return new HelloWorld();
   }
}
```

The above code will be equivalent to the following XML configuration:

```xml
<beans>
   <bean id = "helloWorld" class = "com.example.HelloWorld" />
</beans>
```

Here, the method name is annotated with `@Bean` works as bean ID and it creates and returns the actual bean. Your configuration class can have a declaration for more than one `@Bean`. Once your configuration classes are defined, you can load and provide them to Spring container using `AnnotationConfigApplicationContext` as follows:

```java
public class HelloWorld {
   private String message;

   public void setMessage(String message){
      this.message  = message;
   }
   public void getMessage(){
      System.out.println("Your Message : " + message);
   }
}
```

In main app: 

```java
public static void main(String[] args) {
   ApplicationContext ctx = new AnnotationConfigApplicationContext(HelloWorldConfig.class);
   
   HelloWorld helloWorld = ctx.getBean(HelloWorld.class);
   helloWorld.setMessage("Hello World!");
   helloWorld.getMessage();
}
```

You can load various configuration classes as follows:

```java
public static void main(String[] args) {
   AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();

   ctx.register(AppConfig.class, OtherConfig.class);
   ctx.register(AdditionalConfig.class);
   ctx.refresh();

   MyService myService = ctx.getBean(MyService.class);
   myService.doStuff();
}
```



## Out of the box bean scopes (singleton, prototype, request, session, global session)

Scopes defined for Spring Beans:

- **singleton** – Only one instance of the bean will be created for each container. This is the default scope for the spring beans. While using this scope, make sure bean doesn’t have shared instance variables otherwise it might lead to data inconsistency issues.

- **prototype** – A new instance will be created every time the bean is requested.

Web-Aware ApplicationContext bean scopes:

- **request** – This is same as prototype scope, however it’s meant to be used for web applications. A new instance of the bean will be created for each HTTP request.

- **session** – A new bean will be created for each HTTP session by the container.

- **global-session** – This is used to create global session beans for Portlet applications.

Spring Framework is extendable and we can create our own scopes too. However, most of the times we are good with the scopes provided by the framework.

## Autowiring. Types of autowiring.

The Spring framework enables automatic dependency injection. In other words, by declaring all the bean dependencies in a Spring configuration file, Spring container can **autowire relationships between collaborating beans**. This is called Spring bean autowiring.

After enabling annotation injection, we can use **autowiring on properties, setters, and constructors**.

To enable **@Autowired** annotation we can enable annotation-driven injection by using below spring configuration:

```java
@Configuration
@ComponentScan("com.example.autowiringdemo")
public class AppConfig {}
```

## What are the types of Dependency Injection Spring supports

- **Attribute** (property) based injection
- **Constructor** based injection
- **Setter** based injection

As per Spring documentation:
- We should use constructor injection for mandatory dependencies
- We should use setter-based injections for optional dependencies
- Field-based injection is a costlier approach and we should avoid using it (Spring uses reflection for field based injection)




## What are inner beans.

## What modules does Spring Framework have
