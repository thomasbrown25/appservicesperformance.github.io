---
title: "ARR Affinity Azure App Services"
author_name: "Isabel Chavarria"
categories:
    - Windows
    - linux
tags:
    - How it works
toc: true
toc_sticky: true
date: 2023-05-26 09:00:00
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

## ARR Affinity Azure App Services

ARR cleverly identifies the user by assigning them a special cookie
***(known as an affinity cookie)***,which allows the service to choose the right
instance the user
was using to serve subsequent requests made by that user. That means that if we
have the ARR Affinity enabled, a client is tied to a specific web worker until the
session finishes.

## How to check if my application has the ARR affinity enabled

1. Go to the Azure portal.
2. Go to the App Service
    - Configuration
    - General Settings
    - ARR affinity

![flow](/media/2023/arr/01.png)

 **Note:** If you don’t need it, you can disable it there. Just need to select
 off and click on the save button.

## How to check the ARR Affinity cookie on my application

Browsed the URL of your application. On this case my app is
[](https://awesomeappisatest.azurewebsites.net/)

Go to the developer tools of your browser.
Click on the application tab and look for the cookies. You will be able to see
the URL of your application click there.

You can see the ARRAffinity cookie there.  You can use the value and check for
more information.

Use the image below as reference.
![flow](/media/2023/arr/02.png)

Now we can go to kudu of this application. **`<name of the application>`.scm.azurewebsites.net**

Once you are there you will be able to see on the menu an option for the Instance.
There you can see the list of instances assigned to your web application.

![flow](/media/2023/arr/03.png)

If you can see the ARRAffinity cookie starts with the same number **121b** of one
of your instances. That means that this request was redirected to that specific instance.

Finally with that ID you can check which specific instance the application is
reaching. To see this please follow the next steps:

- Go to Azure Portal
- App Service
- Go to Diagnose and solve problems tab
- Availability and performance

![flow](/media/2023/arr/04.png)

- On the search bar write RD

![flow](/media/2023/arr/05.png)

There you can see the information about your instances.
![flow](/media/2023/arr/06.png)
