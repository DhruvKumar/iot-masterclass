# Part 4: Write a Storm Bolt to apply a Spark ML model to each event and predict alerts

So far we have been operating in a very reactive manner. We have observed each event passing through and have used 
some heuristic to raise alerts. What if we could predict the chance of violation occuring before it happens? That's 
the goal of part 4.

## Using Spark ML with Storm

To build predictive intelligence into any application, you need to use machine learning to compute a model and then 
apply it to during run time. Here we follow a similar approach. We have built a regression model using Spark ML 
offline. This model can predict whether a driver is going to cause violation or not based on weather conditions at 
the event's location and driver fatigue. The `timesheet.csv` and `drivers.csv` files contain information about how 
many hours driver has worked in a week. We simulate weather conditions and assign foggy, rainy or windy conditions 
randomly to each event. Since the `MobileEyeEvent` emitted by the sensors doesn't contain weather or driver fatigue 
data, we will use the `timesheet.csv` and `drivers.csv` files to enrich the event at run time and then apply the 
model for prediction. Note that in a production system, the human resource and wage data will likely come from a 
relational store or HBase. 

Once the event is enriched, we ask the model to evaluate the event. The model is loaded into the Storm bolt by 
reading in a JPMML file. PMML or [Predictive Model Markup Language](https://en.wikipedia
.org/wiki/Predictive_Model_Markup_Language) is a XML format for representing trained models. With PMML, you can train
 the model using one tool, export the model as a PMML file and read it in any PMML supported Framework. The PHHML 
 file for this lab is located in the resources folder and is called `predictionModel-PMML.xml`. It was generated 
 by Spark after building the model. We'll use that to  predict violation likelihood. 

There are two labs in this part, and both help you to incrementally build part4.com.hortonworks.lab
.SparkPredictionBolt class:

  * **Lab Task 1**: First, you need to populate the in-memory cache which is simulating a SQL store or HBase:

  ```java
    // in - memory data structures to simulate event enrichment - you'll populate them with Lab Exercise 1
    // normally this info will be loaded in Hive or Hbase from existing ERP and CRM systems
    private static final Map<Integer, _driverRow> driverTable = new HashMap<>();
    private static final Map<Integer, Map<Integer, _weekData>> timesheetTable = new HashMap<>();
  ```
  For doing this, implement the `buildDriverRecords()` method:
  
  ```java
  private void buildDriverRecords() {
      /*
        Lab Exercise 1: Using CSVParser, parse the timesheet.csv and drivers.csv and populate the driverTable and
        timesheetTable maps
       */
  
    }
  ```
  * **Lab Task 2** Apply the JPMML model in the bolt by implementing the `execute()` method:
  
  ```java
  @Override
    public void execute(Tuple input) {
      /*
        Lab Exercise 2:
  
        For each "normal" event passed in, write code to do the following in order:
  
        1) enrich the event by adding certification status, wage plan, hrs driven, miles driven and weather data
        2) call the evaluateJPMMLModel and get the prediction for the enriched event.
        3) emit the prediction + enriched event. See the declareOutputFields() method
        implementation to understand the fields to be emitted.
        4) log each outgoing event with prediction info and other details
  
        Here's code scaffolding to help you get started
       */
  
      String eventType = input.getStringByField("eventType");
      boolean violationPredicted;
      if (eventType.equals("Normal")) {
        // enrich event by calling enrichEvent(Tuple input)
        // run the enriched input through the model and predict violation
        // emit the event:
        // collector.emit( /* what goes here? */  );
        // do logging:
        // LOG.info(prediction + " predicted for " + driverName + " along route " + routeName);
      }
    }
    ```
    
    Compare your solution with the finished bolt in the solutions folder for acccuracy. This completes part 4.

