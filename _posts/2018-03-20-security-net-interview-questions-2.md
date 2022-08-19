---
layout: post
title: Security & .net interview questions
date: 2018-03-20 17:10
author: tmasabari
comments: true
categories: [ASP.NET, ASP.NET MVC, Security, WEBAPI]
---
<h2><a href="https://docs.microsoft.com/en-us/aspnet/identity/overview/getting-started/introduction-to-aspnet-identity">Legacy - Membership - obselete</a></h2>
<ul>
 	<li><a href="https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx" data-linktype="external">ASP.NET Membership</a> was designed to solve site membership requirements that were common in <strong>2005</strong>, which involved <strong>Forms Authentication</strong>, and a <strong>SQL Server database</strong> for<strong> user names, passwords, and profile</strong> data. The limitations of ASP.NET Membership's design make this transition difficult:</li>
 	<li>Today there is a much broader array of data storage options for web applications, but the database <strong>schema</strong> was designed <strong>for SQL Server</strong> and you<strong> can't change</strong> it.
<ul>
 	<li>You can write a provider to store membership information in a <strong>non-relational storage</strong> mechanism, such as Azure Storage Tables, but then you have to work around the relational design by writing a lot of code</li>
 	<li><a href="https://docs.microsoft.com/en-us/aspnet/web-pages/overview/security/16-adding-security-and-membership" data-linktype="relative-path">ASP.NET simple membership</a> was developed as a membership system for ASP.NET Web Pages.</li>
 	<li><a href="http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx" data-linktype="external">ASP.NET Universal Providers</a> were developed on the ASP.NET Membership infrastructure, so they still carry the <strong>same limitations as the SqlMembership</strong> Provider</li>
</ul>
</li>
 	<li class="">Most developers want to enable their sites to<strong> use social identity providers</strong> for authentication and authorization functionality. Since the log-in/log-out functionality is <strong>based on Forms Authentication</strong>, the membership system <strong>can't use <a href="https://docs.microsoft.com/en-us/aspnet/aspnet/overview/owin-and-katana/an-overview-of-project-katana" data-linktype="relative-path">OWIN</a></strong>.</li>
</ul>
&nbsp;
<h2 id="aspnet-identity" class="heading-with-anchor">ASP.NET Identity</h2>
<ol>
 	<li><strong>ASP.NET Identity</strong> is the new <strong>membership system (not authentication system)</strong> for building ASP.NET web applications, phone, and store applications.</li>
 	<li>The ASP.NET Identity module handles user and secure password storage, role mapping etc.</li>
 	<li>ASP.NET Identity can be used with all ASP.NET frameworks, such as ASP.NET Web Forms , MVC, Web Pages, Web API etc.ASP.NET Identity has been developed with some major security features like <strong>Two-Factor Authentication, Account Lockout, and Account Confirmation etc.</strong></li>
 	<li>ASP.NET Identity <strong><a href="https://docs.microsoft.com/en-us/aspnet/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project">invoked by Microsoft OWIN Authentication middleware</a></strong>. So the same authentication packages can be used across multiple frameworks including ASP.NET MVC and Web Forms.</li>
</ol>
<h3><a href="https://coding.abel.nu/2014/06/asp-net-identity-and-owin-overview/">Typical Layering</a></h3>
<img class="wp-image-1220 aligncenter" src="/wp-content/uploads/2018/03/img_5ab2505b7df68.png" alt="" width="679" height="603" />
<ul>
 	<li><strong>Dependency inversion</strong>
<ul>
 	<li>The layers don’t directly interact with each other, instead they inspect and alter the state of the current request. It is effectively a message passing architecture, where there is no hard dependencies between the different middleware modules. They can always be substitued for another middleware that nows how to handle certain “messages” put in the owin context.</li>
 	<li>The ASP.NET Identity module sits at the very bottom of the chain, far, far away from the incoming HTTP Request. In fact, it knows nothing about Http at all.</li>
 	<li>ASP.NET identity doesn’t know (nearly) anything about Owin at all. ASP.NET Identity is working on an application ignorant level, taking care of user and role storage.</li>
 	<li>The MVC controller calls the ASP.NET Identity module in a way that ASP.NET Identity <em>has no dependency on the web infrastructure</em>. In fact, ASP.NET Identity can be used for any kind of application(example console application), not only for web applications.</li>
</ul>
</li>
 	<li>Google interaction flow
<ul>
 	<li>The Owin Middleware modules are responsible for handling the authentication and takes care of the actual interaction with external authentication providers (such as Google) and establishing an application session through a cookie.</li>
 	<li>The Google Authentication Middleware interacts with Google to provide Google signon. In this example I only show Google, but if more social networks such as Facebook or Twitter were offered, they would be next to the Google middleware in the stack.</li>
 	<li>On all subsequent calls the application cookie middleware extracts the contents of the incoming application cookie and sets the claims identity of the current context.</li>
</ul>
</li>
</ul>
<p class="lf-text-block lf-block" data-lf-anchor-id="25753dc9d4193fb3c4d0e44100444acd:0">ASP.NET Identity was developed with the following goals:</p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="8d71ed2bd5996aba13c9a5465102627d:0">
 	<li><strong>OWIN Integration</strong>
<ul>
 	<li>ASP.NET authentication is now <strong>based on OWIN middleware</strong> that can be used on any OWIN-based host. ASP.NET Identity <strong>does not have any dependency on System.Web</strong>. It is a fully compliant OWIN framework and can be used in any OWIN hosted application.</li>
 	<li><strong>ASP.NET Identity uses OWIN Authentication</strong> for log-in/log-out of users in the web site. This means that instead of using FormsAuthentication to generate the cookie, the <strong>application uses OWIN CookieAuthentication</strong> to do that.</li>
</ul>
</li>
 	<li><strong class="">One ASP.NET Identity system</strong>
<ul>
 	<li>ASP.NET Identity can be used with all of the ASP.NET frameworks, such as <strong>ASP.NET MVC, Web Forms, Web Pages, Web API, and SignalR</strong>. (<a href="https://www.codeproject.com/Articles/802435/Authentication-and-Authorization-with-ASP-NET-Iden">WCF can be integrated with Identity 2.0</a>)</li>
 	<li>ASP.NET Identity can be used when you are building web, phone, store, or hybrid applications.</li>
