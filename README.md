# MS Fabric Flood Predictions

This is the repository for our team's entry to Fabric Hacktogether 2024.

Team members are:
- Lilith Barca
- Peter Cooke
- Stuart Thompson


## Introduction

For many people across the world, risk of flooding is a yearly concern, impacting both home life and work life when roads become blocked off and streets are flooded. Floods are a growing problem, with climate change and a reduction in green space increasing the risk of extreme weather events and water runoff.

Our idea for this hackathon was to use the range of functionality within Fabric to surface river level and rainfall data to allow a holistic view of potential future flood risk within a given area. This could then incorporate other data sources such as news reports or Twitter/X posts.

We aimed to build a flood prediction system using input from the UK Environment Agency (EA) public APIs. The dataset contains:
- Flood Warnings / Events
- Flood Area mapping data
- Stations for measuring river height and flow levels, rainfall and temperature

For the purposes of this project most of the data ingested is static, with flood warnings and station readings updating daily.

We have created:
- Pipelines to ingest the data to the Lakehouse and Warehouse
- Stored Procedures to transform the data into a dimensional model
- Notebooks to build the ML model and predictions
- Power BI report to present the results


## Design

![alt text](https://github.com/methodsanalytics/ma_fabric_hack_together_2024/blob/main/Flood%20Predictions%20Diagram.png)

### ETL

1. We used pipelines to perform simple copies and to loop through values to call the EA APIs to copy to CSV and JSON files in the Lakehouse. 

2. We used pipelines to copy these files into staging tables in the Warehouse.

3. We used Stored Procedures in the Warehouse to model this data into Dimensional Models

4. We used Pipelines again to copy the data form the dimensional models back to the Lakehouse for ingestion to the Notebooks

### Data Science

1. We used Jupyter Notebooks to prepare the data for modelling, using the Prophet library to predict future water levels at each measurement station for the proceeding 5 days.

2. The notebook can be scheduled to rerun with refreshed water level data.


### Power BI Reporting

1. We used Microsoft Fabric to construct a fact and dimension-based data model.
   
2. We used PowerBI to visualise both the actual data and model's predictions data.

### Power Automate flow

1. We used Microsoft Power Automate to build a flow to send emails when the pipelines run
   
2. We used Copilot to help build the flow and have added a screenshot of the Copilot responses to the repository

### Future Work

Due to time constraints, there were a number of avenues that were left unexplored. Below are a few ideas that we will be exploring in due course:

- Incorporate a more robust prediction method by inputting rainfall predictions, and potentially other regressors such as measures of how built up an area is, rainfall of upstream areas, how dry the ground is likely to be, and other factors that can impact flood risk.
- Calculate potential area of the flood, and how that would impact road traffic and travel times to key destinations.
- Introduce other data sources to enrich the information shown in the dashboard, such as links to news articles and images of ongoing floods.
- Create a chatbot within Azure OpenAI to allow querying of the data in plain language with a RAG system.
- Generate automatic alerts and reports to be triggered by a threshold level of risk tailored to each measurement station.



## Recreating the project

1. In a Fabric Workspace, create a Lakehouse and Warehouse
2. To build the Warehouse tables and stored procedures run the DDL here DataStorage/Warehouse DDL.txt
3. Create a HTTP connection named 'EA Flood Monitoring' pointing to http://environment.data.gov.uk/flood-monitoring/
4. Create a HTTP conneciton named 'EA Flood Data' pointing to https://environment.data.gov.uk/flood-monitoring/id/
5. Use the files in the 'Pipelines', 'Notebooks', 'Reports' and 'Environments' folders to create the objects in the workspace
