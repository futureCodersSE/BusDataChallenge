# Bus emissions challenge 
---

## Introduction

Kent and Medway have the highest proportion of old buses in the country (~40% of fleet). Old buses are detrimental to the environment as the older buses only have Euro III emissions standards which if used for lots of 
journeys will be dramatically impacting the air quality of the area. 

The client therefore would like us to find out some information which could then be used as evidence to make a case  to improve the bus emissions in the Kent and Medway area.

The datasets we will be using are pubically available. Gov.uk provides data on all bus journeys in the UK and when used in conjunction with Arriva buses fleet emissions data (available from bustimes.org, download [here](https://drive.google.com/uc?export=download&id=1ywtiSwR27JYCC5Sf9G1ZCTOTWNxWBk9_ )) we can build a pretty good 
picture of how many of these old buses are being used for bus journeys in Kent and Medway.

The gov.uk bus data is available in XML format via an api. The data refreshes every 10 seconds so each time you download it, it will show you a snapshot of the buses currently in operation at that time. We have downloaded one snapshot of this 
data and converted it to JSON format accessible to download [here](https://drive.google.com/uc?export=download&id=1a9vMs0Kke7Nh4LuxCnKHkVIkFDr-az_Z)

### Task 1 - investigate bus_journeys data
---

This is the data dictionary for records in the bus_journeys data (all fields are alphanumeric):  

LineRef-----------------------------bus route number  
DirectionRef-----------------------current direction of travel, inbound or outbound   
PublishedLineName---------------timetabled service name (may be same as LineRef)  
OriginName-----------------------start location of the current route  
DestinationName-----------------end destination on the current route  
OriginAimedDepartureTime------the time at which the bus was timetabled to leave its start location    
Ref---------------------------------a uniquely identifier for the bus vehicle  

The bus_journeys data contains a list of records with the fields shown above.  This list contains a records for each bus that is currently on a bus route (assuming that all are tranmitting their locations) 
  
**Task**  
Take a look at the `bus_journeys` dictionary

* Print the first record
* Print the last record
* How is an individual bus journey dictionary structured? 
* How many of these dictionary records are in the list?


**Expected Output**   
First record will have `LineRef` 177  
Last record will have `LineRef` 347  

**COMPLETE THIS TASK IN YOUR USUAL JAVASCRIPT EDITOR**

### Task 2 - investigate vehicle_refs and emission_classes data lists
---
Take a look at the `vehicle_refs` and `emission_classes` lists
* what is the length of each list?
* find how many unique items there are in the emission_classes list - (**hint** : you will need to create another list and use a for loop) *italicised text* 
* print the unique emission_classes items 
* find how many unique items there are in the vehicle_refs list
* print the length of the unique vehicle_ref items 

**COMPLETE THIS TASK IN YOUR USUAL JAVASCRIPT EDITOR**

### Task 3 
---
The client is only concerned about bus routes 116 and 132 specifically.

**Task**
Create a new list of dictionaries which contains only the records where the `LineRef` is either 116 or 132. 

*(**hint**: the datatype of the LineRef might not be what you expect - the data came from a .csv file)*

**Expected output**
There will be 14 records in this list

**COMPLETE THIS TASK IN YOUR USUAL JAVASCRIPT EDITOR**

### Task 4 
---

The indexes of `vehicle_refs` match the indexes of `emissions`.   
Create a new list, which contains dictionaries.  Each dictionary will contain a vehicle_ref and its corresponding emission_class. 
*hint: you will need to use a for loop and indexing and should create dictionaries with two keys: vehicle_ref and emission_class*

**COMPLETE THIS TASK IN YOUR USUAL JAVASCRIPT EDITOR**

### Task 5
The list of dictionaries you created in the last exercise is very long. A more intuitive way to hold this data would be by collating data.

Create a dictionary where each unique emission_class is a key and its corresponding value is a list of all vehicle_refs with that emission_class

(hint: you could think about using the unique_em list you created earlier)

**Example Output**

{"EURO III": [1234, 4567, 8910], "EURO IV": [1028, 1283, 1234]}

**COMPLETE THIS TASK IN YOUR USUAL JAVASCRIPT EDITOR**

### Task 6
---
Find all the polluting buses that were running when the data was collected.   
Using the `bus_journeys` dictionary, find all the records where a Euro III bus was used. 

You can find the `Refs` which are polluting from the dictionary you created in the last task. 

* Create a new list of dictionaries which only contains the records from `bus_journeys` which were found as polluting bus. 
* how many polluting buses were being used?

**COMPLETE THIS TASK IN YOUR USUAL JAVASCRIPT EDITOR**

# Challenge

Can we find out how much pollution one bus on the 116 route emits?

Can we find out how much pollution one bus on the 132 route emits?

Can we find out how much pollution, in total, all the buses on these routes at the recorded point in time will be emitting?

**Some numbers to play with:**  
NOTE: These are NOT fact checked but give a rough idea of some numbers we might be able to use for a rough first model

*  A typical old diesel bus will typically get 5 miles per gallon, which is 2.5km per litre
*  As one litre of diesel fuel has the energy content of 10.8 kWh
*  If the bus's fuel consumption is 2.5km per litre, this gives an energy content of 4.3 kWh/km

Emissions data is in this variable: ***emissions_data***

**Emissions Data dictionary**

Field----------------------------- Data Type---------------Description  

Emission Standard--------------- Alphanumeric----------Euro III, IV, V or VI   
CO2-------------------------------Float--------------------grams of CO2 emitted per KWhr  
Nox-------------------------------Float--------------------grams of Nox emitted per KWhr  
PM--------------------------------Float--------------------grams of particulate matter emitted per gm/KWhr  
			
**Route information**  
The 132 route is 12.5km from end to end  
The 116 route is 15.25km  

#### **Task**  

Write a function that takes the miles per gallon and the route (LineRef) as a parameter and calculates the emission of each of the 3 pollutants for a return journey on that route.

#### **Extension**  

Find all the 116 and 132 buses in the data set (a snapshot of what is on the road at that particular point in time).  

Count how many of these buses are Euro III.  

Then calculate the total emissions for each pollutant for all the buses you have found.

**COMPLETE THIS CHALLENGE IN YOUR USUAL JAVASCRIPT EDITOR**
