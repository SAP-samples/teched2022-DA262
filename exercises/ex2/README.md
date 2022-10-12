# Exercise 2 - Get external Data: German Car Sales Data (mandatory, available in Learning Experience systems)
To get data into the Data Warehouse you have different opportunities and possibilities. If you are using the SAP DWC Access obtained in exercise 0, we recommend using the [external connection](#exercise-2a---external-connection). [Uploading all files as CSVs](#exercise-2b---import-csvs---get-my-companies-sales-data) is the fall back, if you are doing these exercises at a time when trial access is not possible. 


## Exercise 2a - External Connection
As the Data Market Place is not available in learning experience systems, we provided the data through an external connection.

1. Click on "Connection".

![Get Data Product](/exercises/ex1/images/Picture13.png)

Choose “Create”.  

![Get Data Product](/exercises/ex1/images/Picture14.png)

2.	Create an Amazon Athena Connection. 
Click on “Amazon Athena”.

![Get Data Product](/exercises/ex1/images/Picture15.png)

![Get Data Product](/exercises/ex1/images/Picture16.png)


Fill in form with the following data:
* Region: eu-central-1
* Workgroup: primary
* Access Key: AKIA5ZWR7FEGCJ3O4GGN
* Secret Key: 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


![Get Data Product](/exercises/ex1/images/Picture17.png)

Click on “Next Step”.
Enter a Business Name, a Technical Name and a Description. The Technical Name must be ATHENA, if you want to export your space!
3. Validate Connection
Choose your connection and click on validate.

![Get Data Product](/exercises/ex1/images/Picture18.png)

If you successfully created the connection, this should pop up: 

![Get Data Product](/exercises/ex1/images/Picture19.png)

### Import Remote Table
Import the tables from AWS.
1. Click on Data Builder. Click the "Import-Button" and choose "Import Remote Table".

![Get Data Product](/exercises/ex1/images/Picture20.png)

Choose the Athena connection you just created and click on "Next Step".

![Get Data Product](/exercises/ex1/images/Picture21.png)

Click on dwc-data-challenge and choose the tables "rt_car_manufacturer" and "rt_german_car_registration". Choose "Next Step" and check that the tables are ready for import. Click on "import and deploy" to finish importing the tables.

![Get Data Product](/exercises/ex1/images/Picture22.png)

### Create Snapshot (Optional)
When creating a snapshot, you are replicating the table from AWS to a persistent table on the DWC system. 
Go into the Data Integration Monitor. 

![Get Data Product](/exercises/ex1/images/Picture23.png)

Choose one of the remote tables. Click on “Table replication” and choose “Load new Snapshot”.

![Get Data Product](/exercises/ex1/images/Picture24.png)

Do this for both tables. This will increase the performance of your data and visualization.

### Check remote queries (optional)
You can check the remote queries in the data integration monitor (Tab: remote query monitor). You can see the statement DWC sends to the remote source.

## Exercise 2b - Import CSVs - Get My Companies Sales Data
1.	Get the Resource Package from git. xxx
In the resource package, you can find the data in CSV files and models in JSON. The models require a connection with the technical name ATHENA, if you did not create the Connection in from the previous exercise, please to it know
2.	Import the Teched2022_DA262.json into your space.
 
Once completed and the deployment was successful you should see four objects. 
 The objects are a very simplified form of sales reporting. Consisting only out of Sales Data and Product Master Data. The Data comes in through Remote Tables, on top of each remote table is a view, a Dimension View for the master data and an Analytical DataSet view for the sales data. The sales data associate the product dimension. The product dimension has one level-based hierarchy defined uses Group -> Brand -> Model levels. For simplicity there is no customer information in the data, also the time dimension holds only a single day, as it is not important for this exercise. 
 
xxx
1.	Get the Resource Package from git. xxx
In the resource package, you can find the data in CSV files and models in JSON. The models require a connection with the technical name ATHENA, if you did not create the Connection in from the previous exercise, please do it now.
2.	Import the Teched2022_DA262.json into your space.
xxx

## Summary

You've now ...
We have two sets of data, which kind of go together, but since they are coming from different sources, they don’t have common key or join criteria’s that could be used to create a seamless set of data. 

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
