#Azure AD Applications
Azure AD application are azure ad object that describe an application that users can use, users can see their applications are https://myapps.microsoft.com. 

Along side an application sits a service principal the service principal is like a service account for the application. 
The service principal can have a Key (Client Secret/Password). With the Client ID and the Key it is possible to access resource as the application. 


![azure-ad-application-objects-relationship](images/application-objects-relationship.png)

https://azure.microsoft.com/en-us/documentation/articles/active-directory-application-objects/ 

##Application Object
This object represents a definition for your app. You can find a detailed description of its properties in the Application Object section below.

##ServicePrincipal object
This object represents an instance of your app in your directory tenant. You can apply policies to ServicePrincipal objects, including assigning permissions to the ServicePrincipal that allow the app to read your tenant’s directory data. Whenever you change your Application object, the changes are also applied to the associated ServicePrincipal object in your tenant.


##Multi-tenant applications
If your application is configured for external access, changes to the application object are not reflected in a consumer tenant’s ServicePrincipal until the consumer tenant removes access and grants access again.


##How to create
* Use the old Azure Portal: https://manage.windowsazure.com
* Use the new app v2 registration portal https://apps.dev.microsoft.com (https://azure.microsoft.com/en-us/documentation/articles/active-directory-appmodel-v2-overview/) 
* Use a service specific page e.g. powerbi have one https://dev.powerbi.com/apps  
* Do it yourself (https://github.com/sjkp/Angular.Azure.Auth) 

##Application v2
Not ready for production use yet.
https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-limitations/ 

##What is Azure AD Applicatoin Proxy 
It is a completely different service. Think UAG. 
https://azure.microsoft.com/sv-se/documentation/articles/active-directory-application-proxy-publish/ 