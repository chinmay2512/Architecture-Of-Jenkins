# WHAT IS JENKINS ?
 - Jenkins is easy to use `open source` `java based` `CI/CD (Continuous Integration and Continuous Delivery/Deployment)` tool.
 - It has been around for some time, and several organizations use it for their CI/CD needs.
 - It is written in `Java` and provides a user-friendly web interface for managing and automating various tasks related to `building`, `testing`, and `deploying software`.

# JENKINS COMMONLY USED FOR THE FOLLOWING :
- `Continous Integration` for application and `Infrastructure Code`.
- `Continuously Delivery` of pipeline to deploy the application to diiffrent environments using `Jenkins Pipeline As Code`.
- Infrastructure component `Deploy and Management`.
- Run batch operations using `Jenkins Jobs`.
- Run ad-hoc operations like `backups`,`cleanups`,`remote script execution`,`event triggers`, etc.

# JENKINS ARCHITECTURE :

 - **The following diagram shows the overall architecture of Jenkins:**

  <img src="https://devopscube.com/wp-content/uploads/2020/03/jenkins-architecture.png"/>

- **Following are the key components in Jenkins**
   *  `Jenkins Master Node`
   *  `Jenkins Agent Nodes/Clouds`
   *  `Jenkins Web Interface`

## **Let's Looks At Each Components In Details :**

### **Jenkins Master (Server) :**
- Jenkins server or master node holds all key configuration.
- Jenkins master server is like a control server that orchestrates all the workflow defined in the pipeline.
- For example : `Scheduling A Job`, `Monitoring A Jobs`, etc.

## **Let’s Have A Look At The Key Jenkins Master Components :**

# Jenkins Jobs :
- A jobs is a collection of steps that you can use to build your source, test your code, run a shell scripts, run an Ansible role in a remote host or execute a terraform play, etc.
- We normally call it a `Jenkins Pipeline`.


<img src="https://devopscube.com/wp-content/uploads/2021/08/image-27.png"/>


## If you translate the above steps to a Jenkins pipeline job, it looks like the following :
```
pipeline{
    agent any
    stages{
        stage('hello'){
            steps{
                echo 'Hello World'
            }
        }
    }        
}
```

# Jenkins Plugins :
- Plugins are community-developed modules that you can install on your jenkins server.
- It helps you eith more functionalities that are not natively available in **Jenkins**.
- For example: If you want to upload a file to `S3 Bucket` from `Jenkins`, you can install an `AWS Jenkins Plugin` and use abstracted plugin functionalities to upload file rather than writing your own logic in `AWS CLI`.
- The plugin take care of error and exception handling.
- You can install/upgrade all the available plugins from the Jenkins dashbaord itselft.
- For corporate network, you will have to setup a proxy details to connect to the plugin repository.
- You can also download the plugin file and install it by copying it to the plugins directory under `/var/lib/jenkins` folder.
- You can also develop your custom plugins. Check out all plugins from the `Jenkins Plugin Index`.

# Jenkins Global Security :

- Jenkins has the following type of primary authentication methods :

- ## Jenkins Own User's Database :-

  - Set of users maintained by Jenkin's own database.
  - When we say database, its all flat config files (XML files).

- ## LDAP (Lightweight Directory Access Protocol) Integration :-
  - Integrating LDAP (Lightweight Directory Access Protocol) authentication with Jenkins allows you to leverage your existing directory service for user authentication and authorization.
  - Jenkins authentication using corporate LDAP configuration.
  - Once LDAP integration is set up, users will be able to log in to Jenkins using their LDAP credentials, and their permissions will be based on the LDAP groups they belong to.

- ## SAML (Security Assertion Markup Language) Single Sign On(SSO) :-
  - Support single signon using providers like Okta, AzureAD, Auth0 etc..
  - With Jenkins matric-based security you can further assign roles to users on what permission they will have on Jenkins.

# Jenkins Credentials :

