---
layout: post
title: Interview questions ASP.NET - mvc
date: 2018-03-09 13:11
author: tmasabari
comments: true
categories: [Interview Preparation, Prepare, QuickRefresh, Uncategorized]
---
http://www.c-sharpcorner.com/UploadFile/8ef97c/most-asked-Asp-Net-mvc-interview-questions-and-answers/
<ul>
 	<li><em>MVC life cycle</em></li>
 	<li>how routing works in .net MVC from the base.</li>
 	<li><em>MVC Filters</em><em> </em></li>
 	<li><em>How to secure the http request using filter attribute.
</em>&nbsp;</li>
 	<li><em>Exception Attribute.</em></li>
 	<li><em>Different types of Filter Attribute.</em></li>
 	<li><em>HOw to bind the cs value to the javascript using .net MVC.</em></li>
 	<li><em>tempdata,viewbag and viewdata.</em><em>
</em>&nbsp;</li>
 	<li><em>difference between http post and http put.</em></li>
 	<li>in web api usage of IhttpActionResult.</li>
 	<li>Entity Framework basics.</li>
 	<li><em>Adv and dis advantage of entity framework</em></li>
</ul>
<h3>ASP.NET MVC6 | ASP.NET vNext MVCCore</h3>
<ul>
 	<li><strong>Single Programming Model</strong> for ASP.NET MVC and ASP.NET Web API.</li>
 	<li>Optimized for <strong>Cloud Computing</strong>.</li>
 	<li>Supporting <strong>side by side deployment</strong> of runtime and framework along with application.</li>
 	<li>Out of the box support for <strong>dependency injection</strong>.</li>
 	<li>vNext is <strong>Open Source</strong> and supports running on multiple platforms including Linux and Mac.</li>
 	<li>New <strong>JSON-based</strong> project Extension.</li>
 	<li>In order to dynamically compile code, <strong>Roslyn compiler</strong> is used.For details on new features in <strong>ASP.NET vNext</strong>, follow <a title="Top New Features of ASP.NET vNext" href="http://www.webdevelopmenthelp.net/2015/06/features-of-asp-net-vnext.html">here</a>.</li>
</ul>
<h3>ASP.NET MVC5</h3>
<div>
<ul>
 	<li><strong>ASP.NET Identity</strong> for authentication and identity management. Thesedays, modern applications are developed for broader range of clients such as web, mobile in mind. Also, users are actively using their social identities from various social channels like facebook, youtube, twitter etc. ASP.NET Identity is a new Membership system to handle authentication and authorization for variety of clients as well as using user’s existing social identities.</li>
 	<li><strong>Authentication Filters</strong> for authenticating user by custom or third-party authentication provider.</li>
 	<li>With the help of <strong>Filter overrides</strong>, we can now override filters on a method or controller.</li>
 	<li><strong>Bootstrap</strong> replaced the default MVC template.</li>
 	<li><strong>Attribute Routing</strong> is now integrated into MVC5. Basically, MVC Routing is an excellent way to create human friendly and Search Engine Optimized URLs. You can easily get <a title="Understanding Routing in ASP.NET MVC" href="http://www.webdevelopmenthelp.net/2014/03/routing-in-asp-net-mvc.html" target="_blank" rel="noopener">understanding about Routing in ASP.NET MVC</a> here. Attribute based routing enables us to define routes along with action methods as follows:</li>
</ul>
</div>
<p id="WzafTHa"><img class="alignnone size-full wp-image-452 " src="/wp-content/uploads/2017/12/img_5a2a1b5b9cebc.png" alt="" /></p>
<a href="http://www.webdevelopmenthelp.net/2014/10/aspx-view-engine-vs-razor-view-engine.html">http://www.webdevelopmenthelp.net/2014/10/aspx-view-engine-vs-razor-view-engine.html</a>

<strong>Why is Razor?</strong>
<ol>
 	<li>Compact &amp; Expressive.</li>
 	<li>Razor minimizes the number of characters and keystrokes required in a file, and enables a fast coding workflow. Unlike most template syntaxes, you do not need to interrupt your coding to explicitly denote server blocks within your HTML. The parser is smart enough to infer this from your code. This enables a really compact and expressive syntax which is clean, fast and fun to type.</li>
 	<li>Easy to Learn: Razor is easy to learn and enables you to quickly be productive with a minimum of effort. We can use all your existing language and HTML skills.</li>
 	<li>Works with any Text Editor: Razor doesn't require a specific tool and enables you to be productive in any plain old text editor (notepad works great).</li>
 	<li>Has great Intellisense:</li>
 	<li>Unit Testable: The new view engine implementation will support the ability to unit test views (without requiring a controller or web-server, and can be hosted in any unit test project - no special app-domain required).</li>
