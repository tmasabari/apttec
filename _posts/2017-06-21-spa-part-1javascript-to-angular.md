---
layout: post
title: SPA -Part 1:JavaScript to Angular
date: 2017-06-21 12:16
author: tmasabari
comments: true
categories: [Angular, Angular, Client, Client Side, Software, Software, TypeScript, Web Application]
---
<h2>Introduction</h2>
This article is a collection of notes and references from other web sites for the self study of Single Page Applications and Angular. The list of source web sites referred are mentioned in the "POINTS OF INTEREST" section of this article.
<h2>Background</h2>
<ul>
 	<li>Single-Page Applications (SPAs) are Web apps that load a single HTML page and dynamically update that page as the user interacts with the app.</li>
 	<li>SPAs use AJAX and HTML5 to create fluid and responsive Web apps, without constant page reloads. However, this means much of the work happens on the client side, in JavaScript<img class="aligncenter" src="https://i-msdn.sec.s-msft.com/dynimg/IC690875.png" alt="The Traditional Page Lifecycle vs. the SPA Lifecycle" width="240" height="266" /></li>
 	<li>In a traditional Web app, every time the app calls the server, the server renders a new HTML page. This triggers a page refresh in the browser.</li>
 	<li>An SPA renders only one HTML page from the server, when the user starts the app. Along with that one HTML page, the server sends an application engine to the client. The engine controls the entire application including processing, input, output, painting, and loading of the HTML pages.</li>
 	<li>In an SPA, after the first page loads, all interaction with the server happens through AJAX calls. These AJAX calls return data—not markup—usually in JSON format. The app uses the JSON data to update the page dynamically, without reloading the page.</li>
 	<li><strong>Benefits</strong>
<ul>
 	<li>One benefit of SPAs is obvious: Applications are more fluid and responsive, without the jarring effect of reloading and re-rendering the page.</li>
 	<li>Typically, 90–95 percent of the application code runs in the browser; the rest works in the server when the user needs new data or must perform secured operations such as authentication. Because dependency on the server is mostly removed, an SPA autoscales in the Angular 2 environment: No matter how many users access the server simultaneously, 90–95 percent of the time the app's performance is never impacted.</li>
 	<li>Sending the app data as JSON creates a separation between the presentation (HTML markup) and application logic (AJAX requests plus JSON responses).</li>
 	<li>In a pure SPA, all UI interaction occurs on the client side, through JavaScript and CSS. After the initial page load, the server acts purely as a service layer.</li>
