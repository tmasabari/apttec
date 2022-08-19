---
layout: post
title: REST, API - 4 0 2 WebAPI - updated - docx
date: 2018-03-20 17:24
author: tmasabari
comments: true
categories: [Interview Preparation, WEBAPI]
---
&nbsp;

<strong>Explain what is REST and RESTFUL?</strong>

REST represents REpresentational  State Transfer; it is entirely a new aspect of writing a web app.

RESTFUL: It is term written by applying REST architectural concepts is called RESTful services. It focuses on system resources and how the state of the resource should be transported over HTTP protocol

REST is architectural style. It has defined guidelines for creating services which are scalable. REST used with HTTP protocol using its verbs GET, PUT, POST and DELETE.

<strong>Who can consume WebAPI?</strong>

WebAPI can be consumed by any client which supports HTTP verbs such as GET, PUT, DELETE, POST. As WebAPI services don’t need any configuration, they are very easy to consume by any client. Infract, even portable devices like Mobile devices can easily consume WebAPI which is certainly the biggest advantages of this technology.
<div>

<strong>What New Features comes with ASP.NET Web API 2.0?</strong>

The latest features of ASP.NET Web API framework v2.0 are as follows:
<ul>
 	<li>Attribute Routing</li>
 	<li>Cross-Origin Resource Sharing</li>
 	<li>External Authentication</li>
 	<li>Open Web Interface NET</li>
 	<li>HttpActionResult</li>
 	<li>Web API OData</li>
</ul>
&nbsp;

&nbsp;

</div>
<strong>7) Web API supports which protocol? </strong>Web App supports HTTP protocol.

<strong>8) Which .NET framework supports Web API?  </strong>NET 4.0 and above version supports web API.

<strong>9) Web API uses which of the following open-source library for JSON serialization? </strong>Web API uses Json.NET library for JSON serialization.

<strong>6) What are main return types supported in Web API?</strong>

A Web API controller action can return following values:
<ul>
 	<li>Void – It will return empty content</li>
 	<li>HttpResponseMessage – It will convert the response to an HTTP message.</li>
 	<li>IHttpActionResult – internally calls ExecuteAsync to create an HttpResponseMessage</li>
 	<li>Other types – You can write the serialized return value into the response body</li>
</ul>
<h4>How to Return View from ASP.NET Web API Method?</h4>
(A tricky Interview question) No, we can't return view from ASP.NET Web API method.

&nbsp;

<strong>How Can assign alias name for ASP.NET Web API Action?</strong>

We can give alias name for Web API action same as in case of ASP.NET MVC by using “ActionName” attribute as follows:
<div id="crayon-5a97d7a2cbd35249437016-1" class="crayon-line"><span style="color: #ff0000;"><span class="crayon-sy">[</span><span class="crayon-v">HttpPost</span></span><span class="crayon-sy"><span style="color: #ff0000;">]</span> //restrict method to specific verbs</span></div>
<div id="crayon-5a97d7a2cbd35249437016-3" class="crayon-line"><span style="color: #99cc00;"><span class="crayon-sy">[</span><span class="crayon-e">ActionName</span><span class="crayon-sy">(</span><span class="crayon-s">"SaveStudentInfo"</span><span class="crayon-sy">)</span></span><span class="crayon-sy"><span style="color: #99cc00;">]</span> //alternate name</span></div>
<div id="crayon-5a97d7a2cbd35249437016-5" class="crayon-line"><span class="crayon-m">public</span> <span class="crayon-t">void</span> <span class="crayon-e">UpdateStudent</span><span class="crayon-sy">(</span><span class="crayon-e">Student </span><span class="crayon-v">aStudent</span><span class="crayon-sy">)</span></div>
<div></div>
<strong>Explain exception filters?</strong>

It will be executed when exceptions are unhandled and thrown from a controller meth<em>o</em>d. The reason for the exception can be anything. Exception filters will implement “IExceptionFilter” interface.
<div id="crayon-5a97d7a2cbd36327889277-1" class="crayon-line"><span class="crayon-sy">[</span><span class="crayon-v" style="color: #800080;">NotImplExceptionFilter</span><span class="crayon-sy">]</span></div>
<div id="crayon-5a97d7a2cbd36327889277-3" class="crayon-line"><span class="crayon-m">public</span> <span class="crayon-e">TestCustomer </span><span class="crayon-e">GetMyTestCustomer</span><span class="crayon-sy">(</span><span class="crayon-t">int</span> <span class="crayon-v">custid</span><span class="crayon-sy">)</span></div>
<div></div>
<h1><strong>Web API Design Book</strong></h1>
<u><a href="http://www.infoq.com/news/2012/03/web-api-design-book" target="_blank" rel="noopener">http://www.infoq.com/news/2012/03/web-api-design-book</a></u>

