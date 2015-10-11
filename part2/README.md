# Part 1: Set up development environment, generate events and push to Kafka.
 
This master class uses Shane Kumpf's Hadoop Mini Clusters to start Kafka, Storm, etc. in a local mode. I've uploaded 
a slightly changed version of the mini clusters on my Github repository. You'll need to get that first and install 
locally before doing anything.

```bash
$ git clone https://github.com/DhruvKumar/hadoop-mini-clusters.git
$ cd hadoop-mini-clusters
$ mvn clean install -DskipTests
```

This should install `hadoop-mini-clusters-0.0.15-SNAPSHOT.jar` in your local repository. You can check if it's 
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


