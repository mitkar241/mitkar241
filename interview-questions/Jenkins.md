# Jenkins
---
## Introduction
---
Jenkins is an open-source, free server that allows testers and engineers to develop reliable technologies for Continuous Integration or flexible construction applications on systems that use Java for coding. It has over 1600 plugins to support any kind of development task.

#### What is Jenkins?
---
Jenkins is a self-contained, open-source automation server that can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software. Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.

Jenkins has many appealing features for developers:

- Installation is easy: It is a platform-independent, Java-based software that can install quickly on Windows, Mac OS, and Unix-like operating systems.
- Configuration is easy: Its web interface is simple to install and customize, and it includes error checks as well as a designed support feature.
- Plugins are available: The update center has hundreds of extensions that integrate with any tool in the CI and CD toolchain.

#### Explain Continuous Integration, Continuous Delivery, and Continuous Deployment?
---
- Continuous Integration: A software development process where the changes made to software are integrated into the main code as and when a patch is ready so that the software will be always ready to be - built, tested, deployed, monitored - continuously.
- Continuous Delivery: This is a Software Development Process where the continuously integrated (CI) changes will be tested & deployed continuously into a specific environment, generally through a manual release process, after all the quality checks are successful
- Continuous Deployment: A Software Development practice where the continuously integrated (CI) changes are deployed automatically into the target environment after all the quality checks are successful

Based on the level of automation, the above three paradigms can be better represented as below -

- CInteg: development - build - integration
- CDeliv: development - build - integration - release
- CDepol: development - build - integration - release - deploy

#### Jenkins use cases?
---
Jenkins is often used to consistently design and validate software applications. It makes it easy for developers to implement updates to the code and for users to get the latest version quickly. Jenkins uses plugins to accomplish Continuous Integration. Plugins essentially allow DevOps stages to be integrated.

#### Explain DevOps and how Jenkins is used in it?
---
Azure DevOps (formerly known as Visual Studio Team Services - VSTS) is a series of tools for creating, evaluating, and distributing software. Developing and installing software has become even more effective with Azure DevOps. It is not only a series of software for automating CI-CD using the Microsoft stack but it can also be conveniently integrated with a variety of other third-party tools.

## Setup
---
#### System Requirements
---
- Hardware Prerequisites
  - RAM : at least 256 MB of RAM
  - Hard Disc : at least 1 GB
- Software Prerequisites
  - Since Jenkins is based on Java, you'll need the most recent update of either the Java Development Kit (JDK) or the Java Runtime Environment (JRE).

#### Explain the process of installation of Jenkins
---
The measures below should be taken to install Jenkins effectively:

- Go to https://www.jenkins.io/download/ and choose the platform you want to use. 
- Unzip the downloaded package from your local computer's download spot. Double-click the jenkins.msi file that has been unzipped. 
- Press next on the Jenkins setup pad.
- Selecting the directory where you want the Jenkins instance to be saved (the default location is C: Program Files (x86)Jenkins).
- Click on the install option.
- When the installation is completed, click on finish.

#### How do I change the Jenkins running port?
---
Jenkins' default port is `8080`.

- ##### Update using Config File
  - Change port number in the config file `/etc/default/jenkins` to 8081 (`HTTP_PORT=8081`)
  - Restart Jenkins: `sudo service jenkins restart`
- ##### Update using `jenkins.war`
```bash
java -jar jenkins.war --httpPort=8081
```
- ##### Update using Dashboard
  - `Manage Jenkins` > `Configure System` > Jenkins URL to 8081

## Master-Slave Architecture
---

#### Explain Jenkins' Master-Slave architecture?
---
Jenkins supports the owner-slave model, in which a master employs a large number of slaves. Jenkins Distributed Builds is another name for it. It allows you to run jobs on a variety of platforms, including Linux, macOS, and Windows. We may also use Jenkins Distributed Builds to perform a similar project on several conditions in parallel, allowing you to achieve the best results quickly using this distributed approach. The rest of the task results are collected and analyzed on the master hub.

#### What is a Jenkins Workspace, and how does it work?
---
Jenkins has a built-in command-line interface that allows you to access it from the content of the shell. This is useful for automating repetitive errands, mass alerts, and inconvenience research, among other things. The Jenkins CLI client, which is a Java JAR file distributed with Jenkins, is used to use this interface.

#### What is the JENKINS_HOME directory used for?
---
The JENKINS_HOME directory contains all of the settings, logs, and configurations.

#### How do you copy and move Jenkins to a new server from an older one?
---
- The `JENKINS_HOME` directory contains all of the configurations and parameters.
```
JENKINS_HOME=/var/lib/Jenkins
```
- Copying this directory to the new server should be sufficient.
- The command `sync` can be used to do this.

