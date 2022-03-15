# hello-world-java

# Configure Local Env

## Install OpenJDK

```bash
# Create jvm dir
$ sudo mkdir /usr/lib/jvm
$ cd /usr/lib/jvm

# Download
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

## Pom (pom.xml) Changes

`<artifactId>my-app</artifactId>` to `  <artifactId>hello-world-java</artifactId>`
`<name>my-app</name>` to `  <name>hello-world-java</name>`


# Package

```bash

$ mvn clean

$ mvn validate

$ mvn package

$ java -cp target/hello-world-java-1.0-SNAPSHOT.jar com.mycompany.app.App

```

