---
layout: post
title: Angular .NET CORS integration
date: 2018-08-21 13:00
author: tmasabari
comments: true
categories: [Code, Snippets]
---
Angular lock file need to be included in git repository. <a href="https://stackoverflow.com/questions/44206782/do-i-commit-the-package-lock-json-file-created-by-npm-5">https://stackoverflow.com/questions/44206782/do-i-commit-the-package-lock-json-file-created-by-npm-5</a>

<a href="https://github.com/nodejs/citgm/issues/451">https://github.com/nodejs/citgm/issues/451</a>

Since node 8 and npm 5, npm install creates a package-lock.json to lock the versions of dependencies that are installed.
They recommend to commit this file.

&nbsp;

If if it’s ignored,   always test the latest version of our dependencies (especially in CI) ?

I think no. Because the CI is usually driven by an assembly that is checked for production, in this case it should be assembled with the same dependencies as the version that you have on the local host, in this way package-lock.json must always commit.

&nbsp;

&nbsp;

Open your startup project's properties (<em>Project-&gt;{ProjectName} Properties...</em> from the main menu or right click your project in the <em>Solution Explorer</em> and choose <em>Properties</em>), then navigate to the <em>Web</em> tab and under <em>Start Action</em> choose <em>Don't open a page. Wait for a request from an external application</em>.

You will still be able to use any browser (or Fiddler, whatever) to access the running application, but it won't open the browser window automatically, it'll just start in the background and wait for any requests.

For VS 15.7.1 Options -&gt; Projects and Solutions -&gt; Web Projects -&gt; (uncheck) Stop debugger when browser window is closed

Updated answer for a .NET Core Web Api project... Untick the 'Launch browser' checkbox (enabled by default).

<a href="https://stackoverflow.com/questions/716494/stop-visual-studio-from-launching-a-new-browser-window-when-starting-debug">https://stackoverflow.com/questions/716494/stop-visual-studio-from-launching-a-new-browser-window-when-starting-debug</a>

Run multiple websites Go to Solution properties -&gt; Common properties -&gt; Startup Project and select Multiple startup projects.

Better create separate solution for API and Angular

<a href="https://github.com/damienbod/AspNetCoreOpeniddictAngularImplicitFlow">https://github.com/damienbod/AspNetCoreOpeniddictAngularImplicitFlow</a>

&nbsp;

Chrome net internals

<a href="https://stackoverflow.com/questions/21177387/caution-provisional-headers-are-shown-in-chrome-debugger">https://stackoverflow.com/questions/21177387/caution-provisional-headers-are-shown-in-chrome-debugger</a>

