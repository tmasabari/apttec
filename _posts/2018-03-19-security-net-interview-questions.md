---
layout: post
title: IIS .NET OWIN & Core
date: 2018-03-19 09:25
author: tmasabari
comments: true
categories: [ASP.NET, Interview Preparation, Security]
---
<h2>ASP.NET</h2>
<h3 id="challenges-raised-by-the-historical-model" class="heading-with-anchor">Challenges Raised by the Historical Model</h3>
<ul>
 	<li>Firstly, the framework was <strong>monolithic</strong>, with logically disparate units of functionality being <strong>tightly coupled</strong> in the same <strong>System.Web.dll</strong> assembly (for example, the core HTTP objects with the Web forms framework).</li>
 	<li>Secondly, ASP.NET was included as a <strong>part of the larger .NET Framework</strong>, which meant that the <strong>time between releases was on the order of years.</strong> This made it difficult for ASP.NET to keep pace with all of the changes happening in rapidly evolving Web development.</li>
 	<li>Finally, <strong>System.Web.dll itself was coupled</strong> in a few different ways to a specific Web hosting option: Internet Information Services (IIS).</li>
 	<li><strong class="">ASP.NET team took several evolutionary steps to enable ASP.NET as a family of pluggable Web components rather than a single framework</strong>.</li>
 	<li>ASP.NET MVC was released as an independent download.</li>
 	<li>Another major shift in Web application development was the <strong>shift from dynamic, server-generated Web pages</strong> to <strong>static initial markup with dynamic sections of the page generated from client-side script</strong> communicating <strong>with backend Web APIs through AJAX requests</strong>.</li>
 	<li>The engineering team took advantage of the opportunity and <strong>built ASP.NET Web API such that it had no dependencies on any of the core framework types found in System.Web.dll</strong>.</li>
 	<li>Additionally, the power and flexibility of Web API's self-hosting capability proved very attractive to developers who wanted a <strong>small, lightweight host</strong> for their services.</li>
</ul>
<h2>IIS and .NET dependency</h2>
<ol>
 	<li> IIS provides a rich set of features for logging, tracing, monitoring etc. These features are not always needed.</li>
 	<li>It is often no longer the server that produces HTML – it only responds to Ajax calls with JSON and it is up to the client to process it. This applies especially to mobile applications that consume cloud based web services which only respond with JSON.</li>
 	<li>The goal is to simplify web hosts to make them more responsive, more scalable and cheaper to maintain as the processing time of a request will be a lot faster.</li>
 	<li>Asp.Net framework is strongly dependent on IIS and its capabilities, so it can be hosted only within IIS. This has made the portability of Asp.Net application an impossible task.</li>
 	<li>In particular, Asp.Net applications are basically build upon the assembly called System.Web which in turn heavily depends on IIS for providing many of the web infrastructure features like <strong>request/response filtering, IIS logging, performance counters</strong> etc.</li>
 	<li>System.Web assembly also includes <strong>many default components that are plugged into the Http pipeline regardless of its usage</strong> in the application. This means there are some unwanted features that are executed in the pipeline for every request which degrades the performance.</li>
 	<li>The other major drawback of System.Web assembly is it<strong> is bundled as part of .Net framework installer</strong> package. This has made the delivery of updates and bug-fixes to Asp.Net components a difficult and time consuming task for the Microsoft’s Asp.Net team.</li>
</ol>
<h2 id="what-is-middleware" class="heading-with-anchor">What is middleware?</h2>
<p class="lf-text-block lf-block" data-lf-anchor-id="b1b4d02e055cb4f9ac4d48ce8b39ce38:0">Middleware is software that's assembled into an application pipeline to handle requests and responses. Each component:</p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="9bc42d2f5d38667b3f8becc76f23da55:0">
 	<li>Chooses whether to pass the request to the next component in the pipeline.</li>
 	<li>Can perform work before and after the next component in the pipeline is invoked.</li>
</ul>
<p id="EpmPHZO"><img class="wp-image-1084 aligncenter" src="/wp-content/uploads/2018/03/img_5aaf9fd011582.png" alt="" width="394" height="132" /></p>

