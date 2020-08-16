Integration means we  are getting all the work from different members of the dev teams into the software. When trying to get all parts at the final phase of the project, we could potentially get into trouble as different parts will not behave as it should.
  
Instead of trying integration phase at the end of the project, we could try to spread it on the whole length of the development.

Software is always in a working state and ready to run. If a change breaks the product we can fix it immediately.

I. **Build phase**
- headless build = our project can run independently without a tool (independent of the IDE)   
- automated on SCM commit = ideally, when a dev commits something it should build automatically
- dependency management system = ability to resolve automatically the dependency (3rd party libraries)
- run unit and integration tests
II. **Publish phase**
- builds are packaged into artifacts (could be executables, jar, archives etc) and published on the build server
III. **Deploy phase**
- pull artifacts and deploy to a bootstrap test server (real working server, virtual server)
IV. **Verification phase**
- run automation tests against test server
- run integration tests
- run performance tests
- run security tests
- produce reports (qualitative)
V. **Production**
- sometimes we need to monitor feedback (continous delivery) (usually in case of SaS (System as a Service))
- analyse usage

## CI Pipeline

![CI Pipeline](images/Continous%20Integration/CI_pipeline.png)

## CI Tools

- SCM - Source control management tools (version control)
- Build tools - create artifacts
- CI server/build server - orchestrate pipeline

![CI Server](images/Continous%20Integration/CI_server.png)

- Automatic deployment tools - deploy to test server and/or productioon
- Automated testing tools

### SCM

- **Open source:**
  * SVN
  * Git
  * Mercurial
- **Commercial**
  * Perforce
  * Clear Case
  * Microsoft TFS
  
### Build Tools (Java)
* Compile code
* Package/Resolve dependencies
* Package application
* can run unit tests, integration tests and possibly automation tests
* the build can run from the command line and not depend on the IDE

  * **Ant**  
uses XML  
need to write own scripts for building the app  
doesn't have dependency management but can be integrated with other tools to do that  
  * **Maven**  
replaces Ant  
most popular right now  
have dependency management  
can pull dependencies from a remote server  
  * **Gradle**  
newest  
uses Groovy as a script language  
much more flexibility over Maven  

### Continous Integration Server
Orchestrates various tasks in the CI Pipeline  
  * **Jenkins**  
most popular  
many plugins  
flexible build plans  
can work with Groovy  
  * **Bamboo (Atlassian)**
commercial product  
less plugin options than Jenkins  
  * **TeamCity (Jetbrains)**  

### Deployment Tools
Used to deploy to the test server and/or production  
Two types of mechanisms (push & pull) - pushing scripts to the Node from the development machine, or getting an agent from the node to pull scripts from the publishing server  
* **Chef**  
most mature  
pull mechanisms  
language based on Ruby  
* **Puppet**  
most mature  
pull mechanisms  
language based on Ruby  
* **Ansible**  
written in Python  
push mechanism  
much simpler to work with than Chef or Puppet  
* **Salt**  
written in Python  
supports both push or pull mechanisms  

* **Docker**  
not really a deployment tool   
container system  
running an isolated subsystem on the VM  
packages everything that we need in order to run our application  

### Automated Testing Tools
Used in both build & verification phase   
Build = unit & integration tests
- **JUnit**   
unit and integration testing for Java
- **Selenium**  
automation & acceptance tests used in verification phase  
runs a browser in the background (good for web apps)  
- **Cucumber**  
runs on top of Selenium  
define tests using use cases  
very easy to organize tests in a human redable format  
written in Ruby (supports Java, JS, Python, Ruby)

## GIT HOSTING

**Git on-premise hosting for the enterprise**  
Organizational accounts can be created on github to provide organizations with an SCM hosting solution.

**Github enterprise**  
https://enterprise.github.com/home

GitHub Enterprise is the on-premises version of GitHub, which can be deployed on your own servers in your network. Organizations that cannot use github on the cloud can choose this option.

**Bitbucket server**  
https://www.atlassian.com/software/bitbucket/server

Bitbucket is a product by Atlassian which provides a git repository server. It provides both a hosted solution and an on-premise solution for organizations.

Bitbucket Server is an obvious choice if your development toolchain already heavily depends on other Atlassian products like JIRA and Bamboo.

**Gitlab**  
https://about.gitlab.com/

GitLab is an application to code, test, and deploy code together. It provides Git repository management with fine grained access controls, code reviews, issue tracking, activity feeds, wikis, and continuous integration.

GitLab Inc. has 4 product offerings:

GitLab Community Edition (CE) - free, self hosted application, support from Community

GitLab Enterprise Edition (EE) - paid, self hosted application, comes with additional features and support

GitLab.com - free SaaS for public and private repositories, support can be purchased

GitHost.io - a private single-tenant GitLab instance run by us

**Perforce Helix4git**  
https://www.perforce.com/products/helix4git

Perforce is a commercial SCM product. It provides git support with its helix4git solution. Perforce is an on-premise solution.

Perforce server with support for Git.

**Microsoft Team Foundation Server**  
Microsoft's own code management Team foundation Server supports git. It can be used with git as its underlying version control.

## GIT WORKFLOWS  

- **CENTRALIZED WORKFLOW**  
Everybody performs a clone on a centralized repository and work on the master branch pushing their changes  