The way I found about the extension that was blocking my resource was through the net-internals tool in Chrome:
<ul>
 	<li>Type chrome://net-internalsin the address bar and hit enter.</li>
 	<li>Open the page that is showing problems.</li>
 	<li>Go back to net-internals, click on <strong>events (###)</strong>and use the textfield to find the event related to your resource (use parts of the URL).</li>
 	<li>Finally, click on the event and see if the info shown tells you something.</li>
</ul>
<a href="https://weblog.west-wind.com/posts/2016/Sep/26/ASPNET-Core-and-CORS-Gotchas">https://weblog.west-wind.com/posts/2016/Sep/26/ASPNET-Core-and-CORS-Gotchas</a>

I am running a full js stack, angular front end and node back end on SSL, and the API is on a different domain running on port 8081, so I am doing CORS requests and withCredentials as I am dropping a session cookie from the API

So specifically my scenario was: POST request, withCredentials to port 8081 caused the "CAUTION: provisional headers are shown" message in the inspector and also of course blocked the request all together.

My solution was to set up apache to proxy pass the request from the usual SSL port of 443 to the node SSL port of 8081 (node has to be on a higher port as it cannot be ran as root in prod). So I guess Chrome doesn't like SSL requests to unconventional SSL ports, but perhaps their error message could be more specific.

<a href="https://stackoverflow.com/questions/37138196/asp-net-5-core-vnext-cors-not-working-even-if-allowing-pretty-much-everything">https://stackoverflow.com/questions/37138196/asp-net-5-core-vnext-cors-not-working-even-if-allowing-pretty-much-everything</a>

<strong>The CORS middleware only works on actual cross-domain requests</strong>

It is <strong>not</strong> fired if you just access a same domain request like typing a URL into the browser.

This means if you are testing you have to either use an actual cross-domain request from an XHR client on another port or domain, or an HTTP client that can explicitly poke an origin header into the HTTP request.

&nbsp;

&nbsp;

<a href="https://stackoverflow.com/questions/22284111/php-jquery-ajax-call-throws-neterr-empty-response/22401307#22401307">https://stackoverflow.com/questions/22284111/php-jquery-ajax-call-throws-neterr-empty-response/22401307#22401307</a>

I believe your request is not classed as a "simple request" under the CORS specification:

<a href="http://www.w3.org/TR/cors/#simple-cross-origin-request-0">http://www.w3.org/TR/cors/#simple-cross-origin-request-0</a>

since you are setting a response header for Content-Type: application/json.

So your server will need to handle the preflight request, which involves setting some additional headers on both the request and response for the CORS request to be successful

Here is a good article on what you need to do - check out the bit under "not so simple":

<a href="http://www.html5rocks.com/en/tutorials/cors/">http://www.html5rocks.com/en/tutorials/cors/</a>

&nbsp;

&nbsp;

&nbsp;

<a href="https://scotch.io/tutorials/debugging-angular-cli-applications-in-visual-studio-code">https://scotch.io/tutorials/debugging-angular-cli-applications-in-visual-studio-code</a> debugging with VS Code.

&nbsp;

For VS 2017 there is an template for angular 6

<a href="https://marketplace.visualstudio.com/items?itemName=AndreyFomin.AngularCLIProjectTemplate#overview">https://marketplace.visualstudio.com/items?itemName=AndreyFomin.AngularCLIProjectTemplate#overview</a>

&nbsp;

&nbsp;

<a href="https://www.linkedin.com/pulse/6-easy-steps-angular-5-visual-studio-irabanta-chingangbam/">https://www.linkedin.com/pulse/6-easy-steps-angular-5-visual-studio-irabanta-chingangbam/</a>

<strong>PRE-REQUISITES:</strong>
<ul>
 	<li>Node.Js <a href="https://nodejs.org/en/download/">Install</a></li>
 	<li>Visual Studio 2013 or 2015 or 2017 or Code</li>
 	<li><a href="https://www.microsoft.com/en-us/download/details.aspx?id=48593">Typescript for visual studio</a> 2015 or <a href="https://www.microsoft.com/en-us/download/details.aspx?id=55258">TypeScript SDK for Visual Studio 2017</a></li>
 	<li>Angular-CLI: This is installed by executing the following command in command prompt</li>
</ul>
<ul>
 	<li>1&gt;node --version</li>
 	<li>1&gt;v10.6.0</li>
 	<li>1&gt;npm --version</li>
 	<li>1&gt;6.1.0</li>
 	<li>1&gt;npm install --only=production</li>
 	<li>1&gt;npm WARN deprecated <a href="mailto:istanbul-lib-hook@1.2.1">istanbul-lib-hook@1.2.1</a>: 1.2.0 should have been a major version bump</li>
</ul>
npm install -g @angular/cli

&nbsp;

<strong>STEP 1: Create asp.net or MVC web application in visual studio</strong>

Say project name 'MY-ANGULAR' is created in the path "C:/PRACTICE". This means the .csproj file is generated in this folder 'c:/practice/my-angular'

Underscores, dot, numbers are not accepted as angular 6 application name <a href="https://github.com/angular/angular-cli/issues/9655">https://github.com/angular/angular-cli/issues/9655</a>

&nbsp;

<strong>STEP 2: Generate angular application using angular cli command</strong>

C:/PRACTICE&gt; ng new MY-ANGULAR

Hey its the same folder where MVC or asp.net application was created. We are also generating the angular codes inside it so that we can merge.

&nbsp;

<strong>STEP 3: Include all angular-cli generated outputs into the project created in step 1</strong>

In the visual studio MVC project created in step 1, use solution explorer window to show all files. Then include all the folders and files generated in step 2. DO NOT Include folder "node_modules"

<strong>STEP 4: Configure visual studio project to build angular app with CLI</strong>

Right click on the MVC project and properties. Goto build events and enter the following command in PRE BUILD EVENT

(ng build)

Then we can tell visual studio not build the typescripts so that angular-cli take care of the build for typescript. For this, unload the MVC project file and edit to insert the following lines

&lt;PropertyGroup&gt;    <em>&lt;!-- Makes the TypeScript compilation task a no-op --&gt;</em>    &lt;TypeScriptCompileBlocked&gt;true&lt;/TypeScriptCompileBlocked&gt;&lt;/PropertyGroup&gt;

&nbsp;

&nbsp;

STEP 5: Prepare the MVC default.cshtml to host angular

Since we are not going to undergo ASP.NET or MVC development, we can wipe out all the content in default.cshtml and replace by html generated by angular-cli build. Execute the following command in command prompt!

C:\PRACTICE\MY-ANGULAR&gt; ng build

All the build output should be there inside '<strong>dist</strong>' folder. Copy the content of the INDEX.HTM file and overwrite in DEFAULT.CSHTML. Make sure relative path of files linked are correctly modified.

&lt;script type="text/javascript" src="~/dist/runtime.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript" src="~/dist/polyfills.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript" src="~/dist/styles.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript" src="~/dist/vendor.js"&gt;&lt;/script&gt;

&lt;script type="text/javascript" src="~/dist/main.js"&gt;&lt;/script&gt;

&nbsp;

<strong>STEP 6: Setup publish to include the angular CLI compiled output</strong>

I was trying to publish the MVC project to IIS or in Azure App but the angular-cli build outputs generated in '<strong>dist</strong>' folder were not deployed to target. To make it working, I have to add the following XML in the publish.xml file just above &lt;/Project&gt; tag

&lt;Target Name="CustomCollectFiles"&gt;    &lt;ItemGroup&gt;      &lt;_CustomFiles Include="dist\**\*" /&gt;      &lt;FilesForPackagingFromProject Include="%(_CustomFiles.Identity)"&gt;        &lt;DestinationRelativePath&gt;dist\%(RecursiveDir)%(Filename)%(Extension)&lt;/DestinationRelativePath&gt;      &lt;/FilesForPackagingFromProject&gt;    &lt;/ItemGroup&gt;  &lt;/Target&gt;  &lt;PropertyGroup&gt;    &lt;CopyAllFilesToSingleFolderForPackageDependsOn&gt;CustomCollectFiles;      ;&lt;/CopyAllFilesToSingleFolderForPackageDependsOn&gt;    &lt;CopyAllFilesToSingleFolderForMsdeployDependsOn&gt;CustomCollectFiles;      ;&lt;/CopyAllFilesToSingleFolderForMsdeployDependsOn&gt;  &lt;/PropertyGroup&gt;

&nbsp;
