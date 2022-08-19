---
layout: post
title: Angularjs
date: 2018-03-09 13:11
author: tmasabari
comments: true
categories: [Angular, Client Side, Prepare, QuickRefresh, Software, Web Application]
---
<a href="https://www.codeproject.com/Articles/891718/AngularJS-Interview-Questions-and-Answers">https://www.codeproject.com/Articles/891718/AngularJS-Interview-Questions-and-Answers</a>

<a href="http://www.c-sharpcorner.com/article/top-50-angularjs-interview-questions-and-answers/">http://www.c-sharpcorner.com/article/top-50-angularjs-interview-questions-and-answers/</a>

<a href="https://www.tutorialspoint.com/angularjs/angularjs_interview_questions.htm">https://www.tutorialspoint.com/angularjs/angularjs_interview_questions.htm</a>

<a href="https://www.toptal.com/angular-js/interview-questions">https://www.toptal.com/angular-js/interview-questions</a>

<a href="http://www.c-sharpcorner.com/UploadFile/97fc7a/right-angle-to-angularjs-basic-application-life-cycle/">http://www.c-sharpcorner.com/UploadFile/97fc7a/right-angle-to-angularjs-basic-application-life-cycle/</a>

AngularJS is an open-source JavaScript framework developed by Google. It is a structural framework for dynamic Web apps.
<ul>
 	<li>It supports Dependency Injection.</li>
 	<li>It supports two-way data binding.</li>
 	<li>It provides routing features.</li>
 	<li>Testing was designed right from the beginning; so you can build robust tests.</li>
 	<li>For DOM manipulation, jqLite is built-in; which is kind of like the Mini-Me of jQuery.</li>
 	<li>Separation of the client side of an Application from the Server side.</li>
 	<li>The AngularJS framework uses Plain Old JavaScript Objects(POJO), it doesn’t need the getter or setter functions.</li>
 	<li>Application written in AngularJS is cross-browser compliant. AngularJS automatically handles JavaScript code suitable for each browser.</li>
</ul>
&nbsp;

DOM Vs BOM

The DOM is the Document Object Model. It’s the view part of the UI. Whatever we are changing in page elements is reflected in the DOM.

BOM is the Browser Object Model, which specificies the global browser objects like <code>window</code>, <code>localstorage</code>, and <code>console</code>.

&nbsp;
<table border="1" width="100%" cellspacing="1" bgcolor="#ffffff">
<tbody>
<tr bgcolor="#0270bf">
<td width="105"><strong>Component of Angular</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td width="105">Module</td>
<td>Modules serve as containers to assist in organizing code within your AngularJs application. Modules can contain sub-modules.</td>
</tr>
<tr>
<td width="105">Services</td>
<td>Services are a point where you can put common functionality to an AngularJs application. For example if you would like to share data with more than one controller then the best way is to promote that data to a service and then make it available via the service. Services extend controllers and make them more globally accessible.</td>
</tr>
<tr>
<td width="105">Routes</td>
<td>Routes allow us to determine ways to navigate to specific states within our application. It also allows us to define configuration options for each specific route, such as which template and controller to use.</td>
</tr>
<tr>
<td width="105">View</td>
<td>The view in AngularJs is what exists after AngularJs has compiled and rendered the DOM. It's a representation of whatever outcome from</td>
</tr>
<tr>
<td width="105">@scope</td>
<td>$scope is essentially the “glue” between the view and controller within an AngularJs application. And somewhere supports two-way binding within the application.</td>
</tr>
<tr>
<td width="105">Controller</td>
<td>The controller is responsible for defining methods and properties that the view can bind to and interact with. Controllers should be lightweight and only focus on the view they're controlling.</td>
</tr>
<tr>
<td width="105">directive</td>
<td>A directive is an extension of a view in AngularJs in that it allows us to create custom, reusable elements. You can also consider directives as decorators for your HTML. Directives are used to extend views and to make these extensions available for use in more than one place.</td>
</tr>
<tr>
<td width="105">Config</td>
<td>The config block of an AngularJs application allows for the configuration to be applied before the application actually runs. This is useful for setting up routes, dynamically configuring services and so on.

