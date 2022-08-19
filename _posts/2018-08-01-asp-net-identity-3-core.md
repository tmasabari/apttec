---
layout: post
title: ASP.NET Identity 3 Core
date: 2018-08-01 11:56
author: tmasabari
comments: true
categories: [ASP.NET, ASP.NET Core, Identity, Security]
---
<ul>
 	<li><a href="http://www.apttec.com/security-net-interview-questions-2/">Legacy membership to ASP.NET Identity 2 - interview questions</a></li>
</ul>
&nbsp;

If you build MVC5 application you can only use Identity 2. If you are building ASP.Net Core application you can only use Identity 3.

Identity 2 is in support, but not in active development. I.e. bugs will be fixed, but no new features will be provided.

If you are starting a new project, then I don't see a reason to use MVC5. All green-field projects should be done in ASP.Net Core with Identity 3

&nbsp;
<h2>Identity DB Context Customization</h2>
https://medium.com/@goodealsnow/asp-net-core-identity-3-0-6018fc151b4
<ol>
 	<li>Never use ASP NET Core Identity ? because nvarchars and GUIDs are evil.</li>
 	<li>The Id column should be named AspNetUserId and</li>
 	<li>The tables should not be pluralized. So instead of AspNeUsers it should be AspNetUser.</li>
 	<li>In addition, that nothing should be on the dbo schema instead it should be in its own schema called Security.</li>
</ol>
&nbsp;