* When you set up Jenkins pipelines, there are scenarios where it needs to connect to a cloud account, a server, a database, or an API endpoint using secrets.

  - In Jenkins, you can save different types of secrets as a credential.

    * Secret Text :
      * In Jenkins, you can manage sensitive information such as passwords, API keys, and other credentials using the built-in Credentials Plugin.
      * This plugin allows you to securely store and manage credentials within Jenkins, making them accessible to jobs and pipelines without exposing them in plaintext.
    * Username & Password :
      * This is a basic type of credential used for storing an `Username` and it's associated `Password`.
      * It's commonly used for authenticating with systems such as `Databases`, `Version Control Systems`, `APIs(Application Programming Interface)`.
    * SSH Keys :
      * This credential type is used for storing `SSH Private Key` along with an optional passphrase.
      * It's commonly used for authenticating with remote servers or Git repositories over `SSH`.
 

 * All credential are encrypted (AES-Advanced Encryption Standard). The secrets are stored in `JENKINS_HOME/secrets` directory. It is very important to secure this directory and exclude it from Jenkins backups.

 # Jenkins Nodes/Clouds :

 * You can configure multiple agents nodes `(Linux/Windows)` or `Clouds (Docker, Kubernetes)` for existing Jenkins jobs.
    
### - Nodes :
 * Nodes in Jenkins are individual machines (Physical or Virtual) that Jenkins used to execute build jobs.

**Various Types Of Nodes :**
- Master Node:-
    * This is central Jenkins server that manages the overall system and coordinates the workload distribution among the nodes.
- Slave Node(or Agent):-
    * This are the worker machines that perform the actual build tasks.
    * Jenkins can have multiple slaves nodes, which can be different operating systems or configuration.
    * They connect to the master node to receive instructions on what jobs to run.
- Permanent Agent:-
    * A permanent agent is a slave node that is configured to be always online and available for running jobs.
    * It is suitable for long-running or frequent tasks.
- Cloud Agent:-
    * Cloud agent are slave nodes that are provisioned dynamically from cloud infrastructure (Sucj as AWS, Azure, Google Cloud) as needed.
    * Jenkins can automatically spin up these agents when thereis a demand for more capacity and tear them down when they are no longer required.

### - Clouds :
 * In Jenkins, clouds refer to the integration of Jenkins with cloud computing platforms to dynamically provision and manage computing resources. Clouds enable Jenkins to scale its capacity by leveraging resources from cloud provider.

**Here's How It Typically Works:**
- Cloud Plugin:-
    * Jenkins provides plugins that allow integration with various cloud providers (e.g. `Amazon EC2`, `Google Compute Engine`, `Microsoft Azure`).
    * These plugins enable Jenkins to communicate with the cloud provider's API to provision and manage vitual  machine as a Jenkins node. 
- Templates:-
    * Cloud plugins usually allow you to define templates for virtual machine instaces, speccifying attributes such as operating system, harware configuration, software environment, etc. 
- Scaling:-
    * Jenkins autonatically spin up additonal cloud agentwhen th workload increases and terminate them when they are no longer needed.
    * This helps efficiently utilizing resources and reducing costs.
- Configuration:-
    * Adminstrators configure cloud setting in Jenkins, specifying details such as cloud provider credentials, region, instance types, and other parameters neccesary for provisioning nodes dynamically.

# Jenkins Global Settings (Configure System)
  * Under Jenkins global configuration, you have all the configuaration of all installed plugins and native `Jenkins Global Configuration`.
  * Also, you can configyre global environment variables under this section.
  * For.Example: You can store the tools `(Nexus,Sonarqube,etc)` URLs as global environment variables and use them in hte pipeline.
  * This way it is easier to make URL changes that get reflected in all the `Jenkins Jobs`.

# Jenkins Logs:

* Provides logging information on all Jenkins server actions including jobs logs, plugin logs, webhook logs, etc.

 - Jenkins Master Logs:-
    * These logs contain information about the Jenkins master node itself, including startup messages, HTTP requests, plugin loading, and other system-level activities.
    * You can find these logs in the Jenkins home directory under the logs subdirectory. Common files include `jenkins.log`, `access_log`, and `error_log`.
 - Job Build Logs:
    * Each build of a Jenkins job generates its own log.
    * hese logs capture the output of the build process, including console output, error messages, warnings, and any other information printed during the execution of build steps.
    * ou can access these logs from the Jenkins web interface by navigating to the specific build of a job and clicking on the `Console Output` link.
 - Plugin Logs:-
    * Jenkins plugins may generate their own logs to provide additional information about their behavior or any errors encountered.
    * Plugin logs are typically stored alongside the Jenkins master logs and can be helpful for diagnosing issues related to specific plugins.
 - Agent/Slave Logs:-
    * If you're using Jenkins agents (also known as slaves) to execute build jobs, these agents will have their own logs that capture information about the execution of build jobs on those agents.
    * These logs are usually located on the agent machine itself and can vary depending on the agent configuration.
 - System Logs:-  
    * Depending on the operating system and Jenkins deployment setup, `system-level logs` `(e.g., syslog on Unix-based systems, Event Viewer on Windows)` may also contain relevant information about Jenkins-related activities, such as service startup/shutdown events, resource utilization, and system errors.

