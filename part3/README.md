# Part 3: Write a Storm Bolt to track event characteristics and raise alerts according to some policy

In this section we introduce business logic into our storm toplogy and do some event processing. Event processors in 
Storm are called Bolts. Each Bolt has an `execute(Tuple input)` method which Storm invokes on each input event. 
Some processing logic needs to be present in this method for a storm topology to do more than just event movement.

**Lab Task**: You need to finish writing the `part3.com.hortonworks.lab.TruckEventRuleBolt`, by implement the 
`execute` method. Keep a track of number of violations per driver using:

```java
public Map<Integer, LinkedList<String>> driverEvents = new HashMap<Integer, LinkedList<String>>();
```

Next, finish writing the execute method:

```java
@Override
  public void execute(Tuple input) {
    int driverId = input.getIntegerByField("driverId");
    String driverName = input.getStringByField("driverName");
    int routeId = input.getIntegerByField("routeId");
    String routeName = input.getStringByField("routeName");
    int truckId = input.getIntegerByField("truckId");
    Timestamp eventTime = (Timestamp) input.getValueByField("eventTime");
    String eventType = input.getStringByField("eventType");
    double longitude = input.getDoubleByField("longitude");
    double latitude = input.getDoubleByField("latitude");
    long correlationId = input.getLongByField("correlationId");


    LOG.info("Processing truck event[" + eventType + "]  for driverId[" + driverId + "], truck[" + truckId + "], " +
        "route[" + routeName + "], correlationId[" + correlationId + "]");
    processEvent(driverId, driverName, routeId, truckId, eventTime, eventType, longitude, latitude,
        correlationId, routeName);
    collector.ack(input);
  }


  public void processEvent(int driverId, String driverName, int routeId, int truckId, Timestamp eventTime, String
      event, double longitude, double latitude, long currentCorrelationId, String routeName) {

    // Lab: implement me to raise an alert if the num violations have exceeded MAX_UNSAFE_EVENT value
  }
```
To verify if your answer is correct, run the Lab class provided in the solutions directory. This completes part
 3. In the next part, we will use a Spark model in our bolt to predict future events.