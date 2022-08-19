---
layout: post
title: .NET Core configuration and Options pattern
date: 2018-08-08 14:22
author: tmasabari
comments: true
categories: [ASP.NET, ASP.NET Core]
---
https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.1

https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/index?view=aspnetcore-2.1&amp;tabs=basicconfiguration
<h2>Configuration</h2>
<p class="">The Configuration API provides a way to configure an ASP.NET Core web app based on a list of name-value pairs. Configuration is read at runtime from multiple sources. Name-value pairs can be grouped into a multi-level hierarchy.</p>
There are configuration providers for:
<ul>
 	<li>File formats (INI, JSON, and XML).</li>
 	<li><span style="background-color: #ffff00;">Command-line arguments. [builder.<span class="line-highlight">AddCommandLine(args);]</span>
</span></li>
 	<li>Environment variables.</li>
 	<li><span style="background-color: #ffff00;">In-memory .NET objects. (Ex. <span class="hljs-keyword">new</span> Dictionary&lt;<span class="hljs-keyword">string</span>, <span class="hljs-keyword">string</span>&gt;)</span></li>
 	<li>The unencrypted <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-2.1" data-linktype="relative-path">Secret Manager</a> storage.</li>
 	<li>An encrypted user store, such as <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1" data-linktype="relative-path">Azure Key Vault</a>.</li>
 	<li>Custom providers (installed or created).</li>
</ul>
<ol>
 	<li>Each configuration value maps to a string key.</li>
 	<li>If duplicate keys are provided, the last key-value pair is used.</li>
 	<li>There's built-in binding support to deserialize settings into a custom <a href="https://wikipedia.org/wiki/Plain_Old_CLR_Object" data-linktype="external">POCO</a> object (a simple .NET class with properties).</li>
</ol>
<h2 id="configuration-by-environment" class="heading-with-anchor">Configuration by environment</h2>
<ul>
 	<li>It's typical to have different configuration settings for different environments.</li>
 	<li>ASP.NET Core reads the environment variable <code>ASPNETCORE_ENVIRONMENT</code> at app startup and stores the value in <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname" data-linktype="absolute-path">IHostingEnvironment.EnvironmentName</a>.</li>
 	<li>You can set <code>ASPNETCORE_ENVIRONMENT</code> to any value, but <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.hosting.environmentname" data-linktype="absolute-path">three values</a> are supported by the framework:  <code>Development</code>, <code>Staging</code>, or <code>Production</code>.</li>
 	<li>The method for setting the environment depends on the operating system.</li>
 	<li>If <code>ASPNETCORE_ENVIRONMENT</code> isn't set, it defaults to <code>Production</code>.</li>
 	<li><span class="hljs-tag">&lt;<span class="hljs-name">p</span>&gt;</span> ASPNETCORE_ENVIRONMENT = @hostingEnv.EnvironmentName<span class="hljs-tag">&lt;/<span class="hljs-name">p</span>&gt;</span></li>
</ul>
&nbsp;
<h3>Development</h3>
<ul>
 	<li>The development environment can enable features that shouldn't be exposed in production.</li>
 	<li>The <strong>environment for local machine development can be set</strong> in the <em class="x-hidden-focus">Properties\launchSettings.json</em> file of the project.</li>
 	<li>This json file holds project specific settings associated with each debug profile, Visual Studio is configured to use to launch the application, including any environment variables that should be used.</li>
 	<li>You can define framework for your project for compilation and debugging for specific profiles.</li>
 	<li>The Visual Studio project properties <strong>Debug</strong> tab provides a GUI to edit the <em>launchSettings.json</em></li>
 	<li class="">Changes made to project profiles may not take effect until the web server is restarted. Kestrel must be restarted before it can detect changes made to its environment</li>
 	<li><em>launchSettings.json</em> is read if available. <code>environmentVariables</code> settings in <em>launchSettings.json</em> override environment variables.</li>
 	<li class="">The hosting environment is displayed.</li>
 	<li><em>launchSettings.json</em> shouldn't store secrets. The <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-2.1" data-linktype="relative-path">Secret Manager tool</a> can be used to store secrets for local development.</li>
 	<li>The Secret Manager tool doesn't encrypt the stored secrets and shouldn't be treated as a trusted store. It's for development purposes only. The keys and values are stored in a JSON configuration file in the user profile directory.</li>
 	<li></li>
