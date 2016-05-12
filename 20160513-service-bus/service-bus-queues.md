# Service Bus Queues
The best queue solution in Azure. 

Should be the go to solution unless you specifically needs something that Storage Queues offers (smaller price tag, simpler deployment, larger queue size).

## Questions 
    1. What is a Queue
        a. Queues offer First In, First Out (FIFO) message delivery to one or more competing consumers.
    2. What can we use Queues for
    3. How does using more different solutions with individual SLA levels affect the overall SLA of an application [link](https://www.troyhunt.com/the-cloud-never-goes-down-azure-slas/)
    
![Queues](sb-queues-08.png)


## Sending Messages
Create a QueueClient (ensure that the queue is created). I recommend that you create the queue as part of the ARM template that you hopefully deploy your service bus namespace with. 

That way your code doesn't need the `Manage` permission level, which means that you can accidently delete your queues from your code. 

```CSharp
string connectionString =
    CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

Client.Send(new BrokeredMessage());
```

Use the [BrokeredMessage](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.aspx) class, will automatically serialize the input.

Interesting properties

* DeliveryCount
* MessageId
* Properties 
* ScheduledEnqueueTimeUtc
* SequenceNumber
* TimeToLive

Beware that the max size of the serialized message is 256 KB.

## Recieving Messages
Use the client from before to recieve the messages, preferably your recieving code is using a connection string that can only Read. 

```CSharp
// Configure the callback options.
OnMessageOptions options = new OnMessageOptions();
options.AutoComplete = false;
options.AutoRenewTimeout = TimeSpan.FromMinutes(1);

// Callback to handle received messages.
Client.OnMessage((message) =>
{
    try
    {
        // Process message from queue.
        Console.WriteLine("Body: " + message.GetBody<string>());
        Console.WriteLine("MessageID: " + message.MessageId);
        Console.WriteLine("Test Property: " +
        message.Properties["TestProperty"]);

        // Remove message from queue.
        message.Complete();
    }
    catch (Exception)
    {
        // Indicates a problem, unlock message in queue.
        message.Abandon();
    }
}, options);
```