&nbsp;</td>
</tr>
</tbody>
</table>
<h3 class="intro">An AngularJS module defines an application.</h3>
<ul>
 	<li class="intro">The module is a container for the different parts of an application.</li>
 	<li class="intro">The module is a container for the application controllers.</li>
 	<li class="intro">Controllers always belong to a module.</li>
 	<li>Global functions should be avoided in JavaScript. They can easily be overwritten or destroyed by other scripts. AngularJS modules reduces this problem, by keeping all functions local to the module.</li>
</ul>
&nbsp;
<ul>
 	<li>Data binding is the automatic synchronization of data between model and view components. ng-model directive is used in data binding.</li>
 	<li>Scopes are objects that refer to the model. They act as glue between controller and view.</li>
 	<li>Controllers are JavaScript functions that are bound to a particular scope. They are the prime actors in AngularJS framework and carry functions to operate on data and decide which view is to be updated to show the updated model based data.</li>
 	<li>AngularJS come with several built-in services. For example $https: service is used to make XMLHttpRequests (Ajax calls). Services are singleton objects which are instantiated only once in app.</li>
 	<li>Filters select a subset of items from an array and return a new array. Filters are used to show filtered items from a list of items based on defined criteria.</li>
 	<li>Angular expressions are unit of code which resolves to value. This code is written inside curly braces “{“ can also be written inside a directive: <code class="w3-codespan">ng-bind="<em>expression</em>"</code></li>
 	<li>Directives are markers on DOM elements (such as elements, attributes, css, and more). These can be used to create custom HTML tags that serve as new, custom widgets.AngularJS directives are only used to extend HTML and DOM elements' behavior. Directives are attributes decorated on the HTML elements. All directives start with the word “ng”. As the name says <strong>directive it directs Angular what to do</strong>.
<ul>
 	<li><strong>ngBind / Expressions</strong>, Binds the content of an HTML element to application data.</li>
 	<li><strong>ngModel</strong> define the model/variables value to be used in AngularJS Application’s HTML controls  it also provides two-way binding behavior</li>
 	<li><strong>ngClass </strong>Specifies CSS classes on HTML elements.</li>
 	<li><strong>ngApp </strong>indicate starting of an Angular Application to AngularJS HTML compiler ($compile), like a “Main()” function. If we do not use this directive first and directly try to write other directives, it gives an error. This directive ng-app tells that this element is the "owner" of an AngularJs application.</li>
 	<li>ngInit Defines initial values for an application.</li>
 	<li>ngRepeat</li>
</ul>
</li>
 	<li>Templates are the rendered view with information from the controller and model. These can be a single file (like index.html) or multiple views in one page using "partials".</li>
 	<li>Routing is concept of switching views. AngularJS based controller decides which view to render based on the business logic.</li>
 	<li>Deep linking allows you to encode the state of application in the URL so that it can be bookmarked. The application can then be restored from the URL to the same state.</li>
</ul>
<h3> Life cycle</h3>
<a href="http://www.informit.com/articles/article.aspx?p=2271482&amp;seqNum=3">http://www.informit.com/articles/article.aspx?p=2271482&amp;seqNum=3</a>

The three phases of the life cycle of an AngularJS application happen each time a web page is loaded in the browser. The following sections describe these phases of an AngularJS application.
<h4>The Bootstrap Phase</h4>
The first phase of the AngularJS life cycle is the bootstrap phase, which occurs when the AngularJS JavaScript library is downloaded to the browser. AngularJS initializes its own necessary components and then initializes your module, which the <tt>ng-app</tt> directive points to. The module is loaded, and any dependencies are injected into your module and made available to code within the module.
<h4>The Compilation Phase</h4>
The second phase of the AngularJS life cycle is the HTML compilation stage. Initially when a web page is loaded, a static form of the DOM is loaded in the browser. During the compilation phase, the static DOM is replaced with a dynamic DOM that represents the AngularJS view.

This phase involves two parts: traversing the static DOM and collecting all the directives and then linking the directives to the appropriate JavaScript functionality in the AngularJS built-in library or custom directive code. The directives are combined with a scope to produce the dynamic or live view.
<h4>The Runtime Data Binding Phase</h4>
The final phase of the AngularJS application is the runtime phase, which exists until the user reloads or navigates away from a web page. At that point, any changes in the scope are reflected in the view, and any changes in the view are directly updated in the scope, making the scope the single source of data for the view.

AngularJS behaves differently from traditional methods of binding data. Traditional methods combine a template with data received from the engine and then manipulate the DOM each time the data changes. AngularJS compiles the DOM only once and then links the compiled template as necessary, making it much more efficient than traditional methods.
<h3>communicate between modules</h3>
Common ways to communicate between modules of your application using core AngularJS functionality include:
<ul>
 	<li>Using services - easy to test. Services are injected, and in a test either a real service can be used or it can be mocked.</li>
 	<li>Using events - can be tested.</li>
 	<li>By assigning models on <code>$rootScope -<span style="color: #000000;"> testable, but sharing data through $rootScope is not considered a good practice.</span></code></li>
 	<li>Directly between controllers, using <code>$parent</code>, <code>$$childHead</code>, <code>$$nextSibling</code>, etc.</li>
 	<li>Directly between controllers, using <code>ControllerAs</code>, or other forms of inheritance</li>
</ul>
<h3>interpolation</h3>
It relies on $interpolation, a service which is called by the compiler. It evaluates text and markup which may contain AngularJS expressions. For every interpolated expression, a “watch()” is set. $interpolation returns a function, which has a single argument, “context”. By calling that function and providing a scope as context, the expressions are “$parse()”d against that scope.

&nbsp;

events
<table class="w3-table-all notranslate">
<tbody>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-blur.asp">ng-blur</a></td>
<td>Specifies a behavior on blur events.</td>
</tr>
</tbody>
</table>
&nbsp;
<table class="w3-table-all notranslate">
<tbody>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-keydown.asp">ng-keydown</a></td>
<td>Specifies a behavior on keydown events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-keypress.asp">ng-keypress</a></td>
<td>Specifies a behavior on keypress events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-keyup.asp">ng-keyup</a></td>
<td>Specifies a behavior on keyup events.</td>
</tr>
</tbody>
</table>
<table class="w3-table-all notranslate">
<tbody>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-copy.asp">ng-copy</a></td>
<td>Specifies a behavior on copy events.</td>
</tr>
<tr>
<td></td>
<td></td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-cut.asp">ng-cut</a></td>
<td>Specifies a behavior on cut events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-dblclick.asp">ng-dblclick</a></td>
<td>Specifies a behavior on double-click events.</td>
</tr>
</tbody>
</table>
<table class="w3-table-all notranslate">
<tbody>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-mousedown.asp">ng-mousedown</a></td>
<td>Specifies a behavior on mousedown events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-mouseenter.asp">ng-mouseenter</a></td>
<td>Specifies a behavior on mouseenter events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-mouseleave.asp">ng-mouseleave</a></td>
<td>Specifies a behavior on mouseleave events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-mousemove.asp">ng-mousemove</a></td>
<td>Specifies a behavior on mousemove events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-mouseover.asp">ng-mouseover</a></td>
<td>Specifies a behavior on mouseover events.</td>
</tr>
<tr>
<td><a href="https://www.w3schools.com/angular/ng_ng-mouseup.asp">ng-mouseup</a></td>
<td>Specifies a behavior on mouseup events.</td>
</tr>
</tbody>
</table>
&nbsp;

&lt;body <strong>ng-controller</strong>="MainCtrl"&gt;
&lt;input type="text" <strong>ng-model="name"</strong>&gt;
&lt;p&gt;Hello {{name}}!&lt;/p&gt;
&lt;/body&gt;

&lt;script src="app.js"&gt;&lt;/script&gt;

var app = angular.module('plunker', []);

var controller = <strong>function</strong>($scope) {
$scope.name = 'World';
}

app.controller(<strong>'MainCtrl', controller </strong>);

&nbsp;

“ng-controller” is a directive.Controllers are attached to the HTML UI by using the “ng-controller” directive tag and the properties of the controller are attached by using “ng-model” directive.
<pre class="notranslate" data-lang-guess="HTML"><span class="code-keyword">&lt;</span><span class="code-leadattribute">div</span> <span class="code-attribute">ng-controller</span><span class="code-keyword">="</span><span class="code-keyword">Customer"</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">input</span> <span class="code-attribute">type</span><span class="code-keyword">=</span><span class="code-keyword">text </span><span class="code-attribute">id</span><span class="code-keyword">="</span><span class="code-keyword">CustomerName"</span>  <span class="code-attribute">ng-model</span><span class="code-keyword">="</span><span class="code-keyword">CustomerName"</span><span class="code-keyword">/</span><span class="code-keyword">&gt;</span><span class="code-keyword">&lt;</span><span class="code-leadattribute">br</span> <span class="code-keyword">/</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">input</span> <span class="code-attribute">type</span><span class="code-keyword">=</span><span class="code-keyword">text </span><span class="code-attribute">id</span><span class="code-keyword">="</span><span class="code-keyword">CustomerCode"</span>  <span class="code-attribute">ng-model</span><span class="code-keyword">="</span><span class="code-keyword">CustomerCode"</span><span class="code-keyword">/</span><span class="code-keyword">&gt;
</span></pre>
<pre id="pre821445" class="notranslate" lang="”html”">The <span class="code-sdkkeyword">value</span> total cost <span class="code-keyword">is</span> {{ quantity * cost }}</pre>
<pre id="pre276913" class="notranslate" data-lang-guess="HTML"> <span class="code-keyword">&lt;</span><span class="code-leadattribute">/div</span><span class="code-keyword">&gt;</span></pre>
&nbsp;

Manual binding

<img class="alignnone size-full wp-image-423 " src="/wp-content/uploads/2017/12/img_5a28fb7b7aa1a.png" alt="" />
<h2><a name="Explain$scopeinAngular"></a>Explain $scope in Angular?</h2>
“$scope” is an object instance of a controller. “$scope” object instance get’s created when “ng-controller” directive is encountered.

For example in the below code snippet we have two controllers “Function1” and “Function2”. In both the controllers we have a “ControllerName” variable.
<p id="gqNzvAL"><img class="alignnone size-full wp-image-424 " src="/wp-content/uploads/2017/12/img_5a290193c88b9.png" alt="" /></p>

<h2><a name="Whatis“$rootScope”andhowisitrelatedwith“$scope”"></a>What is “$rootScope” and how is it related with “$scope”?</h2>
“$rootScope” is a parent object of all “$scope” angular objects created in a web page.
<p id="bcFIXMJ"><img class="alignnone size-full wp-image-425 " src="/wp-content/uploads/2017/12/img_5a2901d0547fc.png" alt="" /></p>

<h2><a name="Explaintheconceptofdigestcycle,watchersanddirtychecking"></a>Explain the concept of digest cycle, watchers and dirty checking?</h2>
In a nutshell, on every digest cycle all scope models are compared against their previous values. That is <em>dirty checking</em>. If change is detected, the watches set on that model are fired. Then another digest cycle executes, and so on until all models are stable.

when external code changes models the digest cycle needs to be called manually. Usually to do that, “.$apply()” or similar is used

Digest cycle follows four important steps:-
<ol>
 	<li>Step 1:- Some kind of event is triggered by the end user like typing (onchange), button click etc and due to this activity model value changes.</li>
 	<li>Step 2:- Angular first checks if the new value and old values are same. If they are same he does not do anything. If they are not it then it invokes the digest cycle.</li>
 	<li>Step 3:- Digest cycle then runs through the scope objects to check which objects are getting affected because of this change. Every object in the scope have watchers. Watchers as the name says it listens whether the model has changed or not. Digest cycle informs the watchers about the model change and then watchers synchronize the view with the model data.</li>
 	<li>Step 4 :- In step 3 watchers update the view and due that update its very much possible that the model changes again. Now due to this model change we have to reevaulate the view again. So the digest loop runs once again to ensure that all things are synched up. This second loop which runs is termed as dirty check loop.</li>
</ol>
Below is the figure where in we have highlighted all the four steps.
<p id="ItpNPGg"><img class="alignnone size-full wp-image-426 " src="/wp-content/uploads/2017/12/img_5a29032eebf79.png" alt="" /></p>
So summarizing definitions for the above three concepts:-
<ul>
 	<li>Digest cycle: - It is a simple loop which updates the model and view.</li>
 	<li>Watchers :- They are listeners which are attached to expression and angular directives and fire when the model data changes.</li>
 	<li>Dirty check :- This is a extra digest loop which runs to check any cascading left over updates due to the first digest cycle.</li>
</ul>
If there lot of unnecessary watchers then digest cycle has to work harder. Consider the below simple example where we have two ng-models and three expression. So in all we should have 5 watchers for the below screen
<p id="HrZBxRK"><img class="alignnone size-full wp-image-427 " src="/wp-content/uploads/2017/12/img_5a2903f639cae.png" alt="" /></p>
There are lot of great open source tools which help you to figure out the number of watchers , one such tool is the “batarang” tool. It’s a simple Google chrome extension which you can install separately.

&nbsp;

Validations

Below are some example of new form elements introduced in HTML 5 and Angular works with almost all of them :-
<ul>
 	<li>Color.</li>
 	<li>Date</li>
 	<li>Datetime-local</li>
 	<li>Email</li>
 	<li>Time</li>
 	<li>Url</li>
 	<li>Range</li>
 	<li>Telephone</li>
 	<li>Number</li>
 	<li>Search</li>
</ul>
SPA is a concept where rather loading pages from the server by doing post backs we create a single shell page or master page and load the webpages inside that master page.

SPA can be implemented using routes in angular

Step 1: - Add the “Angular-route.js” file to your view.
<div id="premain735554" class="pre-action-link"><span id="prehide735554">Hide</span>   <span id="copycode735554">Copy Code</span></div>
<pre id="pre735554" class="notranslate" lang="html"><span class="code-keyword">&lt;</span><span class="code-leadattribute">script</span> <span class="code-attribute">src</span><span class="code-keyword">="</span><span class="code-keyword">~/Scripts/angular-route.js"</span><span class="code-keyword">&gt;</span><span class="code-keyword">&lt;</span><span class="code-keyword">/</span><span class="code-leadattribute">script</span><span class="code-keyword">&gt;</span></pre>
Step 2: - Inject “ngroute” functionality while creating Angular app object.
<div id="premain638043" class="pre-action-link"><span id="prehide638043">Hide</span>   <span id="copycode638043">Copy Code</span></div>
<pre id="pre638043" class="notranslate" lang="html">var app = angular.module("myApp", ['ngRoute']);</pre>
Step 3: - Configure the route provider.

In route provider we need to define which URL pattern will load which view. For instance in the below code we are saying “Home” loads “Yoursite/Home” view and “Search” loads “YourSite/Search” view.
<div id="premain708768" class="pre-action-link"><span id="prehide708768">Hide</span>   <span id="copycode708768">Copy Code</span></div>
<pre id="pre708768" class="notranslate" lang="html">app.config(['$routeProvider',
            function ($routeProvider) {;

                $routeProvider.
                        when('/Home, {
                            templateUrl: 'Yoursite/Home',
                            controller: 'HomeController'
                        }).
                        when('/Search', {
                            templateUrl: YourSite/Search',
                            controller: 'SearchController'
                        }).
                        otherwise({
                            redirectTo: '/'
                        });
            }]);</pre>
