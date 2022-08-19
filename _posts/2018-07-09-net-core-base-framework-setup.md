---
layout: post
title: .NET core- Startup, middleware -base framework setup
date: 2018-07-09 20:16
author: tmasabari
comments: true
categories: [C#, Code, MicroServices, Services, VS, Web Application, WEBAPI]
---
https://docs.microsoft.com/en-us/aspnet/core/migration/http-modules?view=aspnetcore-2.1#migrating-module-insertion-into-the-request-pipeline

https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-2.1&amp;tabs=aspnetcore2x
<h2 id="what-is-middleware" class="heading-with-anchor">What is middleware?</h2>
Middleware is software that's assembled into an application pipeline to handle requests and responses. Each component:
<ul>
 	<li>Chooses whether to pass the request to the next component in the pipeline.</li>
 	<li>Can perform work before and after the next component in the pipeline is invoked.</li>
</ul>
Request delegates are used to build the request pipeline. The request delegates handle each HTTP request.
<ul>
 	<li>Request delegates are configured using <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.runextensions" data-linktype="absolute-path"><span style="background-color: #ffff00;">Run</span></a><span style="background-color: #ffff00;">, <a style="background-color: #ffff00;" href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.mapextensions" data-linktype="absolute-path">Map</a>, and <a style="background-color: #ffff00;" href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.useextensions" data-linktype="absolute-path">Use</a> extension methods</span>.</li>
 	<li>An individual request delegate can be specified in-line as an anonymous method (called in-line middleware),</li>
 	<li>or it can be defined in a reusable class.</li>
 	<li>These reusable classes and in-line anonymous methods are <em>middleware</em>, or <em>middleware components</em>.</li>
 	<li>Each middleware component in the request pipeline is responsible for invoking the next component in the pipeline, or short-circuiting the chain if appropriate.</li>
</ul>
&nbsp;
<p id="IKQVEtL"><img class="alignnone size-full wp-image-1610 " src="/wp-content/uploads/2018/07/img_5b4db61e01eb0.png" alt="" /></p>

<h2 id="ordering" class="heading-with-anchor">Ordering</h2>
<p class="">The order that middleware components are added in the <code>Configure</code> method defines the order in which they're invoked on requests, and the reverse order for the response. This ordering is critical for security, performance, and functionality.</p>
The Configure method (shown below) adds the following middleware components:
<ol>
 	<li>Exception/error handling</li>
 	<li>Static file server</li>
 	<li>Authentication</li>
 	<li>MVC</li>
</ol>
<div class="codeHeader" data-bi-name="code-header"><span class="language">C#</span></div>
<pre><code class="lang-csharp"><span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">void</span> <span class="hljs-title">Configure</span>(<span class="hljs-params">IApplicationBuilder app</span>)
</span>{
    app.UseExceptionHandler(<span class="hljs-string">"/Home/Error"</span>); <span class="hljs-comment">// Call first to catch exceptions</span>
                                            <span class="hljs-comment">// thrown in the following middleware.</span>

    app.UseStaticFiles();                   <span class="hljs-comment">// Return static files and end pipeline.</span>

    app.UseAuthentication();               <span class="hljs-comment">// Authenticate before you access</span>
                                           <span class="hljs-comment">// secure resources.</span>

    app.UseMvcWithDefaultRoute();          <span class="hljs-comment">// Add MVC to the request pipeline.</span>
}</code></pre>
<ul>
 	<li>In the code above, <code>UseExceptionHandler</code> is the first middleware component added to the pipeline—therefore, it catches any exceptions that occur in later calls.</li>
 	<li>The static file middleware is called early in the pipeline so it can handle requests and short-circuit without going through the remaining components. The static file middleware provides <strong>no</strong> authorization checks. Any files served by it, including those under <em>wwwroot</em>, are publicly available.</li>
</ul>
<h2 id="modules-and-handlers-revisited" class="heading-with-anchor">Modules and handlers revisited</h2>
Before proceeding to ASP.NET Core middleware, let's first recap how HTTP modules and handlers work:<img class="size-full wp-image-1674 aligncenter" src="/wp-content/uploads/2018/08/img_5b6a8e6769007.png" alt="" />
<ul>
 	<li>The roles of both modules and handlers have been taken over by middleware.</li>
 	<li>
<p class=""><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware/index?view=aspnetcore-2.1#middleware-run-map-use" data-linktype="relative-path">Pipeline branching</a> lets you send requests to specific middleware, based on not only the URL but also on request headers, query strings, etc.</p>
</li>
</ul>
<h2>Difference between Middleware and HttpModule</h2>
<table class=" table table-hover table table-hover">
<tbody>
<tr>
<th>HttpModule</th>
<th>Middleware</th>
</tr>
<tr>
<td>HttpModules are configured via web.config or global.asax</td>
<td>Middleware are configured via code rather than web.config. ASP.NET Core 1.0 has <a href="http://www.exceptionnotfound.net/the-startup-file-in-asp-net-5-what-does-it-do/"><u>Startup.cs</u></a> file (entry point for application) where middlewares are added.</td>
</tr>
<tr>
<td>As a developer, you don’t have control on their order of execution. As order of modules is mainly based on application life cycle events.</td>
<td>Unlike modules, you are in full control of what get’s executed and in what order. As they are executed in the order in which they are added.</td>
</tr>
<tr>
<td>The execution order remains same for requests and responses.</td>
<td>Order of middleware for responses is the reverse from that for requests.</td>
</tr>
<tr>
<td>HttpModules helps you to attach code specific to a application events.</td>
<td>Middleware is independent of these events.</td>
</tr>
<tr>
<td>HttpModules are tied to <code>System.web</code>.</td>
<td>Middlewares are host independent.</td>
</tr>
</tbody>
</table>
<ul>
 	<li>Terminating the request Your module might terminate a request, for example if the user isn't authorized: <span style="background-color: #ffff00;">context.Response.End();</span></li>
 	<li>A middleware handles this by <span style="background-color: #ffff00;">not calling <code>Invoke</code></span> on the next middleware in the pipeline. Keep in mind that this doesn't fully terminate the request, because p<span style="background-color: #ffff00;">revious middlewares will still be invoked</span> when the response makes its way back through the pipeline.</li>
 	<li>In an <code>HttpModule</code>, you had to execute code based on the various stages of a request, things such as <code>AuthenticateRequest</code>, <code>AuthorizeRequest</code>, <code>PostResolveRequestCache</code>, and other slightly confusingly named events. <em>This is no longer the case with Middleware, things just make sense now. everything is simply a linear execution of your code. You can have multiple middleware’s defined to execute in your application and each one is registered explicitly in your Startup.cs file.</em></li>
 	<li>As a developer, you are in full control of what get’s executed and in what order instead of not knowing which HttpModules are executing and not really in control of their order of execution. Middleware can simply modify a request and continue calling the next one in the chain, or it can just terminate the pipeline and return a result.</li>
 	<li>This middleware (replaces handler) is very similar to the middleware corresponding to modules. The only real difference is that here there's no call to <code>_next.Invoke(context)</code>. That makes sense, because the handler is at the end of the request pipeline, so there will be no next middleware to invoke.</li>
 	<li>If you only want requests with a given extension to reach your middleware. That would give you the same functionality you had with your HTTP handler.
<ul>
 	<li>One solution is to branch the pipeline for requests with a given extension, using the <code>MapWhen</code> extension method.</li>
 	<li><span class="line-highlight"> <span class="hljs-comment">// Create branch to the MyHandlerMiddleware. </span></span> <span class="line-highlight">
<span class="hljs-comment">// All requests ending in .report will follow this branch.</span></span> <span class="line-highlight"><span class="line-highlight">
<code>
app.MapWhen(
context =&gt; context.Request.Path.ToString().EndsWith(".report"),
appBranch =&gt; {
// ... optionally add more middleware to this branch
appBranch.UseMyHandler();
});
app.MapWhen(
context =&gt; context.Request.Path.ToString().EndsWith(".context"),
appBranch =&gt; {
appBranch.UseHttpContextDemoMiddleware();
});</code></span></span></li>
</ul>
</li>
 	<li><code>MapWhen</code> takes these parameters:
<ol>
 	<li>A lambda that takes the <code>HttpContext</code> and returns <code>true</code> if the request should go down the branch. This means you can branch requests not just based on their extension, but also on request headers, query string parameters, etc. <span class="line-highlight"><code>context =&gt; context.Request.Path.ToString().EndsWith(".report")</code></span></li>
 	<li>
<p class="">A lambda that takes an <code>IApplicationBuilder</code> and adds all the middleware for the branch. This means you can add additional middleware to the branch in front of your handler middleware. <span class="line-highlight"><code>appBranch =&gt; {
// ... optionally add more middleware to this branch
appBranch.UseMiddleware&lt;MyHandlerMiddleware&gt;()</code></span></li>
</ol>
</li>
</ul>
<h2 id="built-in-middleware" class="heading-with-anchor">Built-in middleware</h2>
ASP.NET Core ships with the following middleware components, as well as a description of the order in which they should be added:
<div class="table-scroll-wrapper">
<table>
<thead>
<tr>
<th>Middleware</th>
<th>Description</th>
<th>Order</th>
</tr>
</thead>
<tbody>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity?view=aspnetcore-2.1" data-linktype="relative-path">Authentication</a></td>
<td>Provides authentication support.</td>
<td>Before <code>HttpContext.User</code> is needed. Terminal for OAuth callbacks.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/cors?view=aspnetcore-2.1" data-linktype="relative-path">CORS</a></td>
<td>Configures Cross-Origin Resource Sharing.</td>
<td>Before components that use CORS.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/error-handling?view=aspnetcore-2.1" data-linktype="relative-path">Diagnostics</a></td>
<td>Configures diagnostics.</td>
<td>Before components that generate errors.</td>
</tr>
<tr>
<td><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions" data-linktype="absolute-path">Forwarded Headers</a></td>
<td>Forwards proxied headers onto the current request.</td>
<td>Before components that consume the updated fields (examples: scheme, host, client IP, method).</td>
</tr>
<tr>
<td><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.httpmethodoverrideextensions" data-linktype="absolute-path">HTTP Method Override</a></td>
<td>Allows an incoming POST request to override the method.</td>
<td>Before components that consume the updated method.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-2.1#require-https" data-linktype="relative-path">HTTPS Redirection</a></td>
<td>Redirect all HTTP requests to HTTPS (ASP.NET Core 2.1 or later).</td>
<td>Before components that consume the URL.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/enforcing-ssl?view=aspnetcore-2.1#http-strict-transport-security-protocol-hsts" data-linktype="relative-path">HTTP Strict Transport Security (HSTS)</a></td>
<td>Security enhancement middleware that adds a special response header (ASP.NET Core 2.1 or later).</td>
<td>Before responses are sent and after components that modify requests (for example, Forwarded Headers, URL Rewriting).</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/performance/caching/middleware?view=aspnetcore-2.1" data-linktype="relative-path">Response Caching</a></td>
<td>Provides support for caching responses.</td>
<td>Before components that require caching.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/performance/response-compression?view=aspnetcore-2.1" data-linktype="relative-path">Response Compression</a></td>
<td>Provides support for compressing responses.</td>
<td>Before components that require compression.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-2.1" data-linktype="relative-path">Request Localization</a></td>
<td>Provides localization support.</td>
<td>Before localization sensitive components.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-2.1" data-linktype="relative-path">Routing</a></td>
<td>Defines and constrains request routes.</td>
<td>Terminal for matching routes.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/app-state?view=aspnetcore-2.1" data-linktype="relative-path">Session</a></td>
<td>Provides support for managing user sessions.</td>
<td>Before components that require Session.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/static-files?view=aspnetcore-2.1" data-linktype="relative-path">Static Files</a></td>
<td>Provides support for serving static files and directory browsing.</td>
<td>Terminal if a request matches files.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/url-rewriting?view=aspnetcore-2.1" data-linktype="relative-path">URL Rewriting</a></td>
<td>Provides support for rewriting URLs and redirecting requests.</td>
<td>Before components that consume the URL.</td>
</tr>
<tr>
<td><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/websockets?view=aspnetcore-2.1" data-linktype="relative-path">WebSockets</a></td>
<td>Enables the WebSockets protocol.</td>
<td>Before components that are required to accept WebSocket requests.</td>
</tr>
</tbody>
</table>
</div>
Some of the built-in diagnostics middleware are,
<ul>
 	<li>UseDeveloperExceptionPage()</li>
 	<li>UseDatabaseErrorPage()</li>
 	<li>UseExceptionHandler()</li>
 	<li>UseStatusCodePages()</li>
 	<li>UseRuntimeInfoPage() Removed in 1.0 release. Check here.</li>
 	<li>UseWelcomePage()</li>
 	<li>UseElmPage() and UseElmCapture()</li>
</ul>
&nbsp;

Logging using NLog
<ol>
 	<li>https://github.com/NLog/NLog.Web/wiki/Getting-started-with-ASP.NET-Core-2</li>
 	<li>Install the latest NLog NLog.Web.AspNetCore</li>
 	<li>Create a nlog.config file. https://github.com/NLog/NLog/wiki/Configuration-file
<ol>
 	<li>Enable copy to bin folder</li>
</ol>
</li>
 	<li>Add log in the program.cs - main method
<ol>
 	<li>using Microsoft.Extensions.Logging;
using NLog;
using NLog.Web;</li>
 	<li>Read configuration from main https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-2.1&amp;tabs=basicconfiguration#webconfig-file
//https://stackoverflow.com/questions/41738692/read-appsettings-json-in-main-program-cs</li>
 	<li>//Setup the NLog variables in nlog.config
GlobalDiagnosticsContext.Set("LogFolder", Configuration["LogFolder"] );
GlobalDiagnosticsContext.Set("LogConnectionString", Configuration["LogConnectionString"] );</li>
 	<li><code>
//Enable NLog
//https://github.com/NLog/NLog.Web/wiki/Getting-started-with-ASP.NET-Core-2
//SQL Server Log https://github.com/damienbod/AspNetCoreNlog
// NLog: setup the logger first to catch all errors
var logger = NLog.Web.NLogBuilder.ConfigureNLog("nlog.config").GetCurrentClassLogger();
try
{
//use startup class to host the web site
IWebHostBuilder webHostBuilder = CreateWebHostBuilder(args);
webHostBuilder.ConfigureLogging(logging =&gt;
{
logging.ClearProviders();
logging.SetMinimumLevel(Microsoft.Extensions.Logging.LogLevel.Trace);
})
.UseNLog()  // NLog: setup NLog for Dependency injection
.Build()
.Run();
}
</code></li>
</ol>
</li>
 	<li>Create an action filter to catch necessary logs
<code>public class LogFilter : ActionFilterAttribute</code></li>
 	<li>Inject the filter as service in dependency injection
<code>services.AddScoped&lt;LogFilter&gt;();</code></li>
 	<li>The Logging configuration specified in appsettings.json overrides any call to SetMinimumLevel. So either remove "Default": or adjust it correctly to your needs.
<code>{
"Logging": {
"LogLevel": {
"Default": "Trace",
"Microsoft": "Information"
}
}
}</code></li>
 	<li>Inject the ILogger in your controller:
<code><code>
private readonly ILogger _logger;</code></code>public HomeController(ILogger logger)
{
_logger = logger;
}</li>
 	<li>Write Log <code>_logger.LogInformation("Index page says hello");</code></li>
 	<li>Create common LoggerFactory
<ol>
 	<li><a href="https://stackify.com/net-core-loggerfactory-use-correctly/?utm_referrer=https://www.google.co.in/">How do you do logging in a class library that is consumed by this ASP.NET project?</a></li>
 	<li>create a little static helper class ApplicationLogging  that becomes the owner of the LoggerFactory. You can then use this ApplicationLogging class in any code that you want to use logging from and not have to worry about recreating LoggerFactory objects over and over. After all, logging needs to be fast</li>
</ol>
</li>
</ol>
&nbsp;

&nbsp;

Exception handling
<ul>
 	<li>https://www.devtrends.co.uk/blog/handling-errors-in-asp.net-core-web-api</li>
 	<li>Customising the response structure for consistency</li>
 	<li>Create GlobalExceptionFilter
<ul>
 	<li>https://github.com/devkimchi/ASP.NET-Core-Tips-and-Tricks-Sample/blob/master/src/AspNetCoreTipsAndTricksSample/Filters/GlobalExceptionFilter.cs</li>
</ul>
</li>
 	<li>Create Custom Middleware
<ul>
 	<li>https://stackoverflow.com/questions/38630076/asp-net-core-web-api-exception-handling</li>
 	<li>https://blog.kloud.com.au/2016/03/23/aspnet-core-tips-and-tricks-global-exception-handling/</li>
 	<li>http://www.talkingdotnet.com/aspnet-core-diagnostics-middleware-error-handling/</li>
</ul>
</li>
</ul>