</ul>
</li>
</ul>
<h2>ECMAScript Vs TypeScript</h2>
<b>ECMAScript</b> (or <b>ES</b>) is a <a title="Trademarked" href="https://en.wikipedia.org/wiki/Trademarked">trademarked</a> <a title="Scripting-language" href="https://en.wikipedia.org/wiki/Scripting-language">scripting-language</a> <a title="Specification (technical standard)" href="https://en.wikipedia.org/wiki/Specification_(technical_standard)">specification</a> standardized by <a title="Ecma International" href="https://en.wikipedia.org/wiki/Ecma_International">Ecma International</a> in <b>ECMA-262</b> and ISO/IEC 16262.
<ul>
 	<li>It was created to standardize <a title="JavaScript" href="https://en.wikipedia.org/wiki/JavaScript">JavaScript</a>, so as to foster multiple independent implementations. ECMAScript is the language, whereas JavaScript, JScript, and even ActionScript 3 are called "dialects".</li>
 	<li>ES5 is the JavaScript you know and use in the browser today. ECMAScript version 5 was finished in December 2009,  the latest versions of all major browsers (Chrome, Safari, Firefox, and IE)  have implemented version 5. So ES5 does not require a build step (transpilers) to transform it into something that will run in today's browsers.</li>
 	<li>Coders commonly use ECMAScript for <a title="Client-side scripting" href="https://en.wikipedia.org/wiki/Client-side_scripting">client-side scripting</a> on the <a title="World Wide Web" href="https://en.wikipedia.org/wiki/World_Wide_Web">World Wide Web</a>, and it is increasingly being used for writing server applications and services using <a title="Node.js" href="https://en.wikipedia.org/wiki/Node.js">Node.js</a>.</li>
 	<li>TypeScript is a strongly typed, object oriented, compiled language. It was designed by Anders Hejlsberg (designer of C#) at Microsoft. TypeScript is both a language and a set of tools. TypeScript is a typed superset of JavaScript compiled to JavaScript. In other words, TypeScript is JavaScript plus some additional features.</li>
</ul>
<img src="https://www.codeproject.com/KB/Articles/1192587/Working/TypeScript.png" />
<ul>
 	<li>As data types are introduced in Typescript below concepts are applicable
<ul>
 	<li>Variable declaration with datatypes</li>
 	<li>Type conversion/casting</li>
 	<li>Function overloading</li>
 	<li>Generics</li>
</ul>
</li>
 	<li>As OOPs are inbuilt in Typescript below concepts are applicable
<ul>
 	<li>Class declarations with private, public, protected, static members</li>
 	<li>Constructor</li>
 	<li>Inheritence, Overriding, Interfaces, this and base operators</li>
</ul>
</li>
</ul>
<h2>OOPs in ECMA Vs TypeScript</h2>
<ul>
 	<li>An object is an unordered list of name-value pairs. Each item in the list can be a <em>property</em> or <em>methods</em>.</li>
 	<li>JavaScript does not have classes. The classes in ES2015 are just a cleaned up syntax for setting up prototype inheritance between objects.</li>
 	<li>ECMA5 has a prototype-based inheritance mechanism: Every JavaScript function has a <strong>prototype property</strong>, and you attach properties and methods on this prototype property when you want to implement inheritance (to make those methods and properties available to instances of that function).This prototype property is not enumerable; that is,only one object can be assigned.</li>
 	<li>A <strong>constructor</strong> is a function used for initializing new objects, and you use the new keyword to call the constructor.</li>
</ul>
In ES5 and earlier, constructor functions defined “classes” like this:
<pre id="pre131365" class="notranslate">function Person(firstName, lastName) {
  <span class="code-keyword">this</span>.firstName = firstName;
  <span class="code-keyword">this</span>.lastName = lastName;
}
<span class="code-keyword">var</span> person = <span class="code-keyword">new</span> Person(<span class="code-string">"</span><span class="code-string">Bob"</span>, <span class="code-string">"</span><span class="code-string">Smith"</span>);</pre>
ES2015 introduces a new syntax using the class keyword:
<pre id="pre705251" class="notranslate" data-lang-guess="C#"><span class="code-comment">//</span><span class="code-comment"> the name of the ES5 constructor</span>
<span class="code-comment">//</span><span class="code-comment"> function is name of the ES2015 class</span>
<span class="code-keyword">class</span> Person {

  <span class="code-comment">//</span><span class="code-comment"> observe there is no "function" keyword</span>
  <span class="code-comment">//</span><span class="code-comment"> also, the word "constructor" is used, not "Person"</span>
  constructor(firstName, lastName) {

    <span class="code-comment">//</span><span class="code-comment"> this represents the new object being</span>
    <span class="code-comment">//</span><span class="code-comment"> created and initialized</span>
    <span class="code-keyword">this</span>.firstName = firstName;
    <span class="code-keyword">this</span>.lastName = lastName;

  }
} 
<span class="code-keyword">var</span> person = <span class="code-keyword">new</span> Person(<span class="code-string">"</span><span class="code-string">Bob"</span>, <span class="code-string">"</span><span class="code-string">Smith"</span>);</pre>
<pre id="pre581314" class="notranslate" data-lang-guess="C#"><span class="code-comment">//</span><span class="code-comment"> TypeScript</span>

<span class="code-keyword">class</span> Person {
  
  firstName: <span class="code-keyword">string</span>;
  lastName: <span class="code-keyword">string</span>; 
  
  constructor(firstname:<span class="code-keyword">string</span>, lastname:<span class="code-keyword">string</span> ){
  <span class="code-keyword">this</span>.firstName = firstname;
  <span class="code-keyword">this</span>.lastName = lastname; 
  } 
}

<span class="code-keyword">var</span> person = <span class="code-keyword">new</span> Person(<span class="code-string">"</span><span class="code-string">Mary"</span>, <span class="code-string">"</span><span class="code-string">Smith"</span>, <span class="code-digit">39</span>);</pre>
Hello World from TypeScript
<pre id="pre358706" class="notranslate" data-lang-guess="HTML"><span class="code-keyword">&lt;</span><span class="code-leadattribute">!DOCTYPE</span> <span class="code-attribute">html</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">html</span> <span class="code-attribute">lang</span><span class="code-keyword">="</span><span class="code-keyword">en"</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">head</span><span class="code-keyword">&gt;</span>
    <span class="code-keyword">&lt;</span><span class="code-leadattribute">title</span><span class="code-keyword">&gt;</span>TypeScript HTML App<span class="code-keyword">&lt;</span><span class="code-leadattribute">/title</span><span class="code-keyword">&gt;</span>
    <span class="code-keyword">&lt;</span><span class="code-leadattribute">script</span> <span class="code-attribute">src</span><span class="code-keyword">="</span><span class="code-keyword">app.js"</span><span class="code-keyword">&gt;</span><span class="code-keyword">&lt;</span><span class="code-keyword">/</span><span class="code-leadattribute">script</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">/head</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">body</span><span class="code-keyword">&gt;</span>
    <span class="code-keyword">&lt;</span><span class="code-leadattribute">div</span> <span class="code-attribute">id</span><span class="code-keyword">="</span><span class="code-keyword">content"</span><span class="code-keyword">&gt;</span><span class="code-keyword">&lt;</span><span class="code-leadattribute">/div</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">/body</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">/html</span><span class="code-keyword">&gt;</span>

//app.ts
class Greeter {
    element: HTMLElement;

    constructor(element: HTMLElement) {
        this.element = element;
        this.element.innerHTML = "Hello World";
    }
}

window.onload = () =&gt; {
    var el = document.getElementById('content');
    var greeter = new Greeter(el);
};

//Tranaspiled code
var Greeter = (function () {
    function Greeter(element) {
        this.element = element;
        this.element.innerHTML = "Hello World";
    }
    return Greeter;
})();

window.onload = function () {
    var el = document.getElementById('content');
    var greeter = new Greeter(el);
}</pre>
<h2>Points of Interest</h2>
You can explore more on the objects and OOPs in Javscript in below references.
<ul>
 	<li><a href="https://msdn.microsoft.com/en-us/magazine/dn463786.aspx">https://msdn.microsoft.com/en-us/magazine/dn463786.aspx</a></li>
 	<li><a href="https://en.wikipedia.org/wiki/Single-page_application">https://en.wikipedia.org/wiki/Single-page_application</a></li>
 	<li>ECMAScript 6 <a href="https://ponyfoo.com/articles/es6">https://ponyfoo.com/articles/es6</a></li>
 	<li><a href="http://kangax.github.io/compat-table/es6/">http://kangax.github.io/compat-table/es6/</a></li>
 	<li>Free book <a href="http://exploringjs.com/es6/">http://exploringjs.com/es6/</a></li>
 	<li><a href="http://www.wintellect.com/devcenter/nstieglitz/5-great-features-in-es6-harmony">http://www.wintellect.com/devcenter/nstieglitz/5-great-features-in-es6-harmony</a></li>
 	<li><a href="https://stackoverflow.com/questions/35210406/class-definition-confuse-in-typescript-and-es6">https://stackoverflow.com/questions/35210406/class-definition-confuse-in-typescript-and-es6</a></li>
 	<li><a href="https://en.wikipedia.org/wiki/TypeScript">https://en.wikipedia.org/wiki/TypeScript</a></li>
 	<li><a href="https://www.cheatography.com/gregfinzer/cheat-sheets/typescript/">https://www.cheatography.com/gregfinzer/cheat-sheets/typescript/</a></li>
 	<li><a href="https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html">https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html</a></li>
 	<li><a href="https://www.joshmorony.com/ionic-2-typescript-vs-ecmascript-6/">https://www.joshmorony.com/ionic-2-typescript-vs-ecmascript-6/</a></li>
 	<li><a href="https://www.codeproject.com/Articles/1121703/Quick-Reference-for-Typescript">https://www.codeproject.com/Articles/1121703/Quick-Reference-for-Typescript</a></li>
 	<li><a href="http://zenithsal.com/assets/documents/typescript_cheatsheet.pdf">http://zenithsal.com/assets/documents/typescript_cheatsheet.pdf</a></li>
 	<li><a href="https://learnxinyminutes.com/docs/typescript/">https://learnxinyminutes.com/docs/typescript/</a></li>
 	<li><a href="http://www.typescriptlang.org/play/">http://www.typescriptlang.org/play/</a></li>
</ul>
<h2>History</h2>
Version 1.0 - 2017  June 21 - Initial