Step 4: - Define hyperlinks.

Define hyper link with the “#” structure as shown below. So now when user clicks on the below anchor hyperlinks, these actions are forwarded to route provider and router provider loads the view accordingly.
<div id="premain92767" class="pre-action-link"><span id="prehide92767">Hide</span>   <span id="copycode92767">Copy Code</span></div>
<pre id="pre92767" class="notranslate" lang="html"><span class="code-keyword">&lt;</span><span class="code-leadattribute">div</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">a</span> <span class="code-attribute">href</span><span class="code-keyword">="</span><span class="code-keyword">#/Home"</span><span class="code-keyword">&gt;</span>Home<span class="code-keyword">&lt;</span><span class="code-leadattribute">/a</span><span class="code-keyword">&gt;</span><span class="code-keyword">&lt;</span><span class="code-leadattribute">br</span> <span class="code-keyword">/</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">a</span> <span class="code-attribute">href</span><span class="code-keyword">="</span><span class="code-keyword">#/Search"</span><span class="code-keyword">&gt;</span> Search <span class="code-keyword">&lt;</span><span class="code-leadattribute">/a</span><span class="code-keyword">&gt;</span><span class="code-keyword">&lt;</span><span class="code-leadattribute">br</span> <span class="code-keyword">/</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">/div</span><span class="code-keyword">&gt;</span></pre>
Step 5: - Define sections where to load the view.

