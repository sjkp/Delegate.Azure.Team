#Web Job Architecture

##What is Web Jobs
Web jobs are jobs that run inside your Azure App Service
* Run out-of-process from the web site
* Can run: ondemand, continuously or on a schedule
* The can be programmed in any of the following languages
    * .fsx (using the F# fsi.exe interactive compiler)
    * .cmd, .bat, .exe (using windows cmd)
    * .ps1 (using powershell)
    * .sh (using bash)
    * .php (using php)
    * .py (using python)
    * .js (using node)
    * .jar (using java)
    * project.json (using Dnx - [details here](http://ahmelsayed.com/running-dnx-based-webjobs))
* You get a nice mini portal, to monitor your job executions in the KUDU portal
    
###Question
How much does it cost to use web jobs? 
    

##How to deploy web jobs
Web Jobs are deployed together with the Web Application (or they can be deployed with an empty web application)

The KUDU portal is responsible for picking up the web jobs and starting them. It looks for files in `wwwroot\App_Data\jobs\<job-type>\<your-job-name>`

Job type can be one of the following: 
* continuous 
* triggered

Trigger - run the job every time an API to start the job is called or a schedule is reached.
Continuous - KUDU makes sure that the job is always running (job should have a while loop but when it goes down we bring it back up).

In `<your-job-name>` it loosk for job files in the following order
* Per file type we look first for a file named: run.{file type extension} (for example run.cmd or run.exe).
* If it doesn't exists for all file types, we'll then look for the first file with a supported file type extension.
* The order of file types extension used is: .cmd, .bat, .exe, .ps1, .sh, .php, .py, .js.
* The recommended script file to have in your job directory is: run.cmd.
* Note: We'll only look for a script under the root directory of that job (not under sub directories of it).
* Note: make sure .bat/.cmd files don't include the UTF-8 BOM (inserted by some editors such as Visual Studio by default), which can break things!


##Demo in C-Sharp
```
class Program
    {
        // Please set the following connection strings in app.config for this WebJob to run:
        // AzureWebJobsDashboard and AzureWebJobsStorage
        static void Main()
        {            
            var host = new JobHost();
            // The following code ensures that the WebJob will be running continuously
            host.RunAndBlock();
        }
    }

```

##Logging 
###Continuous Web Jobs
For continuous WebJobs - Console.Out and Console.Error are routed to the "application logs", they will show up as file, blob or table storage depends on your configuration of the application logs (similar to your Website).

Also the first 100 lines in each invocation will also go to the WebJob log file (to ease debugging pain when the WebJob fails at startup) accessible using the Azure portal (but also saved on your site's file system at data/jobs/continuous/jobName).


###Triggered
For triggered WebJobs - Console.Out/Console.Error are routed to the WebJobs specific run log file also accessible using the Azure portal and stored at data/jobs/triggered/jobName/runId.

Console.Out is treated (marked) as INFO and Console.Error as ERROR.

###Customized logging
You can also use add a parameter `TextWriter` to you job function and get access to the log writer as it has been configured

```            
    class Program
    {
        // Please set the following connection strings in app.config for this WebJob to run:
        // AzureWebJobsDashboard and AzureWebJobsStorage
        static void Main()
        {            
            JobHostConfiguration config = new JobHostConfiguration();                       
            config.Tracing.ConsoleLevel = TraceLevel.Verbose;
            config.Tracing.Tracers.Add(new CustomTraceWriter(TraceLevel.Verbose));
            var host = new JobHost(config);
            // The following code ensures that the WebJob will be running continuously
            host.RunAndBlock();
        }
    }
```
 
###Question
What logging approach would you prefere? 


##Settings
If you want to configure how KUDU handle your web job, you need to place a `settings.job` file next in the job folder. 

https://github.com/projectkudu/kudu/blob/master/Kudu.Contracts/Jobs/JobSettings.cs

```
{ 
    "is_in_place": true/false,
    "stopping_wait_time": 60, 
    "schedule": "0 * * * * *" 
}
``` 

##Web Jobs API
https://github.com/projectkudu/kudu/wiki/WebJobs-API


##Documentation 
Since Web Jobs are owned by the KUDU team, the best documentation is found on the [projectkudu](https://github.com/projectkudu/kudu/) github repo (unfortunately the documentation in general is not super great). 

https://github.com/projectkudu/kudu/wiki/Web-jobs 


##Discussion
Things you could see Web Jobs being used for? 