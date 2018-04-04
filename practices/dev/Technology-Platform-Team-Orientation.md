# Technology Platform Team Orientation
## 1. Access checklist
### 1.1. Development
* OSI email
* Slack account in CWDS organization
* [State SharePoint](https://osicagov.sharepoint.com/_layouts/15/sharepoint.aspx) (the same credentials as for OSI email) 
* [GitHub](https://github.com/ca-cwds) account added to CWDS organization
* [DockerHub](https://hub.docker.com/u/cwds/dashboard/) account added to CWDS organization
* OpenVPN
* SSH access to AWS environments (Pre-Int) 
* [Kibana Logs](http://logs.cwds.io) for all dev environments (Pre-Int, Preview, Int) 
* [Pre-Int Jenkins](http://jenkins.mgmt.cwds.io:8080/login) 
* Access to development environments: [Pre-Int](web.preint.cwds.io), [Preview](preview.cwds.ca.gov), [Int](https://web.integration.cwds.io)
* [Pivotal Tracker](https://www.pivotaltracker.com/n/projects/2011319)/ JIRA
### 1.2. Legacy
* CWS/CMS application ID
* SAF account

## 2. Coding and Indenting standards
* Technology Platform Teams (TPT) adheres to [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html). IntelliJ IDEA plugin can be used to enforce Google Code Style. More about [Code Standards](https://github.com/ca-cwds/API/wiki/Coding-Standards).
## 3. Code Quality and Naming conventions
* We adhere to the coding approach described in the book [Clean Code by Robert Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882).
* [Sonarqube](http://sonar.dev.cwds.io:9000/projects/favorite) is used by all TPT as code quality tool to enforce coding best practices. The common project quality gate is applied to all modules.
## 4. Test Coverage
* All TPT projects are covered by JUnit tests. Gradle is used to generate test report.
* We are using JaCoCo for testing coverage measuring. More details on how you can integrate JaCoCo into the application [here](https://github.com/ca-cwds/cals-api/wiki/Code-Coverage-Approach).
* The application shall be covered by unit tests and achieve **at least 70% of coverage**. 
* JMeter for performance testing
* Sonarqube with additional plugins for security static code analyses. Additional tools now are considered to be used for static and dynamic security scanning
## 5. Development environment
### 5.1. Desktop Security requirements
CWDS Requirements for all vendor devices, each device (including your smartphones and tablets) used to access OSI or CWDS data or environments has several minimum requirements:

* Whole Disk/Device Encryption
* Anti-Malware/Security Software Installed and Updated
* Lastest OS version is installed (and kept patched)
* Device/OS Password enabled and changed every 90 days
* Firewall enabled

Strongly suggested the following:

* Firewall - "Stealth mode" and Application Blocking enabled
* Firewall -  Only essential services allowed access to the internet (outbound) or device (inbound)
* Always use VPN - When using public Wi-Fi networks, you should always use a personal or company VPN. If you do not have either of these, use the free Opera Web browser (Win/Mac/Lin) which includes built-in VPN or the free Opera VPN (iOS/Android)

### 5.2. Development Tools
* [Java 8 SDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* IDE - IntelliJ IDEA, Eclipse
* IntelliJ IDEA SonarLint plugin for real-time static code analyses
* IntelliJ IDEA Google-java-format for code formatting
* [Docker Toolbox](https://www.docker.com/products/docker-toolbox) (select Kitematic during installation)

## 6. Continuous Integration and Continuius Delivery

* [Development Pipeline](https://osicagov.sharepoint.com/sites/projects/CWS-NS/releasemanagement/_layouts/15/WopiFrame.aspx?sourcedoc=%7Bbb79fd6b-acba-43a7-b20d-dcda49edcbbd%7D&action=interactivepreview)
* [CI Pipeline](https://osicagov.sharepoint.com/sites/projects/CWS-NS/releasemanagement/_layouts/15/WopiFrame.aspx?sourcedoc=%7B84c02331-aa50-40ba-a94e-d75b52d2dea1%7D&action=interactivepreview)

### 6.1. Jenkins pipeline
* [CALS API pipeline example](http://jenkins.dev.cwds.io:8080/job/cals-api/) 
* [Jenkins file example](https://github.com/ca-cwds/cals-api/blob/development/Jenkinsfile) 

## 7. Project Structure
### 7.1. Digital Services
* Intake 
* CALS 
* Case Management 1
* Case Management 2
### 7.2. Technology Platform
* TPT 1 - supports Intake team
* TPT 2 - supports CALS team
* TPT 3 - support Case Management teams
### 7.3. Other Teams
* DevOps
* Implementation
* External Interfaces and Data Team
* DesignOps 

## 8. Solution architecture
* [Technology Stack](https://osicagov.sharepoint.com/sites/projects/CWS-NS/TST/_layouts/15/WopiFrame.aspx?sourcedoc=%7Bebf49d9e-1dfe-4c92-b9d5-e3e975cac3f7%7D&action=default&slrid=6a4c299e-50a5-4000-89fb-29fb96add4ad)
* [Architectural Diagram](https://osicagov.sharepoint.com/sites/TechnologyPlatformTeam2/Shared%20Documents/Forms/AllItems.aspx?id=/sites/TechnologyPlatformTeam2/Shared%20Documents/Architecture/gateway.pdf&parent=/sites/TechnologyPlatformTeam2/Shared%20Documents/Architecture)
* [Security Development Guide](https://osicagov.sharepoint.com/sites/TechnologyPlatformTeam2/_layouts/15/WopiFrame.aspx?sourcedoc=%7BEB8E8C6A-481B-49E3-A855-09DA49CF976B%7D&file=CWDS%20API%20Security%20Developer%27s%20Guide.docx&action=default)
### 8.1. Technology Platform Components
#### 8.1.1. TPT 1
* [Ferb API](https://github.com/ca-cwds/API) - Intake Screening and Investigation
#### 8.1.2. TPT 2
* [CALS API](https://github.com/ca-cwds/cals-api) - Facility, RFA 
* [Perry](https://github.com/ca-cwds/perry) - Authentication, Authorization, integration with SAF
* [Dora API](https://github.com/ca-cwds/dora) - Search API based on Elasticsearch
* [Geo Services API](https://github.com/ca-cwds/geo-services-api) - address validation, lookup, integration with SmartyStreets
* [Document Management System API](https://github.com/ca-cwds/dms-api) - provides ability to create/update/delete documents, generate documents base on templates based on Nuxeo
* [Forms API](https://github.com/ca-cwds/forms-api) - CRUD API for form based functionality

#### 8.1.3. Shared Projects
* [Neutron Jobs](https://github.com/ca-cwds/jobs) - ETL to load data from DB2 and Postgresql to Elasticsearch
* [API Core](https://github.com/ca-cwds/api-core) - shared code used by other API modules
* [DB2 Data](https://github.com/ca-cwds/db2data) - DB2 migration scripts

### 8.2. API architecture
* [Key architecture concepts](https://github.com/ca-cwds/API/wiki/Architecture-and-Design----Changes-and-Elaborations)

### 8.3. Development Artifacts Versioning 
[Naming convention for artifacts as jar libraries, Docker images, etc](https://osicagov.sharepoint.com/sites/TechnologyPlatformTeam2/_layouts/15/WopiFrame.aspx?sourcedoc=%7B3282CF58-693B-4C9E-B2AF-CFFDA014F02A%7D&file=Artifacts%20Versioning.pptx&action=default&IsList=1&ListId=%7B23359B33-C3B6-481F-A33C-027B0A464AB5%7D&ListItemId=17)

## 9. FOSS
* AGPL is currently selected as a target license for CWDS code base
* Make sure you are using AGPL compliant open source licenses as Apachev2, MIT, BSD, LGPL
* Do not use Eclipse Public License 1.0, CDDL, GPLv2

## 10. Scrum
### 10.1. Technical Debt
[Analyzing, Identifying and Managing Technical Debt](https://osicagov.sharepoint.com/sites/projects/CWS-NS/Agile/_layouts/15/WopiFrame.aspx?sourcedoc=%7B0196183f-5a42-497a-8207-38ccfe86d58b%7D&action=default)

## 11. Legacy Development
* [Legacy Development Guide](https://osicagov.sharepoint.com/sites/TechnologyPlatformTeam2/_layouts/15/WopiFrame.aspx?sourcedoc=%7B7D553D6A-0A5B-4FEE-A2AE-CD6A8ED5D6F6%7D&file=Legacy%20Development%20Guide.docx&action=default&IsList=1&ListId=%7B23359B33-C3B6-481F-A33C-027B0A464AB5%7D&ListItemId=26) - work in-progress
