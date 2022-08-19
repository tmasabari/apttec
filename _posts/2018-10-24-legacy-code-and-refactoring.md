---
layout: post
title: Unit test legacy code
date: 2018-10-24 16:58
author: tmasabari
comments: true
categories: [Code Review, Refactor, Testing, Unit Test, Unit Test]
---
<!-- wp:heading -->
<h2>What is legacy code?</h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol>
<li>Legacy code is any code that does not have test coverage. (no test or lack of tests)
<ul>
<li>The age of the code has nothing to do with it. People are writing legacy code right now, maybe on your project.</li>
<li>The special problem of legacy code is that it was never designed to be testable.</li>
</ul>
</li>
<li>Legacy code is something still used, but hard to maintain and difficult  to change. The fact is that over a period of time code begins to rot. This can be because of
<ol>
<li>requirement changes,</li>
<li>a not-very-well-thought-through design,</li>
<li>applied anti-patterns, or</li>
<li>lack of appropriate tests.</li>
</ol>
</li>
<li>One of the most effective approaches to prevent your code from rotting, can be to write code that is testable and then generate sufficient unit tests for the code.</li>
</ol>
<!-- /wp:list -->

<!-- wp:heading -->
<h3>Maintaining legacy code</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol>
<li>The reasons for sustaining these systems generally revolve around the cost and time involved in building a similar new system—though sometimes there is a lack of awareness about the future implications of current coding efforts.</li>
<li>Most of the fear involved in making changes to large code bases is fear of introducing subtle bugs; fear of changing things inadvertently. With tests, you can make things better with impunity.</li>
</ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} --><!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 id="mce_2">Catch 22 of Legacy code</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>Unit tests act as agents that continuously probe the system for
<ol>
<li>uncovered paths,</li>
<li>identify troublesome errors, and</li>
<li>provide indicators whether changes introduced into a subsystem have a good or bad effect on the overall software.</li>
<li>Unit tests give confidence to the developer that the any code change will not introduce any regressions.</li>
</ol>
</li>
<li>Whenever you have to change legacy code, you should make sure it has coverage. You cannot change production code if not covered by tests
<ul>
<li>Only exception is just automated refactorings (via IDEs) are allowed, if needed to write the test</li>
</ul>
</li>
<li>If legacy system is a huge convoluted mess of spaghetti code, where it is very difficult or downright impossible to isolate small parts to be unit tested. So before unit testing, you need to refactor the code to make it more testable.</li>
<li><strong>However, in order to refactor safely, you must have unit tests</strong> to verify that you haven't broken anything with your changes... This is the catch 22 of legacy code.</li>
</ul>
<!-- /wp:list -->

<!-- wp:heading --><!-- /wp:list -->

<!-- wp:heading -->
<h2>Project planning to include unit tests to the legacy code</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Adding unit tests to an existing code base of any sizable project size is a LARGE undertaking which requires commitment and persistence.</p>
<ul>
<li>You can't change something fundamental, expect a lot of learning on the way and ask your sponsor to not expect any ROI by halting the flow of business value. That won't fly, and frankly it shouldn't.
<ul>
<li>Start somewhere and start adding tests while you make progress from the customer's perspective</li>
<li>Your approach should be to add tests to your code base WHILE you are making progress in terms of functionality.</li>
</ul>
</li>
<li>What you are doing is paying off technical debt. And you are doing so while still serving your customers ever changing needs. Gradually as debt is paid off, the situation improves, and it is easier to serve the customer better and deliver more value. Etc.</li>
</ul>
<p>You should do <strong>at the very least</strong></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul>
<li>Any new code you write should be completely under unit test</li>
<li>Any old code you happen to touch (bug fix, extension, etc.) should be put under unit test. The best way to go, IMO, is to add tests as you go.</li>
<li>That is, for every change you make, apply the following steps:
<ol>
<li>See whether existing tests sufficiently describe the current functionality.</li>
<li>If necessary, add tests to capture the current functionality of that particular part / module / class / function / ...</li>
<li>Verify that they pass.Refactor existing code if necessary.</li>
<li>Modify the tests to reflect the intended new behavior.</li>
<li>Modify the code to make the tests pass.</li>
<li>Refactor.</li>
</ol>
</li>
</ul>
<p>Steps 4 through 6 are just basic TDD; the only addition is that you retroactively add tests as needed before you start the actual TDD cycle.If you follow this procedure, and the tests you add in step 2 are sufficient, the codebase will gradually move towards full test coverage</p>
<!-- /wp:paragraph -->

<!-- wp:list --><!-- /wp:paragraph -->

