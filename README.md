# Creating a HubSpot Contact and Company from an ASP.NET MVC Site[HubSpot](https://www.hubspot.com/) is a popular customer relations management (CRM) platform that offers a REST API for third-party integrations. Trouble is, HubSpot hasn't done a good job of guiding developers through a simple setup and integration scenario. This document provides the simplest steps to get a HubSpot account, create your API key and set up a barebones MVC/HubSpot integration.## Create Your Developer Account and Test HubYou can sign up for a free developer account on HubSpot. The developer account is limited in that you can work with the API to add Contacts to HubSpot but _you don't get the Marketing dashboard to see a list of those contacts with the HubSpot UI_. This was a very confusing waste of time. **What you need is the full-featured trial version of HubSpot**.### Creating a Developer Account1. Navigate to https://developers.hubspot.com/2. In the upper right area, click Create an Account.3. Fill in the developer account details (as shown in the image below) and click Start Building Apps:
![HubSpot Developer Account](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/createhubspotdevacct.png)
HubSpot announces that your account is ready and then shifts to the Development screen.
### Creating a HubSpot Test Hub1. While still logged in to HubSpot with your developer account, click the **Testing** menu item at the top left area of the screen as shown in the following image:
![Testing Menu](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hubspottest.png)
2. On the Testing page, near the bottom, click Start testing.3. On the Create Test Hub ID pop-up, provide a test hub name (for example, hubspotmvc) and click Create as shown in the image below:
![Create Test Hub ID](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hotspotcreatetesthug.png)
The Testing page displays a grid with the Test Hub you just created, as shown in the following image:
![Test Hub Created](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hubspottestidcreate.png)
### Generate Your HubSpot API Key
1. Click the Profile and Preferences area in the top right of the screen:
![Profile and Preferences](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hubspotintegrations.png)
2. Click Integrations.3. On the Integrations screen click HubSpot API Key and then click Generate New Key:
![HubSpot API Key](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hotspotgenerateAPIKey.png)
The new HAPIkey appears along with the API Key History as shown below:
![HubSport HAPIKey](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hotspotgeneratedHAPIKey.png)
4. Copy the HAPIKey to a file and save it for use in a following step. **Do not publish your API key publicly**.
## Create an ASP.NET MVC Integration for HubSpot
Once you have a HubSpot Test Hub and API key, you can create an ASP.NET MVC application that inserts a contact and a company into the Test Hub. This topic uses a simple REST client to provide .NET bindings for the HubSpot CRM from https://github.com/dmitrybakaev/hubspot-rest-client
### Create an ASP.NET MVC Web Site
1. In Visual Studio 2015 or later, create a new ASP.NET Web Application named HubSpotIntegrationExample (File > New Project > ASP.NET Web Application) choosing the MVC template.
![Visual Studio MVC Web Application](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/visualstuidiowebapplication.png)
2. From GitHub, download the archive of the Visual Studio project from [dmitrybakaev/hubspot-rest-client](https://github.com/dmitrybakaev/hubspot-rest-client/archive/master.zip)3. Unarchive the hubspot-rest-client to your local machine, retaining the folder structure.4. In the Visual Studio HubSpotIntegrationExample solution, add the HubSpotRestClient project (Add > Existing Project).5. In the Visual Studio HubSpotIntegrationExample project, add a reference to the HubSpotRestClient project.
![Add Reference](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/HubSpotIntegrationExamplereference.png)
6. Ensure that the solution builds. (You may need to use the Nuget Package Manager to adjust versions of some components.)7. In the Visual Studio HubSpotIntegrationExample project, from the Controllers folder, open HomeController.cs in the editor.8. Replace the existing Index() method with the following code and substitute the unique HAPIKey (captured previously) in the highlighted area:
![Controller Index](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/controllerindex.png)
8. Run the Web page.
### Confirming the Contact and Company Insertion in HubSpot
1. In HubSpot, navigate to your trial account as shown in the image below:
![Navigate to Account](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/navigatetoaccount.png)
2. From the upper left area, click Contacts > Contacts. Note that the contact has been inserted as shown below:
![Added Contact](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hotspotaddedcontact.png)
3. From the upper left area, click Contacts, Companies. Confirm that the company has been inserted as shown below:
![Added Company](https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/hotspotcompanycreated.png)
## Alternative to Using the HubSpotRestClient project
Rather than importing a library to insert the contact and company, you can create the required payload and post it using .NET code in your project.
This example shows a simplified use of the REST API where you manually build a JSON string containing the properties that you then post to the REST API as a byte array.
)https://github.com/KenCox/HubSpotMVC/blob/master/GistImages/postcontenttohubspot.png)