</ol>
<table border="1" width="100%" cellspacing="1" bgcolor="#ffffff">
<tbody>
<tr bgcolor="#0270bf">
<td><strong>Razor View Engine</strong></td>
<td><strong>ASPX View Engine (Web form view engine)</strong></td>
</tr>
<tr>
<td>The namespace used by the Razor View Engine is System.Web.Razor</td>
<td>The namespace used by the ASPX View Engine is System.Web.Mvc.WebFormViewEngine</td>
</tr>
<tr>
<td>The file extensions used by the Razor View Engine are different from a web form view engine. It uses cshtml with C# and vbhtml with vb for views, partial view, templates and layout pages.</td>
<td>The file extensions used by the Web Form View Engines are like ASP.Net web forms. It uses the ASPX extension to view the aspc extension for partial views or User Controls or templates and master extensions for layout/master pages.</td>
</tr>
<tr>
<td>The Razor View Engine is an advanced view engine that was introduced with MVC 3.0. This is not a new language but it is markup.</td>
<td>A web form view engine is the default view engine and available from the beginning of MVC</td>
</tr>
<tr>
<td>Razor has a syntax that is very compact and helps us to reduce typing.</td>
<td>The web form view engine has syntax that is the same as an ASP.Net forms application.</td>
</tr>
<tr>
<td>The Razor View Engine uses @ to render server-side content.</td>
<td>The ASPX/web form view engine uses "&lt;%= %&gt;" or "&lt;%: %&gt;" to render server-side content.</td>
</tr>
<tr>
<td>By default all text from an @ expression is HTML encoded.</td>
<td>There is a different syntax ("&lt;%: %&gt;") to make text HTML encoded.</td>
</tr>
<tr>
<td>Razor does not require the code block to be closed, the Razor View Engine parses itself and it is able to decide at runtime which is a content element and which is a code element.</td>
<td>A web form view engine requires the code block to be closed properly otherwise it throws a runtime exception.</td>
</tr>
<tr>
<td>The Razor View Engine prevents Cross Site Scripting (XSS) attacks by encoding the script or HTML tags before rendering to the view.</td>
<td>A web form View engine does not prevent Cross Site Scripting (XSS) attack.</td>
</tr>
<tr>
<td>The Razor Engine supports Test Driven Development (TDD).</td>
<td>Web Form view engine does not support Test Driven Development (TDD) because it depends on the System.Web.UI.Page class to make the testing complex.</td>
</tr>
<tr>
<td>Razor uses "@* â€¦ *@" for multiline comments.</td>
<td>The ASPX View Engine uses "&lt;!--...--&gt;" for markup and "/* â€¦ */" for C# code.</td>
</tr>
<tr>
<td>There is only three transition characters with the Razor View Engine.</td>
<td>There are only three transition characters with the Razor View Engine.</td>
</tr>
</tbody>
</table>
The Razor View Engine is a bit slower than the ASPX View Engine.
<table width="95%" align="center">
<tbody>
<tr>
<td class="TDWithBorder" width="50%">
<h2>ASPX View Engine</h2>
</td>
<td class="TDWithBorder" width="50%">
<h2>Razor View Engine</h2>
</td>
</tr>
<tr>
<td class="TDWithBorder" width="50%"><strong><em>System.Web.Mvc.WebFormViewEngine</em></strong> is the namespace for ASPX View Engine.</td>
<td class="TDWithBorder" width="50%">Namespace for ASPX view Engine is <em><strong>System.Web.Razor</strong></em>.</td>
</tr>
<tr>
<td class="TDWithBorder" width="50%">File Extension for this View Engine is similar to WebForm as:
<ul>
 	<li>.aspx, for Views just like Web Form pages.</li>
 	<li>.ascx, for Partial Views &amp; Editor Template just like User Controls.</li>
 	<li>.master, for Layout and Master Pages just like Master Pages in Web Forms.</li>
