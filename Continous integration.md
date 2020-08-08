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
