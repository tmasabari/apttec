---
layout: post
title: SPA -Part 2:JavaScript to Angular
date: 2018-04-02 06:04
author: tmasabari
comments: true
categories: [Angular, Client Side, Web Application]
---
<h2>Introduction</h2>
In this part, we'll look below topics
<ol>
 	<li>Inheritance in Javascript and the need for TypeScript</li>
 	<li>Angular - Introduction</li>
</ol>
<h2>Background</h2>
(Optional) Is there any background to this article that may be useful such as an introduction to the basic ideas presented?
<h2>Using the code</h2>
<h2>Inheritence in ECMAScript</h2>
<ol>
 	<li>An object’s prototype attribute points to the object’s “parent”—the object it inherited its properties from.</li>
 	<li><strong>Object.prototype Properties Inherited by all Objects</strong>. All objects in JavaScript inherit properties and methods from Object.prototype. Object.prototype is the prototype attribute (or the prototype object) of all objects created with new Object () or with {}. All built-in constructors (Array (), Number (), String (), etc.) were created from the Object constructor, and as such their prototype is Object.prototype.</li>
</ol>
<p id="TUiHgkw"><img class="wp-image-1407 aligncenter" src="/wp-content/uploads/2018/04/img_5ac179d64e0da.png" alt="" width="383" height="199" /></p>

<h2>Why Angular?</h2>
<table border="1" cellspacing="1" cellpadding="1">
<tbody>
<tr>
<td>
<ul>
 	<li>Angular is an <b>open-source JavaScript framework</b> providing everything needed to create a client-side of a website.</li>
 	<li>
<h3>MVC pattern</h3>
<p id="UTlHfMF"><img class="alignnone size-full wp-image-1408 " src="/wp-content/uploads/2018/04/img_5ac17a0f220fd.png" alt="" /></p>
The Model-View-Controller pattern allows to split the project's data into three components: model, view, and controller. This way, the modification of each component can be conducted independently leading to tighter code and increasing the quality of the final product.

Except for MVC patterns, there are also Model-View-Presenter (MVP) and Model-View-View-Model (MVVM).</li>
 	<li>
<h3 id="templating">Templating</h3>
Talking about Angular 2 benefits, worth to mention its ease of display templates writing. Having really straightforward UI for your data, Angular allows you to get the end result with the more intuitive approach to the user interface that demands less code and seems to be more 'obvious'.</li>
 	<li>
<h3 id="data-binding">Data Binding</h3>
Angular uses <b>two-way data binding.</b> With its help, the framework is able to connect DOM to Model data via the Controller. In a nutshell, when users interact with inputs and give a new value to your app - not only View can be updated but the Model too. Accordingly, you do not need to write any method for tracking this changes within the app.</li>
 	<li>Angular 2.0 is written in TypeScript, a programming language from Microsoft that adds type checking and other enhancements to JavaScript.</li>
 	<li>TypeScript is a typed superset of JavaScript and ES6 that in addition to bringing new features that are in proposal stage (like decorators) enhances the language with type annotations. Type annotations enable a better developer experience because they can be used to discover errors before they happen at runtime or improving development tooling.</li>
</ul>
</td>
<td>&nbsp;

&nbsp;</td>
</tr>
</tbody>
</table>
<h2>Angular Vs AngularJs Vs React</h2>
Angular (4) isn't an upgrade from Angular 1 (AngularJs) but rather a completely new, different, and more advanced framework. Proficiency in Angular is already a highly sought-after skill for building high-performing, scalable, robust, and modern cross-platform applications.

