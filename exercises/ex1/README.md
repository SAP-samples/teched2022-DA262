# Exercise 1 - Get external Data: German Car Sales Data

There are 4 different ways to load data into the SAP Data Warehouse Cloud. 
You can choose either of 3 to load the needed data:
- Exercise 1.1 - Via Data Market Place (optional, not available in Learning Experience systems)
- Exercise 1.2 - External Connection
- Exercise 1.3 - Import Remote Table
- Exercise 1.4 - Import table from SAP S/4 HANA
- Exercise 1.5 - Import CSVs

## Exercise 1.1 - Via Data Market Place (optional, not available in Learning Experience systems)
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

## Exercise 1.2 - External Connection
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
Region: eu-central-1
Workgroup: primary
Access Key: AKIA5ZWR7FEGCJ3O4GGN
Secret Key: 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
 
![Get Data Product](/exercises/ex1/images/Picture17.png)
Click on “Next Step”.
Enter a Business Name, a Technical Name and a Description. The Technical Name must be ATHENA, if you want to export your space!
3. Validate Connection
Choose your connection and click on validate.
![Get Data Product](/exercises/ex1/images/Picture18.png)
If you successfully created the connection, this should pop up: 
![Get Data Product](/exercises/ex1/images/Picture19.png)

## Exercise 1.3 - Import Remote Table
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




## Summary

You've now ...

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)
