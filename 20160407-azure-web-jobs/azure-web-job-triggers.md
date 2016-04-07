#Azure Web Jobs - Trigger Types
The power of Azure Web Jobs is in knowing how to use the different trigger/output types.  

Using them correctly can save you from writing a lot infrastructure code, and focus solely on the business logic.

So far we have seen QueueTrigger and ServiceBusTrigger - besides those some of the other commonly used Triggers/Output types are 

* BlobTrigger
* Table
* Blob
* Queue


##Blog Trigger
https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/BlobOperations/Functions.cs


##Other Triggers
The triggers mention in the previous section comes with the nuget `Microsoft.Azure.WebJobs` but the Web Job team have also create other great trigger/output types

* ServiceBusTrigger / ServiceBus - nuget package: `Microsoft.Azure.WebJobs.ServiceBus`
* TimerTrigger - nuget package: `Microsoft.Azure.WebJobs.Extensions`
* FileTrigger/File - nuget package `Microsoft.Azure.WebJobs.Extensions`
* SendGrid - nuget package `Microsoft.Azure.WebJobs.Extensions`
* ErrorTrigger - nuget package `Microsoft.Azure.WebJobs.Extensions`
* WebHooks - nuget package `Microsoft.Azure.WebJobs.Extensions.WebHooks`
* DocumentDb 
* NotificationHub


###WebJobs.Extensions
If you are interested in using any of these trigger see the docs in https://github.com/Azure/azure-webjobs-sdk-extensions 

###Question
Does any of the triggers mention here seems interesting to you? 

Do you have ideas for custom triggers, that we could build? 



###Question
How do e.g. a TimerTrigger makes sure that it is not activated on multiple instances if we are running with serveral servers? 


What if we don't mind having the job run on multiple instances (e.g because we use deployment slots and they should each have their own job). 
```
config.HostId = args[0];
```