#The Basics
<table>
<thead>
<tr>
<th>Attribute</th>
<th>AngularJS</th>
<th>Angular 2/4</th>
<th>React</th>
</tr>
</thead>
<tbody>
<tr>
<td><em>Version</em></td>
<td>1.5.0-rc1 / 1.49</td>
<td>2.0.0 - In Beta</td>
<td>0.14.6</td>
</tr>
<tr>
<td><em>Author</em></td>
<td>Google</td>
<td>Google</td>
<td>Facebook</td>
</tr>
<tr>
<td><em>Language</em></td>
<td>JavaScript/HTML</td>
<td>TypeScript</td>
<td>JSX</td>
</tr>
<tr>
<td><em>Size</em></td>
<td>143k</td>
<td>764k</td>
<td>151k</td>
</tr>
<tr>
<td><em>Github Stars</em></td>
<td>46.4k</td>
<td>8.4k</td>
<td>34.4k</td>
</tr>
<tr>
<td><em>Github Contributors</em></td>
<td>1,386</td>
<td>189</td>
<td>604</td>
</tr>
</tbody>
</table>
#The Meta Stuff
<table>
<thead>
<tr>
<th>Attribute</th>
<th>AngularJS</th>
<th>Angular 2/4</th>
<th>React</th>
</tr>
</thead>
<tbody>
<tr>
<td><em>Churn</em></td>
<td>Reduced</td>
<td>Reduced</td>
<td>High</td>
</tr>
<tr>
<td><em>Tooling</em></td>
<td>Low</td>
<td>High</td>
<td>High</td>
</tr>
<tr>
<td><em>Code Design</em></td>
<td>JS into HTML</td>
<td>JS into HTML</td>
<td>JavaScript Centric</td>
</tr>
<tr>
<td><em>JavaScript “Fatigue”</em></td>
<td>Less</td>
<td>Less</td>
<td>More</td>
</tr>
</tbody>
</table>
#The Other Information
<table>
<thead>
<tr>
<th>Attribute</th>
<th>AngularJS</th>
<th>Angular 2/4</th>
<th>React</th>
</tr>
</thead>
<tbody>
<tr>
<td><em>DOM</em></td>
<td>Regular DOM</td>
<td>Regular DOM</td>
<td>Virtual DOM</td>
</tr>
<tr>
<td><em>Learning Curve</em></td>
<td>High</td>
<td>Medium</td>
<td>Low</td>
</tr>
<tr>
<td><em>Packaging</em></td>
<td>Weak</td>
<td>Medium</td>
<td>Strong</td>
</tr>
<tr>
<td><em>Abstraction</em></td>
<td>Weak</td>
<td>Strong</td>
<td>Strong</td>
</tr>
<tr>
<td><em>Debugging General</em></td>
<td>Good HTML / Bad JS</td>
<td>Good JS/Good HTML</td>
<td>Good JS / Bad HTML</td>
</tr>
<tr>
<td><em>Debug Line NO</em></td>
<td>No</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td><em>Unclosed Tag Mentioned?</em></td>
<td>No</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td><em>Fails When?</em></td>
<td>Runtime</td>
<td>Runtime</td>
<td>Compile-Time</td>
</tr>
<tr>
<td><em>Binding</em></td>
<td>2 Way</td>
<td>2 Way</td>
<td>Uni-Directional</td>
</tr>
<tr>
<td><em>Templating</em></td>
<td>In HTML</td>
<td>In TypeScript Files</td>
<td>In JSX Files</td>
</tr>
<tr>
<td><em>Component Model</em></td>
<td>Weak</td>
<td>Strong</td>
<td>Medium</td>
</tr>
<tr>
<td><em>Building Mobile?</em></td>
<td>Ionic Framework</td>
<td>Ionic Framework</td>
<td>React Native</td>
</tr>
<tr>
<td><em>MVC</em></td>
<td>Yes</td>
<td>Yes</td>
<td>View Layer Only</td>
</tr>
<tr>
<td><em>Rendering</em></td>
<td>Client Side</td>
<td>Server Side</td>
<td>Server Side</td>
</tr>
</tbody>
</table>
<h2>Points of Interest</h2>
<ul>
 	<li><a href="https://angular.io/features">https://angular.io/features</a></li>
 	<li><a href="https://www.cleveroad.com/blog/react-vs-angular-ultimate-performance-research-2017">https://www.cleveroad.com/blog/react-vs-angular-ultimate-performance-research-2017</a></li>
 	<li><a href="https://www.pluralsight.com/guides/front-end-javascript/angular-vs-react-a-side-by-side-comparison">https://www.pluralsight.com/guides/front-end-javascript/angular-vs-react-a-side-by-side-comparison</a></li>
 	<li><a href="https://www.quora.com/Is-React-killing-Angular">https://www.quora.com/Is-React-killing-Angular</a></li>
 	<li><a href="https://www.ibm.com/developerworks/library/wa-implement-a-single-page-application-with-angular2/index.html">https://www.ibm.com/developerworks/library/wa-implement-a-single-page-application-with-angular2/index.html</a></li>
 	<li><a href="https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90">https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90</a></li>
</ul>
