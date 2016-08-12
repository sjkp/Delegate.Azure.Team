#Lab 4 - Enterprise Integration Pack

In this lab we will play around with the powerful integration pack. 

[Help to get started with Enterprise Integration Pack](https://azure.microsoft.com/da-dk/documentation/articles/app-service-logic-enterprise-integration-transform/) 

The challenge is to setup a workflow that does the following. 

1) Runs on a 24 hours schedule
2) On every run, download an XML file into blob storage (the XML file is a extract from the danish CVR register with the daily updates)
3) Once the xml file is in blob storage we want to transform it
4) We want to extra every Company name and CVR that was updated and write them to another file in blob storage (image this step be replaced with an update to a CRM or ERP system)