<ul>
 	<li>In earlier or old versions of ASP.NET, there was a concept of modules and handlers, which use to take care of the requests and responses.</li>
 	<li>In ASP.NET Core, this is done by middleware. For e.g. a middle ware could be added in the request pipeline to handle authentication and authorization.</li>
 	<li>Each middleware has an option to perform operations before receiving and after delegating the request and eventually generate the response needed. Thus, each middleware component decides whether to delegate the request onto the next component or not.</li>
 	<li>For example,  authentication middleware component finds the request is not authorized and it will not pass the request to the next component in the pipeline and return the response result from its own component.</li>
</ul>
<h2>OWIN- Open Web Interface for .NET</h2>
<ul>
 	<li>OWIN defines a open standard (community-owned specification) <strong>interface between .NET web servers (like IIS) and web applications</strong>.</li>
 	<li>OWIN defines an interface specification to de-couple webserver and application using a simple delegate structure.</li>
</ul>
<h3>Aims</h3>
<ul>
 	<li>OWIN aims to decouple the relationship between<strong> ASP.NET applications and IIS</strong> (<strong>decouple server and application) </strong>by defining a standard interface.
<ul>
 	<li>Prior to OWIN, Microsoft's <a title="ASP.NET" href="https://en.wikipedia.org/wiki/ASP.NET">ASP.NET</a> technology w<strong>as designed on top of <a title="Internet Information Services" href="https://en.wikipedia.org/wiki/Internet_Information_Services">IIS</a></strong>, and Web applications could not easily be run on another Web server (although note that despite this the Mono community developed several ASP.NET compatible Web servers, such as <a title="XSP (software)" href="https://en.wikipedia.org/wiki/XSP_(software)">XSP</a>).</li>
</ul>
</li>
 	<li>Developers of Web servers can be sure that, if they implement OWIN correctly, ASP.NET <strong>applications will run on their server</strong>.</li>
 	<li>Similarly, new <a title="Web framework" href="https://en.wikipedia.org/wiki/Web_framework">Web frameworks</a> could be developed as an <strong>alternative to ASP.NET</strong>. So long as they target OWIN, they will run on any OWIN compatible Web server, including IIS.</li>
 	<li>By being an <strong>open standard</strong>, stimulate the open source ecosystem of .NET web development tools.</li>
 	<li>OWIN allows <strong>chaining</strong> together <a title="Middleware" href="https://en.wikipedia.org/wiki/Middleware">middleware</a> into a pipeline.
<ul>
 	<li>A Web framework can interact with OWIN without knowing whether it is interacting directly with the underlying web server, or with one or more layers of middleware (each implementing OWIN) on top of the Web server.</li>
 	<li>This allows infrastructure concerns, such as <a title="Authentication" href="https://en.wikipedia.org/wiki/Authentication">authentication</a>, to be split out into separate modules. This is desirable as it decouples them from the application's own code, and makes them reusable across applications.</li>
</ul>
</li>
 	<li>OWIN <strong>includes middleware</strong> components for authentication, including support for
<ul>
 	<li>log-ins using external identity providers (like <strong>Microsoft Accounts, Facebook, Google, Twitter</strong>), and</li>
 	<li>log-ins using organizational accounts from <strong>on-premises Active Directory or Azure Active Director</strong>y.</li>
 	<li>OWIN also includes support for <strong>OAuth 2.0, JWT and CORS</strong>.</li>
</ul>
</li>
 	<li>MVC, WebAPI, SignalR are supported. WCF is not supported on OWIN at this point of time.</li>
</ul>
<h3 class="ArticleSubtitle"><strong>Project Katana to Asp.Net Core</strong></h3>
<ol>
 	<li>
<p class="ArticleContent">Project Katana is Microsoft’s first own implementation of OWIN specification and it is delivered as Nuget packages. Developers can include these packages from Nuget and start working.</p>
</li>
 	<li>
<p class="ArticleContent">The next version after Asp.Net 4.6 with full support of OWIN is planned and thus Project Katana was slowly retiring. Note – Any project implementation with Katana libraries will continue to work as expected.</p>
</li>
 	<li>
