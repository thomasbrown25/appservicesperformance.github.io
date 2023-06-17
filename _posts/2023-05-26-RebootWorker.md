---

title: "How to Reboot Specific Worker in Azure App Service"

author_name: "Sree Vani Koneru"

categories:

    - Windows # Azure App Service on Linux, Azure App Service on Windows

toc: true

toc_sticky: true

date: 2023-05-26 12:00:00

---

<html>
<head>
  <!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-0DC5DVJXR5"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-0DC5DVJXR5');
</script>
</head>
</html>

## How to Reboot a Specific Instance in an App Service Plan
Azure provides a variety of services and tools that enable developers to build, deploy, and manage cloud applications. One of the key services offered by Azure is the Reboot Worker API, which enables users to reboot their virtual machines in a cloud environment.

When a worker instance is rebooted, the App Service is immediately moved to a new instance. This process is quicker rather than waiting for the VM to restart, but it is also advantageous as moving an App Service to a new instance can cure many ills that the App Service is experiencing.

There is an API used for instance reboot. This will reboot your instance, and thus, it will assign you to another worker instance. You will find the documentation at - [App Service Plans - Reboot Worker ](https://learn.microsoft.com/en-us/rest/api/appservice/app-service-plans/reboot-worker)




## Calling the Reboot Worker API from Microsoft Learn
![flow](/media/2023/Rebootworker/01.jpg)

After pressing “Try It”, you will be presented with the login screen on the right side of the screen. After logging in, you will get the following screen:

![flow](/media/2023/Rebootworker/02.jpg)

Parameters:

**Name**: App Service Plan Name

**resourceGroupName**: Resource Group of your App Service Plan

**subscriptionId**: The Subscription your App Service Plan is under

**workerName**: The name of the worker instance. 

**Api-Version**: The date of the lastest API release

At the bottom of the screen, you'll see a request preview:

![flow](/media/2023/Rebootworker/03.jpg)

Press RUN ▶ and the API will do its magic.


## Calling the Reboot Worker API from Azure CLI
You can also use Azure CLI to call the API directly without the need to specify an authentication token. You would call the API using the "az rest" command. You will need to login to Azure CLI and, if necessary, set the subscription prior to executing the "az rest" command.

az rest --method POST --uri /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/serverfarms/{name}/workers/{workerName}/reboot?api-version=2022-03-01


