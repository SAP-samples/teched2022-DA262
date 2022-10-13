# Exercise 1B - Get external Data: German Car Sales Data (optional)

There are a lot of different ways to load data into the SAP Data Warehouse Cloud. If you are not using the trial system, you can use these instructions. 
These will show you all other ways to load the data into the SAP DWC.

- [Exercise 1.1 - Import CSVs](#exercise-11---import-csvs)
- [Exercise 1.1 - Via Data Market Place (optional, not available in Learning Experience systems)]([#exercise-11---via-data-market-place)
- [Exercise 1.2 - External Connection](#exercise-12---external-connection)
- [Exercise 1.3 - Import Remote Table](#exercise-13---import-remote-table)
- [Exercise 1.4 - Import table from SAP S/4 HANA](#exercise-14---Import-table-from-SAP-S/4-HANA)
- [Exercise 1.5 - Import CSVs](#exercise-15---Import-CSVs)

## Exercise 1.1 - Import CSVs

Upload your data directly. This can make sense if your tenant does not have any sources connected to it. 

1. Navigate to the Data Builder.
2. Choose "Import CSV File". <br> ![Get Data Product](/exercises/ex1/images/3.png) <br>
3. Choose your file and click "Upload". <br> ![Get Data Product](/exercises/ex1/images/4.png) <br>
4. Check that the data types were correctly detected and click on "Deploy". <br> ![Get Data Product](/exercises/ex1/images/5.png) <br>
5. Repeat these steps for all your files. 

## Exercise 1.1 - Via Data Market Place
(optional, not available in Learning Experience systems)
Skip this, if you use the DWC Access provided in "Exercise 0".

1.	Open Data Market Place –> Landing Page.

![Data Market Place](/exercises/ex1/images/Picture2.png)

2.	Find “Car Registrations Germany - Q1.2022 – Kraftfahrtbundesamt”

![Data Product](/exercises/ex1/images/Picture3.png)

3.	Click on the button “Load for Free”.

![Get Data Product](/exercises/ex1/images/Picture4.png)

4.	Select your Space and click “Load Product.”

![Choose a space](/exercises/ex1/images/Picture5.png)

![Get Data Product](/exercises/ex1/images/Picture6.png)
  
### Check the installation 
There are two ways of checking the acquisition of data. 
a) The logs of the installation can be found in the Data Market Place -> My Data Products. 

![Goto the Data Market Place](/exercises/ex1/images/Picture7.png)

Check all three tabs (My Product, Updates and Delivery Tracking) for information on your data delivery.

![Get Data Product](/exercises/ex1/images/Picture9.png)

The data product you just downloaded will be shown as Status: "Success" if everything went well. 

![Get Data Product](/exercises/ex1/images/Picture10.png) 

It will show “failed”, if a problem occurred e.g. not enough storage. 

![Get Data Product](/exercises/ex1/images/Picture11.png)

If the Status is signified as “downloading”, you will have to wait a moment longer as the data product is not ready yet.


b) You can also have a look into your space and see the table with data. (xxx)

![Get Data Product](/exercises/ex1/images/Picture12.png)

**XXX**
## Skip Step 1B - Get My Companies Sales Data

In the resource package, you can find the data in CSV files and models in JSON. The models require a connection with the technical name ATHENA, if you did not create the Connection in the exercise 1A, please do it now.

1.	Get the Resource Package from git. The files are in the [DA262_Resource.zip](DA262_Resource.zip) in this GitHub Repo.

In the resource package, you can find the data in CSV files and models in JSON. The models require a connection with the technical name ATHENA, if you did not create the Connection in from the exercise 1A, please do it now.

2. Open the "Data Builder". Select your space.
3. Click on Import->"Import Objects from CSN/JSON file" <br> ![Get Data Product](/exercises/ex1/images/1.png)
4. Import the Teched2022_DA262.json into your space. Choose all objects by selecting them and click "Import CSN File".
![Get Data Product](/exercises/ex1/images/2.png)
5.If successfull, you shoud get a "Success" message and the objects should start appearing in your space.

Once completed and the deployment was successful you should see four objects. 
 The objects are a very simplified form of sales reporting. Consisting only out of Sales Data and Product Master Data. The Data comes in through Remote Tables, on top of each remote table is a view, a Dimension View for the master data and an Analytical DataSet view for the sales data. The sales data associate the product dimension. The product dimension has one level-based hierarchy defined uses Group -> Brand -> Model levels. For simplicity there is no customer information in the data, also the time dimension holds only a single day, as it is not important for this exercise. 
 




**xxx**



## Exercise 1.2 - Import table from SAP S/4 HANA


## Summary

You've now ...
Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)
