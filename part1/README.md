# Part 1: Set up development environment, generate events and push to Kafka

## Software Prerequisites 

Please make sure you have the following installed on your machine. Install them in the same order as listed here if you 
don't.

  * [Oracle JDK Standard Edition 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
  * [Apache Maven 3.2+](https://maven.apache.org/download.cgi)
  * [Git](https://git-scm.com/downloads)
  * [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://eclipse.org/downloads/) or [Netbeans](https://netbeans.org/downloads/)
  
> IntelliJ IDEA is preferred but any IDE will work as the labs use Maven. IntelliJ Community edition is free. 

## Environment Setup

### Installing Hadoop Mini Clusters
 
This master class uses Shane Kumpf's [Hadoop Mini Clusters](https://github.com/sakserv/hadoop-mini-clusters) to start Kafka, Storm, etc. in a local mode. I've 
uploaded a slightly changed version of Shane's Mini Clusters project on my Github [repository](https://github
.com/DhruvKumar/hadoop-mini-clusters.git) to get around some Maven Shade plugin issues.
 
You'll need to get a copy of it first and install the jar locally before doing anything else. 

If you're on a Mac or Linux, open the terminal and do the following to download and install the mini clusters from my
 repository:

```bash
$ git clone https://github.com/DhruvKumar/hadoop-mini-clusters.git
$ cd hadoop-mini-clusters
$ mvn clean install -DskipTests
```

If you're using Windows:

1. Download the Hadoop Mini Clusters project using _one_ of the following methods:
 * Use the Git client and clone the project from https://github.com/DhruvKumar/hadoop-mini-clusters.git
 * Or, download the project as a zipped file from [this link.](https://github
 .com/DhruvKumar/hadoop-mini-clusters/archive/master.zip). Unzip the folder and note the location.
2. Open the command prompt from Start menu, or run `cmd` to get to it.
3. Navigate to the directory in Command Terminal where you have cloned or downloaded the mini clusters.
4. Type: `mvn clean install -DskipTests`. 

> **Note** From now on, I'll assume you're working on a Mac or Linux. In Windows, the maven 
commands will be the same, but system commands like changing directory will be different.

This should install `hadoop-mini-clusters-0.0.15-SNAPSHOT.jar` in your local Maven repository. You can check if its 
correctly installed on Mac OS X and Linux by checking the local `.m2` folder like this:

```bash
$ ls -alh ~/.m2/repository/com/github/sakserv/hadoop-mini-clusters/0.0.15-SNAPSHOT/
total 261776
drwxr-xr-x  9 dkumar  staff   306B Oct 11 10:24 .
drwxr-xr-x  8 dkumar  staff   272B Sep 27 11:42 ..
-rw-r--r--  1 dkumar  staff   321B Sep 27 11:42 _remote.repositories
-rw-r--r--  1 dkumar  staff   256K Sep 27 11:42 hadoop-mini-clusters-0.0.15-SNAPSHOT-javadoc.jar
-rw-r--r--  1 dkumar  staff    20M Sep 27 11:42 hadoop-mini-clusters-0.0.15-SNAPSHOT-sources.jar
-rw-r--r--  1 dkumar  staff   108M Sep 27 11:42 hadoop-mini-clusters-0.0.15-SNAPSHOT.jar
-rw-r--r--  1 dkumar  staff    10K Sep 27 11:42 hadoop-mini-clusters-0.0.15-SNAPSHOT.pom
-rw-r--r--  1 dkumar  staff   1.1K Sep 27 11:42 maven-metadata-local.xml
-rw-r--r--  1 dkumar  staff   355B Oct 11 10:24 resolver-status.properties
```

In Windows, the `m2` folder is usually present at `c:\Users\<username>\.m2`. Navigate to it, and check if the jar is 
present under the `repository\com\github\sakserv\hadoop-mini-clusters\0.0.15-SNAPSHOT\` folder.

> **Important** Make sure that the `0.0.15-SNAPSHOT` version is installed. The SNAPSHOT suffix is very important as it 
differentiates this copy from the original project.
 
### Downloading the Master Class Labs

Now that the Hadoop Mini Clusters project is installed, let's download the masterclass and its labs: 

```bash
$ git clone https://github.com/DhruvKumar/iot-masterclass.git
```

Windows users should download via the Git client or directly as a [Zipped folder](https://github
.com/DhruvKumar/iot-masterclass/archive/master.zip).
 

### Setting up the IDE

Next, let's bring the masterclass labs into our IDE. There are two broad ways to do this:

1. Recommended: Manually import as a Maven project into the IDE.
2. Generate IDE specific project file using Maven, and open the project file.

#### Approach 1: Maven import into IDE

This is recommended. Just open up your IDE, and create a new project/workspace/module etc from the masteclass root 
pom.xml file. This will bring all the parts and the labs into your IDE.

#### Approach 2: Generate IDE specific project files

Alternatively, you can generate Intellij IDEA or Eclipse specific project file using Maven and open them up from IDEA
 or Eclipse. Here's how you can do it for IntelliJ:
 
```bash
$ cd iot-masterclass
$ mvn idea:project
```
This will generate a new `iot-masterclass.ipr` file which can be opened by IntelliJ. You can also open it directly 
from the command line in IntelliJ:

```
$ open iot-masterclass.ipr
```

> If IntelliJ prompts in a notification pop up to treat the pom.xml as a maven project, click on yes.

Similarly, you can generate Eclipse project files by doing:

```bash
$ cd iot-masterclass
$ mvn eclipse:eclipse
```

Here's how the master class looks like in my IntelliJ after importing:

![Project Structure in IDE](/images/part1/projectSetup.png)

For more details, see IDEA [plugin](https://maven.apache.org/plugins/maven-idea-plugin/) and Eclipse [plugin](https://maven.apache.org/plugins/maven-eclipse-plugin/) 
documentation.