Once the action comes to the router provider it needs a place holder to load views. That’s defined by using the “ng-view” tag on a HTML element. You can see in the below code we have created a “DIV” tag with a place holder. So the view will load in this section.
<div id="premain789904" class="pre-action-link"><span id="prehide789904">Hide</span>   <span id="copycode789904">Copy Code</span></div>
<pre id="pre789904" class="notranslate" lang="html"><span class="code-keyword">&lt;</span><span class="code-leadattribute">div</span> <span class="code-attribute">ng-view</span><span class="code-keyword">&gt;</span>

<span class="code-keyword">&lt;</span><span class="code-leadattribute">/div</span><span class="code-keyword">&gt;</span></pre>
So if we summarize angular routing is a three step process (Below is a visual diagram for the same): -
<ul>
 	<li>Step 1: - End user clicks on a hyperlink or button and generates action.</li>
 	<li>Step 2: - This action is routed to the route provider.</li>
 	<li>Step 3: - Router provider scans the URL and loads the view in the place holder defined by “ng-view” attribute.</li>
</ul>
<p id="IAodSJw"><img class="alignnone wp-image-428 " src="/wp-content/uploads/2017/12/img_5a290660be548.png" alt="" width="347" height="210" /></p>
&nbsp;

&nbsp;

&nbsp;
<h3>Performance improvement</h3>
The two officially recommended methods for production are disabling debug data and enabling strict DI mode.

The first one can be enabled through the $compileProvider:
<pre><code class="language-js">myApp.config(function ($compileProvider) {
  $compileProvider.<strong>debugInfoEnabled(false);</strong>
});
</code></pre>
That tweak disables appending scope to elements, making scopes inaccessible from the console. The second one can be set as a directive:
<pre><code class="language-html">&lt;html ng-app=“myApp” ng-strict-di&gt;
</code></pre>
The performance gain lies in the fact that the <strong>injected modules are annotated explicitly, hence they don’t need to be discovered dynamically.</strong>

You don’t need to annotate yourself, just use some automated build tool and library for that.

Two other popular ways are:
<ul>
 	<li><strong>Using one-time binding where possible</strong>. Those bindings are set, e.g. in “{{ ::someModel }}” interpolations by prefixing the model with two colons. In such a case, no watch is set and the model is ignored during digest.</li>
 	<li>Making $httpProvider use applyAsync:</li>
</ul>
<pre><code>myApp.config(function ($httpProvider) {
  $httpProvider.useApplyAsync(true);
});
</code></pre>
… which <strong>executes nearby digest calls just once, using a zero timeout</strong>.

&nbsp;

&nbsp;
