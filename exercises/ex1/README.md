# Introduction
In this exercise get to know and import all necessary data. This consists of: 
- Internal Data
    - MyCompany Sales - represents daily sales in units per product of the *MyCompany* business
    - MyCompany Products - Product Master of the *MyCompany* business 
- External data
    - German Car Registrations - Monthly car registrations in Germany by model & brand 

# How to load the data
Normally, your sales data and product masters would be original in your S/4 system and be loaded into SAP Data Warehouse Cloud as part of your normal modelling work. External data is best found and integrated using [SAP Data Marketplace](https://blogs.sap.com/2021/12/13/sap-data-warehouse-cloud-data-marketplace-an-overview/), which itself is an integral part of SAP Data Warehouse Cloud. Once all data has been loaded, the data harmonization, modelling & reporting steps would be performed

In the context of this TechEd workshop, our main aim is we focus primarily on the harmonization, modelling & reporting steps. We'd like to showcase SAP Data Marketplace as well, but since it is not available in the DWC Guided Experience systems, we can only point you to background information (TODO doc and link) on it. The rest of the data integration to SAP Data Warehouse Cloud is amply covered in TechEd workshop DA160 (TODO link) and we are therefore decided to take a shortcut on the data integration bits. If you are interested to learn more on alternative ways of integrating the workshop data into SAP Data Warehouse Cloud (e.g. into your own tenant outside Guided Experience, please follow this link (**TODO link**)) data integration in the context , please  need to   and thus are taking a shortcut on the data loading parts. This is why you'll load all data simply from the connected HANA cloud system 

- show you how easy data integration we , our focus is primarily on the modelling side of the house and not on the data loading. So we decided to make data loading as simple as possible by not on the data loading
# Skip Steps

- [Exercise 1.1 - Import CSVs](#exercise-11---import-csvs)
- [Exercise 1.1 - Via Data Market Place (optional, not available in Learning Experience systems)]([#exercise-11---via-data-market-place)
- [Exercise 1.2 - External Connection](#exercise-12---external-connection)
- [Exercise 1.3 - Import Remote Table](#exercise-13---import-remote-table)
- [Exercise 1.4 - Import table from SAP S/4 HANA](#exercise-14---Import-table-from-SAP-S/4-HANA)
- [Exercise 1.5 - Import CSVs](#exercise-15---Import-CSVs)

## Exercise 0B - SAP DWC Account
If you have already have an account on an SAP DWC System, you can use that account.

## Exercise 1B - Import CSVs

Upload your data directly. This can make sense if your tenant does not have any sources connected to it. 

1. Navigate to the Data Builder.
2. Choose "Import CSV File". <br> ![Get Data Product](/exercises/ex1/images/3.png) <br>
3. Choose your file and click "Upload". <br> ![Get Data Product](/exercises/ex1/images/4.png) <br>
4. Check that the data types were correctly detected and click on "Deploy". <br> ![Get Data Product](/exercises/ex1/images/5.png) <br>
5. Repeat these steps for all your files. 

## Exercise 2B -  Skip Modeling

In the resource package, you can find the data in CSV files and models in JSON. The models require a connection with the technical name ATHENA, if you did not create the Connection in the exercise 1A, please do it now.

1.	Get the Resource Package from git. The files are in the [DA262_Resource.zip](DA262_Resource.zip) in this GitHub Repo.

In the resource package, you can find the data in CSV files and models in JSON. The models require a connection with the technical name ATHENA, if you did not create the Connection in from the exercise 1A, please do it now.

2. Open the "Data Builder". Select your space.
3. Click on Import->"Import Objects from CSN/JSON file" <br> ![Get Data Product](/exercises/ex1/images/1.png)
4. Import the Teched2022_DA262.json into your space. Choose all objects by selecting them and click "Import CSN File".
![Get Data Product](/exercises/ex1/images/2.png)
5.If successfull, you shoud get a "Success" message and the objects should start appearing in your space.

## Exercise 3B - Skip the Business Builder

1. Go to the "Data Builder" and select "New Graphical View".
2. Join the KBA-VIEW with the MyCompany Sales Dimension.
3. Join the resulting table to the "MyCompany Sales Data"-View.
4. Select the resulting view and toggle the "Expose for Consumption"-Switch.
![Get Data Product](/exercises/ex1/images/002.png)
5.Give your View a name.
6. Save and Deploy the new view.
7. Now change over to the SAC.
![Get Data Product](/exercises/ex1/images/003.png)

## Exercise 4B - Skip SAC
This is the last step, if you run out of time just skip it.


# Exercise 1B - Get external Data: German Car Sales Data (optional)

There are a lot of different ways to load data into the SAP Data Warehouse Cloud. If you are not using the trial system, you can use these instructions. 
These will show you all other ways to load the data into the SAP DWC.

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


## Exercise 1.2 - Import table from SAP S/4 HANA


## Summary

You've now ...
Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)
