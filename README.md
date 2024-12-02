[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/teched2022-DA262)](https://api.reuse.software/info/github.com/SAP-samples/teched2022-DA262)

# DA262 - Modeling External and SAP HANA Data in SAP Data Warehouse Cloud

## Overview
This hands-on workshop will give you the opportunity to build a model in SAP Data Warehouse Cloud and SAP Analytics Cloud. Find out how the SAP Data Warehouse Cloud solution helps the line-of-business user to get the job done. Discover flexible connection features. Learn how you can access data from different sources. Create an extendable business semantic model in an agile way. Connect analytics and visualization components in the context of a data warehouse.

## Scenario
MyCompany provides fleet management services for large enterprise customers. They are organizing the procurement of cars from multiple manufacturers for their customers. They would like to understand where there is potential for additional car sales with their existing customer base. Their goal is to achieve a 20% market share. 

*Question to answer: Which brand has a market share lower than 20%?*  

* Learning Goal: Learn how to join messy data and create a multifact model.
* Time: 2-4 h
* Provided data tables: [TechEd_2022_DA262.zip](TechEd_2022_DA262.zip)
* Finished Product: Dashboard showing number of cars by manufacturer by county/state.

## Requirements
- Google Chrome
- Access to this GitHub repository
- Access to a Guided Experience system of SAP Data Warehouse Cloud tenant (if you don't have one yet, please follow the instructions of [exercise 0](/exercises/ex0/))
- This [ressource archive](/TechEd_2022_DA262.zip) will be required in [exercise 1](/exercises/ex1/) 

## Exercises
- [Overview on Exercises and Object Model](exercises/overview/) (also as [DA262.pdf](./DA262.pdf) for classroom training)
- [Exercise 0 - Preparations](exercises/ex0/)
- [Exercise 1 - Load data from SAP HANA Cloud](exercises/ex1/)
  - [Exercise 1.1 - Load JSON](exercises/ex1#exercise-11---load-json)
  - [Exercise 1.2 - Create Snapshot and inspect data](exercises/ex1/README.md#exercise-12---create-snapshot-and-inspect-data)
- [Exercise 2 - Map external car registration data to internal product master data](exercises/ex2/)
  - [Exercise 2.1 - Wrap Remote Table with Car Registration Data in Graphical View and Add Keys](exercises/ex2#exercise-21---wrap-remote-table-with-car-registration-data-in-graphical-view-and-add-keys)
  - [Exercise 2.2 - Create an Intelligent Lookup between Car Registration View and Product Master](exercises/ex2#exercise-22---create-an-intelligent-lookup-between-car-registration-view-and-product-master)
- [Exercise 3 - Preparing Analytic Data Consumption via the Business Layer](exercises/ex3/)  
  - [Exercise 3.1 - Create a Dimension for Product](exercises/ex3/README.md#exercise-31---create-a-dimension-for-product)
  - [Exercise 3.2 - Create Analytical DataSet for My Company Sales](exercises/ex3/README.md#exercise-32---create-analytical-dataset-for-my-company-sales)
  - [Exercise 3.3 - Create Analytical Dataset for Car Registration Data](exercises/ex3/README.md#exercise-33---create-analytical-dataset-for-car-registration-data)
  - [Exercise 3.4 - Create Multifact Consumption Model that brings together the numbers for car registrations and internal sales](exercises/ex3/README.md#exercise-34---create-multifact-consumption-model-that-brings-together-the-numbers-for-car-registrations-and-internal-sales)
  - [Exercise 3.5 - Add key figures](exercises/ex3/README.md#exercise-35---add-key-figures)
- [Exercise 4 - Create an SAC Story (optional)](exercises/ex4/)
  - [Excercise 4.1 - Show Sales Data in SAC](exercises/ex4/README.md#excercise-41---show-sales-data-in-sac)
  - [Excercise 4.2 - Show Marketshare in SAC](exercises/ex4/README.md#excercise-42---show-marketshare-in-sac)
  

## Extended Scenario
- [TechEd 2022 DA160 - Explore SAP Data Warehouse Cloud from A to Z](https://github.com/SAP-samples/teched2022-DA160)
- [All TechEd 2021 materials on SAP Data Warehouse Cloud](https://blogs.sap.com/2021/10/21/sap-data-warehouse-cloud-at-sap-teched-2021/)

## Disclaimer
Some user interface elements may differ from the screenshot used in the exercise.
Be aware that some of the exercises are based on each other, therefore flagged as mandatory. Other parts can work based on prebuilt parts to save you some time, marked as optional. This gives you the flexibility to decide which exercises you would like to focus on.

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