</ul>
</li>
 	<li><strong>Persistence control</strong>
<ul>
 	<li>By default, the ASP.NET Identity system stores all the user information in a <strong>relational database</strong>.</li>
 	<li>ASP.NET Identity uses <strong>Entity Framework <em>Code First</em></strong> to implement all of its persistence mechanism. So changing schema ( table names or the data type of primary keys) is simple to do.</li>
 	<li>It's <strong>easy to plug in different storage mechanisms</strong> such as SharePoint, Azure Storage Table Service, NoSQL databases, etc., without having to throw <code>System.NotImplementedExceptions</code>exceptions.</li>
</ul>
</li>
 	<li><strong>Ease of plugging in profile data about the user</strong></li>
 	<li><strong>Role provider-</strong>restrict access to parts of your application by roles. You can easily create roles such as "Admin" and add users to roles.</li>
 	<li><strong>Claims Based -</strong>supports claims-based authentication, where the user's identity is represented as a set of claims. Claims allow developers to be a lot more expressive in describing a user's identity than roles allow. Whereas <strong>role membership is just a boolean</strong> (member or non-member), a <strong>claim can include rich information</strong> about the user's identity and membership.</li>
 	<li><strong>Social Login Providers- </strong>Microsoft Account, Facebook, Twitter, Google, and others to your application, and <strong>store the user-specific data in your application</strong>.</li>
 	<li><strong>Azure Active Directory</strong></li>
 	<li><strong>Unit testability</strong></li>
 	<li><strong>NuGet package-</strong>redistributed as a NuGet package which is installed in the ASP.NET MVC, Web Forms and Web API templates that ship with Visual Studio 2013. -<span style="font-size: 1rem;">easier for the ASP.NET team to iterate on new features and bug fixes, and deliver in an agile manner.</span></li>
</ul>
<p id="Bgqwvxk"></p>

<h3>ASP.NET Identity core abstractions</h3>
<img class=" wp-image-1213 alignleft" src="/wp-content/uploads/2018/03/img_5ab22ac51abbc.png" alt="" width="513" height="441" />
<p id="KPEDcBJ"><img class="alignnone wp-image-1214 " src="/wp-content/uploads/2018/03/img_5ab22ba1ed665.png" alt="" width="242" height="435" /></p>

<ul>
 	<li>A user object must implement the IUser interface, which requires every user to have at least an ID and a name.</li>
 	<li>IUserStore defines the bare minimum functionality you’d want for users - CRUD
<ul>
 	<li>IUserPasswordStore which implements IUserStore  - to allow users to create local accounts with passwords</li>
 	<li>IUserLoginStore - For third party logins (Twitter and Facebook, for example)</li>
 	<li>IUserClaimStore - For claims storage</li>
</ul>
</li>
</ul>
<h2 id="components-of-aspnet-identity" class="heading-with-anchor">Components of ASP.NET Identity</h2>
<img class="wp-image-1077 aligncenter" style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5aaf489761d9c.png" alt="" width="762" height="309" />
<ul>
 	<li><strong>Microsoft.AspNet.Identity.EntityFramework </strong>– Contains EF implementations for identity types. These types are used to manage information for identity users, roles, claim login etc. This package has the Entity Framework implementation of ASP.NET Identity which will <strong>persist the ASP.NET Identity data</strong> and schema</li>
 	<li><strong>Microsoft.AspNet.Identity.Core </strong>– Contains classes and interfaces for managing users and roles in ASP.NET Identity. It contains <strong>classes for User validation, User login information</strong> etc. This package has the core interfaces for ASP.NET Identity. This package can be used to write an implementation for ASP.NET Identity that targets <strong>different persistence stores</strong> such as Azure Table Storage, NoSQL databases etc.</li>
 	<li><strong>Microsoft.AspNet.Identity.OWIN </strong>– Contains classes used to manage identities associated with OWIN. This package contains functionality that is used to plug in OWIN authentication with ASP.NET Identity in ASP.NET applications. This is used when you add log in functionality to your application and call into OWIN Cookie Authentication middleware to generate a cookie.</li>
 	<li><a href="http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/" data-linktype="external">Microsoft.Owin.Security.Cookies</a>
Middleware that enables an application to use cookie based authentication, similar to ASP.NET's Forms Authentication.</li>
</ul>
&nbsp;
<h3><a class="question-hyperlink" href="https://stackoverflow.com/questions/31960433/adding-asp-net-mvc5-identity-authentication-to-an-existing-project">Adding ASP.NET MVC5 Identity Authentication to an existing project</a></h3>
<ol>
 	<li>First install these NuGet packages in Package Manager Console:
<pre class="default prettyprint prettyprinted"><code><span class="pln">PM</span><span class="pun">&gt;</span> <span class="typ">Install</span><span class="pun">-</span><span class="typ">Package</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">AspNet</span><span class="pun">.</span><span class="typ">Identity</span><span class="pun">.</span><span class="typ">Owin</span><span class="pln"> 
PM</span><span class="pun">&gt;</span> <span class="typ">Install</span><span class="pun">-</span><span class="typ">Package</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">AspNet</span><span class="pun">.</span><span class="typ">Identity</span><span class="pun">.</span><span class="typ">EntityFramework</span><span class="pln">
PM</span><span class="pun">&gt;</span> <span class="typ">Install</span><span class="pun">-</span><span class="typ">Package</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">Owin</span><span class="pun">.</span><span class="typ">Host</span><span class="pun">.</span><span class="typ">SystemWeb</span> </code></pre>
</li>
 	<li>Also you could install additional package and configure them to meet your requirement like <code>Microsoft.Owin.Security.Facebook</code> or whichever you want.<img class="alignnone size-full wp-image-1216 " style="color: #555555; font-family: Monaco, Menlo, Consolas, 'Courier New', monospace; font-size: 0.75rem;" src="/wp-content/uploads/2018/03/img_5ab23f984aae7.png" alt="" /><img class="alignnone size-full wp-image-1217 " style="color: #555555; font-family: Monaco, Menlo, Consolas, 'Courier New', monospace; font-size: 0.75rem;" src="/wp-content/uploads/2018/03/img_5ab23fc789d41.png" alt="" /><img class="alignnone size-full wp-image-1218 " style="color: #555555; font-family: Monaco, Menlo, Consolas, 'Courier New', monospace; font-size: 0.75rem;" src="/wp-content/uploads/2018/03/img_5ab240166f717.png" alt="" /></li>
 	<li>Almost done just add this line of code to your <code>web.config</code> file so OWIN could find your startup class.</li>
 	<li>