#### How does one copy files and create a backup in Jenkins?
---
- You can back up your JENKINS_HOME directory regularly to make a snapshot.
- All build job configurations, slave node configurations, and build history are stored in this directory.
- Copy this directory to make a backup, or copy a working directory to duplicate some job or rename the directory.

#### In Jenkins, what is meant by an agent?
---
The agent determines the pipeline's execution point for a specific stage or the whole pipeline.

#### Define the Jenkins parameters?
---
Several input parameters may influence the execution of a construct. If you do have several test suites but just want to run one, for example. You can choose which one to run by setting a parameter. To use parameters in work, you must do so when specifying the parameter. The parameter may be a string, a register, or something else entirely.

#### How does one configure communications between Jenkins master and its node agent?
---
There are two ways to start a node agent:

- Browser: A JNLP (Java Web Start) file is downloaded if the Jenkins node agent is launched from a browser. This file starts a new job-running loop on the client computer.
- Command-line: The executable agent.jar file is required to launch the node agent from the command line. When you run this file, it starts a loop on your client who communicates with Jenkins to create jobs.

## Pipeline
---
#### Explain the Jenkins pipeline?
---
A pipeline is a set of interconnected jobs that are executed one after another in a predetermined order. Jenkins pipelines have several modules that can be used to combine and incorporate continuous deployment pipelines. Code is used to convey the directions to be followed.

Jenkins pipeline (or just "Pipeline") is a collection of plugins that help you set up and use continuous distribution pipelines in Jenkins. A continuous distribution pipeline is an integrated representation of the product delivery process, from source code to consumers and customers.

#### What is DSL Jenkins?
---
Jenkins DSL (Domain Specific Language) is a plugin that allows jobs to be specified programmatically but in a human-readable manner. The UI settings are intuitively converted into code using this plugin. You'll be able to build a version for the job while still keeping track of the updates. The translated code is written in the Groovy programming language.

#### Name the types of pipelines in Jenkins?
---
There are 3 types:

- CI-CD pipeline (Continuous Integration Continuous Delivery)
- Scripted pipeline
- Declarative pipeline

#### Explain what Groovy means?
---
Jenkins uses a domain-specific language (DSL) called "Groovy" inside a Pipeline Project (read plugin), which will describe a new pipeline as just a script. That single script may articulate a flow that would typically take several "standard" Jenkins jobs chained around.

Groovy will work in conjunction with Java, and the two languages' syntaxes are very close. While writing Groovy, when you forget the grammar, you can write in Java syntax. Groovy may be used as one of the Java platform's scripting languages. Groovy scripts could be named from inside Java, reducing the amount of time spent on Java development.

#### What are scripted pipelines, and how do they work?
---
With the aid of a lightweight agent, a scripted Jenkins pipeline continues to run on the Jenkins ace. It makes use of a limited number of assets to interpret the pipeline into nuclear directions. Both declarative and scripted language structures are distinct from one another and are distinguished in unusual ways.

#### Explain the code for a pipeline in Jenkins and enumerate the pipeline types?
---
Pipeline-as-a-code is a strategy or collection of features that allows you to keep the CI/CD workflow logic throughout the source code repository despite making extra Jenkins branch configurations. This is specific to projects with a Jenkins file folder in the repo's root folder (containing a pipeline script). Declarative and syntax pipeline syntax are the two forms of pipeline syntax.

#### What is meant by an Agent Directive in Jenkins?
---
Jenkins is guided by the agent directive about how and when to conduct the Pipeline or its subsets. Agents are required for all pipelines. The agent creates a workspace for the pipeline, including source control checkout files and other required working files. When an executor is usable, it also triggers Jenkins to run the steps needed for execution.

## Continuous Integration
---
#### What are the differences between Continuous Deployment, Continuous Delivery, and Continuous Integration?
---
Continuous Integration (CI) is the practice of continuously incorporating modifications into the essential program at all phases of the distribution pipeline after being validated in a prototype environment. Jenkins and Bamboo servers make use of CI.

Continuous Delivery is the manual delivery of code (shipping) to a specific test, integration, or manufacturing area.

Continuous Deployment is the automated release of code into the staging or development process after it has passed the CI stage's testing.

#### How does Jenkins achieve Continuous Integration?
---
Continuous Integration is a programming process that requires developers to commit updates to the source code in a public repository many times a day or at frequent intervals. A repository is created for any commitments made. As a result, any challenges can be spotted by the team early on. Moreover, the Continuous Integration platform performs various other tasks, such as deploying the development application to the test server, informing the relevant teams about the construct and test performance, etc. Jenkins uses plugins to accomplish Continuous Integration. Plugins generally allow DevOps stages to be integrated.

