--Introduction--

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


--Design--

-ETL-

1. We used pipelines to perform simple copies and to loop through values to call the EA APIs to copy to CSV and JSON files in the Lakehouse. 

2. We used pipelines to copy these files into staging tables in the Warehouse.

3. We used Stored Procedures in the Warehouse to model this data into Dimensional Models

4. We used Pipelines again to copy the data form the dimensional models back to the Lakehouse for ingestion to the Notebooks

-Data Science-

1. We used Jupyter Notebooks to prepare the data for modelling, using the Prophet library to predict future water levels at each measurement station for the proceeding 5 days.

2. The notebook can be scheduled to rerun with refreshed water level data.


-Power BI Reporting-

1. We used Microsoft Fabric to construct a fact and dimension-based data model.
   
2. We used PowerBI to visualise both the actual data and model's predictions data.


--Future Work—-

Due to time constraints, there were a number of avenues that were left unexplored. Below are a few ideas that we will be exploring in due course:

- Incorporating a more robust prediction method by inputting rainfall predictions
- Investigate usage of more data sources such as Tweets and further weather data
