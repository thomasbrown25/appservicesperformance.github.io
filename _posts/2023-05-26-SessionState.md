---

title: "Session state in Asp.net"

author_name: "Sree Vani Koneru"

categories:

    - Windows # Azure App Service on Linux, Azure App Service on Windows

toc: true

toc_sticky: true

date: 2023-05-26 12:00:00

---

In Azure Web Apps, you can store session state using various methods. Here are a few options:

1. InProc: This is the default session state mode in Azure Web Apps. InProc mode stores session data in the memory of the web server hosting your application. However, note that when you scale out your application to multiple instances or if the application restarts, the session data will be lost.

2. Azure Redis Cache: You can use Azure Redis Cache as a session state provider. Redis Cache provides an in-memory data store that can be shared across multiple instances of your web app. To use Azure Redis Cache as a session state provider, you need to configure your web app to use it by setting up the necessary connection string and configuration settings.

3. Azure SQL Database: Another option is to store session state in an Azure SQL Database. This approach provides persistence and scalability, as the session data is stored in a database rather than in-memory. To configure Azure SQL Database as the session state provider, you need to set up the necessary connection string and configuration settings for your web app.

To configure session state in Azure Web Apps, you typically need to modify the web.config file of your application and specify the desired session state provider and its corresponding configuration settings. The specific configuration steps may vary depending on the programming language and framework you are using.

It's important to note that storing session state in external services like Azure Redis Cache or Azure SQL Database can incur additional costs and may introduce some latency compared to using InProc mode. You should consider the needs of your application and choose the appropriate session state management method based on factors such as scalability, persistence, and cost.

To configure session state in Azure Web Apps, you need to make changes to the web.config file of your application. Here's an example of configuring session state to use Redis in web.config. 

    <configuration>
                <system.web>
                    <sessionState mode="Custom" customProvider="RedisSessionStateProvider">
                    <providers>
                        <add name="RedisSessionStateProvider" 
                            type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                            host="your-redis-cache.redis.cache.windows.net" 
                            port="6380" 
                            accessKey="your-access-key" 
                            ssl="true" 
                            throwOnError="true" 
                            retryTimeoutInMilliseconds="5000" 
                            databaseId="0" 
                            applicationName="your-app-name" />
                    </providers>
                    </sessionState>
                </system.web>
                </configuration>
    
Replace your-redis-cache.redis.cache.windows.net with the hostname of your Azure Cache for Redis instance and your-access-key with the access key for your Redis instance. Adjust other settings as per your requirements.

Remember to ensure that your application code is session-aware and correctly uses the session object to store and retrieve session data.

Note: If you're using Azure Functions, there is no built-in support for session state management since functions are designed to be stateless. In that case, you might need to consider other approaches for managing session-like data, such as using external storage services or stateful backends like Azure SignalR Service.