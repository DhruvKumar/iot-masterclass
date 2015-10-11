# Internet of Any Thing Masterclass

## Introduction 

Welcome to the IoAT Masterclass. Using the labs in this repository, you'll learn how to build a real time event 
processing application on the Hortonworks Data Platform (HDP) with tools like Spark, Storm, Kafka, Akka, Hbase, and 
Hive. 
There are multiple parts to this master class which build on each other.
By following the parts in sequence, you'll construct an app which does the following in local mode:

|Part|Goals|Tools|
| ---- | --- | --- |
| 1 | Set up dev. environment, start Zookeeper and Kafka in local mode. Simulate event generation using Akka, push to 
a Kafka producer. | Kafka, Zookeeper, Akka | 
| 2 | Start Storm in local mode, connect Kafka to Storm. Execute simple storm topology with a Kafka event spout | 
Kafka, Storm | 
| 3 | Write a Storm Bolt to track event characteristics and raise alerts according to some policy | Storm |
| 4 | Write a Storm Bolt to apply a Spark ML model to each event and predict future alerts | Spark, 
Storm, JPMML |

At the end of part 4, you should have a very good understanding of how to construct a production IoAT app using HDP, 
similar to the one showed in Hadoop Summit 2015:
 
<a href="http://www.youtube.com/watch?feature=player_embedded&v=FHMMcMYhmNI&t=1h30m2s
" target="_blank"><img src="http://img.youtube.com/vi/FHMMcMYhmNI/0.jpg" 
alt="Hadoop Summit 2015" width="240" height="180" border="10" /></a>

## Structure 

Each part is contained in its own folder. So, part 1 is in folder part1, part 2 is in folder part2 and so on. These 
folders contain two directories - lab and solution. In the `lab` folder, you'll find pre-written code with some 
missing parts. You'll need to fill in the missing parts by understanding the API in order to finish the lab. 
Solutions are present in the `solutions` directory for you to verify your code's correctness. 
As you can see from the table above, different tools are used in different labs, so you'll learn different APIs in a 
gradual manner. 

## Target Audience

Software Engineers, Developers, Architects with 3 to 5 years of Java and 1 year Hadoop programming experience using 
core APIs. 

## Software and Hardware Requirements

JDK 6+, Maven 3.2.x, IntelliJ IDEA or Eclipse. Mac OS X, Windows, and Linux are supported. At least 4GB RAM is 
recommended.  

## Next

Go to part1 to learn how to start the dev environment.


