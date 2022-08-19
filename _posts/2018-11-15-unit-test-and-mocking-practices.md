---
layout: post
title: Unit test and mocking practices
date: 2018-11-15 17:45
author: tmasabari
comments: true
categories: [Mock, Test Doubles, Testing, Unit Test]
---
<!-- wp:heading -->
<h2>Practices</h2>
<!-- /wp:heading -->

<!-- wp:heading -->
<h2>What to unit Test</h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Unit tests are a tool, like any other, and should be applied in such a way that the&nbsp;<strong>benefits (catching bugs) outweigh the costs (the effort writing them).</strong><ul><li>A&nbsp;<strong>developer can only write ~N lines of code a week</strong>&nbsp;and you need to figure out what percentage of that code should be&nbsp;<strong>unit test code vs production code</strong>.</li><li>Unit Testing is usually worth the effort, but the amount of effort required isn’t going to be the same for everybody.Its important to realize the unit tests are not a silver bullet and&nbsp;<strong>there&nbsp;<em>is</em></strong>&nbsp;such a thing as&nbsp;<strong>too much unit testing</strong>.&nbsp;“Imperfect&nbsp;<strong>tests, run frequently, are much better</strong>&nbsp;than perfect tests that are never written at all”. I interpret this as giving me permission to write tests where I think they’ll be most useful even if the rest of my code coverage is woefully incomplete.</li></ul></li><li><strong>Make sure you unit tests tests what needs to be unit tested…and nothing more.</strong><ol><li><strong>Don’t</strong>&nbsp;need to test code which has not logic like&nbsp;<strong>POCO classes</strong></li><li>It is a good practice to&nbsp;<strong>unit test only public interfaces</strong>. We usually test for exposed behavior, rather than specific implementation. Increased coupling between the test and the code, may result in the test breaking when the internal implementation has changed, while the exposed behavior hasn’t changed.</li></ol></li><li><strong>Your code should be unit testable. If it’s not, you may need to rethink your design.</strong><ol><li>Break the complex class or method – ie. Reduce Cyclomatic complexity for better understanding and</li><li>write smaller testable unit test cases</li></ol></li><li><strong>Write small unit tests to achieve quick wins</strong><ol><li>While 50 or more lines of code in a unit test is definitely a design problem/code smell</li></ol></li><li><strong>Don’t mock everything</strong><ol><li>Don’t mock business objects Or your own code</li></ol></li><li><strong>Use as many Asserts to confirm the behavior&nbsp;works as expected</strong><ol><li>You may return a number of parameters in a ViewModel that HAS to have a list of records, a total, and a page title. I would not make three methods to check each one separately. I would create one unit test with three Asserts.</li></ol></li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>A great&nbsp;<a href="http://www.typemock.com/Best-ever_Introduction_to_Unit_Testing_-_free-webinar">unit test</a>&nbsp;will do the following:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Fail only when a bug has been introduced</li><li>Fail Fast, for instant feedback</li><li>Easy to understand what scenario is being tested and needs fixing</li><li>Prefer to have one assert per test<ul><li>Think of reading the output of the test in the test runner. &nbsp;If you assert 20 things, you still only see a single failure. &nbsp;How will you know at a glance what went wrong — which of your 20 assertions failed?</li></ul></li><li>Avoid Test Interdependence<ul><li>Each test should handle its own setup and tear down.</li><li>Test cases order of execution may get changed for each new test case</li></ul></li><li>Keep It Short, Sweet, and Visible<ul><li>Resist the impulse to abstract test setup (the “arrange”) to other classes, and especially resist the impulse to abstract it into a base class.</li><li>The reasoning here is simple. &nbsp;When a test fails, you want to understand what went wrong at a glance</li><li>If you find that the “arrange” part of your unit test becomes cumbersome, stop what you’re doing. &nbsp;One of the most undercover powerful things about unit tests is that they provide&nbsp;excellent&nbsp;feedback on the design of your code — specifically its modularity. &nbsp;If you find yourself laboring heavily to get a class and method setup so that you can test it, you have a design problem.</li></ul></li><li>Keep unit test part of build<ul><li>If your team has a continuous integration build, add your new unit test suite’s execution to the build. &nbsp;If any tests fail, then the build fails. &nbsp;No exceptions, no ifs, ands or buts. &nbsp;Trust me on this one.</li><li>If unit test failures don’t stop your team’s progress, your team will eventually start ignoring the failures when the pressure to deliver mounts. &nbsp;It’s not a question of if, but when.</li></ul></li></ul>
<!-- /wp:list -->