<pre class="default prettyprint prettyprinted"><code><span class="tag">&lt;appSettings&gt;</span>
    <span class="com">&lt;!-- other setting here --&gt;</span>
    <span class="tag">&lt;add</span> <span class="atn">key</span><span class="pun">=</span><span class="atv">"owin:AppStartup"</span> <span class="atn">value</span><span class="pun">=</span><span class="atv">"MyAppNamespace.IdentityConfig"</span> <span class="tag">/&gt;</span>
<span class="tag">&lt;/appSettings&gt;</span></code></pre>
</li>
 	<li>Or configure namespace which contains Startup class (<strong>partial</strong>) with OwinStartupAttribute attribute
<pre class="EnlighterJSRAW" data-enlighter-language="null">[assembly: OwinStartupAttribute(typeof(SecurityUsingTemplates.Startup))]
namespace SecurityUsingTemplates
{
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
}</pre>
<pre class="default prettyprint prettyprinted"></pre>
</li>
 	<li><strong>Note:</strong> Don't forget add relevant namespaces to your files:
<pre class="default prettyprint prettyprinted"><code><span class="kwd">using</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">AspNet</span><span class="pun">.</span><span class="typ">Identity</span><span class="pun">;</span>
<span class="kwd">using</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">Owin</span><span class="pun">.</span><span class="typ">Security</span><span class="pun">;</span>
<span class="kwd">using</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">AspNet</span><span class="pun">.</span><span class="typ">Identity</span><span class="pun">.</span><span class="typ">Owin</span><span class="pun">;</span>
<span class="kwd">using</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">AspNet</span><span class="pun">.</span><span class="typ">Identity</span><span class="pun">.</span><span class="typ">EntityFramework</span><span class="pun">;</span>
<span class="kwd">using</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">Owin</span><span class="pun">;</span>
<span class="kwd">using</span> <span class="typ">Microsoft</span><span class="pun">.</span><span class="typ">Owin</span><span class="pun">.</span><span class="typ">Security</span><span class="pun">.</span><span class="typ">Cookies</span><span class="pun">;</span>
<span class="kwd">using</span> <span class="typ">Owin</span><span class="pun">;</span></code></pre>
</li>
 	<li>Add a user class and with <code>IdentityUser</code> inheritance:
<pre class="default prettyprint prettyprinted"><code><span class="kwd">public</span> <span class="kwd">class</span> <span class="typ">AppUser</span> <span class="pun">:</span> <span class="typ">IdentityUser</span>
<span class="pun">{</span>
    <span class="com">//add your custom properties which have not included in IdentityUser before</span>
    <span class="kwd">public</span> <span class="kwd">string</span> <span class="typ">MyExtraProperty</span> <span class="pun">{</span> <span class="kwd">get</span><span class="pun">;</span> <span class="kwd">set</span><span class="pun">;</span> <span class="pun">}</span>  
<span class="pun">}</span></code></pre>
</li>
 	<li>Do same thing for role:
<pre class="default prettyprint prettyprinted"><code><span class="kwd">public</span> <span class="kwd">class</span> <span class="typ">AppRole</span> <span class="pun">:</span> <span class="typ">IdentityRole</span>
<span class="pun">{</span>
    <span class="kwd">public</span> <span class="typ">AppRole</span><span class="pun">()</span> <span class="pun">:</span> <span class="kwd">base</span><span class="pun">()</span> <span class="pun">{</span> <span class="pun">}</span>
    <span class="kwd">public</span> <span class="typ">AppRole</span><span class="pun">(</span><span class="kwd">string</span><span class="pln"> name</span><span class="pun">)</span> <span class="pun">:</span> <span class="kwd">base</span><span class="pun">(</span><span class="pln">name</span><span class="pun">)</span> <span class="pun">{</span> <span class="pun">}</span>
    <span class="com">// extra properties here </span>
<span class="pun">}</span></code></pre>
</li>
 	<li>Change your <code>DbContext</code> parent form <code>DbContext</code> to <code>IdentityDbContext&lt;AppUser&gt;.</code>If you use same connection string and enabled migration EF create necessary tables for you.
<pre class="default prettyprint prettyprinted"><code><span class="kwd">public</span> <span class="kwd">class</span> <span class="typ">MyDbContext</span> <span class="pun">:</span> <span class="typ">IdentityDbContext</span><span class="pun">&lt;</span><span class="typ">AppUser</span><span class="pun">&gt;</span>
<span class="pun">{</span>
    <span class="com">// Other part of codes still same </span>
    <span class="com">// You don't need to add AppUser and AppRole </span>
    <span class="com">// since automatically added by inheriting form IdentityDbContext&lt;AppUser&gt;</span>
<span class="pun">}</span></code></pre>
</li>
 	<li>Optionally you could extent <code>UserManager</code> to add your desired configuration and customization:
<pre class="default prettyprint prettyprinted"><code><span class="kwd">public</span> <span class="kwd">class</span> <span class="typ">AppUserManager</span> <span class="pun">:</span> <span class="typ">UserManager</span><span class="pun">&lt;</span><span class="typ">AppUser</span><span class="pun">&gt;</span>
<span class="pun">{</span>
    <span class="kwd">public</span> <span class="typ">AppUserManager</span><span class="pun">(</span><span class="typ">IUserStore</span><span class="pun">&lt;</span><span class="typ">AppUser</span><span class="pun">&gt;</span><span class="pln"> store</span><span class="pun">)</span>
        <span class="pun">:</span> <span class="kwd">base</span><span class="pun">(</span><span class="pln">store</span><span class="pun">)</span>
    <span class="pun">{</span>
    <span class="pun">}</span>

    <span class="com">// this method is called by Owin therefore best place to configure your User Manager</span>
    <span class="kwd">public</span> <span class="kwd">static</span> <span class="typ">AppUserManager</span> <span class="typ">Create</span><span class="pun">(</span>
        <span class="typ">IdentityFactoryOptions</span><span class="pun">&lt;</span><span class="typ">AppUserManager</span><span class="pun">&gt;</span><span class="pln"> options</span><span class="pun">,</span> <span class="typ">IOwinContext</span><span class="pln"> context</span><span class="pun">)</span>
    <span class="pun">{</span>
        <span class="kwd">var</span><span class="pln"> manager </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">AppUserManager</span><span class="pun">(</span>
            <span class="kwd">new</span> <span class="typ">UserStore</span><span class="pun">&lt;</span><span class="typ">AppUser</span><span class="pun">&gt;(</span><span class="pln">context</span><span class="pun">.</span><span class="typ">Get</span><span class="pun">&lt;</span><span class="typ">MyDbContext</span><span class="pun">&gt;()));</span>

        <span class="com">// optionally configure your manager</span>
        <span class="com">// ...</span>

        <span class="kwd">return</span><span class="pln"> manager</span><span class="pun">;</span>
    <span class="pun">}</span>