# Jenkins Agent:-
  <img src="https://devopscube.com/wp-content/uploads/2021/08/image-25.png"/>

 - Jenkins agents are the worker nodes that actually execute all the steps mentioned in a Job.
 - When you create a Jenkins job, you have to assign an agent to it. Every agent has a `label` as a `unique identifier`.
 - When you trigger a Jenkins job from the `Master`, the actual execution happens on the `agent node` that is configured in the job.
 - You can run jobs in the `Jenkins server` without a `Jenkins agent`.
 - In this case, `master nodes` acts as the `agent`.
 - You can have any number of Jenkins agents attached to a master with a combination of `Windows`, `Linux servers`, and even containers as build agents.
 - Also, you can restrict jobs to run on specific agents, depending on the use case.
 - For example: if you have an agent with `java 8` configurations, you can assign this agent for jobs that require `Java 8 environment`.

- Here are some key points about Jenkins agents:
  * `Execution Environment`
  * `Job Execution`
  * `Connectivity`
  * `Dynamic Provisioning`
  * `Customization`
  * `Monitoring and Management`

# Jenkins Master-agent Connectivity:-
  
  **- You can connect a `Jenkins Master` and agent in two ways:**

   - **Using the SSH method:**
      - Uses the ssh protocol to connect to the agent.
      - The connection gets initiated from the Jenkins master.
      - Their should be connectivity over port 22 between master and agent. 
   - **Using the JNLP method:**
      - Uses java JNLP protocol `(Java Network Launch Protocol)`.
      - In this method, a java agent gets initiated from the agent with Jenkins master details.
      - For this, the master nodes firewall should allow connectivity on specified JNLP port.
      - Typically the port assigned will be `50000`. This value is `configurable`.

  **- There are two types of `Jenkins Agents`:**
   
   - **Agent Nodes:-**
      - These are servers (Windows/Linux) that will be configured as static agents.
      - These agents will be up and running all the time and stay connected to the Jenkins server.
      - Organizations use custom scripts to shut down and restart the agents when is not used.
   - **Agent Clouds:-**
      - Jenkins Cloud agent is a concept of having dynamic agents.
      - Means, whenever you trigger a job, a agent gets deployed as a VM/container on demand and gets deleted once the job is completed.   
      - This method saves money in terms of infra cost when you have a huge Jenkins ecosystem and continuous builds.
  

  **Following image shows a high-level view of different types of agents and connectivity types.**

  <img src="https://devopscube.com/wp-content/uploads/2021/08/image-30.png" width="550" height="550" alt="https://devopscube.com/wp-content/uploads/2021/08/image-30.png"/>

# Jenkins Data:-

 * All the Jenkins data gets stored in the following folder location `/var/lib/jenkins/`.
 * Data includes all jobs `config files`, `plugins configs`, `secrets`, `node information`, etc. It makes Jenkins migration very easy as compared to other tools.
 * If you take a jook at `/var/lib/jenkins/` you will find most of the configurations in `xml format`.
 * It is essential to `back up` the Jenkins data folder every day. For some reason, if your Jenkins server data gets corrupt, you can restore the whole Jenkins with the `data backup`.
 * Ideally, when deploying Jenkins in production, a dedicated `extra volume` is attached to the `Jenkins servers` that hold all the `Jenkins data`.

- Here's a breakdown of some key types of data in Jenkins:
  * `Configuration Data`
  * `Job Data`
  * `Build Data`
  * `User Data`
  * `Node/Agent Data`
  * `Plugin Data`
  * `Logs`

<img src="https://devopscube.com/wp-content/uploads/2021/08/image-28-760x517.png"/>
