# Lab 3c - Host a web site in Azure functions

Now you have a good grasph of serverless computing. Why not take it a step further and try to build an entire web page in Azure Functions? 

I could see potential for running single page applications in function apps, where the backend API is also running in a function app. 

Unfortunately, this scenario is not something that Microsoft natively supports, but luckily some people have already done it. 

* Try to implement a simple HttpTrigger function that serves a html file store in the Azure Web App. [http://anthonychu.ca/post/azure-functions-serve-html/](http://anthonychu.ca/post/azure-functions-serve-html/) 