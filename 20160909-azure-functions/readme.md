#Azure Functions - Hands on Labs
This time we are going to dig into Azure Functions as they have recieved a fair amount of improvements since it went into public preview at build 2016. 
It is still in preview, so take that into consideration before you use it in production. I would guess for a GA around ignite (seems unlike with the current state, but then maybe later this fall)

 
```
Run code without thinking about servers.
Pay for only the compute time you consume.
``` 

Azure Functions aims to make it easier to build web job like functionality (as you don't have to create a app hosting plan, app service plan and storage accounts to get started).

Much like logic apps Azure functions supports triggers, and then it supports output. 

Azure functions is meant for event driven programming

It is part of the serverless movement which is getting a lot of traction 

## Hands on labs
The hands on labs today is a little different than last time as some of them are interconnected. 

* [Lab 1 - Getting Started With Azure Functions](lab1-getting-started-with-azure-functions.md)
* [Lab 2 - Process data from Blob Storage](lab2-process-data-from-azure-storage.md)
* [Lab 3a - Host a Web API in Azure Functions](lab3a-host-a-web-API-in-azure-functions.md)
* [Lab 3b - Process Images in Azure Functions, using nuget libraries](lab3b-process-images-in-azure-functions.md)
* [Lab 3c - Host a web site in Azure functions](lab3c-host-a-web-site-in-azure-functions.md)
* [Lab 4 - Use F# in Azure functions](lab4-use-F-sharp.md)
* [Lab 5 - Local development & continues integration](lab5-local-development-and-continues-integration.md)
* [Lab 6 - Integrate with Logic Apps](lab6-integrate-with-logic-apps.md)


## More samples
* [https://github.com/guitarrapc/AzureFunctionsIntroduction](https://github.com/guitarrapc/AzureFunctionsIntroduction)