<!-- wp:heading -->
<h3>Prerequisites </h3>
<h3>1. Code coverage</h3>
<ul>
<li>Measure the quality of <strong>automated tests</strong>. Two rough secondary indicators are
<ul>
<li>total code coverage and</li>
<li>build speed.</li>
</ul>
</li>
<li>
<p>Automated tests are often classified by level as:</p>
<p><!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} --></p>
<ol>
<li><strong>Unit tests</strong> - Individual components (classes, methods)</li>
<li><strong>Integration tests</strong> - Interactions between components</li>
<li><strong>System tests</strong> - The complete application</li>
</ol>
</li>
<li>Use code coverage as a guiding reference of how much of your production code base is under test.</li>
<li>Set up a build server and set up a continuous integration build that <strong>runs on every checkin including all unit tests with code coverage.</strong></li>
<li>Build time should always be FAST. If your build time is slow, your automated testing skills are lagging. Find the slow tests and improve them (decouple production code and test in isolation).</li>
<li>Well written, you should easily be able to have several thousands of unit tests and still complete a build in under 10 minutes (~1-few ms / test is a good but very rough guideline, some few exceptions may apply like code using reflection etc).</li>
</ul>
<h3>2. Training</h3>
<p><!-- /wp:heading -->

<!-- wp:list --></p>
<ul>
<li>Train your people. It is an investment in people, skills AND the quality of the code base and as such it will require time.</li>
<li>Instill sound business focus values in your team. <strong>Quality never comes at the expense of the customer and you can't go fast without quality.</strong></li>
<li>Also, the customer is living in a changing world, and your job is to make it easier for him to adapt. Customer alignment requires both quality and the flow of business value.</li>
<li>Team members need to learn how to break dependencies, write unit tests, learn new habbits, improve discipline and quality awareness, how to better design software, etc.</li>
<li>It is important to understand that when you start adding tests your team members likely don't have these skills yet at the level they need to be for that approach to be successful, so stopping progress to spend all time to add a lot of tests simply won't work.</li>
</ul>
<p><!-- /wp:heading -->

<!-- wp:paragraph --></p>
<p><!-- /wp:paragraph -->

<!-- wp:paragraph --></p>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h2>Pin-down tests</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>The recommended practice is to start with writing "pin-down tests" that test the current behaviour of the code, possibly including bugs, but without requiring you to descend into the madness of discerning whether a given behaviour that violates requirements documents is a bug, workaround for something you're not aware of, or represents an undocumented change in requirements.</li>
<li><strong>It makes the most sense for these pin-down tests to be at a high level, i.e. integration rather than unit tests, so that they'll keep working when you start refactoring.</strong></li>
<li>But some refactorings might be necessary to make the code testable - just be careful to stick to "safe" refactorings.
<ul>
<li>For example, in nearly all cases methods that are private can be made public without breaking anything.</li>
</ul>
</li>
</ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul>
<li>Write the level of test that can endure the refactoring essentially untouched.</li>
<li>Don't write <em>too</em> detailed tests (at least not at the beginning). Try to stay at a high level of abstraction (thus your tests will probably better characterized as regression or even integration tests).</li>
<li>Think:
<blockquote>What essential, publicly-visible behavior will the application have both <em style="font-size: 1rem;">before</em><span style="font-size: 1rem; font-style: italic;"> and </span><em style="font-size: 1rem;">after</em><span style="font-size: 1rem; font-style: italic;"> the refactoring? </span><strong style="font-size: 1rem; font-style: italic;">How can I test that thing still works the same?</strong></blockquote>
</li>
</ul>
<!-- /wp:quote -->

<!-- wp:list -->
<ul>
<li>There is actually significant variety in how people use the term unit test.</li>
<li>Some use it to mean only strictly isolated tests.</li>
<li>Others include any test that runs quickly. Some include anything that runs in a test framework.</li>
<li>But ultimately, it does not matter how you want to define the term unit test. The question is what tests are useful, so we shouldn't get distracted by how exactly we define unit test. </li>
</ul>
<!-- /wp:list -->

<!-- wp:image {"id":1762,"align":"center"} -->
<div class="wp-block-image">
<figure class="aligncenter"><img class="wp-image-1762 aligncenter" src="/wp-content/uploads/2018/10/image.png" alt="" /></figure>
</div>
<!-- /wp:image -->

<!-- wp:heading -->
<h2>Challenges of creating unit test for legacy code </h2>
<p><!-- /wp:heading -->

<!-- wp:list --></p>
<ul>
<li>Creating and maintaining a good unit test suite can be a challenge in itself.</li>
<li>It’s possible to end up writing more code for the test suite than the code under test.</li>
<li>Another challenge is dependencies within the code. The more complex the solution, the more dependencies you are likely to find between classes.</li>
</ul>
<h3>Dependencies</h3>
<p>You need to cut dependencies and introduce barriers into your code, but for two distinct reasons:</p>
<p><!-- /wp:paragraph -->

<!-- wp:list --></p>
<ul>
<li><strong>sensing</strong> - in order to check and verify the effects of executing a piece of code, and</li>
<li><strong>separation</strong> - in order to get the specific piece of code into a test harness first of all.</li>
</ul>
<p><!-- /wp:list -->

