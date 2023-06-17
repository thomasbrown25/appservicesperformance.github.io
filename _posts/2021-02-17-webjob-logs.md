---
title: "Webjob Logs"
author_name: "Isabel Chavarria"
categories:
    - Windows
tags:
    - Collect data
toc: true
toc_sticky: true
date: 2021-02-17 09:00:00
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
## How to get the WebJob Logs

The webjobs on Azure app Service run on the KUDU process, sometimes we are not sure how to retrieve data about my webjob. Is important to mention that you can monitor your WebJobs from the Azure Portal. 

1. Go to your App service and on the left menu. Write on the search box "webjobs" and click on it:

    ![flow](/media/2021/webjob/01.png)

2. You will have a window with all the WebJobs under this App Service. Click on the WebJob that you want to monitor and then click on logs:

![flow](/media/2021/webjob/02.png)

This will open a new window nd you will need to login with the same credentials that you use on the Azure Portal. 

You will be able to monitor the WebJobs from the dashboard. Use the image below as reference: 

![flow](/media/2021/webjob/03.png)

Then you can click the WebJob and review the logs from there

![flow](/media/2021/webjob/04.png)

In the WebJob dashboard you will be able to see how long are taking to complete and the logs of the WebJob. 

You will need to click in once of the recent job. 

![flow](/media/2021/webjob/05.png)

You can download the logs click on “download”.

You can see the time of start and the time when the webjob finished.

![flow](/media/2021/webjob/06.png)

Application Insights is a Service we provide that you can use to monitor live your web application. It includes analytics tools that can help you diagnose issues. You can also add some lines of code so that the WebJobs send the data directly to the Application Insights tool for you to diagnose as well.

## Please refer to the following documentation:

- [Overview](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview )

- [Custom events and metrics](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics)

- [Application insights integration for WebJobs](https://github.com/Azure/azure-webjobs-sdk/wiki/Application-Insights-Integration)