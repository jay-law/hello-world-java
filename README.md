# Overview

This tutorial is designed to walk users through packaging a Java application in three locations: locally, GitHub Actions (cloud), and Azure DevOps (cloud).   It's more of a working example opposed to an in-depth tutorial.

Tested with the following:
- Local machine:
    - Ubuntu 20.04.4 LTS (64-bit)
    - OpenJDK 18
    - Maven 3.8.5
- GitHub Actions:
    - Ubuntu 20.04
    - Java 17
- Azure DevOps:
    - Ubuntu 20.04
    - Java 17

**NOTE** Azure DevOps has two flavors: services and server.  Azure DevOps Server can be installed locally and replaces TFS (Team Foundation Server).  Azure DevOps Services is hosted by Microsoft in the cloud.  Any mention of Azure DevOps below is referring to Azure DevOps Services.  [See more](https://docs.microsoft.com/en-us/azure/devops/user-guide/about-azure-devops-services-tfs?view=azure-devops) 

# Prerequisites

## Technologies Used

- OpenJDK - Java library
    - Skills required - None to moderate, depending on the issues that arise
- Maven - Tool used to build the Java application 
    - Skills required - None to moderate, depending on the issues that arise
- GitHub Actions - Cloud platform used to build the Java project
    - Skills required - None to little
- Azure DevOps - Cloud platform used to build the Java project
    - Skills required - None to little

GitHub Actions and Azure DevOps are paid services that offer free "trial" solutions.  Keep an eye on the costs.

## Create Cloud Accounts

Accounts are required for GitHub Actions and Azure DevOps.  Additionally, a basic working knowledge of Git is required.

Azure DevOps is a single service in the Azure cloud ecosystem.  An Azure account is required to use the service.  

# Configure Local Env

## Clone this Repo

```bash
# Clone repo with SSH if GitHub account is configured with SSH keys
$ git clone git@github.com:jay-law/hello-world-java.git

# or
# Clone repo with HTTPS
$ git clone https://github.com/jay-law/hello-world-java.git

# cd into the repo directory
$ cd hello-world-java/
```

## Install OpenJDK

The JDK (Java Development Kit) is required to build Java apps.  [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK) is a free and open-source implementation of the Java Platform.

Official documentation for installing - https://openjdk.java.net/install/

```bash
# Partial output is included below

# Create jvm dir
$ sudo mkdir /usr/lib/jvm
$ cd /usr/lib/jvm

# Download.  Here jdk 18 (not 1.8) is used.  Probably better to use 17 as it
# has more support
$ sudo wget https://download.java.net/openjdk/jdk18/ri/openjdk-18+36_linux-x64_bin.tar.gz

# Untar
$ sudo tar -xvzf openjdk-18+36_linux-x64_bin.tar.gz

# Update env vars
$ echo "export JAVA_HOME=/usr/lib/jvm/jdk-18" >> ~/.profile
$ echo "export PATH=\"$PATH:/usr/lib/jvm/jdk-18/bin\"" >> ~/.profile

# Update bash session
$ source ~/.profile

# Confirm install
$ java -version

openjdk version "18" 2022-03-22
...
```

## Install Maven

Maven is the build tool that can be used for Java.

Official documentation for installing - https://maven.apache.org/install.html

```bash
# Partial output is included below

# Create maven dir
$ sudo mkdir /opt/maven
$ cd /opt/maven

# Download
$ sudo wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz

# Untar
$ sudo tar -xvzf apache-maven-3.8.5-bin.tar.gz

# Update env vars
$ echo "export M2_HOME=/opt/maven/apache-maven-3.8.5" >> ~/.profile
$ echo "export PATH=\"$PATH:/opt/maven/apache-maven-3.8.5/bin\"" >> ~/.profile

# Update bash session
$ source ~/.profile

# Confirm install
$ mvn -version

Apache Maven 3.8.5 (3599d3414f046de2324203b78ddcf9b5e4388aa0)
...
```

<details>

<summary>Getting the example project to its current state</summary>

This collapsible section contains the steps taken to get the project to its current state.  I wanted to keep the info but it's not required as part of the tutorial.

The official documentation [getting started guide](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) was used to create/download the example project.

```bash
# Create/download the example project
$ mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

Per the instructions, a java project will be created automatically in a directory called `my-app`.  I renamed the directory to `hello-world-java` so it can be pushed to my GitHub repo.  The following updates were made in the `pom.xml` file:
- Change the `artifactId` value to `hello-world-java`
- Change the `name` value to `hello-world-java`
- Change the `maven.compiler.target` value to `17` (or whatever java version is installed locally)
- Change the `maven.compiler.target` value to `17` (or whatever java version is installed locally)

</details>

## Execute

Still following the instructions from earlier, validate and package the project locally.

```bash
# Output is included below

# Validate
$ mvn validate

[INFO] Scanning for projects...
[INFO] 
[INFO] -----------------< com.mycompany.app:hello-world-java >-----------------
[INFO] Building hello-world-java 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.044 s
[INFO] Finished at: 2022-03-16T14:53:17-04:00
[INFO] ------------------------------------------------------------------------

# Package - This will run tests and build
$ mvn package

[INFO] Scanning for projects...
[INFO] 
[INFO] -----------------< com.mycompany.app:hello-world-java >-----------------
[INFO] Building hello-world-java 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
...
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.110 s
[INFO] Finished at: 2022-03-16T14:53:45-04:00
[INFO] ------------------------------------------------------------------------


# Test the app works
$ java -cp target/hello-world-java-1.0-SNAPSHOT.jar com.mycompany.app.App

Hello World!
```

# Package in the Cloud



```bash

```