</ul>
<pre><code>"EnvironmentsSample": {
   "commandName": "Project",
   "launchBrowser": true,
   "applicationUrl": "https://localhost:5001;http://localhost:5000",
   "environmentVariables": {
     "ASPNETCORE_ENVIRONMENT": "Development"
   }
}
</code></pre>
<ul>
 	<li>The <code>applicationUrl</code> property in <em>launchSettings.json</em> can specify a list of server URLs. Use a semicolon between the URLs in the list:</li>
 	<li>
<p class="">The value of <code>commandName</code> specifies the web server to launch. <code>commandName</code> can be any one of the following:</p>

<ul>
 	<li>IIS Express</li>
 	<li>IIS</li>
 	<li>Project (which launches Kestrel)</li>
</ul>
</li>
 	<li>When an app is launched with <a href="https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-run" data-linktype="absolute-path">dotnet run</a>:</li>
</ul>
<h3 id="production" class="heading-with-anchor">Production</h3>
The production environment should be configured to maximize security, performance, and app robustness. Some common settings that differ from development include:
<ul>
 	<li>Caching.</li>
 	<li class="">Client-side resources are bundled, minified, and potentially served from a CDN.</li>
 	<li>Diagnostic error pages disabled.</li>
 	<li>Friendly error pages enabled.</li>
 	<li class="">Production logging and monitoring enabled. For example, <a href="https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net-core" data-linktype="absolute-path">Application Insights</a>.</li>
</ul>
<h2>AppSettings</h2>
The <code>CreateDefaultBuilder</code> extension method in an ASP.NET Core 2.x app adds configuration providers for reading JSON files and system configuration sources:
<ul>
 	<li><em>appsettings.json</em></li>
 	<li><em>appsettings.&lt;EnvironmentName&gt;.json</em></li>
 	<li>Environment variables</li>
</ul>
In the preceding code, the environment variables are read last. Any configuration values set through the environment replace those set in the two previous providers.<code></code>

<strong>Notes</strong>
<ul>
 	<li>Dependency Injection (DI) isn't set up until after <code>ConfigureServices</code> is invoked.</li>
 	<li>The configuration system isn't DI aware.</li>
 	<li><code>IConfiguration</code> has two specializations:
<ul>
 	<li><code>IConfigurationRoot</code> Used for the root node. Can trigger a reload.</li>
 	<li><code>IConfigurationSection</code> Represents a section of configuration values. The <code>GetSection</code> and <code>GetChildren</code> methods return an <code>IConfigurationSection</code>.</li>
 	<li class="">Use <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.extensions.configuration.iconfigurationroot" data-linktype="absolute-path">IConfigurationRoot</a> when reloading configuration or for access to each provider. Neither of these situations are common.</li>
</ul>
</li>
</ul>
<h3 id="webconfig-file" class="heading-with-anchor">Web.config file</h3>
<ul>
 	<li>At first glance, it would appear that things have gotten worse; or at least, more complex. However, the ConfigurationManager method had one massive problem: it was a static class. The result being that most people have written their own wrapper around the ConfigurationManager class. We now have a class that can be injected out of the box; alternatively, you can split your configuration up into classes, and pass the classes around;</li>
 	<li>https://www.pmichaels.net/2018/03/17/short-walks-using-appsettings-json-in-asp-net-core/</li>
 	<li>For .NET Core</li>
 	<li>A <em>web.config</em> file is required when hosting the app in IIS or IIS Express.</li>
 	<li>Settings in <em>web.config </em>enable the <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/aspnet-core-module?view=aspnetcore-2.1" data-linktype="relative-path">ASP.NET Core Module</a> to launch the app and configure other IIS settings and modules.</li>
 	<li>If the <em>web.config</em> file isn't present and the project file includes <code>&lt;Project Sdk="Microsoft.NET.Sdk.Web"&gt;</code>, publishing the project creates a <em>web.config</em> file in the published output (the <em>publish</em> folder). For more information, see <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/index?view=aspnetcore-2.1#webconfig-file" data-linktype="relative-path">Host ASP.NET Core on Windows with IIS</a>.</li>