- **FEATURE BRANCH WORKFLOW**  
Everybody performs a clone on a centralized repository and create a branch for every feature they need to develop. Once someone completes a feature they don't immediately merge it into master. Instead the push the branch and file a pull request asking to merge their additions into master
- **FORKING WORKFLOW**  
Developers fork the central repository (instead of cloning it). Also they have a server-side repository. After pushing their work on their server side repository, the project maintainer can push to the official repository. Only the maintainer have write access to the official codebase.


## BUILD TOOL - MAVEN

- mostly used for Java
- based on a standard project structure
- dependency management (able to resolve 3rd party dependencies, also download them from a repository)
- based on plugins (it has a core + plugins)

![Maven Architecture](images/Continous%20Integration/Maven_architecture.png)

- creates a locat repository for dependencies and copies those dependencies form Maven Central (repo) or other remote locations
 - Maven will ask for an archetype (project type), a group and artifact name and a version for the project
 - Maven project structure:  
     * *src/main/java* = sources
     * *src/main/resources* = resources (images, other files etc)
     * *src/test/java* = unit tests
     * *src/test/resources* = resources used for tests
     * *pom.xml* = project's configuration file

### Command line Maven
using a console (prompt) we can generarate a Maven project:
```apache
mvn archetype:generate
```
we can compile our project using:
```apache
mvn compile
```
to compile and run our unit tests:
```apache
mvn test
```
to build our jar (package):
```apache
mvn package
```
to take the package and install it into our local Maven repository:
```apache
mvn install
```
to clean up the artifact and classes for the project:
```apache
mvn clean
```

### IDE Maven
To use Maven in IntelliJ or Eclipse we can create a new project marked as Maven project. When we need a new dependency included in  the project we can search for it in the Maven Central Repository and paste the dependency snippet inside our pom.xml file in the *dependencies* tag. 

In IntelliJ, if we get the error: *java: error: release version 5 not supported* we need to **change language level** from project -> module also we need to get to Settings >> Build, Execution, Deployment >> Compiler >> Java Compiler and **change target bytecode version** to 11 (or other newer Java SDK version).
Or insert into pom.xml:
```xml
<properties>
       <java.version>11.0.8</java.version>
       <maven.compiler.version>3.8.1</maven.compiler.version>
       <maven.compiler.source>11.0.8</maven.compiler.source>
       <maven.compiler.target>11.0.8</maven.compiler.target>
   </properties>

   <build>
       <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-compiler-plugin</artifactId>
               <version>${maven.compiler.version}</version>
               <configuration>
                   <source>${java.version}</source>
                   <target>${java.version}</target>
               </configuration>
           </plugin>
       </plugins>
   </build>
```


### Example pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>Maven_test_2</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>MavenTest2</name>
    <url>http://maven.apache.org</url>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>


    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13</version>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <version>3.11</version>
        </dependency>

        <dependency>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
        </dependency>
    </dependencies>
</project>
```

### Default lifecycle phases
**Validate**  
**Compile**  
**Test**  
**Package**  
**Verify**  
**Install**  
**Deploy**  

- Maven has a multi-modal capability

# DOCKER

Docker is a container technology that is used to deploy applications. With regard to continuous integration we can use docker in the deploy and production phases of our pipeline to bootstrap a container(or a set of containers ) with our application.

The alternatives to using docker in the pipeline is to use deployment tools like Chef, Puppet or Ansible.

The docker concept is different, where as with the other tools we are configuring a running VM with our latest version of the software , with docker we are always creating a new docker image containing the latest version of our software and running a container based on that image.

### Docker Components

**Docker daemon** - or the docker engine, responsible for running and managing containers.

**Docker client** - issues commands to the docker daemon.

**Docker registry** - used to store docker images. We can use the DockerHub, or setup our own local docker image repository.

**Docker image** - contains the software components that we need to be available to the container. The equivalent of a VM image, only much more lightweight and easy to create. We can automate the creation of docker images using a Dockerfile.

**Docker container** - the actual container that is run based on a docker image.

### Docker Usages

There are several scenarios for which we might use docker as developers or operators.

To bootstrap a container in our build pipeline for automation tests, like we are doing in our course. In that case we might be distributing software to be installed on-premise to our customers and are using docker only for our CI pipeline.

We are a ISV and we are creating docker images for our software and providing those images to our customers, so that they can run our software with docker containers.

We are a SAAS company or an IT organization that is using docker for both development and production and installing various software landscapes with docker. In that case we need a docker orchestration tool like Kubernetes or Swarm in order to scale our docker containers among various VMs. We will also need to monitor and manage many instances, this will usually require using a special docker orchestration suite or a PAAS (Plasform as a service) software.

### PAAS Products using Docker

**Redhat Openshift** - https://www.openshift.com/

**IBM BlueMix** - https://www.ibm.com/cloud-computing/bluemix/

**Docker Datacenter** - https://success.docker.com/Datacenter

(Container as a service)

### Docker Orchestration

**Docker Swarm** - https://docs.docker.com/engine/swarm/

**Kubernetes** - https://kubernetes.io/

# SELENIUM
- help us run automation tests
- open source - Apache licence
- set of different software tools supporting test automation
- Selenium web driver (core tool)
- Selenium IDE - records automation scripts

# PROJECT RESPONSABILITIES

- Development
- Integration tests
- Automation tests
- Infrastructure provisioning
- Deployment
- Security
- Logging
- Monitoring
- Troubleshooting

![What is devops?](images/Continous%20Integration/Devops_culture.png)