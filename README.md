# Overview

This tutorial is designed to walk users through packaging a Java application in three locations: locally, GitHub Actions (cloud), and Azure DevOps (cloud).   It's more of a working example opposed to an in-depth tutorial.

Tested with the following:
- Local machine:
    - Ubuntu 20.04.4 LTS (64-bit)
    - OpenJDK 18
    - Maven 3.8.5
- GitHub Actions:
    - Ubuntu xxx
    - Java 17
- Azure DevOps:
    - Ubuntu xxx
    - Java 17

# Configure Local Env

## Install OpenJDK

```bash
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
```

## Install Maven

Official documentation - https://maven.apache.org/install.html

```bash
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
```

## Create Project

Following instructions here - https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

```bash
$ mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

Per the instructions, a java project will be created automatically in a directory called `my-app`.  I renamed the directory to `hello-world-java` so it can be pushed to my GitHub repo.  The following updates were made in the `pom.xml` file:
- Change the `artifactId` value to `hello-world-java`
- Change the `name` value to `hello-world-java`
- Change the `maven.compiler.target` value to `17` (or whatever java version is installed locally)
- Change the `maven.compiler.target` value to `17` (or whatever java version is installed locally)

# Execute

Still following the instructions from earlier, validate and package the project locally.

```bash

# Validate
$ mvn validate

# Package - This will run tests and build
$ mvn package

# Test the app works
$ java -cp target/hello-world-java-1.0-SNAPSHOT.jar com.mycompany.app.App
```
