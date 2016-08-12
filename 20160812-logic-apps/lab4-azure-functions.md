#Lab 4 - Azure Functions

Sometimes there is not a connector for the task you want to do, and writing an API app might be too big of a hammer for the task. Fortunately in that case you can use an Azure function to do some custom code. 


The challenge is to setup a workflow that does the following: 

1) Triggers on a schedule (lets imaging we are building some kind of batch job, also a scheduled trigger we can manually trigger so it makes testing a lot easier)
2) Executes an Azure function the Azure function could do what ever, but for the sake of simplicity just have it return the current date time
3) Append the time to a file in blob storage 
