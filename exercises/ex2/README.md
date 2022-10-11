# Exercise 2 - Combine the Data into one view (to be updated)

We have two sets of data, which kind of go together, but since they are coming from different sources, they don’t have common key or join criteria’s that could be used to create a seamless set of data. 

Intelligent lookup will provide if the missing link, by creating and filling a mapping table between the two sets of data. 

## Add Keys
The intelligent lookup needs keys in the data sets to join together. Should a Data Set not have a key defined you can add the key by wrapping it into a view. 
1.	Create a new view
2.	Add the German_Car_Registration or other table to the view
3.	Mark the key columns in the view as key. 
In case of the Germany Car Registration Data keys are Time, Modellreihe, Marke, Release ID
The Car Manufacturer table key is: ID

![Data Market Place](/exercises/ex2/images/Picture28.png)

4.	Deploy the view
5.	Repeat until both sources have a keys. 
## Create Intelligent Lookup
1.	New Intelligent lookup. 

![Data Market Place](/exercises/ex2/images/Picture29.png)

2.	Add an input and lookup table. Input should be the larger table, Car Registrations data in this case and lookup table the Car Manufacturer. 
3.	Add the Pairing Column for the Input Table
That is the column the system will use to look into the Lookup Table

![Data Market Place](/exercises/ex2/images/Picture29.png)

4.	Add the Return Columns from the Lookup table 
These are the columns we want to be added to the data model
 
![Data Market Place](/exercises/ex2/images/Picture30.png) 

5.	Define a rule to create the mapping.  
The field “Marke” in the German Car Registration data means Brand. So we are using that field to find the corresponding Brand in the Car Manufacturer Data. Use the exact match for the match strategy. 

![Data Market Place](/exercises/ex2/images/Picture31.png)
 
6.	Deploy 
7.	Run and Preview

![Data Market Place](/exercises/ex2/images/Picture32.png)

By running it, the system will execute the rule of exact match that we created. The result show that 69% of the records from our German Car Registration Data was matched to the Car Manufacturer Data, 31% are not matched. 

![Data Market Place](/exercises/ex2/images/Picture33.png)

The preview also shows which values could not be matched. 

![Data Market Place](/exercises/ex2/images/Picture34.png)
 
8.	Edit you Intelligent Lookup
9.	Add a rule for unmatched records

![Data Market Place](/exercises/ex2/images/Picture35.png)

10.	Define the rule with Fuzzy Search
Use the same to columns "Marke" and "Brand" but with a fuzzy search strategy. 

![Data Market Place](/exercises/ex2/images/Picture36.png)

You can choose the confidences when something automatically matches and when something should be reviewed. 
11.	Deploy, Run, Preview

![Data Market Place](/exercises/ex2/images/Picture37.png)

out of the 31% unmatched records the second rule was able to match 18%, is unsure about 1% and could not find 12%

### Review matches

1.	Review the multiple matches
The multiple tab shows on the left hand side the key combinations that could not be matched. In this case the Marke/Brand “DS”

![Data Market Place](/exercises/ex2/images/Picture38.png)

and on the right hand side the possible options with their score. 
To pick the correct mapping, pick the right entry on the right and hit the match button. The system will now remember your choice for future data that come in. 

![Data Market Place](/exercises/ex2/images/Picture39.png)

The yellow 1% multiple became a second green 1% as we assigned them. 
2.	Review the Unmatched 
The unmatched can be matched similarly. 

![Data Market Place](/exercises/ex2/images/Picture40.png)
 
“VW” as Marke corresponds to Vokswagen in the Brand field 
The 19 in brackets on the left hand side indicate how many records in the Germany Car Registration Data have the Marke (Brand) “VW”. By mapping that we will map additional 5% of the records.
  
### Check the generated Data Set

1.	Open a new graphical view 
2.	Pull in the Intelligent Lookup you created. 
3.	Preview the data. 

![Data Market Place](/exercises/ex2/images/Picture41.png)
 
The data shows records of German Car Registration but you can see that the data now contains the fields brand and country from the car manufacturer table for all records that are mapped. 

## Summary

You've now ...

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