The goal is to make sure that your API is intuitive and easy to use for the app developer.
<h2><strong>Nouns. </strong></h2>
Use nouns instead of verbs in your base URLs, and keep them simple by using two base URLs per resource. Use HTTP verbs (GET, POST, PUT and DELETE) to operate on collections and elements. <u>Use plural rather than singular nouns. Use concrete rather than abstract names.</u> For example, here's how to get all dogs and a specific dog.

GET /dogs

GET /dogs/1

The book discusses options when the client does not support all the different HTTP methods.

Our HTTP verbs are POST, GET, PUT, and DELETE. (We think of them as mapping to the acronym, CRUD (Create-Read-Update-Delete).)

<img class="wp-image-1172" src="/wp-content/uploads/2018/03/image1-6.png" alt="image1 6" />

Concrete names are better than abstract Achieving pure abstraction is sometimes a goal of API architects. However, that abstraction is not always meaningful for developers.
<h3><strong>When a client supports limited HTTP methods</strong></h3>
It is common to see support for GET and POST and not PUT and DELETE

Then the HTTP verb is always a GET but the developer can express rich HTTP verbs and still maintain a RESTful clean API.

<strong>Create</strong> /dogs?method=post

<strong>Read</strong> /dogs

<strong>Update</strong> /dogs/1234?method=put&amp;location=park

<strong>Delete</strong> /dogs/1234?method=delete

<strong>WARNING</strong>: It can be <strong>dangerous</strong> to provide post or delete capabilities using a GET method because if the URL is in a Web page then a <strong>Web crawler like the Googlebot</strong> can create or destroy lots of content inadvertently. Be sure you understand the implications of supporting this approach for your applications' context
<h2><strong>Verbs. </strong></h2>
If your API is sending a response that is not a resource, then it makes better sense to use verbs instead of nouns. Make it clear in your API documentation that these non-resource based APIs are different from the rest of the API. Here's an API call for converting 100 Euros to Chinese Yen.

/convert?from=EUR&amp;to=CNY&amp;amount=100
<h2><strong>Associations. </strong></h2>
Resources almost always have relationships to other resources. What's a simple way to express these relationships in a Web API? Simplify the associations between resources and avoid deep URL levels. Move complexity like parameters and attributes after the HTTP question mark. Here's how we can get all dogs belonging to particular owner, and just the black ones.

GET /owners/1/dogs

GET /owners/1/dogs?color=black
<h3><strong>Sweep complexity behind the ‘?’</strong></h3>
Complexities can include many states that can be updated, changed, queried, as well as the attributes associated with a resource.

To get all red dogs running in the park:

<strong>GET /dogs?color=red&amp;state=running&amp;location=park</strong>
<h2><strong>Errors. </strong></h2>
From the perspective of the developer consuming your Web API, everything at the other side of that interface is a black box. Errors therefore become a key tool providing context and visibility into how to use an API. (Especially for "test driven development" models)

Use HTTP status codes. The usual suspects include HTTP 200, 400, 401, 403, 404, and 500. Make the messages returned in the payload as verbose as possible. Here's an example JSON payload. Notice the use of URLs for more information.

{

"developerMessage" : "...",

"userMessage" : "...",

"errorCode" : 100,

"moreInfo": "http://developers.company.com/errors/100"

}

The book discusses options when the client always expects a HTTP 200, like some versions of Adobe Flash.

There are over <u><a href="http://en.wikipedia.org/wiki/Http_error_codes" target="_blank" rel="noopener">70 HTTP status codes</a></u>. However, most developers don't have all 70 memorized. So if you choose status codes that are not very common you will force application developers away from building their apps and over to Wikipedia to figure out what you're trying to tell them. Therefore, most API providers use a small subset. For example, the Google GData API uses only 10 status codes; Netflix uses 9, and Digg, only 8.

