# Exercise 3 - Preparing Analytic Data Consumption via the Business Layer
To create a reusable model for consumption in SAC, you will need to create a reporting model in the Business Layer. To this end, we create the relevant business entities and subsequently consume them in a *Consumption Model*. 

- Creating Business Entities  
    - [Exercise 3.1 - Create a Dimension for Product](#exercise-31---create-a-dimension-for-product)
    - [Exercise 3.2 - Create Analytical Dataset for Car Registration data](#exercise-32---create-analytical-dataset-for-kba)
    - [Exercise 3.3 - Create Analytical DataSet for Sales Data](#exercise-33---create-analytical-dataset-for-my-company-sales-add-association)
- Create reporting model for SAP Anayltics Cloud
    - [Exercise 3.4 - Create Multifact Consumption Model (Car Registration Data and Sales Data)](#exercise-34---create-multifact-consumption-model-kba-and-sales))
    - [Exercise 3.5 - Create Key Figures)](#exercise-35---create-calculated-key-figures)

## Exercise 3.1 - Create a Dimension for Product
Car registration data and sales data both contain facts about the same entity, namely our product master. In DWC Business Layer terms, we talk about a "shared dimension" of the two fact sources and model the product master data as a *Business Layer dimension*. Subsequently, the two fact sources are modelled as *Business Layer Analytical Datasets* that each have an association towards that product dimension. To create the product dimension, please proceed as follows: 
1. Open the Business Builder app via its button on the left
<br> ![open bus builder](images/open_biz_builder.jpg)
2. Click on “New Dimension”. Choose *V_MY_COMPANY_PRODUCT* as data entity and set its business name to *DIM_MY_COMPANY_PRODUCT*. The technical name will be auto-adjusted to *BE_DIM_MY_COMPANY_PRODUCT*. 
<br> ![Wizard - Data Entity](images/dim_wizard_data_entity.jpg)
3. Confirm take over all attributes & key definitions from the underlying view *V_MY_COMPANY_PRODUCT* and choose *Create*. 
<br> ![Dim Wizard - take over props and keys](images/dim_wizard_copy_props.jpg)
4. This brings you to the main page of the product dimension dialog. The object is auto-saved, so there's nothing you need to do right now, but it would good if you checked the various tabs and its contents
<br> ![Dim main page](images/dim_main_page.jpg) 

5. Leave the dialog by choosing the cross sign in the header.
<br> ![Close dim](images/dim_close.jpg)

## Exercise 3.2 - Create Analytical Dataset for Car Registration Data

Now we have to create an Analytical Dataset for KBA.
1. To create an new Analytical Dataset, click "New Analytical Dataset". <br> ![Test](/exercises/ex3/images/9.png)
2. Choose the Analytical Dataset you created in the Data Builder as a Data entity. Choose your Business Name and Technical Name. Click “Create”. <br> ![Image](/exercises/ex3/images/10a.png 'Test')
3. In the next dialog choose “yes” and copy the properties. Click ”Create”.
4. Choose the "Key definitions" sheet and add a new definition. <br>
![Test](/exercises/ex3/images/11.png)
![Test](/exercises/ex3/images/12.png)
5. Add a Business and a Technical Name. <br> ![Test](/exercises/ex3/images/13.png)
6. Select a "KBA Brand" as a Key. <br> ![Test](/exercises/ex3/images/14.png)
7. Click on the "+"-Button and repeat these for "KBA Model" and "time". <br> ![Test](/exercises/ex3/images/14a.png)
8. Verify your keys and save the definition. <br> ![Test](/exercises/ex3/images/14b.png) <br>
![Test](/exercises/ex3/images/14c.png)
9. Add an association to the product dimension by opening the association tab and clicking "+". <br>
![Test](/exercises/ex3/images/15a.png)
To give a common denominator between two fact sources you need to choose a dimension they both have in common. As described above, this "shared" dimension will be the product dimension created in [exericse 3.1](#exercise-31---create-a-dimension-for-product).
![Test](/exercises/ex3/images/15b.png)
10. Select the "MyCompany Products"-Dimension you just created as the Business Entity. <br> ![Test](/exercises/ex3/images/16a.png)
11. Select the id you want to associate to your product dimension. <br>
![Test](/exercises/ex3/images/17a.png) <br> Choose the "Product ID". This ID will be connected to the Products' Id. This gives you the possibility to filter both models for the same products. <br>
![Test](/exercises/ex3/images/18.png)<br>
12. Give a context name and "Save".<br>
![Test](/exercises/ex3/images/19.png)<br>
13. Choose the "General" sheet and switch the status to "Ready to Use".
14. Click "Save".

## Exercise 3.3 - Create Analytical DataSet for My Company Sales

Repeat the above procedures for "My Company Sales".
1. Add a new Analytical Dataset. <br>
![Test](/exercises/ex3/images/9.png)<br>
2. Choose a name. <br>
![Test](/exercises/ex3/images/20.png)<br>
3. Choose your measure (Sales Unit). <br>
![Test](/exercises/ex3/images/21.png)<br>
![Test](/exercises/ex3/images/22.png)<br>
4. Create Attributes for product and date. <br>
![Test](/exercises/ex3/images/23.png)<br>
![Test](/exercises/ex3/images/24.png)<br>
5. Create key definitions for date and product.
Why? xxx <br>
![Test](/exercises/ex3/images/25.png) <br>
Don't forget to verify your keys.<br>
![Test](/exercises/ex3/images/26.png)<br>
![Test](/exercises/ex3/images/27.png)<br>
6. Set your status to "Ready to use".<br>
![Test](/exercises/ex3/images/28.png)<br>

## Exercise 3.4 - Create Multifact Consumption Model (KBA and Sales)

1. Create a new Consumption Model. <br>
![Test](/exercises/ex3/images/29.png)<br>
2. Add a name and click "Step 2".<br>
![Test](/exercises/ex3/images/30.png)<br>
3. Choose your Sales Model to start creating the Consumption Model. Click on the "MyCompany Sales" Model and click on "Step 3".<br>
![Test](/exercises/ex3/images/31.png)<br>
4. Choose an alias and click on "Create".<br>
![Test](/exercises/ex3/images/32.png)<br>
5. Add a new Fact Source. <br>
![Test](/exercises/ex3/images/33a.png) <br>
6. Add the KBA Dataset and click on "Step 2". <br>
![Test](/exercises/ex3/images/34.png) <br>
7. Give your data source an alias click on "Step 3". Then click on create.  <br>
![Test](/exercises/ex3/images/35.png) <br>
8. Add a new Dimension Source, choose "MyCompany Products" and click on "Step 2".  <br>
![Test](/exercises/ex3/images/38.png) <br>
9. Add an Alias and click on "Step 3". <br>
![Test](/exercises/ex3/images/39.png) <br>
Now you connect the Fact Sources to the Product Dimension.  <br>
![Test](/exercises/ex3/images/40.png) <br>
10. Click on the Fact Source and click on the "Expand"-Icon.  <br>
![Test](/exercises/ex3/images/41.png) <br>
11. Click on the Products and click the "Link"-Icon.  <br>
![Test](/exercises/ex3/images/42.png) <br>
12. Now you have to do the same thing for the other Fact Model. <br>
Click on the Sales Model and click on the "Expand"-Button. <br>
![Test](/exercises/ex3/images/43.png) <br>
![Test](/exercises/ex3/images/44.png) <br>
13. Click on the newly expanded Product Dimension and click on the "Link"-Icon. <br>
![Test](/exercises/ex3/images/45.png) <br>
![Test](/exercises/ex3/images/46.png) <br>
14. Click on "Create". <br>
![This is how the model should look now](/exercises/ex3/images/48.png) <br>

## Exercise 3.5 - Create (Calculated) Key Figures

1. Now add the Measures (BEV, Cabriolets, Sales Unit, All).  <br>
![Test](/exercises/ex3/images/49a.png) <br>
2. Next we add a calculated measure. Add a measure and choose "Calculated Measure".  <br>
![Test](/exercises/ex3/images/50.png) <br>
3. Create the calculation for market share. <br>
![Test](/exercises/ex3/images/51.png) <br>
Divide "Sales Unit" by "All Vehicles". And click "Save". <br>
![This is all measures that we just created.](/exercises/ex3/images/52.png) <br>
4. Now we have to create the attributes, the model will be filtered by (Brand, Group, Model, Orign).  <br>
![Test](/exercises/ex3/images/53.png) <br>
![Test](/exercises/ex3/images/54.png) <br>
![Test](/exercises/ex3/images/55.png) <br>
5. Go to the "General" sheet and check the "Allow public data access" box. Then click "Save".  <br>
![Test](/exercises/ex3/images/56.png) <br>
Now there should be a green check in the right upper corner. If there is a red cross something went wrong. Please check the failure message. <br>
![Test](/exercises/ex3/images/57.png) <br>
6. To create a story based on this Fact Model, you need to create a perspective. You can either do this by clicking the "+"-Button or by clicking on the "Data Preview". Click on the "Data Preview". <br>
![Test](/exercises/ex3/images/58.png) <br>
7. Create a table to base your perspective on by drag-and-drop.  <br>
![Test](/exercises/ex3/images/59.png)  <br>
8. Click "Save New" and enter a name. <br>
![Test](/exercises/ex3/images/60.png) <br>

9. Lastly we need to deploy the view. Click to open the perspective you just created.
![Open](/exercises/ex3/images/011.png)
10. Click on deploy.
![Deploy](/exercises/ex3/images/012.png)

## Summary

You've now created a consumption model to use in visualization.
If you want to, you can now go into the SAP SAC to create a story from the SAP DWC dataset. Just choose the DWC as a data source and create your visualization.
Continue to - [Exercise 4 - Create SAC Story (Optional)](../ex4/README.md)