<p class="ArticleContent">.Net Core 1.0 is another implementation of .Net Framework. .Net Core is a <strong>portable, open-source, modular framework</strong> and it is re-built from scratch with <strong>new implementation of CLR</strong>.</p>
</li>
 	<li>
<p class="ArticleContent">Asp.Net 5.0 was renamed to <strong>Asp.Net Core</strong> since this framework was <strong>re-written from scratch</strong>. Asp.Net Core is <strong>delivered as Nuget packages</strong> and it will run on both <strong>.Net Core 1.0 and .Net Framework 4.5.1+</strong> frameworks. There is no <code>System.Web</code> anymore and everything which came with it.</p>
</li>
 	<li>As part of <a href="https://stackify.com/net-core-2-0-changes/">.NET Core</a>, Microsoft (and the community) has created a whole new web server called <strong>Kestrel</strong>. The goal behind it has been to make it as lean, mean, and fast as possible. IIS is awesome but comes with a very dated pipeline model and carries a lot of bloat and weight with it. In some <a href="https://github.com/aspnet/benchmarks" target="_blank" rel="noopener noreferrer">benchmarks</a>, I have seen Kestrel handle up to <strong>20x more requests per second</strong>. Yowzers!</li>
 	<li>You can use IIS as a reverse proxy sitting in front of Kestrel to take advantage of some of it’s features that Kestrel does not have. Things like virtual hosts, logging, security, etc. <strong><em>Microsoft still recommends using IIS to sit in front of your ASP.NET Core apps.</em></strong></li>
</ol>
<h2 id="components-of-aspnet-identity" class="heading-with-anchor">Components of Katana</h2>
<ul>
 	<li>The <strong>Microsoft.Owin.Hosting</strong> package will also install a number of dependencies such as Owin and Microsoft.Owin. These are the core <strong>Katana libraries</strong>.
<ul>
 	<li>Owin contains the core OWIN <strong>abstractions</strong>, whereas Microsoft.Owin is the <strong>Microsoft extension to OWIN</strong>.</li>
</ul>
</li>
 	<li>The <strong>Microsoft.Owin.Host.HttpListener</strong> library includes classes to communicate with the operating system. It also enables us to build a small app that listens to HTTP requests on a port.</li>
 	<li>The Startup class must have a Configuration method which accepts an IAppBuilder object which resides in the Owin namespace. Add the following stub to the Startup class:
<pre class="EnlighterJSRAW" data-enlighter-language="null">public class Startup
{
   public void Configuration(IAppBuilder appBuilder)
   {
      appBuilder.Run(owinContext =&gt;
      {
         owinContext.Response.ContentType = "text/plain";
         return owinContext.Response.WriteAsync("Hello World!");
      });
   }
}</pre>
</li>
 	<li> IAppBuilder includes methods that help us configure an application, in particular how it will respond to HTTP requests.</li>
 	<li>There are a lot of extension methods to the IAppBuilder interface. They are available in different Owin-related libraries. So as you reference additional Owin packages from NuGet you’ll see new extension methods available for the IAppBuilder interface. This provides you a way to enable new features as they become necessary.</li>
 	<li>The Run() <a title="Extension methods part 1: the basics" href="https://dotnetcodr.com/2014/03/06/extension-methods-part-1-the-basics/">extension method</a> helps us configure how the application will handle HTTP requests. Katana will call into this method to process the requests. It accepts a <a title="Events, delegates and lambdas in .NET C# part 5: lambda, Func, Action" href="https://dotnetcodr.com/2014/02/27/events-delegates-and-lambdas-in-net-c-part-5-lambda-func-action/">Func delegate</a> which returns a Task object and accepts an IOwinContext object as parameter. This is a lambda expression that accepts an IOwinContext object which will be inferred by the compiler.</li>
 	<li>As you type “owinContext.” IntelliSense will provide a list of interesting properties:
<ul>
 	<li>Authentication: to access properties of the current user, such as <a title="Introduction to Claims based security in .NET4.5 with C# Part 1: the absolute basics" href="https://dotnetcodr.com/2013/02/11/introduction-to-claims-based-security-in-net4-5-with-c-part-1/">Claims</a></li>
 	<li>Environment: helps you to retrieve a range of OWIN-related properties from the current OWIN context</li>
 	<li>Request: to access the properties related to the HTTP request such as headers and cookies</li>
 	<li>Response: to build and manipulate the HTTP response</li>
</ul>
</li>
 	<li>We’ll also use another object from OWIN called WebApp to set up our web server. It is a Katana component residing in the Microsoft.Owin.Hosting namespace. It has a Start method where you can specify the class that includes your configuration. Add the following code to Main:
<pre class="EnlighterJSRAW" data-enlighter-language="null">string uri = "http://localhost:7990";
 
using (WebApp.Start&lt;Startup&gt;(uri))
{
        Console.WriteLine("Web server on {0} starting.", uri);
        Console.ReadKey();
    Console.WriteLine("Web server on {0} stopping.", uri);
}</pre>
&nbsp;</li>
</ul>
<h2><a href="https://brockallen.com/2013/10/24/a-primer-on-owin-cookie-authentication-middleware-for-the-asp-net-developer/"><strong>OWIN cookie authentication middleware</strong></a></h2>
<ol>
 	<li>Previously, for local authentication we used to use Forms authentication and its job was to issue a cookie to represent the current logged in user. Upon subsequent requests from the user, Forms authentication would validate the cookie and make a principal object available that represents the user’s identity.</li>
 	<li>Now, the new cookie-based implementation is called the OWIN cookie authentication middleware. This performs the same task — it can issue a cookie and then validates the cookie on subsequent requests. One improvement the OWIN cookie authentication middleware has over the previous Forms authentication is that <strong>it is claims-aware</strong>.</li>
 	<li>The OWIN Cookie Authentication is a <strong>cookie and claims based authentication</strong> mechanism that can be used by <strong>any framework hosted on <a href="https://msdn.microsoft.com/magazine/dn451439.aspx" data-linktype="external">OWIN</a> or IIS</strong>.</li>
</ol>
<h3><a href="https://coding.abel.nu/2014/05/whats-this-owin-stuff-about/">OWIN &amp; Katana components</a></h3>
<ul>
 	<li><strong>OWIN- declares single interface IAppBuilder</strong></li>
 	<li><strong>Microsoft’s framework (<code>Microsoft.Owin.*</code>namespace)</strong> is called <strong><em>Katana</em> </strong>and is open sourced on <a href="http://katanaproject.codeplex.com/" target="_blank" rel="noopener">codeplex</a>. Katana contains a set of standard middleware for things like authentication, static file serving, logging and the self host</li>
 	<li>Important packages
<ul>
 	<li>Microsoft.Owin.Security.Cookies for the cookie middleware.</li>
 	<li>Microsoft.Owin.Security.Google for the Google authentication.</li>
 	<li>Microsoft.Owin.Host.SystemWeb to run the Owin pipeline on top of IIS.</li>
</ul>
</li>
 	<li>Microsoft.Owin.selfhost requires
<ul>
 	<li>Microsoft.Owin
<p id="NNbKuqK"><img class="alignnone wp-image-1209 " src="/wp-content/uploads/2018/03/img_5ab21f14ec251.png" alt="" width="138" height="80" /></p>
</li>
 	<li>Microsoft.Owin.Hosting
<p id="GyqGyzh"><img class="alignnone wp-image-1210 " src="/wp-content/uploads/2018/03/img_5ab22057c60a0.png" alt="" width="261" height="239" /></p>
</li>
 	<li>Microsoft.Owin.Diagnostics
<p id="pbrmGRa"><img class="alignnone wp-image-1212 " src="/wp-content/uploads/2018/03/img_5ab2227ddce80.png" alt="" width="208" height="249" /></p>
</li>
 	<li>Microsoft.Owin.Host.HttpListener