How many status codes should you use for your API? When you boil it down, there are really only 3 outcomes in the interaction between an app and an API:

• Everything worked - success

• The application did something wrong – client error

• The API did something wrong – server error

But you shouldn't need to go beyond 8.

• 200 - OK • 400 - Bad Request  • 500 - Internal Server Error

If you're not comfortable reducing all your error conditions to these 3, try picking among these additional 5:

• 201 - Created • 304 - Not Modified • 404 – Not Found • 401 - Unauthorized • 403 - Forbidden
<h3><strong>Tips for handling exceptional behaviour</strong></h3>
Some applications (like some versions of flash) will not provide an opportunity to intercept the error code to developers if you send an HTTP response that is anything other than HTTP 200 OK.

Overall recommendations: 1 - Use suppress_response_codes = true 2 - The HTTP code is no longer just for the code

3 - Push any response code that we would have put in the HTTP response down into the response message

<strong>Always return OK </strong>/dogs?suppress_response_codes = true

<strong>Code for ignoring</strong> 200 - OK

<strong>Message for people &amp; code </strong>

{response_code" : 401, "message" : "Verbose, plain language description of the problem with hints about how to fix it." "more_info" : "http://dev.tecachdogrest.com/errors/12345", "code" : 12345}
<h2><strong>Versions. </strong></h2>
Make versioning in your API mandatory. Specify the version with a 'v' prefix and put it on the first level. Don't use the dot notation like v1.2 because it implies a granularity of versioning . Use a simple ordinal number to emphasize this is an interface and not an implementation. Here's an example of getting all dogs for version 1 of your API.

GET /v1/dogs
<h2><strong>Header Vs URL</strong></h2>
In fact, using headers is more correct for many reasons: it leverages existing HTTP standards, it's intellectually consistent with Fielding's vision, it solves some hard realworld problems related to inter-dependent APIs, and more. However, we think the reason most of the popular APIs do not use it is because it's less fun to hack in a browser. Simple rules we follow: If it changes the logic you write to handle the response, put it in the URL so you can see it easily. If it doesn't change the logic for each response, like OAuth information, put it in the header.
<h2><strong>Partial Response and Pagination. </strong></h2>
Use a comma-delimited list to specify what fields you want returned. Use "limit" and "offset" to paginate through resources. These parameters are common and well understood in databases. Here's how to get just the colors and breeds of all the dogs, and the just first 10 dogs.

<strong>My loose rule of thumb for default pagination is limit=10 with offset=0.
</strong><strong>The pagination defaults are of course dependent on your data size. If your resources are large, you probably want to limit it to fewer than 10; if resources are small, it can make sense to choose a larger limit.</strong>

GET /dogs?fields=color,breed

GET /dogs?limit=10&amp;offset=0
<h2><strong>Content-Types. </strong></h2>
It's recommended that APIs support different response formats like JSON and XML. To specify what format to return, use the dot type notation.

<strong>Make JSON the default format, as it is less verbose and can be easily consumed by JavaScript. Here's how to get all dogs in XML.</strong>

GET /dogs/1.xml
<h2><strong>Attributes. </strong></h2>
Use JSON as default. Follow JavaScript conventions for naming attributes. Use CamelCase, the first letter being uppercase or lowercase depending on type of object. Here's an example of a user ID attribute.

{

"userId": 1

}
<h2><strong>Search. </strong></h2>
To do a search across multiple resources, use the verb "search" and the "q" query parameter. Specify the format type using dot type notation. Here's an example of searching for all fluffy resources, in the default and XML formats.

GET /search?q=fluffy

GET /search.xml?q=fluffy

To add scope to your search, you can use a resourceful URL with the query parameter. For example, here's searching for all dogs belonging to a particular owner that are fluffy.

GET /owners/1/dogs?q=fluffy
<h2><strong>Subdomains. </strong></h2>
Consolidate all API requests under one API subdomain. Use something like api.company.com. Also create a dedicated developer portal like developers.company.com. You might also want to redirects users who go to the API subdomain in their browsers to the developer portal.

Your API gateway should be the top-level domain. For example, api.teachdogrest.com
<h2><strong>Authentication. </strong></h2>
Use the <strong>latest</strong> standard OAuth (current is 2.0). It allows API access without sharing of passwords. It allows API providers to revoke access tokens. It allows developers to use the same OAuth libraries they use for other APIs.
<ul>
 	<li>It means that Web or mobile apps that expose APIs don’t have to share passwords.</li>
 	<li>It allows the API provider to revoke tokens for an individual user, for an entire app, without requiring the user to change their original password.</li>
 	<li>This is critical if a mobile device is compromised or if a rogue app is discovered.</li>
 	<li>Above all, OAuth 2.0 will mean improved security and better end-user and consumer experiences with Web and mobile apps.</li>
</ul>
<h2><strong>Chatty APIs. </strong></h2>
Some API designs become very chatty, which means you need a lot of API calls to the server to build a simple application. The recommendation is to create a complete and RESTful API and provide shortcuts or composite responses if needed.

<strong>What kind of shortcut? Say you know that 80% of all your apps are going to need some sort of composite response, then build the kind of request that gives them what they need.</strong>
<h2><strong>SDK. </strong></h2>
It's recommended that API providers complement the API with code samples, libraries and software development kits. It allows for faster adoption on specific platforms. It helps reduce bad or inefficient code that might slow down the service. It helps market the API to different developer communities.
<h2><strong>API Facade. </strong></h2>
<h3><strong>Stakeholders</strong></h3>
<strong>Who are the people in that system - in the API value chain? </strong>The key players include the API team and the app developers.

<img class="wp-image-1168" src="/wp-content/uploads/2018/03/image3-3.png" alt="image3 3" />
<h3><strong>The need</strong></h3>
<ul>
 	<li>Going back to our API value chain, app developers build apps using the APIs provided by the API Team (API provider). Everybody wins if app developers are as productive as possible and adopt your API quickly.</li>
 	<li>Those app developers will help build the value within your organization and to extend that value proposition out beyond the boundaries of your organization into the broader market.</li>
 	<li>This pattern gives you a virtual layer between the interface on top and the API implementation on the bottom. It is a comprehensive view of what the API should be.</li>
 	<li>Importantly, it is the view from the perspective of the app developer and end user of the apps they create.</li>
 	<li>You break one major problem (exposing a set of complex internal systems in such a way as to be beneficial for developers) into three smaller problems (designing the ideal API; implementing the design with data stubs; integrating between the façade and the systems).</li>
 	<li>It also has benefits internally (behind the façade) in that it enables an API team to create an extensible API that allows new systems to be plugged in, allowing your organization to keep pace with both the marketplace and with changing internal systems.</li>
</ul>
There are various ways in architecting your API. The recommended approach is called the "API Facade Pattern", which involves three basic steps.
<ol>
 	<li>Design the ideal API. Design the URLs, parameters, responses, payloads, headers, and so on. The API design should be self-consistent</li>
 	<li>Implement with stubs. This allows developers to use the API and give feedback even before the API is connected to internal systems.</li>
 	<li>Integrate the Facade and the internal systems.</li>
</ol>
<img class="wp-image-1166" src="/wp-content/uploads/2018/03/image2-3.png" alt="image2 3" />

<img class="wp-image-1170" src="/wp-content/uploads/2018/03/image4-2.png" alt="image4 2" />
<h3><strong>The API Team</strong></h3>
<img class="wp-image-1169" src="/wp-content/uploads/2018/03/image6-3.png" alt="image6 3" />

The core of that team includes <strong>architects</strong>, <strong>software engineers</strong>, <strong>operations professionals</strong>, <strong>QA engineers </strong>and <strong>database administrators</strong>. But don’t stop there.

The four main persona of app developer we talk about depends on what kind of API strategy you have – whether <strong>internal</strong>, <strong>partner</strong>, <strong>customer</strong>, or <strong>open</strong>.

<strong>Internal</strong>: The app developer using the API works for the company – the API provider.
<strong>Partner</strong>: The developer works for or is a strategic partner. The go-to-market strategy is one with a shared value proposition.
<strong>Customer</strong>: The “customer developer” is especially important if your organization is a SaaS provider or if a large amount of revenue comes from B2B customers as opposed to consumer end users.
<strong>Open</strong>: The developer in this case is any developer who signs up to build apps against your API.

<strong>Technology for Authorization - OAuth</strong>
<ul>
 	<li>Let's look at how to handle authorization through the API facade. A request comes into the facade with an OAuth token or other indications of the authorization scheme.</li>
</ul>
<ul>
 	<li>The facade can make the calls to the authorization system of record.</li>
 	<li>If the request is valid, the facade passes it to the core system; if invalid, the façade returns with an invalid response code.</li>
</ul>
<img class="wp-image-1173" src="/wp-content/uploads/2018/03/image5-2.png" alt="image5 2" />
<h2><strong>OAuth Vs OWIN</strong></h2>
OAuth 2.0 specifies four roles,
<ol>
 	<li>Resource Owner, (user)</li>
 	<li>Client, (application)</li>
 	<li>Resource Server (service like Twitter or Facebook etc) and</li>
 	<li>Authorization Server.</li>
</ol>
<h2><strong>The OAuth 2.0 flow</strong></h2>
<img class="wp-image-1171" src="/wp-content/uploads/2018/03/image8-3.png" alt="image8 3" />
<h3>Terms you should know</h3>
<ul>
 	<li><strong>Client</strong> -- Also called "the app". It can be an app running on a mobile device or a traditional web app. The app makes requests to the resource server for protected assets on behalf of the resource owner. The resource owner must give the app permission to access the protected resources.</li>
 	<li><strong>Resource owner</strong> -- Also called an "end user". This is generally the person (or other entity) who is capable of granting access to a protected resource. For example, if an app needs to use data from one of your social media sites, then you are the resource owner -- the only person who can grant the app access to your data.</li>
 	<li><strong>Protected resource</strong> -- Data owned by the resource owner. For example, the user's contact list, account information, or other sensitive data.
<ul>
 	<li><strong>Limited Access
</strong>Through the mechanism of scopes, OAuth 2.0 can grant an app limited access to protected resources. For example, an app may have access only to specific resources, may be able to update resources, or may only be granted read-only access. Under so-called "three-legged" OAuth flows, the user typically specifies the level of access through a consent page (for example, a web page where the user selects the scope with a checkbox of other mechanism).</li>
</ul>
</li>
 	<li><strong>Resource server</strong> -- Think of the resource server as a service like Twitter or Facebook, or an HR service on your intranet, or a partner service on your B2B extranet. Apigee Edge is a resource server whenever OAuth token validation is required to process API requests. The resource server needs some kind of authorization before it will serve up protected resources to the app.</li>
 	<li><strong>Authorization server </strong>-- The authorization server is implemented in compliance with the OAuth 2.0 specification, and it is responsible for validating <strong>authorization grants</strong> and issuing the <strong>access tokens </strong>that give the app access to the user's data on the resource server.
<ul>
 	<li>All clients (apps) must register with the OAuth 2.0 authorization server from which they intend to request access tokens. When you register an app, you receive back a set of keys. One is a public key called the client identifier, and the other is a secret key called the client secret. Without these keys, an app cannot issue requests for authorization codes or access tokens to the authorization server.</li>
</ul>
</li>
 	<li><strong>Access token</strong> -- A long string of characters that serves as a credential used to access protected resources.</li>
</ul>
<em>Resources tokens (also called bearer tokens) are passed in Authorization headers, like this:</em>

<strong>$ curl -H "Authorization: Bearer UAj2yiGAcMZGxfN2DhcUbl9v8WsR" \</strong>

<strong>  http://myorg-test.apigee.net/v0/weather/forecastrss?w=12797282</strong>

<em>The resource server understands that the access token "stands in" for credentials like username and password. In addition, the access tokens can be issued with restrictions, so that, for example, the app can read but not write or delete data on the resource server. Note that an access token can be revoked if, for instance, the app is compromised. In this case, you will need to get a new access token to continue using the app; however, you will not have to change your username or password on the protected resources server (for example, Facebook or Twitter). </em>

<em>Access tokens generally have an expiration (for security reasons). Some grant types allow the authorization server to issue an refresh token, which allows the app to fetch a new access token when the old one expires.</em>
<ul>
 	<li><strong>Authorization grant</strong> -- Gives the app permission to retrieve an access token on behalf of the end user. OAuth 2.0 defines four specific "grant types". See "<u><a href="http://docs.apigee.com/api-services/content/oauth-introduction#granttypes" target="_blank" rel="noopener">What are the OAuth 2.0 grant types</a></u>" below.</li>
</ul>
<h1><strong>CORS</strong></h1>
<u><a href="https://msdn.microsoft.com/en-us/magazine/dn532203.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/magazine/dn532203.aspx</a></u>

<u><a href="https://docs.microsoft.com/en-us/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api" target="_blank" rel="noopener">https://docs.microsoft.com/en-us/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api</a></u>

<a href="http://www.w3.org/TR/cors/" target="_blank" rel="noopener">Cross Origin Resource Sharing</a> (CORS) is a W3C standard that allows a server to relax the same-origin policy. Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.

Two URLs have the same origin if they have identical schemes, hosts, and ports. (<a href="http://tools.ietf.org/html/rfc6454" target="_blank" rel="noopener">RFC 6454</a>)

Internet Explorer does not consider the port when comparing origins.
<ul>
 	<li>http://example.net - Different domain</li>
 	<li>http://example.com:9000/foo.html - Different port</li>
 	<li>https://example.com/foo.html - Different scheme</li>
 	<li>http://www.example.com/foo.html - Different subdomain</li>
</ul>
<img class="wp-image-1167" src="/wp-content/uploads/2018/03/image7-3.png" alt="image7 3" />

The general mechanics of CORS are such that when JavaScript is attempting to make a cross-origin AJAX call the browser will “ask” the server if this is allowed by sending headers in the HTTP request (for example, Origin). The server indicates what’s allowed by returning HTTP headers in the response (for example, Access-Control-Allow-Origin). This permission check is done for each distinct URL the client invokes, which means different URLs can have different permissions.

Browsers can ask the server for these permissions in two different ways:

<strong>simple CORS requests and preflight CORS requests.</strong>
<table>
<tbody>
<tr>
<td>Permission/Feature</td>
<td>Request Header</td>
<td>Response Header</td>
</tr>
<tr>
<td>Origin</td>
<td>Origin</td>
<td>Access-Control-Allow-Origin</td>
</tr>
<tr>
<td>HTTP method</td>
<td>Access-Control-Request-Method</td>
<td>Access-Control-Allow-Method</td>
</tr>
<tr>
<td>Request headers</td>
<td>Access-Control-Request-Headers</td>
<td>Access-Control-Allow-Headers</td>
</tr>
<tr>
<td>Response headers</td>
<td></td>
<td>Access-Control-Expose-Headers</td>
</tr>
<tr>
<td>Credentials</td>
<td></td>
<td>Access-Control-Allow-Credentials</td>
</tr>
<tr>
<td>Cache preflight response</td>
<td></td>
<td>Access-Control-Max-Age</td>
</tr>
</tbody>
</table>
<h1><a href="https://stackoverflow.com/questions/39613831/how-to-solve-asp-net-web-api-cors-preflight-issue-when-using-put-and-delete-requ" target="_blank" rel="noopener">How to solve ASP.NET Web API CORS Preflight issue when using PUT and DELETE requests with multiple origins?</a></h1>
<h1><strong>https://stackoverflow.com/questions/39613831/how-to-solve-asp-net-web-api-cors-preflight-issue-when-using-put-and-delete-requ</strong></h1>
protected void Application_BeginRequest(){

if (Request.HttpMethod == "OPTIONS")

{

Response.StatusCode = (int)HttpStatusCode.OK;

Response.AppendHeader("Access-Control-Allow-Origin", Request.Headers.GetValues("Origin")[0]);

Response.AddHeader("Access-Control-Allow-Headers", "Content-Type, Accept");

Response.AddHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE");

Response.AppendHeader("Access-Control-Allow-Credentials", "true");

Response.End();

}}

Since I have different origins calling my web API, I'm using Request.Headers.GetValues("Origin")[0]) to set the origin in the response dinamically.

In the WebApiConfig.cs I still specified the different origins but used wildcards on the headers and methods, as well as setting the SupportsCredentials to true, like this:

var cors = new EnableCorsAttribute("http://localhost:63342,http://localhost:63347,http://localhost:63345", "*", "*");

cors.SupportsCredentials = true;

config.EnableCors(cors);

// TODO: Replace with the URL of your WebService app

var serviceUrl = 'http://mywebservice/api/test';

function sendRequest() {

var method = $('#method').val();

$.ajax({

type: method,

url: serviceUrl

}).done(function (data) {

$('#value1').text(data);

}).error(function (jqXHR, textStatus, errorThrown) {

$('#value1').text(jqXHR.responseText || textStatus);

});

}

Install-Package Microsoft.AspNet.WebApi.Cors

public static class WebApiConfig

{

public static void Register(HttpConfiguration config)

{

// New code

config.EnableCors();

config.Routes.MapHttpRoute(

name: "DefaultApi",

routeTemplate: "api/{controller}/{id}",

defaults: new { id = RouteParameter.Optional }

);

}

}

<strong>Global</strong>

The parameters (in order) are:
<ol>
 	<li>List of origins allowed</li>
 	<li>List of request headers allowed</li>
 	<li>List of HTTP methods allowed</li>
 	<li>List of response headers allowed (optional)</li>
</ol>
public static class WebApiConfig

{

public static void Register(HttpConfiguration config)

{

var cors = new EnableCorsAttribute("www.example.com", "*", "*");

config.EnableCors(cors); // ...

}

}

<strong>Class level</strong>

[EnableCors(origins: "http://mywebclient.azurewebsites.net", headers: "*", methods: "*")]

public class TestController : ApiController

<strong>Method level</strong>

[EnableCors(origins: "http://www.example.com", headers: "*", methods: "*")]

public HttpResponseMessage GetItem(int id) { ... }

[DisableCors]

[EnableCors("http://localhost:55912", // Origin

null,                     // Request headers

"GET",                    // HTTP methods

"bar",                    // Response headers

SupportsCredentials=true  // Allow credentials

)]

public HttpResponseMessage Get(int id)

If the server allows the request, it sets the Access-Control-Allow-Origin header. The value of this header either matches the Origin header, or is the wildcard value "*", meaning that any origin is allowed. If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.

Access-Control-Allow-Origin: <u><a href="http://myclient.azurewebsites.net" target="_blank" rel="noopener">http://myclient.azurewebsites.net</a></u>
<h2><strong>Credentials and Authentication </strong><strong>Passing Credentials in Cross-Origin Requests</strong></h2>
Generally, authentication with Web APIs can be done either with a cookie or with an Authorization header (there are other ways, but these two are the most common).

It’s possible for a JavaScript client to explicitly send credentials (again, typically via the Authorization header). If this is the case, then none of the aforementioned rules or behaviors related to credentials applies.

Explicitly setting a token value in the Authorization header is a safer approach to authentication because you avoid the possibility of cross-site request forgery (CSRF) attacks. You can see this approach in the new Single-Page Application (SPA) templates in Visual Studio 2013.

$.ajax({

url: "http://localhost/WebApiCorsServer/Resources/1",

headers: {

"Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3Mi..."

}

// Other settings omitted

});

<strong>scenario where the browser is implicitly sending credentials:</strong>

In normal browser activity, if one of these has been previously established, then the browser will implicitly pass these values to the server on subsequent requests. With cross-origin AJAX, though, this implicit passing of the values must be explicitly requested in JavaScript (via the withCredentials flag on the XMLHttpRequest) and must be explicitly allowed in the server’s CORS policy (via the Access-Control-Allow-Credentials response header).

<strong>The withCredentials flag does two things: If the server issues a cookie, the browser can accept it; if the browser has a cookie, it can send it to the server.</strong>

[EnableCors(origins: "http://myclient.azurewebsites.net", headers: "*", methods: "*", SupportsCredentials = true)]

Be very careful about setting <strong>SupportsCredentials</strong> to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware. The CORS spec also states that setting <em>origins</em> to "*" is invalid if <strong>SupportsCredentials</strong> is true.

$.ajax({

url: "http://localhost/WebApiCorsServer/Resources/1",

xhrFields: {

withCredentials: true

}

// Other settings omitted

});

Web API implementation

<u><a href="https://docs.microsoft.com/en-us/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api" target="_blank" rel="noopener">https://docs.microsoft.com/en-us/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api</a></u>

You can also create a Web API project using the "Web API" template. The Web API template uses ASP.NET MVC to provide API help pages. I'm using the Empty template for this tutorial because I want to show Web API without MVC. In general, you don't need to know ASP.NET MVC to use Web API.
