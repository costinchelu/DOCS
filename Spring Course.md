www.spring.io  
https://start.spring.io

- Java EE vs Spring?
- Spring simplify Java EE

Core container (Spring Core Framework):
- factory for creating beans
- manage bean dependencies
- support for AOP (Aspect-Oriented-Programming) - add functionality to objects declaratively (logging, security, transactions etc)
- Data Access Layer: JDBC Helper Classes -> ORM (Hybernate) -> Transactions (OXM, JMS (Java Message Service - for sending async messages to a Message Broker))
- Tests

# IoC = outsourcing construction and management of objects

Spring container:
- Primary functions
- Create and manage objects (Inversion of Control)
- Inject object’s dependencies (Dependency Injection)

Bean's scope by default is SINGLETON (cached in memory, will return a shared reference to the same bean, stateless bean). We can use the PROTOTYPE scope to create a new bean everytime we request.

# Default bean names

Annotations - Default Bean Names ... and the Special Case

In general, when using Annotations, for the default bean name, Spring uses the following rule.

If the annotation's value doesn't indicate a bean name, an appropriate name will be built based on the short name of the class (with the first letter lower-cased).

For example:

HappyFortuneService --> happyFortuneService

However, for the special case of when BOTH the first and second characters of the class name are upper case, then the name is NOT converted.

For the case of RESTFortuneService

RESTFortuneService --> RESTFortuneService

No conversion since the first two characters are upper case.

Behind the scenes, Spring uses the Java Beans Introspector to generate the default bean name

# Scope

- Default scope is **Singleton**
- **Prototype** scope will create a hard copy of the same object(bean)

In contrast to the other scopes, Spring does not manage the complete lifecycle of a prototype bean: the container instantiates, configures, and otherwise assembles a prototype object, and hands it to the client, with no further record of that prototype instance.

# Annotatations:

@Component(specify name (between "") OR default will be class name with lowercase on the first letter) = mark this class as a bean

@Autowired = used for dependency injection
Spring injection types (all have the same result):
- constructor injection
- setter injection (method injection)
- field injection

@Qualifier(default name of the class (between "")) = setting the principal bean (when we have more than one implementation). Can be used for all types of injections.

@Value("$(foo.team)") = take value from the .properties file as indicated from the key provided

@Scope("prototype") = refers to the lifecycle of the bean (default is singleton (cached in memory, only one reference))
 
@PostContruct = will run method after the bean is constructed  
@PreDestroy = will run method before the bean is destroyed (cleanup). Methods can not accept any arguments(no-arg). In the case of prototypes, configured destruction lifecycle callbacks are not called. The client code must clean up prototype-scoped objects and release expensive resources that the prototype bean(s) are holding. See scope chapter for a custom bean post-processor

@Configuration = prepare class for bean configuration

@ComponentScan("package name") = equivalent to xml config file

@Bean =  tells Spring that we are creating a bean component manually. We didn't specify a scope so the default scope is singleton.

@PropertySource("classpath:application.properties") = to inject properties (values of the key from a .properties file)



# Spring MVC

Spring MVC – How to include JS or CSS files in a JSP page  
https://mkyong.com/spring-mvc/spring-mvc-how-to-include-js-or-css-files-in-a-jsp-page/



# Hibernate

- ORM