---
layout: post
title: Implement important design patterns in a single solution
date: 2018-03-01 11:50
author: tmasabari
comments: true
categories: [C#, Code, Design, Design Principles, Patterns, Prepare, QuickRefresh, Software]
---
<h1>Background</h1>
Recently I had been provided with the interesting problem "Cube list to be implemented with the double linked list".

I began with solving the problem with the straightforward algorithm. But started refactoring the same with OOP principles and design patterns.

The solution is implemented with C# Core 2.0. You can find the source code <span style="background-color: #f6d5d9;">at </span><a href="https://drive.google.com/file/d/1KcwS6XWkBAhNySDdkzF3i2rtgQIquozQ/view?usp=sharing">Google Drive</a>.
<h2>Phase 1: Use most important design patterns</h2>
The most important design principles and patterns, I applied in the first phase of refactoring are as below.
<ol>
 	<li>Dependency Inversion principle is implemented with necessary interfaces.</li>
 	<li>Factory pattern</li>
 	<li>Service Locator pattern is implemented using inbuilt .NET core dependency injection framework.</li>
 	<li>Iterator pattern is implemented using IEnumerable and yield.</li>
</ol>
<h3>Basic Idea</h3>
<ol>
 	<li>Cube is implemented with both singly linked list and doubly linked list.</li>
 	<li>Both the list classes implement common interface ICubeNode. The Cube list class is not aware of (doesn't care) what type of list is used. (Dependency Inversion principle)</li>
 	<li>The type of list to be used to build the cube can be selected by the user at run-time.</li>
 	<li>The selection is passed as a parameter to the Factory class. (dependency injection)</li>
 	<li>The Factory will generate the required node objects (service locator pattern)</li>
 	<li>Each and every element of the cube can be extracted using Iterator pattern.</li>
</ol>
&nbsp;

Note: Thanks to Armen Shimoon for sharing the idea to <a href="http://dotnetliberty.com/index.php/2016/05/09/asp-net-core-factory-pattern-dependency-injection/" target="_blank" rel="noopener">invoke the factory pattern within the .NET Core dependency injection container</a>.
