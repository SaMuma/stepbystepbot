# Azure Bot Service Bot: Step by Step
a step by step guide to building a bot starting from Bot Service in Azure, running and testing locally, and pushing changes to Azure. We will walk through the following Steps: 
- Create a bot in the Azure portal using Bot Service 
- Download bot source code and run locally in Visual Studio 
- Create a publish profile to push changes to the App Service in Azure 
- Set up a CI/CD Pipeline using Visual Studio Team Services

### Create a Bot in the Azure Portal 
- Search for "Web App Bot" and click create
- Fill in the required fields and click create (note the location)
- Select "pin to dashboard" for easy access to this resource
![alt text](https://raw.githubusercontent.com/SaMuma/stepbystepbot/master/images/1.png)

### Download bot source code and run locally in Visual Studio 
##### Download the application code 
- Navigate to your newly created Web App Bot 
- Click on the build tab, and then select download zip file. (this step takes a minute) 
- Extract the files to your desired location on your computer
##### Open the project in Visual Studio 
- Navigate to your project files and open the .sln file in visual studio
- Ensure that Visual Studio is up to date by clicking the flag icon. Update if necessary. 
- Ensure that all your NuGet packages are up to date (Project>PackageManager>Updates>Update all) 
##### Add Storage Settings
- On the Azure portal, go to the app settings tab of your bot application, and take note of the AzureWebJobsStorage key value. 
- In Visual Studio, open the solution explorer to see your files. Navigate to the web.config file, and in the appsettings, add the following line of code: 
```
<add key="AzureWebJobsStorage" value="" />
```
Fill in the value with the one you just noted from your Azure portal. 
##### Test Locally using Bot Emulator
- Run the Project using IIS Express. Take note of the IP Address that appears in the webpage that you are automatically directed to. 
- Open BotFrameworkEmulator (you can download it here:https://docs.microsoft.com/en-us/azure/bot-service/bot-service-debug-emulator ) 
- Enter the address from the webpage and append "/api/messages" to the end
Click connect and test out the chat 

At this point, here's what's going on. You have your bot app running in the cloud, and now you've downloaded a local copy which you are testing locally. Right now, these two apps are independent of one another.
So the next step is to create a publish process from your local Visual Studio project to your app service online. 

### Create a publish profile to push changes to the App Service in Azure
Create a new Publish Profile
Note that this is only done the first time. After this, all collaborators on an app will be able to see the publish profile already created in their Visual Studio tool and can just use that. 
- Right click on your solution and select publish…
- Create a publish profile by navigating to the proper resource group and app service. 
- Click publish and note that the site you are directed to is azure hosted, as opposed to the local IP address it directed to when you ran it locally. Your local bot has been published to azure! 

Now that we have the capability to push our local project to the cloud, we can set up a continuous integration/ delivery pipeline using VSTS. 

### Set up a CI/CD Pipeline using Visual Studio Team Services
