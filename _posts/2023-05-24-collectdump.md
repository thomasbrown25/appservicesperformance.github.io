---
title: "Collect Memory Dump App Services"
author_name: "Isabel Chavarria"
categories:
    - Windows # Azure App Service on Linux, Azure App Service on Windows, Function App, Azure VM, Azure SDK
toc: true
toc_sticky: true
date: 2023-05-25 12:00:00
---


#### How to collect the dump file on Azure via Azure portal?

Go to App Service Menu, once you have accessed your application, search for “Diagnose and Solve Problems”.

[![](/media/2023/collectdump/01.PNG)](/media/2023/collectdump/01.PNG)

![image](https://github.com/Appservicesperformance/appservicesperformance.github.io/assets/42865334/6e6a53df-fb27-47fd-8592-2b8d284abe77)


Click on “Diagnostics Tools”.

[![](/media/2023/collectdump/02.PNG)](/media/2023/collectdump/02.PNG)


On the Diagnostics Tools on the left side, we will be able to see some tools to collect data on the app services, please select “Collect Memory dump”.

[![](/media/2023/collectdump/03.PNG)](/media/2023/collectdump/03.PNG)

To collect memory dump, you must specify a storage account to store the dump files. You can create a new one or select an existing one.

[![](/media/2023/collectdump/04.PNG)](/media/2023/collectdump/04.PNG)

Select the instances and then click on collect memory dump. Will be start to collect the data it’s important that the issue is occurring at that moment so we will be able to collect accurate data.

[![](/media/2023/collectdump/05.PNG)](/media/2023/collectdump/05.PNG)

After the analysis is completed, you will notice two files once that is .dmp and the .mht file. You can also see the last 5 sessions captured.

[![](/media/2023/collectdump/06.PNG)](/media/2023/collectdump/06.PNG)

The dump file will be the full file and you can analyze it using tools like windbg or DebugDiag.

The .mht contain that analysis of the .diagsession file.