<!-- wp:paragraph --></p>
<p>One of the Pragmatic Programmer's rules of refactoring is make sure that you have unit test coverage before any refactorings to avoid regression.</p>
<p>This makes test double frameworks super useful, especially when the legacy code was not written for test-ability.</p>
<p><span style="font-size: 1rem;">Test doubles are a recognized way of removing these dependencies and testing the code in isolation, but these require additional knowledge and experience from the developer to create effective unit tests.</span></p>
<h3>Problem with Dependency injection for legacy code</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<ul>
<li>
<p>Cutting dependencies safely can be tricky. </p>
</li>
<li>
<p><span style="font-size: 1rem;">Introducing interfaces, mocks and </span><a style="font-size: 1rem;" href="http://en.wikipedia.org/wiki/Dependency_injection">Dependency Injection</a><span style="font-size: 1rem;"> is clean and nice as a goal, </span><strong style="font-size: 1rem;">just not necessarily safe to do at this point (for legacy code)</strong><span style="font-size: 1rem;">.</span></p>
</li>
<li><em>Decoupling</em> is essential for unit testing. DI is a great way to achieve decoupling.But Dependency injection is not essential for unit testing. Inversion of control on other hand is essential when you want to swap one implementation for another.</li>
<li>
<p>You can use <strong>factories or locators</strong> and test as you would with DI (just not as elegant and would require more setup).</p>
</li>
<li>
<p>Also, <strong>Mock Objects</strong> would be important in legacy systems where many calls are delegated to functions instead of dependencies. (Mock Objects can also be extensively utilized in a proper setup as well)</p>
</li>
</ul>
<!-- /wp:paragraph -->

<!-- wp:paragraph --><!-- /wp:paragraph -->

<!-- wp:paragraph -->
<ul>
<li>So sometimes we have to resort to subclassing the class under test in order to override some method which would normally e.g. start a direct request to a DB.</li>
<li>Other times, we might even need to <strong>replace a dependency class/jar with a fake one</strong> in the test environment...</li>
</ul>
<h3>Cutting dependencies without Fakes &amp; code weaving</h3>
<ol>
<li><strong>Problem 1: Communication with the framework is done through static methods </strong>
<ol>
<li>Solution: Wrap all static method calls in a separate class and use dependency injection to mock this object. This will create an extra layer of unnecessary classes in your application. However, this can of course be useful if you want to encapsulate the framework to be able to replace it.</li>
</ol>
</li>
<li><strong>Problem 2: The framework require you to subclass classes that contains static initializers or constructors. </strong>
<ol>
<li>Solution: Move all your code into a delegate and let the framework class simply delegate all method calls.</li>
</ol>
</li>
<li><strong>Problem 3: Mocking private and final methods</strong>
<ol>
<li>Solution: Private methods are not an option. Create a new class and move all private methods to this as public. Use dependency injection and mocking. This can force you to use an unwanted design.</li>
</ol>
</li>
<li><strong>Problem 4: Performance: </strong>
<ol>
<li>Dependency injection is too expensive for you so you want static method calls or a static factory instead. For example if you have extremely large number objects or if you are working with IOT applications</li>
<li>Solution: Create Singleton for each service and somehow make sure that during a test a special instance is created. This sometimes involves breaking the singleton pattern and adding the possibility to change the instance.</li>
</ol>
</li>
</ol>
<p><!-- /wp:paragraph -->

<!-- wp:paragraph --></p>
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li><a href="https://msdn.microsoft.com/en-us/magazine/ee819140.aspx?f=255&amp;MSPPError=-2147217396">https://msdn.microsoft.com/en-us/magazine/ee819140.aspx?f=255&amp;MSPPError=-2147217396</a></li>
<li><a href="https://softwareengineering.stackexchange.com/questions/122014/what-are-the-key-points-of-working-effectively-with-legacy-code/122024">https://softwareengineering.stackexchange.com/questions/122014/what-are-the-key-points-of-working-effectively-with-legacy-code/122024</a></li>
<li><a href="https://softwareengineering.stackexchange.com/questions/318634/how-to-write-unit-tests-before-refactoring?noredirect=1&amp;lq=1">https://softwareengineering.stackexchange.com/questions/318634/how-to-write-unit-tests-before-refactoring?noredirect=1&amp;lq=1</a></li>
<li><a href="https://stackoverflow.com/questions/3476054/can-unit-testing-be-successfully-added-into-an-existing-production-project-if-s">https://stackoverflow.com/questions/3476054/can-unit-testing-be-successfully-added-into-an-existing-production-project-if-s</a></li>
<li><a href="https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/">https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/</a></li>
<li><a href="https://softwareengineering.stackexchange.com/questions/140992/is-dependency-injection-essential-for-unit-testing">https://softwareengineering.stackexchange.com/questions/140992/is-dependency-injection-essential-for-unit-testing</a></li>
<li><a href="https://docs.microsoft.com/en-us/visualstudio/test/isolating-code-under-test-with-microsoft-fakes?view=vs-2017">https://docs.microsoft.com/en-us/visualstudio/test/isolating-code-under-test-with-microsoft-fakes?view=vs-2017</a></li>
<li><a href="http://xunitpatterns.com/XUnitBasics.html">http://xunitpatterns.com/XUnitBasics.html</a></li>
</ul>
<p><!--more--></p>
<!-- /wp:list -->
