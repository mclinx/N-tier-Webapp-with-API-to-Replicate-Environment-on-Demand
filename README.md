# N-tier-Webapp-with-API-to-Replicate-Environment-on-Demand
N-tier Webapp Stack on Cloud

DATABASE LAYER
+MSSQL on Microsoft Server 2016. 
+Windows Domain Controller on Microsoft Server 2016. 
- Host record of API calls to replicate environment

APPLICATION LAYER
+PHP on Linux (Ubuntu 16.04) as application logic.
+CONTAINERIZED (DOCKER)
- Listen for POST and push API to replicate environment (Clone, rename, start)
  -Insert event to DB 
  - Push link to newly created environment to the webpage UI

FRONT END
+APACHE HTML/CSS/JavaScript
- PHP at the top of page to listen for GET/POST requests
