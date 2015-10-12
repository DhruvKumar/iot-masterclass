# Part 2: Connect Kafka to Storm. Execute simple storm topology with a Kafka event spout.

In this part we will take the events received by `KafkaSensorEventsCollector` and push them into a Kafka Spout. This 
lab will show you how to connect Kafka with Storm. We will also deploy a simple storm topology on the cluster 
containing just the Kafka Spout.

## Understanding Storm Schemes

Storm uses the Tuple model for processing data. Each event passing in Storm is a Tuple of specific fields. The fields
 and names make up a Scheme object. We will use the `com.hortonworks.stormprocessors.kafka.TruckScheme2` class to 
 wrap each Kafka producer message into a scheme which Storm can use to deserialize. Here's the code in the 
 `TruckScheme2` class which does that:
  
  ```java
  @Override
    public List<Object> deserialize(byte[] bytes) {
      try {
        String truckEvent = new String(bytes, "UTF-8");
        String[] pieces = truckEvent.split("\\|");
  
        Timestamp eventTime = Timestamp.valueOf(pieces[0]);
        int truckId = Integer.valueOf(pieces[1]);
        int driverId = Integer.valueOf(pieces[2]);
        String driverName = pieces[3];
        int routeId = Integer.valueOf(pieces[4]);
        String routeName = pieces[5];
        String eventType = pieces[6];
        double latitude = Double.valueOf(pieces[7]);
        double longitude = Double.valueOf(pieces[8]);
        long correlationId = Long.valueOf(pieces[9]);
        String eventKey = consructKey(driverId, truckId, eventTime);
  
        LOG.debug("Creating a Truck Scheme with driverId[" + driverId + "], driverName[" + driverName + "], routeId[" +
            routeId + "], routeName[" + routeName + "], truckEvent[" + truckEvent + "], and correlationId[" +
            correlationId + "]");
        return new Values(driverId, truckId, eventTime, eventType, longitude, latitude, eventKey, correlationId,
            driverName, routeId, routeName);
  
      } catch (UnsupportedEncodingException e) {
        throw new RuntimeException(e);
      }
  
    }
  ```
  
  The names of the fields are declared by getOutputFields() method:
  
  ```java
    @Override
    public Fields getOutputFields() {
      return new Fields("driverId", "truckId", "eventTime", "eventType", "longitude", "latitude", "eventKey",
          "correlationId", "driverName", "routeId", "routeName");
  
    }
  ```
  
## Lab

* **Task :** You'll need to fill out the missing code in the `part2.com.hortonworks.lab.Lab` class to wrap the event 
into a compatible Kafka Spout object:
 
 ```java
    //1. instantiate SpoutConfig object with topic as "truck_events", zkRoot as "/", and consumerGroupId as "group1"
     SpoutConfig spoutConfig = null; // implement me
 
     //  2. set scheme as TruckScheme2 on spoutConfig object
     spoutConfig.scheme = new SchemeAsMultiScheme(new TruckScheme2());
 
     //  3. instantiate KafkaSpout using spoutConfig
     KafkaSpout kafkaSpout = new KafkaSpout(spoutConfig);
 
     int spoutCount = 1; // number of kafka spouts
 
     // 4. build basic storm topology with kafkaSpout as the only spout, and no bolts for processing
     TopologyBuilder builder = new TopologyBuilder();
     builder.setSpout("kafkaSpout", kafkaSpout, spoutCount);
     StormTopology topology = builder.createTopology();
 
     // 5. submit to local cluster for execution
     stormLocalCluster.submitTopology("part2: Truck events to Kafka", stormLocalCluster.getStormConf(), topology);
  ```
  
To verify if your answer is correct, look into the Lab class provided in the solutions directory. This completes part
 2. In the next part, we will construct a simple storm bolt to raise alerts.
 
