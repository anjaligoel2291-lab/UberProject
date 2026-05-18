# UberProject
Uber end to end project - Azure and Databricks
-- Architecture of end to end project
-- exaplin all the steps and diagrams
-- booking a ride from app with diagram
-- show events in event hub
-- Add code files in a new folder
-- Azure pipeline explaination
-- Star schema explanation
-- Solve business problems

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/b521a457-a907-4aa3-95b7-a6431a1e153c" />



Data Sources : 
Webapp to get real time rides 
Github for mapping files and historical bulk rides


**Medallian Architecture**

Bronze Layer :

1. Azure Event Hub - Created Azure Event hub namespace and Event hub named "ubertopic"

   Created two access policies at event hub level: Send Policy and Listen Policy

   Webapp to EventHub :

   Prerequisites: Azure, Python, Vs code, Event hub namespace

   In VS Code : Create .env file
               CONNECTION_STRING = "Paste From Send Policy"
               EVENT_HUBNAME = "ubertopic"
       These variables are called in Connection.py

   If we go to the webapp, and click on Book a ride, it will send an event to Event Hub
   
   <img width="1388" height="432" alt="image" src="https://github.com/user-attachments/assets/c2616dfa-32e0-4e53-9f9a-3a82b72623b6" />

2. Azure Data Factory - To load mapping files and historical rides data.

   Github -> ADF -> ADLS

   Created ADF and Strorage Account

   ADF : Linked Services - HTTP for Github and ADLS Gen2 for Data Lake
         Datasets - HTTP - Relative path
       Created a file - file_array.json to implement metadata driven approach for copying all files dynamically

     ADF -
         Lookup Activity -> For each and copy activity
         Lookup Activity reads file_array.json from ADLS
         Foreach gets the file names
         Copy activity copies the looped file data into raw folder in ADLS using parameter to output the file name dynamically.


3. Databricks - 
         
   
