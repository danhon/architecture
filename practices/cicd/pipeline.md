# Development Pipeline

Below is a description of the development pipeline process planned for the CWS-Cares project. Much of this is already in place, but items not in place will be called out below. The expectation is that all teams will use this process. 

1. For a given agile sprint, teams agree on, and pull stories from the JIRA backlog.
1. Teams develop code and when complete, a "pull request" notifies the dev leads that a team member has made a change. The team lead(s) review the code and if all is well, allow the code to be merged into the main branch, and a checkin to Github is done. 
1. The checkin process notifies the team’s CI server which starts a Jenkins process to compile code and run all the testing processes against the code. Static code analysis is performed automatically: Code Climate for front end teams, Sonarqube for API/Platform teams. 
1. If the tests pass successfully, Jenkins kicks off a process to build the tested code into Docker Hub. A base Docker container is specified (e.g. RedHat Linux with Java pre-installed) and the code deployed into the Docker Container. At this point, a working Docker container is built and ready for deployment. Once the container has been built, each team lead can deloy the container into the preint environment. See Figure 1 Sample Environment below
1. **[NEW]** Each team now has access to the "testing bubble". The full set of functional and/or acceptance tests can be run in the bubble, without affecting the ongoing testing and evaluation in the Pre-int environments.
1. For a deployment into an integration testing environment, we currently use a manual process. At the release manager's request -- and after a team has tested their code in Preint -- a DevOps engineer will deploy a specified Docker container into an existing environment. When the new container is deployed, a series of automated tests are run against the container to both verify the environment configuration as well as to identify any regression defects. 
1. **[NEW]** Each night all the functional testing containers will be run against the integration environment. The steps will be executed from a DevOps rundeck job: 
   1. reset mainframe DB2 datasources
   1. reset other data sources (Postgres, ElasticSearch, etc)
   1. execute pipeline of testing containers, capturing and publishing all results
   1. reset datasource back to baseline
1. During the day, QA and SMEs will execute manual tests in both the CARES environments and legacy Integration environments. Any new tests identified are entered into team backlogs for inclusion in the automated testing containers. 
1. When Functional testing has started (not completed) teams can request to promote code into Production where testing containers can run limited (performance flag ON?) performance tests (e.g. response time under load). 
1. Only after functional testing is all passing, and performance tests have been created and run, is a release a candidate for discussion for going to Staging for evaluation.  

To move from this point towards the production environment requires approval by, and coordination with, the project’s Release Manager. See Figure 2 CWDS Pipeline below
1. Several different automated testing tools are used:
    1. Junit – java unit tests for API
    2. Jmeter – Java performance and functional tests for API
    3. Selenium – automated front-end tests against a browser
    4. Rspec – Rails testing tools for front-end

![CWDS Containers](https://raw.githubusercontent.com/wiki/ca-cwds/architecture/images/containers.png)

*Figure 1 Sample Environment*


The diagram above is a picture of a sample environment. Docker containers are deployed into Virtual machines. VMs are created through DevOps scripts. 

The picture below shows the CWDS pipeline. The target process will enable tested code to be deployed into increasingly production-like environments, and up on which automated/manual testing will be performed. As the tests are passed, code moves through the pipeline towards production. 

![pipeline](https://raw.githubusercontent.com/wiki/ca-cwds/architecture/images/pipeline.png)

*Figure 2 CWDS Pipeline*

## Tools/Technologies used in CWDS CI/CD processes

<table>
  <tr>
    <td>Performance Monitoring</td>
    <td>New Relic</td>
    <td>Performance monitoring of full application stack</td>
  </tr>
  <tr>
    <td>Static Code Analysis</td>
    <td>Code Climate</td>
    <td>Code Climate is software as a service that provides static code analysis that is integrated with Github and provides constant feedback on source code quality, security exposures, and more. The TOS is negotiable for "enterprise" accounts.</td>
  </tr>
  <tr>
    <td>Configuration management</td>
    <td>AWS CloudFormation</td>
    <td>Included of AWS subscription. CloudFormation uses JSON or YML formatted templates to define infrastructure components, which are then loaded into the CloudFormation engine and used to create the servers, networks, and security controls defined by a given template. 

All templates created by the project use standard JSON, which is an open standard data markup language similar to XML.</td>
  </tr>
  <tr>
    <td>Project management</td>
    <td>Pivotal Tracker</td>
    <td>Agile project management tool provided as a web-based subscription service (SAAS) at http://pivotaltracker.com/. This service has a TOS (link).</td>
  </tr>
  <tr>
    <td>Version control</td>
    <td>Github</td>
    <td>GitHub is a web service with a free and paid subscription model that provides Source code version control tool based on the open source GIT project. This service has its own TOS (link). </td>
  </tr>
  <tr>
    <td>Asset build tool</td>
    <td>Webpack</td>
    <td>Tool for compiling front end assets</td>
  </tr>
  <tr>
    <td>Back-end build tool</td>
    <td>Gradle</td>
    <td>Open source build automation system that integrates with Jenkins</td>
  </tr>
  <tr>
    <td>Configuration management</td>
    <td>Ansible</td>
    <td>Flexible IT configuration management framework.   </td>
  </tr>
  <tr>
    <td>Continuous integration</td>
    <td>Jenkins</td>
    <td>Provides continuous integration services for software development.</td>
  </tr>
  <tr>
    <td>Front-end build tool</td>
    <td>Rake</td>
    <td>Rails command line tool used for Rails builds</td>
  </tr>
  <tr>
    <td>Asset & Dependency Management</td>
    <td>jFrog Artifactory</td>
    <td>Used to manage build assets as for code (Maven, Gradle) as well as deployment (Docker Registry, RPM and DEB repo)</td>
  </tr>
  <tr>
    <td>Javascript build tool</td>
    <td>Yarn</td>
    <td>Tool for packaging Javascript assets</td>
  </tr>
  <tr>
    <td>Docker Container Registry</td>
    <td>Docker Hub</td>
    <td>Repository for storing Docker images online in versioned repositories (public or private). The project uses DockerHub for the storage and distribution of non-production containers.

Use of DockerHub will be replaced by Amazon Elastic Container Repository (ECR) for Release 2.</td>
  </tr>
  <tr>
    <td>Package and deploy tools</td>
    <td>Docker Toolbox</td>
    <td>Tools for packaging software as Docker containers, provisioning machines and deploying containers. 

Docker containers are managed by the Docker Engine on project application servers, which depend on built in capability of the Linux kernel (namespaces and cgroups)</td>
  </tr>
</table>


