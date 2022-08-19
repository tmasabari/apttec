---
layout: post
title: Frequent Dotnet project commands
date: 2018-08-21 12:58
author: tmasabari
comments: true
categories: [Snippets]
---
EF.Core
<ul>
 	<li>Select 'GRM.Subscription.Identity'</li>
 	<li>Add-Migration -name openiddictintwithoutschema1 -context SubscriptionIdentityDbContext</li>
 	<li>Update-Database -context SubscriptionIdentityDbContext</li>
</ul>
&nbsp;

Install Angular
<ul>
 	<li>Js <a href="https://nodejs.org/en/download/">Install</a> latest version 10+</li>
 	<li><a href="https://www.microsoft.com/en-us/download/details.aspx?id=55258">TypeScript SDK for Visual Studio 2017</a></li>
 	<li>npm install --only=production</li>
 	<li>npm install -g @angular/cli</li>
 	<li>install angular essentials extension pack</li>
 	<li><a href="https://stackoverflow.com/questions/49810580/error-local-workspace-file-angular-json-could-not-be-found">https://stackoverflow.com/questions/49810580/error-local-workspace-file-angular-json-could-not-be-found</a>
<ul>
 	<li>install angular npm install -g @angular/cli</li>
 	<li>update angular ng update @angular/cli</li>
</ul>
</li>
</ul>
update database project <a href="https://social.msdn.microsoft.com/Forums/en-US/5c80a05e-c3aa-448f-a9ab-9e0f393341d6/how-to-quotupdatequot-database-schema-etc-to-quotdatabase-projectquot?forum=vstsdb">https://social.msdn.microsoft.com/Forums/en-US/5c80a05e-c3aa-448f-a9ab-9e0f393341d6/how-to-quotupdatequot-database-schema-etc-to-quotdatabase-projectquot?forum=vstsdb</a>
<ul>
 	<li>Import from database is a just-once action.  It is the intention that the database project is the <em>master </em>for source/object definition changes.  If you have changes in a database you want to integrate into your database project you can do so with Schema Compare. If you Schema Compare the database as a source and database project as the target you can pick which changes you want to take for the database.</li>
</ul>
Use separate project for each db <a href="https://blogs.msdn.microsoft.com/dukek/2010/01/04/implementing-a-database-design-using-multiple-database-projects/">https://blogs.msdn.microsoft.com/dukek/2010/01/04/implementing-a-database-design-using-multiple-database-projects/</a>
