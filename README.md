# <h1>N-tier WLAMP Stack
# <h2>Load Balanced | Containerized | Logically Isolated | MSSQL w/ AD & WDC | Replicate on Demand
**_N-tier WebApp Stack on Skytap Cloud_**

The Tiers will all be logically isolated on 3 separate networks, for security. There will be a front end web server (internet facing), a backend application server (internal), and a database server (internal). 
The web network will connect the internet to the web server. the application network will connect the web server to the application server. The db network will connect the application server to the database server. \
_Web Tier_ \
The front end will be a HAProxy Loadbalancer that is internet facing. It will Load Balance traffic RoundRobin style to the 2 backend dockerized webapp containers. This will be layer 4 HAProxy Loadbalancing.\
_App Tier_ \
The Application tier will be a PHP 7.0 webapp running on Apache2 and hosted on Ubuntu 16.04. The frontend will have an ID and Name Form and a button. This webapp will be containerized with Docker. This entire instance will then be cloned by Skytap as a template and replicated in the same development environment. Traffic will then be loadbalanced between the two instance's docker containers. The front end will be a PHP web page (hosted on Apache) that listens (via button) for PHP POST requests and sends them to the backend PHP application server to be processed. The application server will process the POST request and push an API request to the cloud platform to replicate/clone the existing environment or an existing cloned template of the environment. Additionally, the PHP application layer will insert this event into MSSQL on the Database server. This will be containerized and hosted on a container host. The container host will be replicated/duplicated and have traffic load balanced between the 2 app instances. \
_DB Tier_ \
The database server will host MSSQL which is part of a Windows Domain Controller. It will Authenticate MSSQL access via Active Directory. This tier will host the records of the events pushed by PHP during API calls. 

# <h2>Environment

**DATABASE LAYER** \
MSSQL on Microsoft Server 2016. \
Windows Domain Controller on Microsoft Server 2016. \
- Host record of API calls to replicate environment

**APPLICATION LAYER** \
PHP on Linux (Ubuntu 16.04) as application logic. \
CONTAINERIZED (DOCKER) \
APACHE + HTML/CSS/JavaScript \
- PHP at the top of page to listen for GET/POST requests
- Button that hits backend PHP
- Listen for POST and push API to replicate environment (Clone, rename, start)
  -Insert event to DB 
  - Push link to newly created environment to the webpage UI

**FRONT END** \
- HAproxy Instance that frontends the webapp and loadbalances traffic between both container hosts.

# <h2> Setup
**NETWORK** 

1. Create 2 Automatic Networks
	1. Web Network
	1. App Network
1. Create 1 Manual Network (for Windows Domain Controller)
	1. DB Network

**VMs** 
1. Provision 4 VMs 

_WEB_
1. 1 Linux (Ubuntu 16.04)
	1. Deploy in Web Network		

_APP_

1. 1 Linux (Ubuntu 16.04)
	1. Deploy in App Network
		1. Container Host 

_DB_
1. 2 Windows Server 2016
	1. Deploy in DB Network
		1. WDC
		1. MSSQL

