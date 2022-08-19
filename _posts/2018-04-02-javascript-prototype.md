---
layout: post
title: Javascript prototype
date: 2018-04-02 06:12
author: tmasabari
comments: true
categories: [Client Side, Software, Web Application]
---
<h2>Prototype Pattern</h2>
function Employee () {}
​Employee.prototype.firstName = "Abhijit";
Employee.prototype.lastName = "Patel";
Employee.prototype.fullName = function () {
console.log (this.firstName + " " + this.lastName);
};
​
​var emp = new Employee();
<h2>Constructor Pattern</h2>
function Employee (name, profession) {
​this.name = name;
​this.profession = profession;
} // Employee () is the constructor function because we use the &lt;em&gt;new&lt;/em&gt; keyword below to invoke it.​
​
​var richard = new Employee (“Richard”, “Developer”) // richard is a new object we create from the Employee () constructor function.​
​
console.log(richard.name); //richard​
console.log(richard.profession); // Developer
<blockquote>Quote:

<strong>JavaScript Prototype</strong>
In JavaScript, you add methods and properties on the prototype property when you want instances of an object to inherit those methods and properties. This is the reason we add the methods on the User.prototype property, so that they can be used by all instances of the User object.</blockquote>
<h2>Encapsulation in JavaScript</h2>
&nbsp;
<ol>
 	<li><strong>This in essence is the prototype chain:</strong>
<ol>
 	<li>the chain from an object’s prototype to its prototype’s prototype and onwards. And JavaScript uses this prototype chain to look for properties and methods of an object.</li>
 	<li>If the property does not exist on any of the object’s prototype in its prototype chain, then the property does not exist and <em>undefined</em> is returned.</li>
 	<li>Moreover, all objects that inherit from another object also inherit a <em>constructor</em> property.</li>
</ol>
</li>
</ol>
<h2>Points of Interest</h2>
<ul>
 	<li><a href="http://javascriptissexy.com/javascript-objects-in-detail/">http://javascriptissexy.com/javascript-objects-in-detail/</a></li>
 	<li><a href="http://javascriptissexy.com/javascript-prototype-in-plain-detailed-language/">http://javascriptissexy.com/javascript-prototype-in-plain-detailed-language/</a></li>
 	<li><a href="http://javascriptissexy.com/oop-in-javascript-what-you-need-to-know/">http://javascriptissexy.com/oop-in-javascript-what-you-need-to-know/</a></li>
 	<li><a href="http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/">http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/</a></li>
 	<li><a href="https://philipwalton.com/articles/implementing-private-and-protected-members-in-javascript/">https://philipwalton.com/articles/implementing-private-and-protected-members-in-javascript/</a></li>
 	<li><a href="https://www.nczonline.net/blog/2010/03/02/maintainable-javascript-dont-modify-objects-you-down-own/">https://www.nczonline.net/blog/2010/03/02/maintainable-javascript-dont-modify-objects-you-down-own/</a></li>
</ul>
