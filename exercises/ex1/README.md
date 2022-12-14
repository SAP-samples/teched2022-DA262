# Exercise 1 - Load data from SAP HANA Cloud


## Introduction
In this exercise get to know and import all necessary data. This consists of: 
- Internal Data 
    - MyCompany Sales - Remote table containing daily sales in units per product of the *MyCompany* business. In the scenario, the sales data is used in other projects and thus already wrapped in a view that can be consumed directly by SAC. 
    - MyCompany Product Master - Product Master of the *MyCompany* business. Again, other projects are also using it and their requirements have been met by wrapping it also in a view. 
- External data
    - German Car Registrations - Quarterly car registrations in Germany by model & brand for Q1 2022

Normally, your sales data and product masters would be original in your S/4 system and be loaded into SAP Data Warehouse Cloud as part of your normal modelling work. External data is best found and integrated using [SAP Data Marketplace](https://blogs.sap.com/2021/12/13/sap-data-warehouse-cloud-data-marketplace-an-overview/), which itself is an integral part of SAP Data Warehouse Cloud. Once all data has been loaded, the data harmonization, modelling & reporting steps would be performed

In the context of this TechEd workshop, we focus primarily on the harmonization, modelling & reporting steps. We'd love to showcase SAP Data Marketplace as well, but since it is not available in the DWC Guided Experience systems, we can only point you to [background information](https://blogs.sap.com/2021/12/13/sap-data-warehouse-cloud-data-marketplace-an-overview/) on it. 

The rest of the data integration to SAP Data Warehouse Cloud is amply covered in [TechEd workshop DA160](https://github.com/SAP-samples/teched2022-DA160) and we therefore decided to take a shortcut on the data integration bits. We are planning to provide dedicated own information about how to run the exercise outside of the DWC Guided Experience system (e.g. by using your own SAP Data Warehouse Cloud tenant and uploading CSVs or connecting to Amazon Athena with it). The respective information will be published in this repository as well.  

## Exercise 1.1 - Load JSON

1. Download [this archive](/TechEd_2022_DA262.zip). It contains all metadata that the SAP Data Warehouse Cloud repository needs to identify & connect the HANA cloud tables relevant for this exercise as well as the views for sales & product data. In essence, the objects marked in green on the [overview page](/exercises/overview/README.md) are contained. For your convenience, also a copy of the data is provided as CSV, but what you really need is only metadata file *Connection_HANA.json*
2. Unpack the archive to a local folder. Find file *Connection_HANA.json*
3. Open the Data Builder in the SAP Data Warehouse Cloud.   
If prompted, choose your space (in DWC Guided Experience systems, there's only one space by default, so you should not be prompted). <br> ![](images/open_data_builder.jpg)
3. Click on the *Import* icon in the action bar and choose *Import Objects from CSN/JSON*. Navigate to the file *Connection_HANA.json* and choose *Open*.  <br> ![](images/import_csn_json.png) 
4. In the import dialog, select all five objects (i.e. three remote tables & two views) and choose *Import CSN File*. <br> ![](images/import_dialog.jpg). 
5. Wait for the import to complete. You'll get a notification about this.
6. In the Data Builder, check check all five objects and choose *Deploy* from the action bar. Wait for a success message of the deployment before you proceed further.
<br> ![](images/mass_deploy.jpg)

**Note:** As said, you could also load the same table data directly from [SAP Data Marketplace](https://blogs.sap.com/2021/12/13/sap-data-warehouse-cloud-data-marketplace-an-overview/) or by [uploading the respective CSVs](https://help.sap.com/docs/SAP_DATA_WAREHOUSE_CLOUD/c8a54ee704e94e15926551293243fd1d/8bba251c78874736963703cff56b1b74.html) directly into tables.  We will be adding an own chapter on both ways after TechEd. For the time being, we concentrate on the straight-forward way as described here. 

## Exercise 1.2 - Create Snapshot and inspect data

By default, remote tables are accessed on the fly in a "federated" fashion. In some situations, it can be helpful to replicate the data though, esp. if latency or other performance considerations apply. To become  familiar also with this functionality, you draw a replicated "snapshot" of the data in SAP Data Warehouse Cloud.

For **each of the three remote tables**, do the following:
1. Click on the table name in the Data Builder. <br> ![](images/open_remote_table.jpg)
2. In section *Remote*, find the the save icon and click on *Load New Snapshot*.  <br> ![](images/load_snapshot.jpg)  
3. You should get a "Replication started"-message. <br>![](images/replication_started.jpg)  
4. Inspect the table data by choosing the Data Preview icon in the action bar. <br> ![](images/data_preview.jpg)

**Note:** You can also check the replication status of the remote tables under menu item *Data Integration Monitor > Remote Table Monitor*. Replications can also be started & scheduled from within the monitor by navigating into an individual remote table. <br>
![data integration monitor](images/data_integration_monitor.jpg)

# Summary
You have now imported and replicated three tables as well as two views building on top of these tables. You have thus laid the foundation for subsequent modeling, harmonization & reporting steps. You can now continue to - [Exercise 2 - Map car registration data to internal brand master](../ex2/README.md). <br>
If you want to, [you can jump ahead and start a small SAC Story](/exercises/ex4#excercise-41---show-sales-data-in-sac). You will not be able to do exercise 4.2 that way!
