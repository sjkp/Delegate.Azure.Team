#Lab 1 - Getting Started with Azure Storage 

The challenge is to setup a workflow that does the following.

1. Triggers when a message arrives on a Azure Storage Queue (e.g. imaging a scenario where a web site writes to a queue)
2. Writes a file to an azure blob storage for each message recieved 
3. The file should contain the body of the queue message

You can use http://storageexplorer.com/ to add message to your queue and inspect the storage account