<span class="pun">}</span></code></pre>
</li>
 	<li>Since Identity is based on OWIN you need configure OWIN too: Add a class to <code>App_Start</code> folder (or anywhere else if you want). This class is used by OWIN
<pre class="default prettyprint prettyprinted"><code><span class="kwd">namespace</span> <span class="typ">MyAppNamespace</span>
<span class="pun">{</span>
    <span class="kwd">public</span> <span class="kwd">class</span> <span class="typ">IdentityConfig</span>
    <span class="pun">{</span>
        <span class="kwd">public</span> <span class="kwd">void</span> <span class="typ">Configuration</span><span class="pun">(</span><span class="typ">IAppBuilder</span><span class="pln"> app</span><span class="pun">)</span>
        <span class="pun">{</span><span class="pln">
            app</span><span class="pun">.</span><span class="typ">CreatePerOwinContext</span><span class="pun">(()</span> <span class="pun">=&gt;</span> <span class="kwd">new</span> <span class="typ">MyDbContext</span><span class="pun">());</span><span class="pln">
            app</span><span class="pun">.</span><span class="typ">CreatePerOwinContext</span><span class="pun">&lt;</span><span class="typ">AppUserManager</span><span class="pun">&gt;(</span><span class="typ">AppUserManager</span><span class="pun">.</span><span class="typ">Create</span><span class="pun">);</span><span class="pln">
            app</span><span class="pun">.</span><span class="typ">CreatePerOwinContext</span><span class="pun">&lt;</span><span class="typ">RoleManager</span><span class="pun">&lt;</span><span class="typ">AppRole</span><span class="pun">&gt;&gt;((</span><span class="pln">options</span><span class="pun">,</span><span class="pln"> context</span><span class="pun">)</span> <span class="pun">=&gt;</span>
                <span class="kwd">new</span> <span class="typ">RoleManager</span><span class="pun">&lt;</span><span class="typ">AppRole</span><span class="pun">&gt;(</span>
                    <span class="kwd">new</span> <span class="typ">RoleStore</span><span class="pun">&lt;</span><span class="typ">AppRole</span><span class="pun">&gt;(</span><span class="pln">context</span><span class="pun">.</span><span class="typ">Get</span><span class="pun">&lt;</span><span class="typ">MyDbContext</span><span class="pun">&gt;())));</span><span class="pln">

            app</span><span class="pun">.</span><span class="typ">UseCookieAuthentication</span><span class="pun">(</span><span class="kwd">new</span> <span class="typ">CookieAuthenticationOptions</span>
            <span class="pun">{</span>
                <span class="typ">AuthenticationType</span> <span class="pun">=</span> <span class="typ">DefaultAuthenticationTypes</span><span class="pun">.</span><span class="typ">ApplicationCookie</span><span class="pun">,</span>
                <span class="typ">LoginPath</span> <span class="pun">=</span> <span class="kwd">new</span> <span class="typ">PathString</span><span class="pun">(</span><span class="str">"/Home/Login"</span><span class="pun">),</span>
            <span class="pun">});</span>
        <span class="pun">}</span>
    <span class="pun">}</span>
<span class="pun">}</span></code></pre>
</li>
 	<li>
<pre class="default prettyprint prettyprinted"> You could make roles and add to your users:</pre>
<pre class="default prettyprint prettyprinted"><code><span class="kwd">public</span> <span class="typ">ActionResult</span> <span class="typ">CreateRole</span><span class="pun">(</span><span class="kwd">string</span><span class="pln"> roleName</span><span class="pun">)</span>
<span class="pun">{</span>
    <span class="kwd">var</span><span class="pln"> roleManager</span><span class="pun">=</span><span class="typ">HttpContext</span><span class="pun">.</span><span class="typ">GetOwinContext</span><span class="pun">().</span><span class="typ">GetUserManager</span><span class="pun">&lt;</span><span class="typ">RoleManager</span><span class="pun">&lt;</span><span class="typ">AppRole</span><span class="pun">&gt;&gt;();</span>

    <span class="kwd">if</span> <span class="pun">(!</span><span class="pln">roleManager</span><span class="pun">.</span><span class="typ">RoleExists</span><span class="pun">(</span><span class="pln">roleName</span><span class="pun">))</span><span class="pln">
        roleManager</span><span class="pun">.</span><span class="typ">Create</span><span class="pun">(</span><span class="kwd">new</span> <span class="typ">AppRole</span><span class="pun">(</span><span class="pln">roleName</span><span class="pun">));</span>
    <span class="com">// rest of code</span>
<span class="pun">}</span> </code></pre>
</li>
 	<li>You could add any role to any user like this:
<pre class="default prettyprint prettyprinted"><code><span class="typ">UserManager</span><span class="pun">.</span><span class="typ">AddToRole</span><span class="pun">(</span><span class="typ">UserManager</span><span class="pun">.</span><span class="typ">FindByName</span><span class="pun">(</span><span class="str">"username"</span><span class="pun">).</span><span class="typ">Id</span><span class="pun">,</span> <span class="str">"roleName"</span><span class="pun">);</span></code></pre>
By using <code>Authorize</code> you could guard your actions or controllers:
<pre class="default prettyprint prettyprinted"><code><span class="pun">[</span><span class="typ">Authorize</span><span class="pun">]</span>
<span class="kwd">public</span> <span class="typ">ActionResult</span> <span class="typ">MySecretAction</span><span class="pun">()</span> <span class="pun">{}</span></code></pre>
or
<pre class="default prettyprint prettyprinted"><code><span class="pun">[</span><span class="typ">Authorize</span><span class="pun">(</span><span class="typ">Roles</span> <span class="pun">=</span> <span class="str">"Admin"</span><span class="pun">)]]</span>
<span class="kwd">public</span> <span class="typ">ActionResult</span> <span class="typ">MySecretAction</span><span class="pun">()</span> <span class="pun">{}</span></code></pre>
</li>
 	<li>Consider login action for example
