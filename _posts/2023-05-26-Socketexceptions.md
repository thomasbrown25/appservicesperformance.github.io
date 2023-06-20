---
title: "Troubleshooting Socket exception in Azure App Service"
author_name: "Sree Vani Koneru"
categories:
    - Windows
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

A common requirement for applications is the ability to make outbound network
calls to other network endpoints. This includes calling out to Azure internal
services such as SQL Database and Azure Storage. It also includes cases where
applications make calls to HTTP/HTTPS API endpoints—for example, calling a Bing
Search API or calling an API “application” that implements back-end business
logic for a Web application.

In almost all of these cases, the calling app running on Azure App Service is
implicitly opening a network socket and making outbound calls to endpoints
that are considered “remote” from an Azure Networking perspective. TCP port
exhaustion happens when the sum of connection from a given worker exceeds the
capacity. The number of available TCP ports depend on the size of the worker.

## The maximum connection limits are the following

1,920 connections per B1/S1/P1 instance

3,968 connections per B2/S2/P2 instance

8,064 connections per B3/S3/P3 instance

64K max upper limit per App Service Environment

 When web apps run into these connection limits, they will start intermittently
 failing because calls to those remote endpoints will fail, causing downtime.
 You’ll frequently see errors like the following: “An attempt was made to access
 a socket in a way forbidden by its access permissions aaa.bbb.ccc.ddd.”

## Common Resons for the error

1. Using client libraries which are not implemented to re-use TCP connections.

2. Application code or the client library is leaking TCP socket handles.

3. Burst load of requests opening too many TCP socket connections at once.

4. In case of higher level protocol like HTTP this is encountered if the
Keep-Alive option is not leveraged.

Applications with many longstanding connections require ports to be left
open for long periods of time, which can lead to TCP Connection exhaustion.
TCP Connection limits are fixed based on instance size, so it's necessary to
scale up to a larger worker size to increase the allotment of TCP connections,
or implement code level mitigations to govern connection usage. Similar to SNAT
port exhaustion, you can use Azure Diagnostics to identify a problem exists with
TCP port limits.

## TCP Connections Walkthrough

To examine your TCP Connections more closely, click on the "Diagnose and solve
problems" tab in the left hand menu. Then, search for  the "TCP Connections".

![flow](/media/2023/TCP/03.jpg)

## TCP Connections

Here, you can monitor the total connections on your instances and the state of
the connections, which include TIME_WAIT, ESTABLISHED etc. If your web app has
high outbound connections (> 1500 outbound connections), you will see the IP addresses’
first three octets and the port number in the Summary.
By examining the port number, you can determine what type of remote service is
causing the high outbound connections.

![flow](/media/2023/TCP/04.jpg)

![flow](/media/2023/TCP/01.jpg)

![flow](/media/2023/TCP/02.jpg)