<p id="okpOxka"><img class="alignnone wp-image-1211 " src="/wp-content/uploads/2018/03/img_5ab2223f93ef0.png" alt="" width="215" height="63" /></p>
</li>
</ul>
</li>
</ul>
At the core, Owin is really simple. the <code>Owin.dll</code> contains a single interface, <code>IAppBuilder</code>.
<pre class="EnlighterJSRAW" data-enlighter-language="null">namespace Owin
{
    public interface IAppBuilder
    {
        IDictionary&lt;string, object&gt; Properties { get; }
        object Build(Type returnType);
        IAppBuilder New();
        IAppBuilder Use(object middleware, params object[] args);
    }
}</pre>
&nbsp;
<pre class="EnlighterJSRAW" data-enlighter-language="null">using Owin;
using Microsoft.Owin.Hosting;
namespace ConsoleAppFrameworkOwin
{
using AppFunc = Func&lt;IDictionary&lt;string, object&gt;, Task&gt;; //handler delegate
 
class Program
{
    static void Main(string[] args)
    {
        using (WebApp.Start("http://localhost:4242", Startup)) 
//WebApp requires hosting like Microsoft.Owin.selfhost
        {
            Console.ReadLine();
        }
    }
 
    private static void Startup(IAppBuilder app)
    {
        // Have to explicitly construct the Func&lt;...&gt; since the argument of
        // Use() is of type object.
        app.Use(new Func&lt;AppFunc, AppFunc&gt;(BasicAuthenticationMiddleware));
        app.Use(new Func&lt;AppFunc, AppFunc&gt;(StartPageMiddleware));
    }
 
    private static AppFunc BasicAuthenticationMiddleware(AppFunc next)
    {
        return new BasicAuthenticationHandler(next).InvokeAsync;
    }
 
    private static AppFunc StartPageMiddleware(AppFunc next)
    {
        return new StartPageHandler(next).InvokeAsync;
    }
}</pre>
<p id="AaTLxrd"><img class=" wp-image-1208 alignleft" src="/wp-content/uploads/2018/03/img_5ab20c3ca9b3e.png" alt="" width="269" height="143" /></p>
The hosting environment takes a <code>Startup</code> function that is called to set up everything. That function registers a set of <em>Middleware</em> with the application. For each request, the application calls each of the the middleware components with the head pointer of a linked list to an existing set of <em>handlers</em>. Each middleware can add one or more handlers to the request handling pipeline by returning a reference to the handler that will be the new head of the list. Each handler is responsible for remembering and invoking the next handler in the list.

The handler is a delegate with signature <code>Func&lt;IDictionary&lt;string, object&gt;, Task&gt;;</code>, most often abbreviated to <code>AppFunc</code> through <code>using AppFunc = Func&lt;IDictionary&lt;string, object&gt;, Task&gt;;</code>.

The signature of the middleware is <code>Func&lt;AppFunc,AppFunc&gt;</code>. It takes an <code>AppFunc</code> that is the current head of the linked list and it returns the new head of the list. There are also <a href="http://benfoster.io/blog/how-to-write-owin-middleware-in-5-different-steps" target="_blank" rel="noopener">other ways</a> to add middleware, but for this post, one way is enough.

&nbsp;
<h3>Refernces</h3>
<ul>
 	<li>https://docs.microsoft.com/en-us/aspnet/aspnet/overview/owin-and-katana/an-overview-of-project-katana</li>
 	<li>http://www.codedigest.com/posts/1/what-is-owin-a-beginners-guide</li>
 	<li>https://en.wikipedia.org/wiki/Open_Web_Interface_for_.NET</li>
 	<li>https://dotnetcodr.com/2014/04/14/owin-and-katana-part-1-the-basics/</li>
 	<li>https://www.c-sharpcorner.com/article/asp-net-core-api-day-one-getting-started-and-request-pipeline/</li>
 	<li><a href="https://msdn.microsoft.com/en-us/library/bb470252.aspx">ASP.NET Application Life Cycle Overview for IIS 7.0</a></li>
 	<li><a href="https://docs.microsoft.com/en-us/aspnet/aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline">OWIN Middleware in the IIS integrated pipeline</a></li>
</ul>
