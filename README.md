# DA262 - Modeling External and SAP Software Data in SAP Data Warehouse Cloud

## Description
This repository contains the material session for *DA262 - Modeling External and SAP Software Data in SAP Data Warehouse Cloud* of SAP TechEd 2022. In the session, a fictional fleet management services company is combining their internal rental data with externally available car registration data to analyze their share in the overall market and identify attractive models & brands in which that market share can be boosted. To participate, you just get yourself a free trial account and follow along. 

## Overview
This hands-on workshop gives you the opportunity to build an end-to-end data integration & reporting scenario using SAP Data Warehouse Cloud and SAP Analytics Cloud. You'll learn load data into SAP Data Warehouse Cloud from internal sources, combine it with external data from SAP Data Marketplace, prepare a data model, combine data sets, create an analytical model and finally use it in your reporting in SAP Data Warehouse Cloud

* Goal: Learn how to join messy data without keys from multiple sources.
* Time: 2-4 h
* Provided data tables: (link to be added)
* Finished Product: A dashboard showing market share by manufacturer & country
* Tags: #dwc #IntelligentLookUp #IL #DataMarketplace #BusinessLayer #DataMarketplace #SAP

## Scenario
_MyCompany_ provides fleet management services for large enterprise customers. They are organizing the procurement of cars from multiple manufacturers for their customers. They would like to understand where there is potential for additional car sales with their existing customer base. Their goal is to achieve a 20% market share. Today's question to answer is, for which brands is the share under the target share. 

## Pre-Requisites
- Google Chrome
- Access to this GitHub repository
- Access to a SAP Data Warehouse Cloud tenant ** exercise link how to get there**
- The files in the download folder [DA262_Resource.zip](DA262_Resource.zip) from this GitHub Repo (xxx)

## Exercises

- [Exercise 0 - Preparations (optional, if you  already have access to a DWC tenant)](exercises/ex0/)
- [Exercise 1 - Get external Data German Car Sales Data](exercises/ex1/)
    - [Exercise 1.1 - via Data Marketplace (not available in Learning Experience systems)](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Exercise 1.2 - via external connection](exercises/ex1#exercise-12-sub-exercise-2-description)
- [Exercise 2 - Upload car manufacturer data](exercises/ex2/)
- [Exercise 3 - Combine two data sets](exercises/ex3/)
- [Exercise 4 - Create a Consumption Model in the Business Layer](exercises/ex4/)  
- [Exercise 5 - Create a SAC Story (optional)](exercises/ex4/)  

Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).

## Disclaimer
Your screen shots may look different than those in the exercises; they may contain additional content, depending on what other attendees have entered.
Some user interface elements may differ from the screenshot used in the exercise.
Exercises
Be aware that some of the exercises are based on each other, therefore flagged as mandatory. Other parts can work based on prebuilt parts to save you some time, marked as optional. This gives you the flexibility to decide which exercises you would like to focus on.

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2022 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