</ul>
<h2>Inject Configurations</h2>
<a href="https://developer.telerik.com/featured/new-configuration-model-asp-net-core/">https://developer.telerik.com/featured/new-configuration-model-asp-net-core/</a>
<ol>
 	<li>Create a class -'<code class=" language-csharp">SmtpConfig</code>'</li>
 	<li>Store the settings in a json file in sync with class
"Smtp": {
"Server": "192.168.204.5",
"Email": "abc@abc.com",
"User": "generic",
"Password": "xxx",
"Port": "25"
}</li>
 	<li>Inject the settings as object in<code class=" language-csharp"><span class="token function">ConfigureServices</span></code>
// Register the Smtp object instance which '<code class=" language-csharp">SmtpConfig</code>'binds against.
<pre class=" language-csharp"><code class=" language-csharp">services<span class="token punctuation">.</span>Configure<span class="token operator">&lt;</span>SmtpConfig<span class="token operator">&gt;</span><span class="token punctuation">(</span>Configuration<span class="token punctuation">.</span><span class="token function">GetSection<span class="token punctuation">(</span></span><span class="token string">"Smtp"</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;
</span></code></pre>
</li>
 	<li>ASP.NET Core has built-in dependency injection. The following page model uses <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/dependency-injection?view=aspnetcore-2.1" data-linktype="relative-path">constructor dependency injection</a> with <a href="https://docs.microsoft.com/en-us/dotnet/api/Microsoft.Extensions.Options.IOptions-1" data-linktype="absolute-path">IOptions&lt;TOptions&gt;</a>to access the settings.
To use the <code>SmtpConfig</code> class, you can inject them using the Interface <code>IOptions&lt;T&gt;</code>.
<pre class=" language-csharp"><code class=" language-csharp"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">HomeController</span> <span class="token punctuation">:</span> Controller
<span class="token punctuation">{</span>
    <span class="token keyword">private readonly</span> SmtpConfig SmtpConfig <span class="token punctuation">{</span> <span class="token keyword">get</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>
    <span class="token keyword">public</span> <span class="token function">HomeController<span class="token punctuation">(</span></span>IOptions<span class="token operator">&lt;</span>SmtpConfig<span class="token operator">&gt;</span> smtpConfig<span class="token punctuation">)</span>
    <span class="token punctuation">{</span>
        SmtpConfig <span class="token operator">=</span> smtpConfig<span class="token punctuation">.</span>Value<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
   <span class="token comment" spellcheck="true"> //Action Controller
</span><span class="token punctuation">}</span></code></pre>
</li>
 	<li><strong>How we call this other then web project ?</strong>
Asp.Net Core DI resolve all dependencies before creating controller. So,we can create an interface and implement it. Then We can inject it into controller and from there access the <code>appsettings.json</code>settings.
<pre class="lang-cs prettyprint prettyprinted"><code><span class="pln">services</span><span class="pun">.</span><span class="typ">AddTransient</span><span class="pun">&lt;</span><span class="typ">ICategory</span><span class="pun">,</span> <span class="typ">Category</span><span class="pun">&gt;();</span></code></pre>
</li>
</ol>
<h2>options pattern</h2>
The options pattern uses classes to represent groups of related settings. When configuration settings are isolated by feature into separate classes, the app adheres to two important software engineering principles:
<ul>
 	<li>The <a href="http://deviq.com/interface-segregation-principle/" data-linktype="external">Interface Segregation Principle (ISP)</a>: Features (classes) that depend on configuration settings <strong>depend only on the configuration settings that they use</strong>.</li>
 	<li class=""><a href="http://deviq.com/separation-of-concerns/" data-linktype="external">Separation of Concerns</a>: Settings for different parts of the app aren't dependent or coupled to one another.</li>
</ul>
&nbsp;

References
<ul>
 	<li>Environment and Launch settings
<ul>
 	<li>https://docs.microsoft.com/en-us/aspnet/core/fundamentals/environments?view=aspnetcore-2.1#environments</li>
</ul>
</li>
 	<li>Configuration
<ul>
 	<li>https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/index?view=aspnetcore-2.1&amp;tabs=basicconfiguration</li>
</ul>
</li>
 	<li>Options
<ul>
 	<li>https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.1#basic-options-configuration</li>
</ul>
</li>
</ul>
