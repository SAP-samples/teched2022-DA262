# Create a Consumption Model in the Business Layer 
To create a reusable model for consumption in SAC you will need to create a model in the Business Layer. We will create 2 models and connect them via a multifact model.
## Create a Dimension for Product
To connect the 2 model we first need to find the commonalities. We do this by creating an asscociative dimension.
1. Click on “New Dimension”. Choose the Dimension you created in the Data Builder as a Data entity. Choose your Business Name and Technical Name. Click “next”.
2. In the next dialog choose “yes” and copy the properties. Click ”next”.
3. Choose the "Attributes" sheet. Delete the "id" column from your attributes by clicking the "x" behind the entry.  (what are these attributes used for?)
4. Choose the "General" sheet and switch the status to "Ready to Use"
5. Click "Save".
## Create Analytical Dataset for KBA
Now we have to create an Analytical Dataset for KBA.
1. To create an new Analytical Dataset, click "New Analytical Dataset". ![Test](images/9.png)
2. Choose the Analytical Dataset you created in the Data Builder as a Data entity. Choose your Business Name and Technical Name. Click “Create”. ![Image](images/10a.png 'Test')
3. In the next dialog choose “yes” and copy the properties. Click ”Create”.
4. Choose the "Key definitions" sheet and add a new definition.
![Test](images/11.png)
![Test](images/12.png)
5. Add a Business and a Technical Name. ![Test](images/13.png)
6. Select a "KBA Brand" as a Key. ![Test](images/14.png)
7. Click on the +-Button and repeat these for "KBA Model" and "time" ![Test](images/14a.png)
8. Verify your keys and save the definition. ![Test](images/14b.png)
![Test](images/14c.png)
9. Add an association by opening the association sheet and clicking "+".
![Test](images/15a.png)
To give a common denominator between two different Models you need to choose a dimension they both have in common. This dimension will contain our product.
![Test](images/15b.png)
10. Select the "MyCompany Products"-Dimension you just creates as the Business Entity. ![Test](images/16a.png)
11. Select the id you want to associate to your product dimension.
![Test](images/17a.png) Choose the "Product ID". This ID will be connected to the Products' Id. This gives you the possibility to filter both models for the same products.
![Test](images/18.png)
12. Give a context name and "Save".
![Test](images/19.png)
13. Choose the "General" sheet and switch the status to "Ready to Use"
14. Click "Save".
## Create Analytical DataSet for My Company Sales (Add association)
Repeat the above procedures for "My Company Sales".
1. Add a new Analytical Dataset.
![Test](images/9.png)
2. Choose a name.
![Test](images/20.png)
3. Choose your measure (Sales Unit).
![Test](images/21.png)
![Test](images/22.png)
4. Create Attributes for product and date.
![Test](images/23.png)
![Test](images/24.png)
5. Create key definitions for date and product.
Why?
![Test](images/25.png)
Don't forget to verify your keys.
![Test](images/26.png)
![Test](images/27.png)
6. Set your status to "Ready to use".
![Test](images/28.png)

## Create Multifact Consumption Model (KBA and Sales)

1. Create a new Consumption Model.
![Test](images/29.png)
2. Add a name and click "Step 2".
![Test](images/30.png)
3. Choose your Sales Model to start creating the Consumption Model. Click on the "MyCompany Sales" Model and click on "Step 3".
![Test](images/31.png)
4. Choose an alias and click on "Create".
![Test](images/32.png)
5. Add a new Fact Source
![Test](images/33a.png)
6. Add the KBA Dataset and click on "Step 2".
![Test](images/34.png)
7. Give your data source an alias click on "Step 3"
![Test](images/35.png)
8. Add a new Dimension Source, choose "MyCompany Products" and click on "Step 2".
![Test](images/38.png)
9. Add an Alias and click on "Step 3".
![Test](images/39.png)
Now you connect the Fact Sources to the Product Dimension.
![Test](images/40.png)
10. Click on the Fact Source and click on the "Expand"-Icon.
![Test](images/41.png)
11. Click on the Products and click the "Link"-Icon.
![Test](images/42.png)
12. Now you have to do the same thing for the other Fact Model.
Click on the Sales Model and click on the "Expand"-Button.
![Test](images/43.png)
![Test](images/44.png)
13. Click on the newly expanded Product Dimension and click on the "Link"-Icon.
![Test](images/45.png)
![Test](images/46.png)
14. Click on "Create".
![This is how the model should look now](images/48.png)
## Create (Calculated) Key Figures 
15. Now add the Measures (BEV, Cabriolets, Sales Unit, All)
![Test](images/49a.png)
16. Next we add a calculated measure. Add a measure and choose "Calculated Measure". 
![Test](images/50.png)
17. Create the calculation for market share.
![Test](images/51.png)
Divide "Sales Unit" by "All Vehicles". And click "Save".
![Test](images/52.png)
![This is all measures that we just created.](images/52.png)
18. Now we have to create the attributes, the model will be filtered by (Brand, Group, Model, Orign). 
![Test](images/53.png)
![Test](images/54.png)
![Test](images/55.png)
19. Go to the "General" sheet and check the "Allow public data access" box. Then click "Save". 
![Test](images/56.png)
Now there should be a green check in the right upper corner. If there is a red cross something went wrong. Please check the failure message.
![Test](images/57.png)
20. To create a story based on this Fact Model, you need to create a perspective. You can either do this by clicking the "+"-Button or by clicking on the "Data Preview". Click on the "Data Preview".
![Test](images/58.png)
21. Create a table to base your perspective on by drag-and-drop. 
![Test](images/59.png) 
22. Click "Save New" and enter a name.
![Test](images/60.png)

# Create SAC Story (Optional)
If you want to you can now go into the SAP SAC to create a story from the SAP DWC dataset. Just choose the DWC as a data source and create your visualization.


