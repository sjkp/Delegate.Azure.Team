#Use Azure Storage and Service Bus Queues to Trigger Web Jobs
One of the main purposes of using Web Job is to make a more loosely coupled architecture, that is easy to scale out. 

With web jobs it is easy to move long running tasks or tasks that require a lot of computational resources out of the process hosting the web application. 

The simplest way to obtain the above is to use durable queues. Azure offers two types of Queues.

* Azure Storage Queues
* Service Bus Queues

##Azure Storage Queues vs Service Bus Queues
|Comparison Criteria|Azure Queues|Service Bus Queues|
|---|---|---|
|Scheduled delivery|**Yes**|**Yes**|
|Automatic dead lettering|**No**|**Yes**|
|Increasing queue time-to-live value|**Yes**<br/><br/>(via in-place update of visibility timeout)|**Yes**<br/><br/>(provided via a dedicated API function)|
|Poison message support|**Yes**|**Yes**|
|In-place update|**Yes**|**Yes**|
|Server-side transaction log|**Yes**|**No**|
|Storage metrics|**Yes**<br/><br/>**Minute Metrics**: provides real-time metrics for availability, TPS, API call counts, error counts, and more, all in real time (aggregated per minute and reported within a few minutes from what just happened in production. For more information, see [About Storage Analytics Metrics](https://msdn.microsoft.com/library/azure/hh343258.aspx).|**Yes**<br/><br/>(bulk queries by calling [GetQueues](https://msdn.microsoft.com/library/azure/hh293128.aspx))|
|State management|**No**|**Yes**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.entitystatus.aspx), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.entitystatus.aspx), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.entitystatus.aspx), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.entitystatus.aspx)|
|Message auto-forwarding|**No**|**Yes**|
|Purge queue function|**Yes**|**No**|
|Message groups|**No**|**Yes**<br/><br/>(through the use of messaging sessions)|
|Application state per message group|**No**|**Yes**|
|Duplicate detection|**No**|**Yes**<br/><br/>(configurable on the sender side)|
|WCF integration|**No**|**Yes**<br/><br/>(offers out-of-the-box WCF bindings)|
|WF integration|**Custom**<br/><br/>(requires building a custom WF activity)|**Native**<br/><br/>(offers out-of-the-box WF activities)|
|Browsing message groups|**No**|**Yes**|
|Fetching message sessions by ID|**No**|**Yes**|

https://github.com/Azure/azure-content/blob/master/articles/service-bus/service-bus-azure-and-service-bus-queues-compared-contrasted.md#technology-selection-considerations 

My main motivation normally picking Service Bus Queues, are support for long polling. 


##Question
Is there something we need to consider if we build a web job that uses a lot of system resources? 

##Example - Simple Azure Storage Queue Trigger
https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/HelloWorld


##Example - Simple Service Bus Queue Trigger
https://tfsserver.delegate.dk/tfs/DefaultCollection/JLauritzen/_versionControl#path=%24%2FJLauritzen%2FMain%2FSource%2FPowerBI.Map%2FAlertsJob%2FFunctions.cs&_a=contents

```
class Program
    {
        // Please set the following connection strings in app.config for this WebJob to run:
        // AzureWebJobsDashboard and AzureWebJobsStorage
        static void Main()
        {

            var config = new JobHostConfiguration();
            config.UseServiceBus();
            var host = new JobHost(config);
            
            // The following code ensures that the WebJob will be running continuously
            host.RunAndBlock();
        }
    }
``` 

```
public static void Alerts([ServiceBusTrigger("alerts")] string message)
        {
            // Use your account SID and authentication token instead
            // of the placeholders shown here.
            string accountSID = "<removed>";
            string authToken = "<removed>";

            // Create an instance of the Twilio client.
            TwilioRestClient client;
            client = new TwilioRestClient(accountSID, authToken);

            // Send an SMS message.
            Message result = client.SendMessage(
                "+4525807352", "+4530687942", message);

            if (result.RestException != null)
            {
                //an exception occurred making the REST call
                Console.WriteLine(result.RestException.Message);
            }
        }
```        