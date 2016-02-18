#App Service Enviroment
App Service Enviroment are for customers that want to use Azure App Services, but want to be able to host their site in an virtual network they control. This gives them more power to control access to the web sites, but it also comes at a premium price. 

Another reason to choice app service environment are if you want to have hardware dedicated to your subscription that runs the apps.

** One pretty big downside with App Service Enviroment, at the moment are that they only support V1 virtual networks ** 

https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-intro/

##Networking setup
The app service enviroment consists of one front end pool of machines that does SSL termination and routing and loadbalacing. 
Besides the frontend pool it can contain one to three backend pools that can be configured with different machine sizes. 

A total of 55 compute resources can be assigned to a App Service Environment. Due to fault tolerancy not all compute resource are available. 

The minimum footprint is 2 compute resources in the frontend pool and 2 in the backend pool. Which explains the high price. 

###Task 1 - When to use App Service Enviroments? 


###Resources
* https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-network-architecture-overview/
* https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-an-app-service-environment/