<pre class="default prettyprint prettyprinted"><code><span class="pun">[</span><span class="typ">HttpPost</span><span class="pun">]</span>
<span class="kwd">public</span> <span class="typ">ActionResult</span> <span class="typ">Login</span><span class="pun">(</span><span class="typ">LoginViewModel</span><span class="pln"> login</span><span class="pun">)</span>
<span class="pun">{</span>
    <span class="kwd">if</span> <span class="pun">(</span><span class="typ">ModelState</span><span class="pun">.</span><span class="typ">IsValid</span><span class="pun">)</span>
    <span class="pun">{</span>
        <span class="kwd">var</span><span class="pln"> userManager </span><span class="pun">=</span> <span class="typ">HttpContext</span><span class="pun">.</span><span class="typ">GetOwinContext</span><span class="pun">().</span><span class="typ">GetUserManager</span><span class="pun">&lt;</span><span class="typ">AppUserManager</span><span class="pun">&gt;();</span>
        <span class="kwd">var</span><span class="pln"> authManager </span><span class="pun">=</span> <span class="typ">HttpContext</span><span class="pun">.</span><span class="typ">GetOwinContext</span><span class="pun">().</span><span class="typ">Authentication</span><span class="pun">;</span>

        <span class="typ">AppUser</span><span class="pln"> user </span><span class="pun">=</span><span class="pln"> userManager</span><span class="pun">.</span><span class="typ">Find</span><span class="pun">(</span><span class="pln">login</span><span class="pun">.</span><span class="typ">UserName</span><span class="pun">,</span><span class="pln"> login</span><span class="pun">.</span><span class="typ">Password</span><span class="pun">);</span>
        <span class="kwd">if</span> <span class="pun">(</span><span class="pln">user </span><span class="pun">!=</span> <span class="kwd">null</span><span class="pun">)</span>
        <span class="pun">{</span>
            <span class="kwd">var</span><span class="pln"> ident </span><span class="pun">=</span><span class="pln"> userManager</span><span class="pun">.</span><span class="typ">CreateIdentity</span><span class="pun">(</span><span class="pln">user</span><span class="pun">,</span> 
                <span class="typ">DefaultAuthenticationTypes</span><span class="pun">.</span><span class="typ">ApplicationCookie</span><span class="pun">);</span>
            <span class="typ">AuthManager</span><span class="pun">.</span><span class="typ">SignIn</span><span class="pun">(</span>
                <span class="kwd">new</span> <span class="typ">AuthenticationProperties</span> <span class="pun">{</span> <span class="typ">IsPersistent</span> <span class="pun">=</span> <span class="kwd">false</span> <span class="pun">},</span><span class="pln"> ident</span><span class="pun">);</span>
            <span class="kwd">return</span> <span class="typ">Redirect</span><span class="pun">(</span><span class="pln">login</span><span class="pun">.</span><span class="typ">ReturnUrl</span> <span class="pun">??</span> <span class="typ">Url</span><span class="pun">.</span><span class="typ">Action</span><span class="pun">(</span><span class="str">"Index"</span><span class="pun">,</span> <span class="str">"Home"</span><span class="pun">));</span>
        <span class="pun">}</span>
    <span class="pun">}</span>
    <span class="typ">ModelState</span><span class="pun">.</span><span class="typ">AddModelError</span><span class="pun">(</span><span class="str">""</span><span class="pun">,</span> <span class="str">"Invalid username or password"</span><span class="pun">);</span>
    <span class="kwd">return</span> <span class="typ">View</span><span class="pun">(</span><span class="pln">login</span><span class="pun">);</span>
<span class="pun">}</span></code></pre>
</li>
</ol>
<h2><a href="https://docs.microsoft.com/en-us/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#winauth">Windows Authentication</a></h2>
<ol>
 	<li class="lf-text-block lf-block" data-lf-anchor-id="8f5485a9c598a4ea2f89e043470b4e63:0">If you select <strong>Windows Authentication</strong>, the sample application will be configured to use the <strong>Windows Authentication IIS module for authentication</strong>.</li>
 	<li class="lf-text-block lf-block" data-lf-anchor-id="8f5485a9c598a4ea2f89e043470b4e63:0">The application <strong>will display the domain and user ID of the Active directory or local machine account that is logged into Windows</strong></li>
 	<li data-lf-anchor-id="8f5485a9c598a4ea2f89e043470b4e63:0">but <strong>won't include user registration or log-in UI</strong>. This option is intended for Intranet web sites.</li>
 	<li data-lf-anchor-id="8f5485a9c598a4ea2f89e043470b4e63:0">You can add below lines in &lt;system.web&gt; in web.config</li>
 	<li data-lf-anchor-id="8f5485a9c598a4ea2f89e043470b4e63:0">
<pre class="EnlighterJSRAW" data-enlighter-language="null">&lt;authentication mode="Windows" /&gt;
&lt;authorization&gt;
&lt;deny users="?" /&gt;
&lt;/authorization&gt;</pre>
&nbsp;</li>
 	<li class="lf-text-block lf-block" data-lf-anchor-id="2fefede845be64ccb941e842c123635d:0">Alternatively, you can create an Intranet site that uses AD authentication by choosing the <a href="https://docs.microsoft.com/en-us/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthonprem" data-linktype="self-bookmark">On-Premises option under Organizational Accounts</a>. The On-Premises option uses Windows Identity Foundation (WIF) instead of the Windows Authentication module. Some additional steps are required in order to set up the On-Premises option, but WIF enables features that aren't available with the Windows Authentication module. For example, with WIF you can configure application access in Active Directory and query directory data.</li>
