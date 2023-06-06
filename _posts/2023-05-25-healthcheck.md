---
title: "Health Check"
author_name: "Isabel Chavarria & Sree Vani Koneru"
categories:
    - Windows # Azure App Service on Linux, Azure App Service on Windows, Function App, Azure VM, Azure SDK
toc: true
toc_sticky: true
date: 2023-05-26 12:00:00
---
## Health Check in Azure App Service

Health check is a critical feature for any application that needs to run reliably and continuously. It is particularly important in cloud-based environments, where applications are hosted on shared infrastructure that may experience failures or outages. Azure App Service provides a powerful and flexible health check mechanism that enables users to monitor the health of their web apps and ensure they are running smoothly.

## What is a Health Check?

A health check is a mechanism used to monitor the status of a web app and ensure it is functioning as expected. It typically involves sending requests to the app at a regular interval and checking the response to ensure it is valid. Health checks can be used to detect a wide range of issues, including application failures, network outages, and resource constraints.

## Health Check in Azure App Service (Windows)

Azure App Service provides a flexible and powerful health check mechanism that enables users to monitor the health of their web apps. The health check can be configured at the app level or the endpoint level, depending on the requirements of the application.

At the app level, users can enable the built-in health check endpoint, which is available at the `/healthcheck` URL. This endpoint returns a `200 OK` response if the app is healthy and a `503 Service Unavailable` response if the app is unhealthy. Users can customize the response by adding a custom response body or by configuring the response code.

At the endpoint level, users can define custom health check endpoints for specific resources or APIs. These endpoints can be configured to return a specific response code or body, or they can be configured to perform more complex checks, such as checking the response time or validating the content of the response.

## How it works

The health check feature needs to have a path configured to monitor the health of your application. It's important that if your application needs connectivity to a database and a messaging system, the health check endpoint should connect to those components. If the application can't connect to a critical component, then the path should return a `500`-level response code to indicate that the app is unhealthy.

Health check pings this path on all instances of your App Service app at 1-minute intervals. If there is no response from that path in a minute, the health check ping will be flagged as unhealthy.

If an instance doesn't respond with a status code between `200-299` (inclusive) after 10 requests, App Service determines it's unhealthy and removes it. However, if there are multiple applications under the same app service plan and one of the applications is throwing a `200-299` status code, the instance will not be removed since there is an application working fine.

After removal, the health check continues to ping the unhealthy instance. If the instance begins to respond with a healthy status code (`200-299`), then the instance is returned to the load balancer.

If an instance remains unhealthy for one hour, it will be replaced with another worker if none of the following limits is met:
- The number of workers replaced should follow the configured percentage of allowed workers to be replaced if unhealthy (`WEBSITE_HEALTHCHECK_MAXUNHEALTHYWORKERPERCENT`).
- Maximum 3 workers can be replaced per day per App Service Plan.
- Maximum 1 worker can be replaced per hour.
- A successful health check ping would reset the 1-hour timer.

## How to enable health check

To enable health check, follow these steps:

1. Go to the Azure Portal.
2. Navigate to the App Service.
3. Then go to the Monitoring section from the left menu.
4. Find the Health Check option.
5. Add the Health Check Path.


**NOTE:** Health check configuration changes restart your app. To minimize impact to production apps, we recommend configure slots and swapping to production. **  

### Additional Configuration Options

There are two additional configuration options available for health checks:

| Configuration Option                      | Description                                                                                                    |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| WEBSITE_HEALTHCHECK_MAXPINGFAILURES       | This option defines the required number of failed requests for an instance to be considered unhealthy and removed from the load balancer. |
| WEBSITE_HEALTHCHECK_MAXUNHEALTHYWORKERPERCENT | By default, the health check will no remove more than half of the instances in case of "unhealthy". However; customer can override this behavior, set app setting to a value between 1 and 100. A higher value means more unhealthy instances will be removed (default value is 50).  |

## Health Check Monitoring in Azure

Azure provides a range of monitoring tools that enable users to monitor the health of their web apps and ensure they are running smoothly. These tools include:

- **Azure Monitor**: It provides real-time metrics and logs for web apps, allowing users to track the performance and availability of their applications.

- **Azure Application Insights**: This tool provides detailed insights into the performance and behavior of web apps, helping users identify and troubleshoot issues effectively.

## Conclusion

Health check is a critical feature for any application that needs to run reliably and continuously. Azure App Service provides a flexible and powerful health check mechanism that enables users to monitor the health of their web apps and ensure they are running smoothly. By leveraging the health check mechanism in Azure, users can improve the reliability and performance of their web apps and ensure they are meeting the needs of their users.

## FAQ 

### Application running on just one instance 
If the instance becomes unhealthy, it will not be removed from the load balancer because that would take down the application. However, after one hour of continuous unhealthy pings, the instance is replaced. 
