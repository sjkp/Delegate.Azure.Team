# Lab 2 - Process data from Blob Storage

* Create a Blob trigger, which triggers when files are placed in the inbox container
* Every time a file is placed in the inbox container, copy it to another container, called output (imagine how we could do processing this way)
* Instead of a Blob trigger, create a new Queue trigger that reads from a queue called downloads
* Implement code that whenever a message appears on the queue downloads the html content of the Url contained in the queue message body, use `HttpClient`
* Save the html to Blob Storage (now you have an out of process way to download pages) 

## How does this work
Azure function ensures that the files in the inbox is processed exactly once, that is done using lock files located in XXXXX

If you want to reprocess the files you can delete the lock files 

If you container contains more than 10.000 files the trigger will no longer be instantanously but instead change to a polling mechanism. 