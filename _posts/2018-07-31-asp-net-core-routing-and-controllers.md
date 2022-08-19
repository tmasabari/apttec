---
layout: post
title: ASP.NET Core - Routing and Controllers
date: 2018-07-31 20:50
author: tmasabari
comments: true
categories: [ASP.NET, ASP.NET Core]
---
Routing https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/routing?view=aspnetcore-2.1#mixed-routing-attribute-routing-vs-conventional-routing
<h2 id="mixed-routing-attribute-routing-vs-conventional-routing" class="heading-with-anchor">Mixed routing: Attribute routing vs conventional routing</h2>
<p class="">MVC applications can mix the use of conventional routing and attribute routing. It's typical to use conventional routes for controllers serving HTML pages for browsers, and attribute routing for controllers serving REST APIs.</p>
<p class="">Actions are either conventionally routed or attribute routed. Placing a route on the controller or the action makes it attribute routed. Actions that define attribute routes cannot be reached through the conventional routes and vice-versa. <strong>Any</strong> route attribute on the controller makes all actions in the controller attribute routed.</p>

<div class="NOTE alert">

Note

What distinguishes the two types of routing systems is the process applied after a URL matches a route template. In conventional routing, the route values from the match are used to choose the action and controller from a lookup table of all conventional routed actions. In attribute routing, each template is already associated with an action, and no further lookup is needed.

</div>
<h1>Controller base class</h1>
There is indeed no particular <code>ApiController</code> class anymore since MVC and WebAPI have been merged in ASP.NET Core.

However, the <code>Controller</code> class of MVC brings in a bunch of features you probably won't need when developing just a Web API, such as a views and model binding.

You've got few options :

<strong>Use the <code>ControllerBase</code> class in the <a href="https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.Core/ControllerBase.cs" rel="noreferrer">Microsoft.AspNetCore.Mvc.Core</a> package.</strong>

The <code>ControllerBase</code> class provides access to several properties and methods. In the preceding code, examples include <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest" data-linktype="absolute-path">BadRequest</a> and <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction" data-linktype="absolute-path">CreatedAtAction</a>. These methods are called within action methods to return HTTP 400 and 201 status codes, respectively. The <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate" data-linktype="absolute-path">ModelState</a> property, also provided by <code>ControllerBase</code>, is accessed to handle request model validation.

Since ASP.NET Core 2.1 a new set of types is available to create Web API controllers. You can annotate your controllers with the <code>[ApiController]</code> attribute which enables a few new features such as automatic model state validation and binding source parameter inference. See the docs for more information: <a href="https://docs.microsoft.com/en-us/aspnet/core/web-api/index?view=aspnetcore-2.1#annotate-class-with-apicontrollerattribute" rel="noreferrer">https://docs.microsoft.com/en-us/aspnet/core/web-api/index?view=aspnetcore-2.1#annotate-class-with-apicontrollerattribute</a>.

The <code>[ApiController]</code> attribute is commonly coupled with <code>ControllerBase</code> to enable REST-specific behavior for controllers. <code>ControllerBase</code> provides access to methods such as <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound" data-linktype="absolute-path">NotFound</a> and <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file" data-linktype="absolute-path">File</a>.

<strong>Or</strong>

Create your <code>ApiController</code> base class. The key here is to add the <code>[ActionContext]</code> attribute which injects the current <code>ActionContext</code> instance into the property:
<pre class="lang-cs prettyprint prettyprinted"><code><span class="pun">[</span><span class="pun">ApiController]</span>
<span class="kwd">public</span> <span class="kwd">abstract</span> <span class="kwd">class</span> <span class="typ">ApiControllerBase</span>
<span class="pun">{</span>
    <span class="pun">[</span><span class="typ">ActionContext</span><span class="pun">]</span>
    <span class="kwd">public</span> <span class="typ">ActionContext</span> <span class="typ">ActionContext</span> <span class="pun">{</span><span class="pln"> get</span><span class="pun">;</span> <span class="typ">set</span><span class="pun">;</span> <span class="pun">}</span>
<span class="pun">}</span></code></pre>
Also, add the <code>[Controller]</code> attribute to the class to mark it as a controller for the MVC controller discovery.
<h3 id="automatic-http-400-responses" class="heading-with-anchor">Automatic HTTP 400 responses</h3>
<p class="">Validation errors automatically trigger an HTTP 400 response. The following code becomes unnecessary in your actions:</p>

<div class="codeHeader" data-bi-name="code-header"><span class="language">C#</span><button class="action" data-bi-name="copy">Copy</button></div>
<pre><code class="lang-csharp"><span class="hljs-keyword">if</span> (!ModelState.IsValid)
{
    <span class="hljs-keyword">return</span> BadRequest(ModelState);
}
</code></pre>
The default behavior is disabled when the <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.apibehavioroptions.suppressmodelstateinvalidfilter" data-linktype="absolute-path">SuppressModelStateInvalidFilter</a>property is set to <code>true</code>. Add the following code in <em>Startup.ConfigureServices</em> after <code>services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);</code>:
<div class="codeHeader" data-bi-name="code-header"><span class="language">C#</span><button class="action" data-bi-name="copy">Copy</button></div>
<pre><code class="lang-csharp">services.Configure&lt;ApiBehaviorOptions&gt;(options =&gt;
{
    options.SuppressConsumesConstraintForFormFileParameters = <span class="hljs-literal">true</span>;
    options.SuppressInferBindingSourcesForParameters = <span class="hljs-literal">true</span>;
<span class="line-highlight">    options.SuppressModelStateInvalidFilter = <span class="hljs-literal">true</span>;</span>
});</code></pre>
<table>
<thead>
<tr>
<th class="">Attribute</th>
<th>Binding source</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute" data-linktype="absolute-path">[FromBody]</a></strong></td>
<td>Request body</td>
</tr>
<tr>
<td><strong><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute" data-linktype="absolute-path">[FromForm]</a></strong></td>
<td>Form data in the request body</td>
</tr>
<tr>
<td><strong><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute" data-linktype="absolute-path">[FromHeader]</a></strong></td>
<td>Request header</td>
</tr>
<tr>
<td><strong><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute" data-linktype="absolute-path">[FromQuery]</a></strong></td>
<td>Request query string parameter</td>
</tr>
<tr>
<td><strong><a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute" data-linktype="absolute-path">[FromRoute]</a></strong></td>
<td>Route data from the current request</td>
</tr>
<tr>
<td><strong><a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/dependency-injection?view=aspnetcore-2.1#action-injection-with-fromservices" data-linktype="relative-path">[FromServices]</a></strong></td>
<td>The request service injected as an action parameter</td>
</tr>
</tbody>
</table>
