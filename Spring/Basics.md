# Why Spring framework

### Plain Old Java Objects (POJOs)
POJOs are simple Java Objects that do not contains any dependencies in it. They don’t implement any interface or extend any class as it is required by many frameworks.

The benefits of such approach is that a solution to a problem is not directly tied to the framework or it is not directly tied to other solutions, so if I change some part of the application other part won’t be affected. It modularize the whole application, so the objects can act as a black boxes, they connects with themselves using inputs and outputs, but each of them don’t know how other components (objects) are working. And Spring is taking care of connecting these objects together.

### Inversion of Control (IoC)/Dependency Injection
But how Spring is taking care of these loosely coupled objects?  
It is using the concept of Inversion of Control. The idea is to pass the control of the program lifecycle and process flow from developer to the framework. Spring is taking care of them and if you want to use them, you need to call Spring that will do it for you. To achieve it we need to create some code and then register it into the framework and from that point Spring is creating, using and destroying objects that are within it.

To make sure that certain classes are registered within Spring context it uses specific configuration templates. And there are several ways to do that: with annotations, extending certain framework classes or by using external configuration files (like XML).

Implementation of IoC in Spring is Dependency Injection. With this pattern we don’t need to hard coded creation of the object, framework is doing it for us. For example, when controller class is making use of service class it requires it requires the latter to be created at the first place. But what happens if service class requires another class? For example DAO class? Or maybe it requires several other classes? If it is a small application this dependencies management is doable, but on a large, company scale it is really hard to achieve the most efficient solution.

To illustrate it here is sample code of ‘regular’ approach.
```java
public class UserService {
  
  private UserDAO  userDAO = new UserDAO(); 
  
  public User getUser(String username) {
    return userDAO.getUserByUsername(username); 
  }
}
```
In Spring, instead of creating objects with new Object(…) syntax, we can add @Autowired annotation to the private field so the framework will inject if for us. And by injecting I mean that it will create it on our behalf or use the already existing one.
```java
@Component
public class UserService {
  
  @Autowired
  private UserDAO userDAO;
  
  public User getUser(String username) {
   return userDAO.getUserByUsername(username); 
  }
}
```
You may notice that above class is annotated with another, special annotation — @Component. This one is used to tell Spring that this class needs to be added to the context.

> This approach makes our classes loosely coupled, which makes it more flexible and not implementation-relevant. And that might be very useful when in some time we’ll want to change the code environment, so code re-write won’t be necessary.

Finally it enables easy unit testing, chiefly because we don’t need to worry about dependencies that are included within the class. To illustrate this, imagine that a service class has a DAO class for connecting to a database. With the regular approach (via new operator) we hardcoded DAO class into a service, so to test it we need first to create DAO class, which might end up with complicated preparing phase for testing. And that is not welcomed in unit testing.

### Convention over configuration
So how to achieve this dependency injection thing?  
Here is the best thing of Spring framework. Most of configuration job will be provided by default and if we want to customize it is really easy to do just by modifying one particular thing and not the container configuration.

There are several convenient approaches to achieve it. The most popular ones are based on XML file and Java class code. There is also another way to achieve it — auto scanning for components using Java annotations.
### XML configuration
First one is considered as an old-fashioned. It was introduced in first releases of Spring, so you can find it in the old projects, but it is still used. The idea is to have single or multiple XML files that contains a list of Beans (i.e. Java objects) that can be registered into Spring container. Next, during project deployment, these files must be uploaded to the Spring context.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    	http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="john" class="com.wkrzywiec.library.model.User">
		<property name="firstName" value="John" />
		<property name="lastName" value="Snow" />
		<property name="email" value="john.snow@winterfell.com" />
  		<property name="address">
      			<ref local="johnAddress"/>
   		 </property>
	</bean>

  	<bean id="johnAddress" class="com.wkrzywiec.library.model.Address">
    		<propery name="city" value="Winterfell" />
    		<property name="building" value="Castle" />
  	</bean>