</ol>
&nbsp;
<h2 id="organizational-account-authentication-options" class="heading-with-anchor"><a href="http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/">Organizational account authentication options</a></h2>
<p class="lf-text-block lf-block" data-lf-anchor-id="cf0e248ec53beec44f8b10e301038413:0"><a href="https://docs.microsoft.com/en-us/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthsingle">Several options for Azure Active Directory</a> (Azure AD, which includes Office 365) or Windows Server Active Directory (AD) account authentication:</p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="722ee43f15fb79ecb936ded70ba7c705:0">
 	<li><strong>Cloud – Single Organization</strong> is meant for LoB apps tied to a Windows Azure AD tenant. Ex. <a href="http://www.cloudidentity.com/blog/2013/10/29/using-adals-acquiretokenby-authorizationcode-to-call-a-web-api-from-a-web-app/" target="_blank" rel="noopener">this post</a></li>
 	<li><strong>Cloud – Multiple Organizations</strong> is for <strong>SaaS</strong> applications intended to be used by multiple organizations with their own <strong>Windows Azure AD tenants</strong>; Ex. <a href="http://blogs.technet.com/b/ad/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx" target="_blank" rel="noopener">here</a></li>
 	<li><strong>On-Premises</strong>, the option we want to explore today, allows you to connect to any WS-Federation provider which offers a metadata document. Note that YMMV for any provider other than ADFS, as our testing focused on the latter.</li>
</ul>
If you choose one of the Azure AD options, your project requires a database and you have to sign in to a global administrator account for your Azure AD tenant.
<h4>ADFS configuration</h4>
<ul>
 	<li>Provision a Relying Party Trust to the application
<ul>
 	<li>Log in on the box where ADFS is running. From the Server Manager dashboard, launch the ADFS MMC by choosing “Tools-&gt;AD FS Management”.</li>
 	<li>Enter your web site url (dev, qa, prod), realm( relying party identifier) and other options and complete the provisioning</li>
</ul>
</li>
 	<li>At this point your app is known to ADFS – but we’re not done yet. Here’s why. Whereas Windows Azure AD features a default set of claims that are issued at sign in time, ADFS does not issue ANY claims without your direct configuration.
<ul>
 	<li>Name your rule, select Active Directory ad the attribute store, and go wild with the claims you want to issue. I always suggest to ensure you are issuing at least one “Name” claim, given that often web apps use that claim for display purposes</li>
</ul>
</li>
 	<li>Configure the values in MVC application
<p id="YStXQWp"><img class="alignnone wp-image-1219 " src="/wp-content/uploads/2018/03/img_5ab24b39a1125.png" alt="" width="386" height="272" /></p>

<ul>
 	<li><strong>On-Premises Authority</strong>” – URL of the metadata document of your authority. Get this value from your administrator. The template tool will use that<strong> document for discovering </strong>all of the <strong>relevant info</strong> about your<strong> ADFS</strong> (addresses, signing keys, identifiers, etc) and derive the project’s configuration from it</li>
 	<li>“<strong>App ID URI</strong>” – The realm of your application. this is a <a href="http://www.cloudidentity.com/blog/2013/03/02/url-urn-uri-oh-my/" target="_blank" rel="noopener">URI not an URL</a>. enter the same realm value which was entered in ADFS.</li>
</ul>
</li>
</ul>
<h3 id="require-authenticated-users" class="heading-with-anchor">Require authenticated users</h3>
<ul>
 	<li data-lf-anchor-id="e186400344534cb903c10c4741227f01:0">.NET Framework
<ul>
 	<li data-lf-anchor-id="e186400344534cb903c10c4741227f01:0">use <code>[Authorize]</code> for the ActionMethod. I also know that I can use it for the entire controller so that I don't have to specify it for each and every ActionMethod in it.</li>
</ul>
</li>
 	<li data-lf-anchor-id="e186400344534cb903c10c4741227f01:0">.NET Core
<ul>
 	<li class="lf-text-block lf-block" data-lf-anchor-id="e186400344534cb903c10c4741227f01:0"><strong>Set the default authentication policy</strong> to require users to be authenticated. Having authentication required by default is <strong>safer</strong> than relying on new controllers and Razor Pages to include the <code>[</code><strong>Authorize</strong><code>]</code> attribute.</li>
 	<li class="lf-text-block lf-block" data-lf-anchor-id="e186400344534cb903c10c4741227f01:0">You can <strong>opt out of</strong> authentication at the Razor Page, controller, or action method level with the <code>[</code><strong>AllowAnonymous</strong><code>]</code> attribute. Setting the default authentication policy to require users to be authenticated protects newly added Razor Pages and controllers.</li>
 	<li>In the <code>ConfigureServices</code> method of the <em>Startup.cs</em> file,</li>
 	<li class="">Set the default authentication policy to require users to be authenticated.</li>
 	<li data-lf-anchor-id="e186400344534cb903c10c4741227f01:0">
<pre><code>// requires: using Microsoft.AspNetCore.Authorization;
    //           using Microsoft.AspNetCore.Mvc.Authorization;
    services.AddMvc(config =&gt;
    {
        var policy = new AuthorizationPolicyBuilder()
                         .RequireAuthenticatedUser()
                         .Build();
        config.Filters.Add(new AuthorizeFilter(policy));
    });</code></pre>
</li>
 	<li data-lf-anchor-id="e186400344534cb903c10c4741227f01:0">Add <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute" data-linktype="absolute-path">AllowAnonymous</a> to the Index, About, and Contact pages etc., so anonymous users can get information about the site before they register.</li>
</ul>
</li>
</ul>
<h3>Require HTTPS</h3>
<ol>
 	<li>In essence, the only <strong>practical</strong> way to protect against wiretapping / packet sniffing during login is by using HTTPS or another certificate-based encryption scheme (for example, <a href="https://en.wikipedia.org/wiki/Transport_Layer_Security" rel="noreferrer">TLS</a>) or a proven &amp; tested challenge-response scheme (for example, the <a href="http://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange" rel="noreferrer">Diffie-Hellman</a>-based SRP). <em>Any other method can be easily circumvented</em> by an eavesdropping attacker.</li>
 	<li><a href="https://docs.microsoft.com/en-gb/aspnet/core/security/authorization/secure-data">.NET core</a>
