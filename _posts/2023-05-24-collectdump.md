---
title: "Collect Memory Dump on App Services"
author_name: "Isabel Chavarria"
categories:
    - Windows
tags:
    - Collect data
toc: true
toc_sticky: true
date: 2023-05-25 12:00:00
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

## How to collect the dump file on Azure via Azure portal?

1. Go to App Service Menu, once you have accessed your application, search for
**“Diagnose and Solve Problems”.**

    ![flow](/media/2023/collectdump/01.png)
  
2. Click on **“Diagnostics Tools”**

    ![flow](/media/2023/collectdump/02.png)
  
3. On the Diagnostics Tools on the left side, we will be able to see some tools
to collect data on the app services, please select “Collect Memory dump”.

    ![flow](/media/2023/collectdump/03.png)

4. To collect memory dump, you must specify a storage account to store the dump files.
You can create a new one or select an existing one.

    ![flow](/media/2023/collectdump/04.png)

5. Select the instances and then click on collect memory dump. Will be start to
collect the data it’s important that the issue is occurring at that moment s
o we will be able to collect accurate data.

    ![flow](/media/2023/collectdump/05.png)

6. After the analysis is completed, you will notice two files once that is **.dmp**
and the **.mht** file. You can also see the last 5 sessions captured.

    ![flow](/media/2023/collectdump/06.png)

The dump file will be the full file and you can analyze it using tools like
**windbg or DebugDiag.**

The **.mht** contain that analysis of the .diagsession file.
