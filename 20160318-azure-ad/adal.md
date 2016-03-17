#Azure Active Directory Authentication Library (ADAL)
We used it during the cloud day. It makes authentication with Azure AD considerably easier, as it handles the OAuth2 flows for us (basically we don't need to know the details of OAuth). 

It exists for pretty much any platform you could think of. 

* JavaScript
* Node.js
* C# (mobile/server)
* Cordova
* Native Phone (Apple and Android)

Source: 
https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/

##The Four Major Flows
###Authenticating Users of a Client Application to a Remote Resource 
- OAuth 2.0 authorization code grant type with a public client
###Authenticating Users of a single Page Application to a Remote Resource
-OAuth 2.0 Implicit Grant protocol 
###Authenticating a Server Application to a Remote Resource
- OAuth 2.0 client credentials grant 
###Authenticating a Server Application on Behalf of a User to Access a Remote Resource
- OAuth 2.0 authorization code grant with a confidential client / Delegated User Identity with OpenID Connect
Read More: https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-scenarios/

##How to use from .net Console App
```
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;
using System.Configuration;
using System.Globalization;

namespace DotNetConsole.Azure.Auth
{
    class Program
    {
        private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];
        private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
        private static string appKey = ConfigurationManager.AppSettings["ida:AppKey"];


        static string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);

        static void Main(string[] args)
        {
            var authContext = new AuthenticationContext(authority);
            var clientCredential = new ClientCredential(clientId, appKey);

            var token = authContext.AcquireToken("https://graph.windows.net/", clientCredential);

            Console.WriteLine("Access Token: " + token.AccessToken);
            Console.ReadKey();
        }
    }
}

```