#### Name some Continuous Integration tools, and why is Jenkins better than them?
---
Buddy, Jenkins, TeamCity, Big Eval, GoCD, Bamboo, GitLab CI, and others are examples of continuous integration tools. 
| Before Jenkins | After Jenkins |
|---|---|
| Once all of the developers had finished their allocated coding assignments, they would all commit the code at the very same time. Build is then reviewed and implemented.	| As soon as the developer commits the code, it is designed and tested. Throughout the day, Jenkins will create and validate the code many times. |
| The development process is slow. | The development process moves quickly, and users now have easier access to new features. Profits are increased. |

## Continuous Delivery
---
#### Create and explain the workflow in a Continuous Delivery Workflow?
---
We must first create a branch before we can create a CD workflow. The division is where all of the scriptings, checking, and code updates take place. If the research is over, the division modifications are combined and delivered.

![CD workflow](https://lh3.googleusercontent.com/hxMQWFJXKXvdVL3DcN9SAQ-m9mjXlAbozVXUkd5mZy-q1rX6YgQPkk5fG-6KDuZv9pCnt5ePt8OgaRA_1L_BUQqatm96oaBpF2SDc-yHlbDd7LZFZkbmSCxjpTAmV26pnHg-NzGX)

## Git
---
#### Name the Jenkins suite's essential plugins?
---
The Jenkin suite's essential plugins are Docker, Jira, Slack Notification, Maven, Amazon E2C, jUnit, Pipeline, Mailer, and Greenballs.

#### Explain what is meant by the Git plugin? 
---
Git is software that allows you to trace improvements in a collection of files. It's typically used to coordinate work by programmers working on source code together during software development. Pace, data consistency, and support for distributed, non-linear workflows are among its objectives (thousands of parallel branches running on different systems).

## Build
---
#### What is meant by Maven, and what benefits accrue when Jenkins and Maven are integrated?
---
Maven is a platform for managing builds. All of the dependencies required to create, validate, and run the code can be configured using a simple pom.xml. Maven is in charge of a research project's entire lifecycle. The Maven Webdriver can develop the project and run all tests effectively when it is merged with Jenkins.

#### Explain Jenkins' working in a simple use-case?
---
Let's assume a developer is operating on a code and contributes it to the repository.

- Jenkins server scans for adjustments in the repository detects the code and pulls it to start a build.
- If the build malfunctions, the results are sent to the developer to make changes.
- If it succeeds, the build is deployed to a test server.
- A test report is produced and submitted to the developer when the testing is completed. This method is repeated until the code passes all the checks, after which it is deployed to output.

#### How does one start using Jenkins from the command line?
---
The Jenkins Web application ARchive (WAR) file can be started from the command line in the following manner:

- Download the latest stable Jenkins WAR file to an appropriate directory on your machine.
- Open up a terminal/command prompt window to the download directory.
- Run the command java -jar Jenkins.War.
- Browse to http://localhost:8080 and wait until the unlock Jenkins page appears.
- Continue with the post-installation setup wizard below.

#### If using SVN polling or scheduling a building job in Jenkins, what syntax is used?
---
Cron syntax is used for building a job in Jenkins. Cron syntax is represented by five asterisks, each separated by a space. The syntax is as follows - [minutes] [hours] [day of the month] [month] [day of the week]. For example, if you want to set up a Cron for every Monday at 11.59 pm, it would be 59 11 * * 1.

#### Explain how to build a Jenkins job?
---
The steps for building a Jenkins job are as follows:

- On the Dashboard, click on "New Item."
- Select "Freestyle Project" from the drop-down menu.
- Enter job specifics such as SCM, build triggers, advanced options, and so on.
- It's critical to determine the location of any files that need to be created.
- After you've labeled all options, click on 'Add build stage' and choose the right option. 
- For example, if you wish to create a file, pick the file name and the build command.
- Click on "Build Now" to save the design and perform a test run.

#### Explain user authentication in Jenkins?
---
Due to various optimizations, Jenkins pipeline programs have become the tool of choice for business companies looking to incorporate and transform continuous distribution (CD) pipelines through Jenkins. CD pipelines are streamlined expressions of the mechanism for getting applications from version control to consumers and clients. Jenkins allows you to build CD pipelines using either a web UI or a Jenkins file that has been dedicated to source control.

#### How is a third-party tool used in Jenkins?
---
Let's pretend we want to use Node, a third-party tool.

- Make sure Node is mounted first.
- Install the Jenkins plugin for Node via the Jenkins admin console.
- In the admin console, go to Manage and customize the settings on the Tools page.
- Any optimized nodeJS tool can be added to create a job in a pipeline.
- Because of differences in configurations, the protocol for various third-party tools can vary significantly.

#### What are the differences between Bamboo and Jenkins?
---
| Jenkins | Bamboo |
|---|---|
| Open-source tool | Commercial tool |
| Supported by a huge global community | It has a separate production team |
| Not very user-friendly | More user-friendly features |
| There are several plugins available to execute different functions. | The majority of features are pre-installed, and there are also extensions available on the Atlassian marketplace. |

#### Explain the process used by Jenkins? 
---
Jenkins uses plugins to simplify the whole continuous implementation and distribution process. The steps are as follows:

- Multiple source code updates are committed to the Git repository by developers.
- The Jenkins server monitors database updates and performs a build for each check-in.
- The developed program is then deployed to the test server by Jenkins (like Selenium). The test results are returned as a response.
- The framework is installed on the production server after all tests have been completed on the test server.
- Via the different stages, the input is again submitted to the developer (test server, Jenkins server, Git repo).

![Jenkins CI/CD](https://lh5.googleusercontent.com/Sh-EhPELdp1skf46rdqMA73Ypb5R1tZ4cxtyDWcvk6HmOw3gMNAPseveI6DS9BoSdGfXD23JT1cjmUIqqyMvZbM5k67I96YAdMbD5sklUjZVMfogSHrnAgOD_0JQ6gbqw_5gnCgd)

#### How does one use Jenkins to create a Multibranch Pipeline?
---
The steps are as follows:

- Open the Jenkins dashboard and select "new object" from the top left menu to generate a new item.
- Click OK after entering your project name and selecting "Multi-branch pipeline" from the drop-down menu.
- After that, choose the repository's location, branch source (GitHub/Bitbucket), and branch source credentials.
- Save the project.
- Jenkins builds new Multi-branch Pipelines for servers of branches and pulls requests with Jenkins files automatically.
- The HookURL is used to bind to the GitHub repository. This URL can be found in the repository's settings.
- This HookURL should be added to the Webhooks section.
- Jenkins will automatically trigger the build until the jobs have been generated.

#### What is meant by Blue Ocean when using Jenkins?
---
Blue Ocean is a contemporary Jenkins UI that provides a tailored interface with a modern style. Any user can build, diagnose, and simulate Continuous Delivery pipelines using this guide. Since it is viewed visually, there are no engineering qualifications required to build or comprehend the pipelines. Furthermore, since each stage can be quickly navigated, detecting automation problems is easy.

#### What is the process of continuous testing?
---
The steps are as follows:

- Creating a test automation package from consumer stories/requirements using software
- Create a test environment
- Build a prototype data bed by copying and anonymizing output data
- Monitor APIs using service virtualization
- Do parallel output checking

#### How does one integrate the Jenkins process with Git?
---
The measures to combine Git with Jenkins are as follows:

- Open the Jenkins dashboard and create a new Jenkins career.
- Pick the work form and enter the project name (in the object name). Click on the OK button.
- Fill in the project details. Go to the tab titled "Source Code Management." The choice 'Git' will appear if the Git plugin is already installed in Jenkins.
- If you don't see it, reinstall the GitHub addon, GitHub Branch Source plugin, GitHub API plugin, Gitclient plugin, etc.
- Restart Jenkins after downloading the plugins to display the improvements.
- Enter the repository URL to get the code from GitHub. Install Git if you don't already have it on your computer.

#### What are the differences between Jenkins, Ant, and Maven?
---
Jenkins uses the continuous integration method, while Ant and Maven work on constructed software. Jenkins can run unit tests and deploy programs automatically, while Maven and Ant can only execute build operations.

Ant is a formal method, while Maven is a full declarative process with a lifecycle. Ant scripts cannot be reused. Maven modules, on the other hand, can be reused. Ant is an ancient technique that is now in use by legacy applications. Maven is used for the majority of new apps.

#### What is a Jenkins job?
---
A Job/Project is the fundamental unit of a logical work (like a software build, an automation task, test execution, etc) using the Jenkins automation server and other required plugins, configurations & infrastructures.

Jobs can be of different types like - a freestyle project, a multi-configuration project, a pipeline project, a multi-branch project, etc.

#### What is a Jenkins Pipeline?
---
The pipeline is a special type of Jenkins job - simply a sequence of steps controlled by a defined logic - which Orchestrates long-running activities that can span across multiple build agents. It is suitable for building pipelines (formerly known as workflows) and/or organizing complex activities that cannot be easily achieved using a freestyle job.

#### What are the types of Jenkins pipelines?
---
Jenkins Pipelines can be either - a Declarative pipeline or a Scripted Pipeline. Declarative pipeline makes use of numerous, generic, predefined build steps/stages (i.e. code snippets) to build our job according to our build/automation needs whereas, with Scripted pipelines, the steps/stages can be custom-defined & used using a groovy syntax which provides better control & fine-tuned execution levels.

#### Explain Jenkins Multibranch Pipeline?
---
It is a pipeline job that can be configured to Create a set of Pipeline projects according to the detected branches in one SCM repository. This can be used to configure pipelines for all branches of a single repository e.g. if we maintain different branches (i.e. production code branches) for different configurations like locales, currencies, countries, etc.

#### How do you store credentials in Jenkins securely?
---
Credentials can be stored securely in Jenkins using the Credentials plugin, which stores different types of credentials like - Username with a password, SSH username with the private key, AWS Credentials, Jenkins Build Token, Secret File/Text, X509 & other certificates, Vault related credentials securely with proper encryption & decryption as and when required.

#### How can we stop a scheduled job from being executed temporarily?
---
Disable the job from the job details page to temporarily stop all scheduled executions & other factors/events from triggering the job and enable it back to resume the job schedules/triggers. If a job is not required permanently, we can delete the job from the jobs list view page.

#### What are the ways to trigger a Jenkins Job/Pipeline?
---
There are many ways we can trigger a job in Jenkins. Some of the common ways are as below -

- Trigger an API (POST) request to the target job URL with the required data.
- Trigger it manually from the Jenkins web application.
- Trigger it using Jenkins CLI from the master/slave nodes.
- Time-based Scheduled Triggers like a cron job.
- Event-based Triggers like SCM Actions (Git Commit, Pull Requests), WebHooks, etc.
- Upstream/Downstream triggers by other Jenkins jobs.

#### What is Jenkins Build Cause?
---
Build Cause is a text attribute that represents what made a job's build to be triggered, say it could be a Jenkins User (from UI), Timer for Scheduled jobs, Upstream jobs for a job which was triggered by upstream job, etc. This is mainly used to identify the nature of the builds - be it nightly, manual, automated, etc.

#### How Jenkins knows when to execute a Scheduled job/pipeline and how it is triggered?
---
Jenkins master will have the cron entries set up for the jobs as per the scheduled Job's configurations. As and when the time for a particular job comes, it commands agents (based on the configuration of the job) to execute the job with required configurations.

#### What are the credential types supported by Jenkins?
---
In Jenkins, credentials are a set of information used for authentication with internal/external services to accomplish an action. Jenkins credentials are provisioned & managed by a built-in plugin called - Credentials Binding - plugin. Jenkins can handle different credentials as follows -

- Secret text - A token such as an API token, JSON token, etc.
- Username and password - Basic Authentication can be stored as a credential as well.
- Secret file - A secret file used to authenticate some secure data services & security handshakes.
- SSH Username with a private key - An SSH public/private key pair for Machine to Machine authentication.
- Certificate - a PKCS#12 certificate file and an optional password.
- Docker Host Certificate Authentication credentials.

As we can guess, this can be extended to several other extensible credential types like - AWS credential, Azure secrets, etc. using commonly available plugins.

#### What are the Scopes of Jenkins Credentials?
---
- Global - the credential will be usable across all the jobs configured in the Jenkins instance (i.e. for all jobs). This is more suited for user Jobs (i.e. for the freestyle, pipeline, or other jobs) to authenticate itself with target services/infrastructures to accomplish the purpose of the job)
- System - This is a special scope that will allow the Jenkins itself (i.e. the core Jenkins functionalities & some installed plugins) to authenticate itself to external services/infrastructures to perform some defined tasks. E.g. sending emails, etc.

#### What is a Jenkins Shared Library and how it is useful?
---
As an organization starts using more and more pipeline jobs, there is a chance for more and more code being duplicated in every pipeline job, since a part of the build/automation processes will be the same for most of the jobs. In such a situation, every other new upcoming job should also duplicate the same piece of code. To avoid duplications, the Jenkins project brought in the concept of Shared Libraries, to code - DRY - Don't Repeat Yourself.

Shared libraries are a set of code that can be common for more than one pipeline job and can be maintained separately. Such libraries improve the maintenance, modularity & readability of the pipeline code. And it also speeds up the automation for new jobs.

#### How Jenkins jobs can be Triggered/Stopped/Controlled programmatically?
---
Jenkins Remote Access API can be used to do things like -

- Retrieving information about jobs, views, nodes, builds, etc. from Jenkins for programmatic consumption.
- Trigger a build (both parameterized & non-parameterized), stop/abort a build, enable/disable a Job, group/remove jobs into/from views, etc.
- Create/copy/modify/delete jobs.

and many other programming language-specific functionalities. It has wrappers for main programming languages like - Python, Ruby & Java. It can be triggered via CURL as below -

- Jobs without parameters: Simply an HTTP POST on JENKINS_URL/job/JOBNAME/build.
- Jobs with parameters: Simple example - sending "String Parameters":

```bash
curl JENKINS_URL/job/JOB_NAME/buildWithParameters  --user USER:TOKEN --data id=123 --data verbosity=high
```

#### How to get the Jenkins version programmatically in Jobs/Pipelines or nodes other than master?
---
To check the version of Jenkins, load the top-level page or any top-level Remote Access API path like the '.../api/' page and then check for the 'X-Jenkins' response header.

This contains the version number of Jenkins, like "1.404". This is also a good way to check if an URL is a Jenkins URL.

#### What happens when a Jenkins agent is offline and what is the best practice in that situation?
---
When a job is tied to a specific agent on a specific node, the job can only be run on that agent and no other agents can fulfill the job request. If the target node is offline or all the agents on that particular node are busy building other jobs, then the triggered job has to wait until the node comes online or an agent from that node becomes available to execute the triggered build request.

As a result, a triggered job may sometimes wait indefinitely without knowing that the target node is offline. So, it is always the best practice to tie the jobs to a group of nodes & agents, referred to with a 'Label'. Once a job is tied to a Label, instead of a specific node/agent, any of the nodes/agents falling under the label can fulfill a build request, when a job is triggered. This way we can reduce the overall turn-around time of the builds.

Even then if a job is waiting for more time for the nodes/agents, then it is time to consider adding more nodes/agents.

#### What is the Blue Ocean?
---
Blue Ocean is the redefined user experience for Jenkins. Designed from the ground up for Jenkins Pipeline, it is still compatible with freestyle jobs, Blue Ocean reduces clutter and increases clarity. Blue Ocean’s main features include -

- Sophisticated visualizations of continuous delivery (CD) Pipelines, allowing for fast and intuitive comprehension of your Pipeline’s status.
- Pipeline editor - makes the creation of Pipelines approachable by guiding the user through an intuitive and visual process to create a Pipeline.
- Personalization to suit the role-based needs of each member of the team.
- Pinpoint precision when intervention is needed and/or issues arise. Blue Ocean shows where in the pipeline attention is needed, facilitating exception handling and increasing productivity.
- Native integration for branch and pull requests, enables maximum developer productivity when collaborating on code with others in GitHub, Bitbucket, etc.

#### What is the Jenkins User Content service?
---
Jenkins has a mechanism known as "User Content", where administrators can place files inside the `$JENKINS_HOME/userContent` folder and these files are served from yourhost/jenkins/userContent.

This can be thought of as a mini HTTP server to serve images, stylesheets, and other static resources that you can use from various description fields inside Jenkins.

#### How is continuous integration achieved using Jenkins?
---
Continuous integration is a process where a developer’s code changes are constantly integrated into the main code and the same will be tested automatically and the results of the tests will decide whether the change is ready for deployment. In this process -

- Developer Makes a change - commit/pull_request - in feature/dev branch
- Source Control Management system generates appropriate events
- SCM Specific Jenkins Plugins like Git/SVN will detect those events from the configured repositories and these events will be used to Trigger - build/dependent/test - jobs on Jenkins
- After the Test/Dependent jobs are completed, the change/patch will be labeled according to the status of the test job
- Based on the Status (i.e. readiness of a change to be merged with the main branch), the Continuous Delivery or Continuous Deployment strategy/tool will take it forward.

#### What is Artifact Archival & how to do it in Pipelines?
---
Artifacts are the exportable/storable/archivable results of a specific job build. This can be configured using a plugin called - Copy artifact Plugin. Based on the configured pattern, the files/directories matching the configured patterns will be archived for a Jenkins build, which can be used for future references. In the pipeline, it can be configured as follows -

archiveArtifacts artifacts: `output/**/*`

#### How to configure inclusions & exclusions in Artifacts Archival?
---
Artifact archival takes in a pattern for matching target files. Similarly, it also takes in a pattern (ANT build system pattern for matching files) for exclusion as well which will be ignored while selecting the files for archival.

For e.g. archiveArtifacts artifacts: 'output/\*.txt', excludes: 'output/specific_file.txt'

The above command will archive all the text files from the output folder except specific_file.txt

#### How can we share information between different build steps or stages in a Jenkins Job?
---
Every build step or stage will be running in its process and hence sharing information between two different build steps is not so direct. We can use either a File, a Database Entry, an Environment Variable, etc. to share info from one build step to another or a post-build action.

#### How code coverage is measured/tracked using Jenkins in a CI environment?
---
Using language-specific code coverage plugins like JaCoCo, CodeCov, etc or generic tools/plugins like Sonarqube which will add the code coverage data to builds with some minor tweaks in the code and the same can be displayed as a graph in Jenkins.

#### Default Environment Variables by Jenkins & How to introduce custom environment variables?
---
Jenkins provides several environment variables by default like - BRANCH_NAME, BUILD_NUMBER, BUILD_TAG, WORKSPACE, etc.

#### How can a job configuration be reset to an earlier version/state?
---
From the Job details page, we can use Job Config History to - See diff, Review & Revert the Job configs from the history of changes we have made to a particular job. This will be super useful when a job is misconfigured by someone by mistake, it can be reviewed and reverted easily to any of its earlier states.

#### How to do Global Tools Configuration in Jenkins?
---
Global Tools are tools that need to be installed outside the Jenkins environment and need to be controlled from within the Jenkins environment. Hence it needs its corresponding Jenkins plugin as well. Steps to using a Global Tool generally include -

- Install the tool Plugin into the Jenkins instance, to include the global tool into a list of global tools used by Jenkins.
- Install the tool in the Jenkins instance or provide away (maybe a command to download and) install the tool during runtime.
- Go to Manage Jenkins -> Global Tools Configuration and Scroll through the tool list and configure the global tool-specific configurations.
- Make use of the installed global Tool in your job/pipeline.

#### How to create & use a Shared Library in Jenkins?
---
Basic requirements for a Jenkins shared library to be used in a Pipeline Code are -

- A Repository with pipeline shared library code in SCM.
- An appropriate SCM Plugin configuration for the Jenkins instance.
- Global Shared Library should be configured in Jenkins Global configuration.
- Include the Shared Library in the Pipeline Code and use the methods defined in the Jenkins Shared Library.

#### How to install a Custom Jenkins Plugin or a Version of Plugin Not available in Jenkins Update Center?
---
Generally, it is the best practice to use the latest version of a plugin. But there are ways to install custom plugins or outdated versions of a published plugin. Jenkins Plugins are exported using a .hpi file and the same can be installed in multiple ways -

`Using the Jenkins CLI`

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ install-plugin SOURCE ... [-deploy] [-name VAL] [-restart]
```

The above command Installs a plugin either from a file, an URL or from the update center.

- SOURCE: If this points to a local file, that file will be installed. If this is an URL, Jenkins downloads the URL and installs that as a plugin. Otherwise, the name is assumed to be the short name of the plugin in the existing update center (like "findbugs") and the plugin will be installed from the update center.
- -deploy: Deploy plugins right away without postponing them until the reboot.
- -name VAL: If specified, the plugin will be installed as this short name (whereas normally the name is inferred from the source name automatically).
- -restart: Restart Jenkins upon successful installation.

`Advanced Installation - via - Web UI`

Assuming a .hpi file has been downloaded, a logged-in Jenkins administrator may upload the file from within the web UI:

- Navigate to the Manage Jenkins > Manage Plugins page in the web UI.
- Click on the Advanced tab.
- Choose the .hpi file under the Upload Plugin section.
- Upload the plugin file.
- Restart the Jenkins instance

`Advanced Installation - via - On the master`

Assuming a .hpi file has been explicitly downloaded by a systems administrator, the administrator can manually place the .hpi file in a specific location on the file system.

Copy the downloaded .hpi file into the JENKINS_HOME/plugins directory on the Jenkins controller (for example, on Debian systems JENKINS_HOME is generally /var/lib/jenkins).

The master will need to be restarted before the plugin is loaded and made available in the Jenkins environment.

#### How to download the Console log for a particular Jenkins build programmatically?
---
Using the Jenkins CLI - console - command
```bash
java -jar jenkins-cli.jar console JOB [BUILD] [-f] [-n N]
```
Produces the console output of a specific build to stdout, as if you are doing 'cat build.log'

- JOB: Name of the job
- BUILD: Build number or permalink to point to the build. Defaults to the last build
- -f: If the build is in progress, append console output as it comes, like tail -f
- -n N: Display the last N lines.

```bash
ssh -l <ssh_username> -p <port_no> <Jenkins_URL> console <JOB_NAME>
```

#### What is Jenkins Remote Access API?
---
Jenkins provides remote access API to most of its functionalities (though some functionalities are programming language-dependent). Currently, it comes in three flavors -

- XML
- JSON with JSONP support
- Python

Remote access API is offered in a REST-like style. That is, there is no single entry point for all features, and instead, they are available under the ".../api/" URL where the "..." portion is the data that it acts on.

For example, if your Jenkins installation sits at interviewbit.com, visiting /api/ will show just the top-level API features available – primarily a listing of the configured jobs for this Jenkins instance.

Or if we want to access information about a particular build, e.g. https://ci.jenkins.io/job/Infra/job/jenkins.io/job/master/lastSuccessfulBuild/, then go to https://ci.jenkins.io/job/Infra/job/jenkins.io/job/master/lastSuccessfulBuild/api/ and you’ll see the list of functionalities for that build.

#### What is In-process Script Approval and how it works?
---
Jenkins, and several plugins, allow users to execute Groovy scripts in Jenkins. To protect Jenkins from the execution of malicious scripts, these plugins execute user-provided scripts in a Groovy Sandbox that limits what internal APIs are accessible.

This protection is provided by the Script Security plugin. As soon as an unsafe method is used in any of the scripts, the "In-process Script Approval" action should appear in "Manage Jenkins" to allow Administrators to make a decision about which unsafe methods, if any, should be allowed in the Jenkins environment.

This in-process script approval inherently improves the security of the overall Jenkins ecosystem.

#### Can we monitor Jenkins using common Observability tools?
---
Common monitoring platforms like DataDog, Prometheus, JavaMelody & few others - have their corresponding Jenkins plugin, which when configured, sends Metrics to the corresponding Monitoring platform, which can then be Observed with the latest tools & technologies. The same can be configured with Alarms & Notifications for immediate attention when something goes wrong.

#### What is a Ping Thread in Jenkins and how it works?
---
Jenkins installs "ping thread" on every remote connection, such as Controller/Agent connections, regardless of its transport mechanism (such as SSH, JNLP, etc.). The lower level of the Jenkins Remoting Protocol is a message-oriented protocol, and a ping thread periodically sends a ping message that the receiving end will reply to. The ping thread measures the time it takes for the reply to arrive, and if it’s taking excessive time (currently 4 minutes and configurable), then it assumes that the connection was lost and initiates the formal close down.

This is to avoid an infinite hang, as some of the failure modes in the network cannot be detected otherwise. The timeout is also set to a long enough value so that a temporary surge in the load or a long garbage collection pause will not trip off the close-down.

Ping thread is installed on both controller & agent; each side pings the other and tries to detect the problem from their sides.

The ping thread time out is reported through java.util.logging. Besides, the controller will also report this exception in the agent launch log. Note that some agent launchers, most notably SSH agents, writes all stdout/stderr outputs from the agent JVM into this same log file, so you need to be careful.

#### How does one set up the process for a Jenkins job?
---
Jenkins manages project builds with the help of jobs. There are a few steps to setting up a job:

- Create a new object and mark it after the work.
- Press OK after selecting the freestyle project.
- Fill out the job description and specify the number of builds to keep and how long they should be kept.
- Set up the archive (Example Git). Enter the URL as well as your login credentials.
- Define your create triggers.
- You will save the work.
- Verify the job by pressing the "Build Now" button.

#### What measures are used to secure Jenkins?
---
Jenkins can be secured and global protection configured by doing the following:

- Launch Jenkins by deploying Jenkins.war to the server.
- Go to Manage Jenkins from the homepage (via URL).
- Click the "Setup Security" button on this page.
- Check the box labeled "Enable Protection."
- For security reasons, having your database is a good idea. In the "Security Realm," choose this option and check the "Allow users to sign up" checkbox.

#### What is meant by a trigger? 
---
Triggers determine where and how pipelines are operated.

- When Jenkins is combined with a source control system (SCM), such as Git, the repository can be polled whenever a commit is made.
- The Git module should be installed and configured first.
- Then you can create a trigger that tells you when a new build should start.

#### What and when is the backup plugin used? 
---
This is a handy plugin that saves all of the important settings and parameters for future use. This is particularly helpful in case of a malfunction, as it prevents the settings from being lost.

#### What does one do if one has a broken project build?
---
There are two ways to fix a faulty construct:

- Open the monitor and verify that all of the files have been taken. If any modifications are missed, make sure they are placed right.
- To debug and correct the error, replicate the problem on your local setup.

#### When working on a pipeline, the first job was successful, if the second job fails, what should one do?
---
- First we start debugging by checking in which step the second job failed.
- Compare the same step with first job
  - we can use some `diff tool` for this purpose
  - would suggest diff in Notepad++ / VS code for proprietary codebase.
- Using the `restart from level` command, we can restart the pipeline from where it failed.

## Testing
---
#### How are automated tests run on Jenkins?
---
- Tool used
  - `Selenium` or `Maven` can be used to run automated testcases that are written in Java.
  - For GoLang / Python similar frameworks can be used.
- Another option, that would work for any language, is to use `ansible` for testing.
- After prevalidation, executable build, uploading to artifactory, testing can begin.
- This way developers can schedule the test runs if needed.
- Jenkins shows the test results and gives the developers a note.
- HTML plugin can be used to display the result for better visibility.
- Also the test result and build result can be shared over Email and Slack channel.

## Conclusion
---
With these Jenkins pipeline interview questions and answers and interview questions on Jenkins for testers, you will be able to ace your interview. Though not comprehensive, it lays the groundwork for impressing recruiters with your Jenkins skills. Jenkins is indeed a real-time tool for testing and combining mostly automated builds. It keeps track of a small version of a large Java code piece, culminating in system automation, which saves users and developers time.

If you are interested in making a career in the Data Science domain, our 11-month in-person Postgraduate Certificate Diploma in Data Science course can help you immensely in becoming a successful Data Science professional.
