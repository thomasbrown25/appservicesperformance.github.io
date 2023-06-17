---

title: "Async/Await - Best Practices"

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

Deadlocks is a state where two or more threads are stuck indefinitely waiting for each other. This is technically a freeze and not a performance problem.
Deadlock happens when the application has a call where AsyncTask awaits a Result.
To fix it, the application should not block by using the .Result property of an asynchronous call.  Patterns such as marking the function async, or the aspx page as async and calling with ‘await’ will fix this issue. If a Deadlock occurs due to Task.Result getting called inappropriately, then the whole application is unstable.

This issue is known and nicely documented at the following places. 

 [https://weblogs.asp.net/pglavich/asp-net-web-api-request-response-usage-logging](https://weblogs.asp.net/pglavich/asp-net-web-api-request-response-usage-logging)
            [http://blog.stephencleary.com/2012/07/dont-block-on-async-code.html](http://blog.stephencleary.com/2012/07/dont-block-on-async-code.html)
            [https://stackoverflow.com/questions/9343594/how-to-call-asynchronous-method-from-synchronous-method-in-c](https://stackoverflow.com/questions/9343594/how-to-call-asynchronous-method-from-synchronous-method-in-c)
       [https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming#async-all-the-way](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming#async-all-the-way)

**Asp.net core:**
[https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md#avoid-using-taskresult-and-taskwait](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios/blob/master/AsyncGuidance.md#avoid-using-taskresult-and-taskwait)