<ol>
 	<li>A more secure approach is to add the <a href="https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx" data-linktype="external">RequireHttps</a> filter to the application</li>
 	<li>Add <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment" data-linktype="absolute-path">IHostingEnvironment</a> to <code>Startup clas. <span class="hljs-keyword">private</span> IHostingEnvironment Environment { <span class="hljs-keyword">get</span>; }</code></li>
 	<li>In the <code>ConfigureServices</code> method of the <em>Startup.cs</em> file, add the <a href="https://docs.microsoft.com/en-us/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute" data-linktype="absolute-path">RequireHttpsAttribute</a> authorization filter. If you're using Visual Studio Code or testing on a local platform that doesn't include a test certificate for HTTPS set <code>"LocalTest:skipSSL": true</code> in the <em>appsettings.Developement.json</em> file.</li>
 	<li>
<pre><code>var skipHTTPS = Configuration.GetValue("LocalTest:skipHTTPS");
    // requires using Microsoft.AspNetCore.Mvc;
    services.Configure(options =&gt;
    {
        // Set LocalTest:skipHTTPS to true to skip SSL requrement in 
        // debug mode. This is useful when not using Visual Studio.
        if (Environment.IsDevelopment() &amp;&amp; !skipHTTPS)
        {
            options.Filters.Add(new RequireHttpsAttribute());
        }
    });</code></pre>
</li>
</ol>
</li>
 	<li>.Net Framework
<ol>
 	<li>Register the <code>RequireHttpsAttribute</code> as a global filter - to secure <a href="https://stackoverflow.com/questions/3285014/mvc-requirehttps-entire-site">entire site</a>
<pre class="EnlighterJSRAW" data-enlighter-language="null">protected void Application_Start()
{
    GlobalFilters.Filters.Add(new RequireHttpsAttribute());

    //... other stuff
}</pre>
<a href="https://stackoverflow.com/questions/1639707/asp-net-mvc-requirehttps-in-production-only">For a particular controller or action</a>
<pre class="EnlighterJSRAW" data-enlighter-language="csharp"><code>#if !DEBUG
[RequireHttps] //apply to all actions in controller
#endif
public class SomeController 
{
    //... or ...
#if !DEBUG
    [RequireHttps] //apply to this action only
#endif
    public ActionResult SomeAction()
    {
    }

}</code></pre>
</li>
 	<li>Force Anti-Forgery tokens to use SSL/TLS:
<pre class="default prettyprint prettyprinted"><code><span class="typ">AntiForgeryConfig</span><span class="pun">.</span><span class="typ">RequireSsl</span> <span class="pun">=</span> <span class="kwd">true</span><span class="pun">;</span></code></pre>
</li>
 	<li> Require Cookies to require HTTPS by default by changing the Web.config file:
<pre class="default prettyprint prettyprinted"><code><span class="tag">&lt;system.web&gt;</span>
    <span class="tag">&lt;httpCookies</span> <span class="atn">httpOnlyCookies</span><span class="pun">=</span><span class="atv">"true"</span> <span class="atn">requireSSL</span><span class="pun">=</span><span class="atv">"true"</span> <span class="tag">/&gt;</span>
<span class="tag">&lt;/system.web&gt;</span></code></pre>
</li>
 	<li>Also if using <code>&lt;authentication mode="Forms"&gt;</code>, inside you must have <code>&lt;forms requireSSL="true"&gt;</code></li>
 	<li>Use the NWebSec.Owin NuGet package and add the following line of code to enable Strict Transport Security accross the site. Don't forget to add the Preload directive below and submit your site to the <a href="https://hstspreload.appspot.com/" rel="noreferrer">HSTS Preload site</a>. More information <a href="http://rehansaeed.com/nwebsec-asp-net-mvc-security-through-http-headers/" rel="noreferrer">here</a> and <a href="https://developer.mozilla.org/en-US/docs/Web/Security/HTTP_strict_transport_security" rel="noreferrer">here</a>. Note that if you are not using OWIN, there is a Web.config method you can read up on on the <a href="https://github.com/NWebsec" rel="noreferrer">NWebSec</a> site.
<pre class="default prettyprint prettyprinted"><code><span class="com">// app is your OWIN IAppBuilder app in Startup.cs</span><span class="pln">
app</span><span class="pun">.</span><span class="typ">UseHsts</span><span class="pun">(</span><span class="pln">options </span><span class="pun">=&gt;</span><span class="pln"> options</span><span class="pun">.</span><span class="typ">MaxAge</span><span class="pun">(</span><span class="pln">days</span><span class="pun">:</span> <span class="lit">30</span><span class="pun">).</span><span class="typ">Preload</span><span class="pun">());</span></code></pre>
</li>
 	<li>Use the NWebSec.Owin NuGet package and add the following line of code to enable Public Key Pinning (HPKP) across the site. More information <a href="http://rehansaeed.com/nwebsec-asp-net-mvc-security-through-http-headers/" rel="noreferrer">here</a> and <a href="https://visualstudiogallery.msdn.microsoft.com/6cf50a48-fc1e-4eaf-9e82-0b2a6705ca7d" rel="noreferrer">here</a>.
<pre class="default prettyprint prettyprinted"><code><span class="com">// app is your OWIN IAppBuilder app in Startup.cs</span><span class="pln">
app</span><span class="pun">.</span><span class="typ">UseHpkp</span><span class="pun">(</span><span class="pln">options </span><span class="pun">=&gt;</span><span class="pln"> options
    </span><span class="pun">.</span><span class="typ">Sha256Pins</span><span class="pun">(</span>
        <span class="str">"Base64 encoded SHA-256 hash of your first certificate e.g. cUPcTAZWKaASuYWhhneDttWpY3oBAkE3h2+soZS7sWs="</span><span class="pun">,</span>
        <span class="str">"Base64 encoded SHA-256 hash of your second backup certificate e.g. M8HztCzM3elUxkcjR2S5P4hhyBNf6lHkmjAHKhpGPWE="</span><span class="pun">)</span>
    <span class="pun">.</span><span class="typ">MaxAge</span><span class="pun">(</span><span class="pln">days</span><span class="pun">:</span> <span class="lit">30</span><span class="pun">));</span></code></pre>
</li>
 	<li>Include the https scheme in any URL's used. <a href="http://rehansaeed.com/content-security-policy-for-asp-net-mvc/" rel="noreferrer">Content Security Policy (CSP)</a> HTTP header and <a href="http://rehansaeed.com/subresource-integrity-taghelper-using-asp-net-core/" rel="noreferrer">Subresource Integrity (SRI)</a> do not play nice when you imit the scheme in some browsers. It is better to be explicit about HTTPS. e.g.
