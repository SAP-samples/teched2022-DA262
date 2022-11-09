# Exercise 2 - Map external car registration data to internal product master data

One of the challenges when working with external data is that they regularly don't quite fit 100% with your internal data, making joint reporting of external and internal data together quite difficult. 

In the case at hand, the brand names used by the external data set for car registrations do not fit 100% to your brand names used in your product master data RT_MY_COMPANY_PRODUCT. Also some of the model names differ. Examples are: 

Brand name in external data set | Brand name in product master | Issue 
---|---|---
| BMW   | BMW     | none    |
| CITROEN | CITROEN | none | 
| NISSAN | Nissan | upper vs. lower case | 
| TOYOTA | Toyota | upper vs. lower case | 
| Volkswagen VW     | VW       | different brand name      |
| MERCEDES | Mercedes-Benz | different brand name | 


This leads to the situations that simply joining the car registration data for car models with the product master data on these car models will not lead to the desired result. Luckily, SAP Data Warehouse Cloud has an own operator to help in this situation, namely the [Intelligent Lookup](https://blogs.sap.com/2021/12/21/one-stop-shop-to-intelligent-lookup-in-sap-data-warehouse-cloud/) operator. It helps to bring data together that "almost" matches, but not quite - just as in our situation here. It does this by formulating a series of match rules that define when certain entities (in our case brand names) match to each other. In the background, Intelligent Lookup uses the rules to build up a match table of IDs used on either side denominating the same thing (here: brands). By help of this hidden "pairing table" the two "unjoinable" tables now become joinable.  

In order to make use of the Intelligent Lookup, we need to ensure that the participating entities (i.e. in our case car registration table and product master view satisfy certain conditions: remote tables need to be wrapped in views and all entities need to have key definitions. So this is what we are going to do: 

- [Exercise 2.1 - Wrap Remote Table with Car Registration Data and Add Keys](#exercise-21---wrap-remote-table-with-car-registration-data-in-graphical-view-and-add-keys)
- [Exercise 2.2 - Create Intelligent Lookup between Car Registration View and Product View](#exercise-22---create-an-intelligent-lookup-between-car-registration-view-and-product-master)

## Exercise 2.1 - Wrap Remote Table with Car Registration Data in Graphical View and Add Keys
Since Intelligent Lookup requires key columns in the participating entities, let's wrap the car registration table in a view and set its key columns:

1.	Go to the Data Builder. If prompted, choose your space from [exercise 1](../ex1/). 
2.	Click on "New Graphical View". <br> ![New Graphical View](/exercises/ex2/images/004.png)
3.	From the repository pane on the left, drag & drop your table *RT_GERMAN_CAR_REGISTRATION*. <br> ![Data Market Place](images/drag_table.jpg)
4. Choose the table node *RT_GERMAN_CAR_REGISTRATION*. In its context pad, choose the function symbol to create a calculation node. <br> ![add calculation node](images/add_calc_node.jpg)
5. In the properties panel of the calculation node, create a new calculated column by choosing Plus-sign > Calculated Column. This column will later play a role as ["pairing column"](https://blogs.sap.com/2021/12/21/intelligent-lookup-faq/#WhatIsAPairingColumn) of the Intelligent Lookup. 
<br> ![add calculated column](images/add_calc_column.jpg)
6. In the empty panel of the new calculated column, fill these fields:
    - Business Name: *ModelBrand*
    - Technical Name: *ModelBrand*
    - Data Type: *String*
    - Length: *5000*  
      **Note: This length is important. Please do not use a shorter length**
    - Expression (choose *Validate* to confirm correctness): <code>CONCAT(CONCAT(model,' ',),marke)</code>
      <br>**Note: The length changes when validating, make sure it is 5000**
    

    <br> ![configure calculated column](images/configure_calc_column_modelbrand.jpg)

8. Choose the calculation node and add a projection node in the context pad. Projection nodes allow exlusion of columns (here: *release_id*) and renaming of columns (here: from *id* to *Product_Id*). <br> ![Add projection node](images/add_projection_node.jpg)
9. In the details panel of the projection node, choose column "release_id", open the three dots and choose *Exclude column*. <br> ![Exclude Column](images/exclude_release_id.jpg)

10. Inspect your data choosing the preview icon in the context pad of the projection node. If you look closely, you see that the car registration data contains a summary number "All models" that simply sums up the individual registration numbers of individual models of a given brand. 
<br> ![data preview w summary numbers](images/view_sum_all_models.jpg)

11. In order to avoid double counts during reporting, we need to filter these records out.  
We create a new filter node by choosing the filter icon on the context pad of the projection node
<br> ![create filter node](images/view_create_filter_node.jpg)

12. In the properties panel of the filter node, we set the filter expression to <code>model != 'All Models'</code>  
Check the data preview panel that these records are indeed filtered out
<br> ![Filter node settings](images/filter_node_props.jpg)

13. Now let's do final adjustments on the last node. For once, choose the final node and select column *Time*. Select the three dots to open its context menu. Choose the menu entry *Set as key* to make time a key column of the view. <br> ![set as key](images/set_key.jpg)
14. Also turn *model* and *marke* (German for "brand") into key columns. 
    **Note: It is important to have all three keys correctly set**

15. In the properties panel of the final node, change drop-down for Semantic Usage to *Analytical Dataset* and toggle *Expose for consumption* to ON. This turns the current view into a multi-dimensional artefact that can be consumed directly by SAP Analytics Cloud. In order to fully configure the artefact, drag & drop columns *all*, *bev* and *cabriolet* to section *Measures*
<br> ![ADS settings](images/view_ads_settings.jpg)
12. Choose *Save* in the action bar. <br> ![save button](images/save_button.jpg)
13. In the prompt, set technical and business name to *V_GERMAN_CAR_REGISTRATION*. <br> ![Save as](images/Save_view.JPG)
14. Deploy the view by choosing *Deploy* in the action bar. 
<br> ![deploy button](images/deploy_button.jpg)

We have now generated all runtime artefacts in the HANA Cloud system underneath SAP Data Warehouse Cloud to report the external data on car registrations also in SAP Analytics Cloud. The only problem is that the models & brands that the data refers to isn't quite aligned with our internal product master. This is what we will be fixing now.  

## Exercise 2.2 - Create an Intelligent Lookup between Car Registration View and Product Master

1.	In Data Builder, click on "New Intelligent Lookup". 
<br> ![Data Builder - New Intelligent Lookup](images/il_create_new.jpg)

2.	From the repository pane on the left, drag view *V_GERMAN_CAR_REGISTRATION* onto the landing zone for *Input*. Define the column *ModelBrand* as a pairing column by dragging it into section *Pairing Column* from the column list in the detail pane. The error notification on the input node will disappear once this configuration is made.  
The configuration of a *pairing column* ensures that the product ID that was identifed for a given model-brand combination is reused for different dates. To take a concrete example, once *PEUGEOT+108* and *Peugeot+108* are identified as meaning the same model-brand combination, then this information is reused across different records of the car registration view, i.e. across the car registration records for January, February etc. [This FAQ entry](https://blogs.sap.com/2021/12/21/intelligent-lookup-faq/#WhatIsAPairingColumn) explains the background for this in more detail. <br> ![Configure Inpput Table](images/il_configure_input_view.jpg)

 3. From the repository pane on the left, drag view *V_MY_COMPANY_PRODUCT* onto the landing zone for *Lookup*. Define the column *Product_Id* as a return column by      dragging it from the column list onto the section *Return Column*. The error notification on the lookup node will disappear once this configuration is made.   
 A return column is a column that is added to the input view, but its value is "looked up" from the matching entry in the lookup view. 
 <br> ![configure lookup view](images/il_configure_lookup_view.jpg)

 4.	Define a first rule to create initial mappings.  
 Intelligent Lookup differentiates between exact match rules and fuzzy match rules. Exact match rules work roughly like a join and make exact comparisons of field names. Unlike standard joins, they can be graceful about upper-lower case spellings though (advanced setting).  
 Select the rule node and check its detail panel. Via drag & drop, make a mapping between the model column of the input view (car registrations) and the Model_Name column of lookup view (product master). Likewise, make a mapping between the column *marke* (German for *brand*) of input view and the column *brand* of lookup view.  
 In section *Advanced Settings*, uncheck *Case-sensitive*.  
 Through this configuration, you are telling Intelligent Lookup to lookup the respective product master for each record of the car registration by doing a case-insensitive comparision of model and brand fields. In the best of cases, only a single lookup record matches this criterion. Then the match is made, stored & reused for every record in the car registration dataset with the same value of *ModelBrand*. That means also across e.g. car registrations for different points in time, for the same model & brand combination. If more than one lookup record is found, the system will classify this as multiple match. If no lookup record can be found with this rule, the system will classify the record as unmatched. 
 <br> ![Configure first IL rule](images/il_configure_exact_rule.jpg)

 5. Let's see what happens on deployment and run. Choose *Deploy* in the action bar to start deployment. 
 <br> ![IL Deploy](images/il_deploy.jpg) 

 6. In the prompt, give the operator the name *IL_GERMAN_CAR_REGISTRATION*.
<br> ![IL save dialog](images/il_save_prompt.jpg)
7. Once deployment is done (which can take 1-2 minutes), run the operator.
<br> ![Run Intelligent Lookup](images/il_run.jpg)
8. Once the run is successful (which again can take 30sec to one minute), start inspecting the results. 
The first thing to realize is that out of all 321 records of the car registration view, 56% could be matched successfully with this rule while 44% couldn't.
<br> ![IL run result](images/il_run_result_rule_1.jpg)
9. To inspect the results in more detail, open the data preview of the rule and inspect the "buckets" for matched & unmatched records of the car registration dataset. Let's first inspect the matched records by opening the preview via the context pad of the rule and choosing the matched tab.   
When inspecting the results in detail, you realize that Intelligent Lookup did what your standard join would not be able to do: join over columns in a case-insensitive way. In the marked line, the rule identified POLESTAR/1 as being the same as Polestar/1 and thus "matched" the car registration of that model to the respective product master record (Product Id = 1055).
<br> ![IL match results rule #1](images/il_rule1_matched.jpg)
10. Now let's move on to the unmatched records, i.e. those car registration records where the rule couldn't quite figure out which product they belong to in the lookup view. Let's e.g. zoom in on the set of records for *ModelBrand* value A1 S1 AUDI.  
We first set a filter on the product master by clicking on the column header and setting a filter value
<br> ![set filter audi](images/il_rule1_unmatched_filter_audi.jpg)

11. When we now look at the car registration data on the left and the filter product master for *AUDI* on the right, we directly realize what is wrong: the record circuled in red has indeed brand = AUDI, but our product master only knows model *A1*, but the car registrations happened on Audi's model A1 S1. Only domain experts can decide, if this indeed is the same product or not.  
<br> ![IL unmatched records](images/il_run_result_rule_1_unmatched.jpg)

12. Intelligent Lookup allows business users now to take a decision here. Mark both entries and click the *Match* button. This will tell the system that the two records are indeed meaning the same model and transfer the record to the *Matched* tab. 
<br> ![IL Manual Match Audi A1](images/il_manual_match_audi_a1.JPG)
12. Since we don't want to take all these manual decisions one by one, we choose to simplify our life and automate the decision making. To that end, our best bet is to be a bit more relaxed about our matching rule logic and do a fuzzy comparison of the model & brand fields. Intelligent Lookup allows to do this by creating a follow-up rule. So let's add such a follow-up rule by clicking the first rule and selecting *Add rule for Unmatched Records* from the context pad.  
**Note:** If you are interested to understand the difference between the two rule types (i.e. *Add Rule for Multiple Matches* and *Add Rule for Unmatched Records*), check [this FAQ article](https://blogs.sap.com/2021/12/21/intelligent-lookup-faq/#DifferenceBtwNewAndRefineRules). 
<br> ![IL add unmatched rule](images/il_add_rule_for_unmatched.jpg)
12. This time, we parameterize the rule as fuzzy rule and choose to compare the model & brand names in a fuzzy fashion. To this end, we set the *Match Strategy* drop-down to *Fuzzy Match* and add the match columns *model* and *marke* (German for "brand") of the input view and *Model_Name* and *brand* of the lookup view. You will need to use the three dots in section *Match Columns* to define the participating columns. All other settings keep their default values.  
<br> ![IL configure fuzzy rule](images/il_configure_fuzzy_rule.jpg)
13. Deploy the operator again.
<br> ![Deploy IL](images/il_deploy.jpg)
14. Once deployed, start a new run.
<br> ![Run IL](images/il_run.jpg)
15. Now let's inspect the results. The new rule takes those 44% of car registration records that the first rule couldn't make heads or tails of and triages them into distinct buckets: 
- 0% were identifed with such certainty that no human intervention is required ("matched")
- 13% of the records are matched such that that the rule is pretty sure, but suggests a human review (i.e. the fuzzy match metric came out at >80% and <100%)
- 3% are "multiple matches" where more than one lookup record was found and a domain expert needs to make a final call 
- 27% of the records can still not be matched .
<br> ![IL run results rule 2](images/IL_run_result_rule_2.jpg)
16. Let's use the data preview again to better understand what's happening here. Let's first turn to what Intelligent Lookup calls "Review" records. These are records where the fuzzy rule could indeed find single matches in the 80% to 100% fuzzy metric bracket, but since they are not 100%, a human user should review their validity.  
If you look closely at the values, the rule could successfuly match MERCEDES/GLS to Mercedes Benz/GLS as well as SKODA/ENYAK to Škoda Auto/ENYAK. This is exactly what we were hoping for and we can thus select those lines and click *Confirm* to push them over to the *Matched* bucket.
<br> ![IL fuzzy result review](images/il_fuzzy_rule_result_review.jpg)
17. If we continue on to the multiple matches, we find a some interesting artefacts in the data. For example, MERCEDES/A-KLASSE fuzzily matches to all Mercedes-Benz models on the right. While Mercedes-Benz/A-KLASSE has the highest fuzzy score, the other models like B-KLASSE and C-KLASSE are fuzzily too similar for a machine intelligence to take a final decision. Users can select the respective entries and choose to manually take the decision. This is still manual work, but by triaging the irrelevant product master records from the highly relevant ones, the domain expert receives a huge support boost by the system.
<br> ![IL multiple match result fuzzy](images/il_fuzzy_rule_result_multiple.jpg)
18. Finally there are still some unmatched cases in the data, so let's turn to them now. Evidently, none of the lines could be matched through those two rules, but why is this? If we work ourselves through the data a bit we realize different root causes: 
- Car registrations on many up-market brands like PORSCHE, JAGURA, CADILLAC, TESLA, FERRARI, LAMBORGHINI, MASERATI and LEXUS remain unmatched because there is simply no product master for them. How could there be, since our business is about fleet management, not luxury car rental. A domain expert needs to choose to either filter them out or to match them to a new "luxury model" that could be added to the product master. Again, this is entirely a business decision by a domain expert.
- And then there are car registrations listed like MERCEDES/SONSTIGE or Volkswagen VW/SONSTIGE. "Sonstige" is German for "others", meaning that the data source couldn't quite assign them to any of **their** product master entries and thus subsumed them under a catch-all term "others". Again, obviously this does not allow for a matching to our product master for purely business & data reasons that subject matter experts need to decide how to deal with 
<br> ![IL fuzzy unmatched results](images/il_fuzzy_rule_result_unmatched.jpg)
19. Let's finally turn to the output of the Intelligent Lookup, so let's click on the right-most node in the canvas. In the details pane, you can apply some settings like include/exclude of records that are in review or unmatched status. We can set default values, when no *Product Id* could be identified (click the three dots to the right of column *Product Id*) in which case it would make sense to include an *Unmatched Record* column to distinguish default product id values from real ones that might happen to have the same value. 
When we look at the data preview, we find the same 321 car registration records as in the input view *V_GERMAN_CAR_REGISTRATION*, but now we have "looked up" for which *Product Id* they are and added that as an own column. This additional information will come in handy when we do our analyses for those models  later in the process.   
Technically, the Intelligent Lookup is just a join of those two tables, but with a hidden helper table in the background to identify which Ids used in the car registration data set match to which ids of the product master. This means that even though it does quite some magic, it can still be consumed like any ordinary view for modelling or reporting. 
<br> ![IL output node](images/il_output_view.jpg)

## Summary

You've now identified for the car registration data which product master record they belong to. This will become important in the next exercise since now both the internal data (*RT_MY_COMPANY_SALES*) and the external data about car registrations now leverage the same product master. In the next exercise, we'll build a multi-fact model that leverages this shared product dimension, thus allowing both data sets to be analyzed along the same dimension for drill-down. 

Continue to - [Exercise 3 - Create a Consumption Model in the Business Layer](../ex3/README.md)