</beans>
```
Above there is a simple user Java class and config XML file snippet. Let’s focus on config file. All beans must be declared within <beans> tag with a <bean> tag and within it there are several attributes:
- id — indicates the unique name of the bean, under which it will be registered in Spring - container,
- class — defines what class is the object,
- <property> — User class contains some fields that can populated with values using name (what field) and value (what value) attributes,
- ref — this one is used to include one bean in another, so in other words to set up dependency between them
- scope — defines beans’ lifecycle scope, e.g. singleton (single object for entire Spring container), request (life cycle of HTTP request), session (lifecycyle of HTTP Sesssion) and other.

Finally to add it to the application context and retrieve bean with specific id use following code:
```java
public class ApplicationStart {
  
    public static void main( String[] args ){
      
        ApplicationContext ctx = new ClassPathXmlApplicationContext("configuration.xml");
         
        User user = (User) ctx.getBean("john");
      
        System.out.println(user.toString());
        
    }
}
```
### Java Class
Another way to register beans into the Spring container is Java-based approach, which in many cases is more convenient way (as it is more readable).
```java
@Configuration
public class AppConfig {
	
    	@Bean(name="john")
	@DependsOn("johnAddress")
    	public User user() {
      		User user = new User();
      		user.setFirstName("John");
      		user.setLastName("Snow");
      		user.setEmail("john.snow@winterfell.com");
     
      		user.setAddress(address());
      		return user;
    	}
	
	@Bean(name="johnAddress")
	public Address address(){
		
		Address address = new Address();
      		address.setCity("Winterfell");
      		address.setBuilding("Castel");
		return address;
	}
}
```
Above Java class has special annotation — `@Configuration` — that tells Spring that it is a config file. Another one, `@DependsOn` is telling that the User bean will be created after the Address, not before.  
And finally to add beans defined in Java config class add use following code:
```java
public class ApplicationStart {
  
	public static void main(String[] args)  {
    
		AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
 		ctx.register(AppConfig.class);
		ctx.refresh();
    
		User user = (User) ctx.getBean("john");
	  
   		 System.out.println(user.toString());		
	}
}
```
### Component scanning
Main drawback of previous examples is that first we need to create specific Java class and then register it in Spring container in config file. Maybe it is not so much work, but still it is not really convenient.

That’s why there is another way to achieve it. Either in XML file or in Java config class we can declare that Spring will scan for Java classes with special annotations. So from this point we only add annotation above class name and the framework will do all the work for us.

To enable auto scanning add following code to config files:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">
	
	<context:component-scan base-package="com.wkrzywiec.library" />

</beans>
```
```java
@Configuration
@ComponentScan(basePackages="com.wkrzywiec.library")
public class Config {
 
  //other configurations
}
```
Using one of these set ups Spring will recursively find all annotated class within the package and its sub packages.

To add object to the Spring container just add one of the following annotation above its name:
- @Component — it is a standard annotation and can be added to any type of Java class, next ones are more specialized, but in most cases they can be replaced by this one,
- @Repository — it is used for Data Access Objects (DAO) that are responsible for retrieving information from the database,
- @Service — this one is used for service layer classes, they working as a middleman between UI and DAO and responsible for processing data and whole business logic,
- @Controller — classes with these annotations are taking care of user requests in UI.

Except for registering beans config files covers other tasks, like database connection configuration, adding external resources, enabling web MVC framework etc.

### Modular Architecture
The whole idea of Spring is to modularize whole framework into smaller pieces that are responsible for other aspect of the applications. There are about 20 modules that are grouped by role they play.   

**Core Container**. You probably noticed that I used this expression in previous section. It is the most important part of the framework, because it provides IoC feature and it can read configuration. It is like a factory for creating beans and managing them.

**Data Access**/Integration. As you might think these modules are responsible for transaction management and communicating with SQL and NoSQL data sources. It allows to connect to them using standard JDBC approach or ORM way with Hibernate.

**Web**. It is also very intuitive. It covers all the aspects related to web applications, like connection, handling HTTP requests, creating REST web service and so on. Container includes also the Spring MVC framework, which I used in my Library Portal project.

**Test**. Spring supports Test Driven Development by providing mock-up objects for unit testing and also many features that allows to make integration tests.

**Aspect Oriented Programming (AOP)**. In short, it is taking care of some common task that are shared within multiple objects, like logging, transaction management, security, etc.

https://wkrzywiec.medium.com/why-spring-framework-is-so-cool-8472ceabaab1

https://www.youtube.com/watch?v=rMLP-NEPgnM&list=PL9ooVrP1hQOEfi91PCFQMawtBJrPpir7y&t=2776s&ab_channel=edureka%21