<pre class="default prettyprint prettyprinted"><code><span class="tag">&lt;script</span> <span class="atn">src</span><span class="pun">=</span><span class="atv">"https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js"</span><span class="tag">&gt;&lt;/script&gt;</span></code></pre>
</li>
</ol>
</li>
 	<li>To redirect HTTP requests to HTTPS, see <a class="xref" href="https://docs.microsoft.com/en-gb/aspnet/core/fundamentals/url-rewriting" data-linktype="relative-path">URL Rewriting Middleware</a>.
<ol>
 	<li style="list-style-type: none;">
<ol>
 	<li>A <em>URL redirect</em> is a client-side operation, where the client is instructed to access a resource at another address. This requires a round-trip to the server. The redirect URL returned to the client appears in the browser's address bar when the client makes a new request for the resource.</li>
 	<li>A <em class="">URL rewrite</em> is a server-side operation to provide a resource from a different resource address. Rewriting a URL doesn't require a round-trip to the server. The rewritten URL isn't returned to the client and won't appear in the browser's address bar.</li>
 	<li>URL Rewrite module with IIS 7
<ol>
 	<li>
<pre class="EnlighterJSRAW" data-enlighter-language="null">&lt;system.webServer&gt;
  &lt;!-- This uses URL Rewrite 2.0 to force the entire site into SSL mode --&gt;
  &lt;rewrite&gt;
        &lt;rules&gt;
            &lt;rule name="Redirect HTTP to HTTPS" stopProcessing="true"&gt;
                &lt;match url="(.*)"/&gt;
                &lt;conditions&gt;
                    &lt;add input="{HTTPS}" pattern="^OFF$"/&gt;
                &lt;/conditions&gt;
                &lt;action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="SeeOther"/&gt;
            &lt;/rule&gt;
        &lt;/rules&gt;
    &lt;/rewrite&gt;
&lt;/system.webServer&gt;</pre>
</li>
</ol>
</li>
 	<li><a href="https://stackoverflow.com/questions/4945883/how-to-redirect-http-to-https-in-mvc-application-iis7-5">Using Global.asax</a>
<pre><code>protected void Application_BeginRequest(){
    if (!Context.Request.IsSecureConnection)
    {
        Response.Clear();
        Response.Status = "301 Moved Permanently";
        Response.AddHeader("Location", Context.Request.Url.ToString().Insert(4, "s"));
        Response.End();
    }
}</code></pre>
</li>
 	<li>Or You could add the same code to an action filter:
<pre><code>public class SSLFilter : ActionFilterAttribute {

    public override void OnActionExecuting(ActionExecutingContext filterContext){
        if (!filterContext.HttpContext.Request.IsSecureConnection){
            var url = filterContext.HttpContext.Request.Url.ToString().Replace("http:", "https:");
            filterContext.Result = new RedirectResult(url);
        }
    }
}</code></pre>
</li>
 	<li><a href="https://benjii.me/2015/10/redirect-to-https-asp-net-mvc/">Register a custom global filter</a></li>
</ol>
</li>
</ol>
</li>
 	<li><a href="https://stackoverflow.com/questions/43886818/enabling-ssl-in-visual-studio-2017">Enable SSL for VS</a>
<ol>
 	<li>The SSL setting is at a different place in ASP.NET and ASP.NET Core projects.
<p id="VBpKeKc"><img class="alignnone wp-image-1079 " src="/wp-content/uploads/2018/03/img_5aaf7c6fa9ed5.png" alt="" width="340" height="204" /></p>
</li>
 	<li>.NET core
<p id="eOVwXHY"><img class="alignnone wp-image-1080 " src="/wp-content/uploads/2018/03/img_5aaf7ca898809.png" alt="" width="447" height="125" /></p>
</li>
 	<li>
<p id="hajUEOh"><img class="alignnone wp-image-1081 " src="/wp-content/uploads/2018/03/img_5aaf7d127f8e0.png" alt="" width="426" height="183" /></p>
</li>
 	<li>
<p id="uoIwpzy"><img class="alignnone wp-image-1082 " src="/wp-content/uploads/2018/03/img_5aaf7d48a41a7.png" alt="" width="401" height="402" /></p>
</li>
</ol>
</li>
</ol>
&nbsp;

&nbsp;
<h3>References</h3>
&nbsp;
<ul>
 	<li><a href="https://docs.microsoft.com/en-us/aspnet/identity/overview/getting-started/aspnet-identity-recommended-resources#qand">ASP.NET Identity Recommended Resources</a></li>
 	<li>https://community.apigee.com/questions/21139/jwt-vs-oauth.html</li>
 	<li>https://www.asp.net/mvc/overview/security</li>
 	<li>https://docs.microsoft.com/en-us/aspnet/identity/overview/getting-started/introduction-to-aspnet-identity</li>
 	<li>https://oauth.net/2/</li>
 	<li>https://aaronparecki.com/oauth-2-simplified/</li>
</ul>
information security
<ul>
 	<li>http://resources.infosecinstitute.com/top-50-information-security-interview-questions/#gref</li>
</ul>
Security
<ul>
 	<li>https://www.globalguideline.com/interview_questions/Questions.php?sc=Dot_Net_Code_Security</li>
 	<li>https://www.codeproject.com/Articles/762822/ASP-NET-Interview-Questions-for-Beginners-and-Pr</li>
 	<li>https://ggopi.wordpress.com/2011/01/12/asp-net-authentication-interview-questions/</li>
 	<li>http://programmingcrackers.blogspot.in/p/and-authorization-what-is-web-security.html</li>
 	<li>test https://www.vskills.in/practice/startPracticeTest/ASP-NET-Security-Questions</li>
 	<li>https://www.globalguideline.com/interview_questions/Questions.php?sc=Dot_Net_Code_Security</li>
</ul>
&nbsp;
<ul>
 	<li>http://interviewquestionsanswerspdf.com/tag/100-top-asp-net-mvc-security-interview-questions/</li>
 	<li>https://career.guru99.com/top-50-asp-net-web-api-interview-questions-and-answers/</li>
</ul>