</ul>
</td>
<td class="TDWithBorder" width="50%">As it’s new and advanced View Engine, it’s extensions are totally different.
<ul>
 	<li>.cshtml (Razor C#), For all including Views, Partial Views, Editor Template and Layout Pages.</li>
 	<li>.vbhtml (Razor VB.NET), For all including Views, Partial Views, Editor Template and Layout Pages.</li>
 	<li></li>
</ul>
</td>
</tr>
</tbody>
</table>
<table width="95%" align="center">
<tbody>
<tr>
<td class="TDWithBorder" width="50%">ASPX syntax is inherited from Web Forms, so it’s understandable for Web Forms developer but it’s not that much clean as compared to Razor View Engine.</td>
<td class="TDWithBorder" width="50%">As Razor View Engine is introduced later in MVC3, it’s syntax is designed to be clean, expressive and easy to learn.</td>
</tr>
<tr>
<td class="TDWithBorder" width="50%">ASPX View Engine does nothing to avoid Cross-Site Scripting attacks by default.</td>
<td class="TDWithBorder" width="50%">By default, Razor View Engine encodes html tags or scripts before it’s being rendered to view that avoids Cross-Site Scripting attacks.</td>
</tr>
</tbody>
</table>
<a href="http://www.c-sharpcorner.com/UploadFile/0ef46a/routing-in-mvc/">http://www.c-sharpcorner.com/UploadFile/0ef46a/routing-in-mvc/</a>

<strong>Explain what is routing in MVC? What are the three segments for routing important?</strong>

<strong>Answer: </strong>Routing is a mechanism to process the incoming url that is more descriptive and give desired response.

Beware that in this URL-based approach, any dots/periods in your parameter values will cause your URL to get picked up by the static file URL manager and your API will not work. This is a known problem with all the ASP.NET MVC routing approaches and there is no properly performing workaround (IMHO). More discussion here: <a href="http://stackoverflow.com/questions/20998816/dot-character-in-mvc-web-api-2-for-request-such-as-api-people-staff-45287">stackoverflow.com/questions/20998816/…</a> Note that a lot of the fixes are specific to a version of MVC, so what works for one may not work on yours

There are two types of routing (after the introduction of ASP.NET MVC 5).
<ol>
 	<li><strong>Convention based routing:</strong> to define this type of routing, we call MapRoute method and set its unique name, url pattern and specify some default values.</li>
 	<li><strong>Attribute based routing:</strong> to define this type of routing, we specify the Route attribute in the action method of the controller. By using the "Route" attribute we can define the URL structure
<ol>
 	<li class="alt"><span class="keyword">public</span> <span class="keyword">class</span> HomeController: Controller</li>
 	<li>{</li>
 	<li class="alt">    [Route(<span class="string">"Users/about"</span>)]</li>
 	<li>    publicActionResultGotoAbout()</li>
 	<li class="alt">    {</li>
 	<li>        <span class="keyword">return</span> View();</li>
 	<li class="alt">    }</li>
 	<li>}</li>
</ol>
</li>
</ol>
There are three segments for routing that are important,
<ol>
 	<li>ControllerName</li>
 	<li>ActionMethodName</li>
 	<li>Parammeter</li>
</ol>
<table border="1" width="100%" cellspacing="1" bgcolor="#ffffff">
<tbody>
<tr bgcolor="#0270bf">
<td><strong>Route definition</strong></td>
<td><strong>Example of matching URL</strong></td>
</tr>
<tr>
<td>{controller}/{action}/{id}</td>
<td>/Products/show/beverages</td>
</tr>
<tr>
<td>{table}/Details.aspx</td>
<td>/Products/Details.aspx</td>
</tr>
<tr>
<td>blog/{action}/{entry}</td>
<td>/blog/show/123</td>
</tr>
<tr>
<td>{reporttype}/{year}/{month}/{day}</td>
<td>/sales/2008/1/5</td>
</tr>
<tr>
<td>{locale}/{action}</td>
<td>/US/show</td>
</tr>
<tr>
<td>{language}-{country}/{action}</td>
<td>/en-US/show</td>
</tr>
</tbody>
</table>
<p id="lMFIVfP">The default ASP.NET MVC project templates add a generic route that uses the following URL convention to break the URL for a given request into three named segments.</p>
<strong>URL: </strong>"{controller}/{action}/{id}"

This route pattern is registered via call to the <strong>MapRoute()</strong> extension method of <strong>RouteCollection</strong>.

<img src="http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/8ef97c/most-asked-Asp-Net-mvc-interview-questions-and-answers/Images/RouteCollection.jpg" alt="RouteCollection" />

Suppose we have a controller named "Admin" and sometime in the future we require to modify the name of that controller.
<div class="dp-highlighter">
<ol class="dp-c" start="1">
 	<li class="alt"><span class="keyword">public</span> <span class="keyword">static</span> <span class="keyword">void</span> RegisterRoutes (RouteCollection routes) {</li>
 	<li>routes.MapRoute (<span class="string">"Admin"</span>,<span class="string">"Admin/{action}"</span>,</li>
 	<li class="alt">    <span class="keyword">new</span> {controller=<span class="string">"Home"</span>});</li>
 	<li>}</li>
</ol>
</div>
Thus, when a request as <strong>/Admin/Index</strong> comes to the server, the controller called is <strong>/Home/Index</strong>,

The same can be done in case of an Action as well, i.e. if an action is removed from the controller, we can have a default route check for that action as well and redirect to the specified and default route URL if not found. Like as below:
<div class="dp-highlighter">
<ol class="dp-c" start="1">
 	<li class="alt">routes.MapRoute(<span class="string">"Admin"</span>,<span class="string">"Admin/department"</span>,</li>
 	<li><span class="keyword">new</span> {controller = <span class="string">"Admin"</span>,action = <span class="string">"Index"</span>});</li>
</ol>
First off, take note that we have added the new, more specific route <strong><em>before the default in the file</em></strong> (which determines the order it is added to the route dictionary). This is because <strong><em>routes are evaluated for a match to an incoming URL in order</em></strong>. The default MVC route is pretty general, and if route order is not carefully considered when adding additional routes to your project, the default route may inadvertently match a URL intended for a different handler.
<h3>Extra parameters in Route</h3>
Parameters are directly supported in MVC by simply adding parameters onto your action methods. Given an action like the following:
<pre><code>public ActionResult GetImages(string artistName, string apiKey)</code></pre>
<pre><code>/Artist/GetImages/?artistName=cher&amp;apiKey=XXX</code></pre>
<pre><code>/Artist/GetImages/cher/api-key</code></pre>
you could add a route like:
<pre><code>routes.MapRoute(
            "ArtistImages",                                              // Route name
            "{controller}/{action}/{artistName}/{apikey}",                           // URL with parameters
            new { controller = "Home", action = "Index", artistName = "", apikey = "" }  // Parameter defaults
        );</code></pre>
<pre><code>routes.MapRoute(
    "ArtistsImages",
    "{ws}/artists/{artist}/{action}/{*apikey}",
    new { ws = "2.0", controller="artists" artist = "", action="", apikey="" }
    );</code></pre>
So if someone used the following route:
<pre><code>ws.audioscrobbler.com/2.0/artists/cher/images/b25b959554ed76058ac220b7b2e0a026/</code></pre>
</div>
<h3>Regular Expressions in Route Constraints</h3>
When a <code>string </code>is provided as a constraint, the MVC framework interprets the <code>string </code>as a Regular Expression, which can be employed to limit the ways a URL might match a particular route. A common scenario in this regard would be to restrict the value of a route parameter to numeric values.

http://domain/blog/posts/123
<pre class="notranslate" lang="cs">routes.MapRoute(
    name: <span class="code-string">"</span><span class="code-string">BlogPost"</span>,
    url: <span class="code-string">"</span><span class="code-string">blog/posts/{postId}"</span>,
    defaults: <span class="code-keyword">new</span>
    {
        controller = <span class="code-string">"</span><span class="code-string">Posts"</span>,
        action = <span class="code-string">"</span><span class="code-string">GetPost"</span>,
    }, 
    <span class="code-keyword">new</span> {postId = <span class="code-string">@"</span><span class="code-string">\d+"</span> }
);

</pre>
<h5 class="pageHeading"><a href="http://techfunda.com/howto/19/naming-conventions-in-asp-net-mvc">What are the naming conventions to follow in ASP.NET MVC?</a></h5>
The <code>Controller</code> suffix is baked into the the <a href="https://github.com/mono/aspnetwebstack/blob/master/src/System.Web.Mvc/ControllerDescriptor.cs#L19" rel="nofollow noreferrer"><code>ControllerDescriptor</code></a> and <a href="https://github.com/mono/aspnetwebstack/blob/master/src/System.Web.Mvc/ControllerTypeCache.cs#L86" rel="nofollow noreferrer"><code>ControllerTypeCache</code></a>classes making it hard to override.

Mainly three naming convention should be followed in ASP.NET MVC application
<ul>
 	<li><strong>Areas</strong> - Areas are used to create different modules inside an ASP.NET MVC application. Each module can have their own set of controllers, models and views and the naming conventions of these will follows the same principal as described above.</li>
 	<li><strong><a href="http://techfunda.com/Howto/asp-net-mvc/controller" target="_blank" rel="noopener">Controller</a></strong> - Its name must end with “controller” word. Eg. PersonalDetails<em>Controller. Generally all controllers should be kept inside ~/Controllers folder of the project.</em></li>
 	<li><strong><a href="http://techfunda.com/Howto/asp-net-mvc/view-form-specific" target="_blank" rel="noopener">Views</a></strong> – There should be a view folder inside ~/Views folder corresponding to each controller. Like for PersonalDetailsController, there should be a folder ~/Views/PersonalDetails</li>
 	<li><strong><a href="http://techfunda.com/Howto/asp-net-mvc/models" target="_blank" rel="noopener">Model</a></strong> - Model name (Singular name) corresponding to the database table should be similar to the database table name (not mandatory, however its  ideal). For example, if the database table name is "PersonalDetails" (Plural), the model name should be "PersonalDetail" (Singular).Generally, all models are kept inside the ~/Models folder of the project.
<ul>
 	<li><a title="Using ViewModel in ASP.NET MVC - List data from more than one tables in asp.net mvc" href="http://techfunda.com/Howto/asp-net-mvc/262/list-data-using-viewmodel" target="_blank" rel="noopener">ViewModel</a> -  View model is a class that contains properties from more than one Models, generally used to list data from more than one database tables, read <a title="List data using ViewModel" href="http://techfunda.com/Howto/asp-net-mvc/262/list-data-using-viewmodel" target="_blank" rel="noopener">more here</a>.</li>
 	<li>the ViewModel name should contain the name of all Models whose properties are kept in this ViewModel (not mandatory)  if the ViewModel contains the properties of PersonalDetail and File models, I would give its name as PersonalDetailFile<em>ViewModel</em>.</li>
 	<li>Sometimes ViewModel names are also kept based on the Action method in which it has to be used. For example, if we have to create a Login page where any of our Model would not fit so we can create a model named Login<em>ViewModel</em></li>
</ul>
</li>
</ul>
MVC Request cycle

https://www.codeproject.com/Articles/1028156/A-Detailed-Walkthrough-of-ASP-NET-MVC-Request-Life

<img class="alignnone wp-image-451 " src="/wp-content/uploads/2017/12/img_5a2a199f65ed6.png" alt="" width="464" height="338" />
<p id="bzReVCZ"><img class="alignnone size-full wp-image-453 " src="/wp-content/uploads/2017/12/img_5a2a1d43183f2.png" alt="" /></p>
<p id="keQQNuJ"><img class="alignnone size-full wp-image-461 " src="/wp-content/uploads/2017/12/img_5a2a74d3c22eb.png" alt="" /></p>

<h2>Filters</h2>
Filters are designed to inject logic in between MVC request life cycle..

<strong>Types of Filters:</strong>

<img class="alignnone size-full wp-image-455 " src="/wp-content/uploads/2017/12/img_5a2a20a4601ff.png" alt="" />

ASP.NET MVC framework supports the following action filters:
<ul>
 	<li><strong>Action Filters:</strong> Action filters are used to implement logic that gets executed before and after a controller action executes. We will look at Action Filters in detail in this chapter.</li>
 	<li><strong>Authorization Filters: </strong>Authorization filters are used to implement authentication and authorization for controller actions.</li>
 	<li><strong>Result Filters:</strong> Result filters contain logic that is executed before and after a view result is executed. For example, you might want to modify a view result right before the view is rendered to the browser.</li>
 	<li><strong>Exception Filters: </strong>Exception filters are the last type of filter to run. You can use an exception filter to handle errors raised by either your controller actions or controller action results. You can also use exception filters to log errors.</li>
 	<li><strong><strong>Authentication Filters:</strong></strong>Authentication filters are new addition from MVC 5. These filters kick in first in the request life cycle and perform the authentication logic.</li>
 	<li>Authorization filters are executed after the Authentication filters successfully executed and authorizes users roles to ensure current user has access to request resource.</li>
 	<li>Action filters are executed next in the request life cycle and execute any custom logic you may want to perform before and after action execution.</li>
 	<li>Result filters are executed before and after result execution.</li>
 	<li>Finally, the exception filters are executed when there is an exception during processing of request.<strong> </strong></li>
</ul>
<strong>ASP.NET MVC provides the following action filters:</strong>
<ul>
 	<li><strong>Output Cache: </strong>This action filter caches the output of a controller action for a specified amount of time.</li>
 	<li><strong>Handle Error:</strong> This action filter handles errors raised when a controller action executes.</li>
 	<li><strong>Authorize: </strong>This action filter enables you to restrict access to a particular user or role.</li>
</ul>
<div class="grid_6">
<div class="last code-sample">
<div class="syntax-container"></div>
</div>
</div>
<p id="LRfBpsC"><img class="alignnone size-full wp-image-456 " src="/wp-content/uploads/2017/12/img_5a2a213593124.png" alt="" /></p>
<strong>ViewData VS ViewBag VS TempData</strong>

Better to use ViewBag as there is not type conversion required and dynamic. Slower
<ol>
 	<li>ViewBag is a dynamic property that takes advantage of the new dynamic features in C# 4.0</li>
 	<li>TempData is able to keep data for the duration of a HTP request, in other words it can keep live data between two consecutive HTTP requests. It will help us to pass the state between action methods. TempData only works with the current and subsequent request. TempData uses a session variable to store the data. TempData Requires type casting when used to retrieve data.</li>
</ol>
<table border="1" width="80%" cellspacing="1" bgcolor="#ffffff">
<tbody>
<tr bgcolor="#e36c0a">
<td bgcolor="#0270bf" height="33"><strong>ViewData</strong></td>
<td bgcolor="#0270bf" height="33"><strong>ViewBag</strong></td>
<td bgcolor="#0270bf" height="33"><strong>TempData</strong></td>
</tr>
<tr>
<td width="235">It is Key-Value Dictionary collection</td>
<td width="217">It is a type object</td>
<td width="225">It is Key-Value Dictionary collection</td>
</tr>
<tr>
<td width="235">ViewData is a dictionary object and it is property of ControllerBase class</td>
<td width="217">ViewBag is Dynamic property of ControllerBase class.</td>
<td width="225">TempData is a dictionary object and it is property of controllerBase class.</td>
</tr>
<tr>
<td width="235">ViewData is Faster than ViewBag</td>
<td width="217">ViewBag is slower than ViewData</td>
<td width="225">NA</td>
</tr>
<tr>
<td width="235">ViewData is introduced in MVC 1.0 and available in MVC 1.0 and above</td>
<td width="217">ViewBag is introduced in MVC 3.0 and available in MVC 3.0 and above</td>
<td width="225">TempData is also introduced in MVC1.0 and available in MVC 1.0 and above.</td>
</tr>
<tr>
<td width="235">ViewData also works with .net framework 3.5 and above</td>
<td width="217">ViewBag only works with .net framework 4.0 and above</td>
<td width="225">TempData also works with .net framework 3.5 and above</td>
</tr>
<tr>
<td width="235">Type Conversion code is required while enumerating</td>
<td width="217">In depth, ViewBag is used dynamic, so there is no need to type conversion while enumerating.</td>
<td width="225">Type Conversion code is required while enumerating</td>
</tr>
<tr>
<td width="235">Its value becomes null if redirection has occurred.</td>
<td width="217">Same as ViewData</td>
<td width="225">TempData is used to pass data between two consecutive requests.</td>
</tr>
<tr>
<td width="235">It lies only during the current request.</td>
<td width="217">Same as ViewData</td>
<td width="225">TempData only works during the current and subsequent request</td>
</tr>
</tbody>
</table>
There following HTML helpers can be used to render (modify and output) HTML form elements:
<ul>
 	<li>BeginForm()</li>
 	<li>EndForm()</li>
 	<li>TextArea()</li>
 	<li>TextBox()</li>
 	<li>CheckBox()</li>
 	<li>RadioButton()</li>
 	<li>ListBox()</li>
 	<li>DropDownList()</li>
 	<li>Hidden()</li>
 	<li>Password(</li>
</ul>
There are the following approach which is used to connect with database to application.
<ul>
 	<li>Database First</li>
 	<li>Model First</li>
 	<li>Code First</li>
</ul>
GET

GET is used to request data from a specified resource. With all the GET request we pass the URL which is compulsory, however it can take the following overloads.

<em>.get(url [, data ] [, success(data, textStatus, jqXHR) ] [, dataType ] ).done/.fail</em>

<strong>POST</strong>

POST is used to submit data to be processed to a specified resource. With all the POST requests we pass the URL which is compulsory and the data, however it can take the following overloads.

<em>.post(url [, data ] [, success(data, textStatus, jqXHR) ] [, dataType ] )</em>

Test

https://stackoverflow.com/questions/36894210/test-if-a-requests-url-is-in-the-route-tablehttps://github.com/NightOwl888/MvcRouteTesting
