---
layout: post
title: Code Review, Best practices Patterns, checklists
date: 2018-03-21 08:18
author: tmasabari
comments: true
categories: [Code Review]
---
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">

<a href="https://stackoverflow.com/questions/140476/what-do-your-code-reviews-involve-and-what-patterns-are-successful">Here are the process summary</a>
<ol>
 	<li>Schedule reviews or inspections regularly and frequently. Review/Inspect whole modules when new, and delta <strong>+ surrounding code</strong> for maintenance. Building up a backlog of stuff to be reviewed makes the whole process intimidating.</li>
 	<li>Everyone's code gets reviewed, from the most junior to the most senior, and anyone can comment without fear of recrimination.</li>
 	<li>The author comments on the code written to give a clue to the reviewer on where to start.</li>
 	<li>The reviewer comments and add defects that will need to be fixed before the review is accepted. Only important things should be marked as defects. Not typos or things that you know the developer will fix before committing.</li>
 	<li>Involve new developers as observers. This is good training to get them familiar with the project.</li>
 	<li>Involve "experts" on the piece of code, as observer or reviewer.</li>
</ol>
Anti-patterns:
<ol>
 	<li>Use the code review tool as a design review tool. It is not suitable for that. Only review code for which a design has been agreed upon.</li>
 	<li>Involve too many reviewers and observers</li>
 	<li>Let the review linger in the system for more than a couple of days.</li>
</ol>
Microsoft checklist https://msdn.microsoft.com/en-us/library/bb871031.aspx

</div>
<h4> Architecture</h4>
a) The code should follow the defined architecture.
<ol>
 	<li>Separation of Concerns followed
<ul>
 	<li>Split into multiple layers and tiers as per requirements (Presentation, Business and Data layers).</li>
 	<li>Split into respective files (HTML, JavaScript and CSS).</li>
</ul>
</li>
</ol>
<ol start="2">
 	<li>Code is in sync with existing code patterns/technologies.</li>
 	<li>Design patterns: Use appropriate design pattern (if it helps), after completely understanding the problem and context.</li>
 	<li>
<h4>4. Non Functional requirements</h4>
<strong>a) Maintainability (Supportability)</strong> – The application should require the least amount of effort to support in near future. It should be easy to identify and fix a defect.
<ol>
 	<li><strong>Readability:</strong> Code should be self-explanatory. <em>Get a feel of story reading, while going through the code</em>. Use appropriate name for variables, functions and classes. If you are taking more time to understand the code, then either code needs refactoring or at least comments have to be written to make it clear.</li>
 	<li><strong>Testability:</strong> The code should be easy to test. Refactor into a separate function (if required). Use interfaces while talking to other layers, as interfaces can be mocked easily. Try to avoid static functions, singleton classes as these are not easily testable by mocks.</li>
 	<li><strong>Debuggability:</strong> Provide support to log the flow of control, parameter data and exception details to find the root cause easily. If you are using <a href="https://www.nuget.org/packages/log4net/" target="_blank" rel="noopener">Log4Net</a> like component then add support for database logging also, as querying the log table is easy.</li>
 	<li><b></b><b>Configurability: </b>Keep the configurable values in place (XML file, database table) so that no code changes are required, if the data is changed frequently.</li>
</ol>
<b>b) </b><b>Reusability</b>
<ol>
 	<li>DRY (Do not Repeat Yourself) principle: The same code should not be repeated more than twice.</li>
 	<li>Consider reusable services, functions and components.</li>
 	<li>Consider generic functions and classes.</li>
</ol>
<b>c) </b><b>Reliability – </b>Exception handling and cleanup (dispose) resources.

<b>d) </b><b>Extensibility – </b>Easy to add enhancements with minimal changes to the existing code. One component should be easily replaceable by a better component.

<b>e) </b><b>Security – </b>Authentication, authorization, input data validation against security threats such as <a href="http://www.w3schools.com/sql/sql_injection.asp" target="_blank" rel="noopener">SQL injections</a> and <a href="https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)" target="_blank" rel="noopener">Cross Site Scripting</a> (XSS), encrypting the sensitive data (passwords, credit card information etc.)

<b>f) </b><b>Performance</b>
<ol>
 	<li>Use a data type that best suits the needs such as StringBuilder, generic collection classes.</li>
 	<li>Lazy loading, asynchronous and parallel processing.</li>
 	<li>Caching and session/application data.</li>
</ol>
<b>g) </b><b>Scalability – </b>Consider if it supports a large user base/data? Can this be deployed into web farms?

<b>h) </b><b>Usability – </b>Put yourself in the shoes of a end-user and ascertain, if the user interface/API is easy to understand and use. If you are not convinced with the user interface design, then start discussing your ideas with the business analyst.</li>
</ol>
<h4>5. Object-Oriented Analysis and Design (OOAD) - SOLID Principles</h4>
&nbsp;

Basics
<ol>
 	<li>Am I able to <b>understand </b>the code easily?</li>
 	<li>Is the code written following the <b>coding standards/guidelines</b>?</li>
 	<li>Is the same code <b>duplicated </b>more than twice?</li>
 	<li>Can I <b>unit test / debug </b>the code easily to find the root cause?</li>
 	<li>Is this function or class <b>too big</b>? If yes, is the function or class having too many responsibilities?</li>
 	<li>No hard coding, use constants/configuration values.</li>
 	<li>Group similar values under an <a href="https://en.wikipedia.org/wiki/Enumerated_type" target="_blank" rel="noopener">enumeration</a> (enum).</li>
 	<li>Comments – Do not write comments for what you are doing, instead write comments on why you are doing. Specify about any hacks, workaround and temporary fixes. Additionally, mention pending tasks in your to-do comments, which can be tracked easily.</li>
 	<li>Avoid multiple if/else blocks.</li>
 	<li>Use framework features, wherever possible instead of writing custom code.</li>
 	<li>d) Remove the commented code as this is always a blocker, while going through the code. Commented code can be obtained from Source Control (like SVN), if required.</li>
 	<li>Formatting
<ol>
 	<li>a) Use alignments (left margin), proper white space. Also ensure that code block starting point and ending point are easily identifiable.b) Ensure that proper naming conventions (Pascal, CamelCase etc.) have been followed.

c) Code should fit in the standard 14 inch laptop screen.</li>
</ol>
</li>
 	<li></li>
</ol>
&nbsp;
<div id="slide_body">

In a few cases, one requirement may contradict with other requirement. So need to trade-off based on the importance of the weight-age, e.g. <strong>Performance vs Security</strong>. Too many checks and logging at multiple layers (UI, Middle tier, Database) would decrease the performance of an application. But few applications, especially relating to finance and banking require multiple checks, audit logging etc. So it is ok to compromise a little on performance to provide enhanced security.
<h3>Tools for Code Reviews</h3>
<ol>
 	<li>The first step while assessing the code quality of the entire project is through a static code analysis tool. Use the tools (based on technology) such as <a href="http://www.sonarqube.org/">SonarQube</a>, <a href="http://www.ndepend.com/" target="_blank" rel="noopener">NDepend</a>, <a href="https://en.wikipedia.org/wiki/FxCop" target="_blank" rel="noopener">FxCop</a>, TFS code analysis rules. There is a myth that static code analysis tools are only for managers.</li>
 	<li>Use plug-ins such as <a href="https://www.jetbrains.com/resharper/" target="_blank" rel="noopener">Resharper</a>, which suggests the best practices in Visual studio.</li>
 	<li>To track the code review comments use the tools like <a href="https://www.atlassian.com/software/crucible/overview" target="_blank" rel="noopener">Crucible</a>, <a href="https://bitbucket.org/" target="_blank" rel="noopener">Bitbucket</a> and TFS code review process.</li>
</ol>
https://www.ibm.com/developerworks/rational/library/11-proven-practices-for-peer-review/
<h4>1. Review fewer than 400 lines of code at a time</h4>
<img class=" wp-image-1189 alignleft" style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5ab1bbd2e9bd7.png" alt="" width="241" height="158" />In practice, a review of 200-400 LOC over 60 to 90 minutes should yield 70-90% defect discovery. So, if 10 defects existed in the code, a properly conducted review would find between seven and nine of them.

</div>
</div>
&nbsp;

&nbsp;

</div>
</div>
</div>
</div>
2. Take your time. Inspection rates should under 500 LOC per hour
3. Do not review for more than 60 minutes at a time
<h4>4. Set goals and capture metrics</h4>
Using <a href="http://en.wikipedia.org/wiki/SMART_criteria" target="_blank" rel="noopener">SMART criteria</a>, start with external metrics. For example, "reduce support calls by 15%," or "cut the percentage of defects injected by development in half."  The most common internal metrics for code review are <em>inspection rate</em>, <em>defect rate</em>, and <em>defect density</em>. For best results, use a code review tool that gathers metrics <em>automatically</em> so that your critical metrics for process improvement are accurate.
<h4>5. Authors should annotate source code before the review</h4>
<h4>6. Use checklists</h4>
It´s very likely that each person on your team makes the same 10 mistakes over and over.

Free checklist https://smartbear.com/SmartBear/media/pdfs/best-kept-secrets-of-peer-code-review.pdf
<h4>7. Verify that the defects are actually fixed Establish a process for fixing defects found</h4>
The best way to ensure that defects are fixed is to use a collaborative <a href="https://smartbear.com/product/collaborator/overview/">code review tool</a> that allows reviewers to log bugs, discuss them with the author, and approve changes in the code.
<h2>8.Foster a good code review culture in which finding defects is viewed positively</h2>
<ul>
 	<li><strong>The point of software code review is to eliminate as many defects as possible, regardless of who "caused" the error.</strong></li>
 	<li>While it´s easy to see defects as purely negative, each bug is actually an opportunity for the team to improve code quality. Peer review also allows <a href="http://blog.smartbear.com/code-review/developing-a-culture-of-mentorship-with-code-review/">junior team members to learn from senior leaders</a> and for even the most experienced programmers to break bad habits.</li>
 	<li> Reports pulled from peer code reviews should never be used in performance reports. If personal metrics become a basis for compensation or promotion, developers will become hostile toward the process and naturally focus on improving personal metrics rather than writing better overall code.</li>
 	<li>
<h3 id="__RefHeading__107_174136755" class="ibm-h3">Beware of the Big Brother effect</h3>
<ul>
 	<li><strong>Metrics should never be used to single out developers, particularly in front of their peers. This practice can seriously damage morale.</strong></li>
 	<li>Metrics should be used to measure the efficiency of the process or the effect of a process change.</li>
 	<li>If metrics do help a manager uncover an issue, singling someone out is likely to cause more problems than it solves.</li>
 	<li>We recommend that managers deal with any issues by addressing the group as a whole, instead. It's best not to call a special meeting for this purpose, because developers might feel uneasy if it looks like there's a problem. Instead, just roll it into a weekly status meeting or other normal procedure.</li>
</ul>
</li>
</ul>
<h2>9. Embrace the subconscious implications of peer review</h2>
This <a href="http://smartbear.com/video-landing-page/jason-cohen-videos/ego-effect/">"Ego Effect"</a> naturally incentivizes developers to write cleaner code because their peers will certainly see it.

You'll be a better developer immediately because you want the general timbre of the "behind your back" conversations to be, "His stuff is pretty tight. He's a good developer;" not "He makes a lot of silly mistakes. When he says he's done, he's not."

Reviewing 20–33% of the code will probably give you maximal Ego Effect benefit with minimal time expenditure and reviewing 20% of your code is certainly better than reviewing none.
<h2>10. Practice lightweight code reviews</h2>
<strong>lightweight code review takes less than 20% the time of formal reviews and finds just as many bugs!</strong>
<h4>Checklist</h4>
https://www.evoketechnologies.com/blog/code-review-checklist-perform-effective-code-reviews/
<p id="TKEGDum"><img class="alignnone size-full wp-image-1190 " src="/wp-content/uploads/2018/03/img_5ab1c1a6bd8b2.png" alt="" /></p>
<a href="https://www.owasp.org/images/7/78/OWASP_AlphaRelease_CodeReviewGuide2.0.pdf">Security code review check list</a>

Sample Checklist Items
1. Documentation: All subroutines are commented in clear language.
2. Documentation: Describe what happens with corner-case
input.
3. Documentation: Complex algorithms are explained and justified.
4. Documentation: Code that depends on non-obvious behavior
in external libraries is documented with reference to external
documentation.
5. Documentation: Units of measurement are documented for
numeric values.
6. Documentation: Incomplete code is indicated with appropriate
distinctive markers (e.g. “TODO” or “FIXME”).
7. Documentation: User-facing documentation is updated (online
help, contextual help, tool-tips, version history).
8. Testing: Unit tests are added for new code paths or behaviors.
9. Testing: Unit tests cover errors and invalid parameter cases.
10. Testing: Unit tests demonstrate the algorithm is performing as
documented.
11. Testing: Possible null pointers always checked before use.
12. Testing: Array indexes checked to avoid out-of-bound errors.
13. Testing: Don’t write new code that is already implemented in
an existing, tested API.
14. Testing: New code fixes/implements the issue in question
15. Error Handling: Invalid parameter values are handled properly
early in the subroutine.
16. Error Handling: Error values of null pointers from subroutine
invocations are checked.
17. Error Handling: Error handlers clean up state and resources
no matter where an error occurs.
18. Error Handling: Memory is released, resources are closed, and
reference counters are managed under both error and nonerror
conditions.
19. Thread Safety: Global variables are protected by locks or
locking subroutines.
20. Thread Safety: Objects accessed by multiple threads are accessed
only through a lock.
21. Thread Safety: Locks must be acquired and released in the
right order to prevent deadlocks, even in error-handling code.
22. Performance: Objects are duplicated only when necessary.
23. Performance: No busy-wait loops instead of proper threadsynchronization
methods.
24. Performance: Memory usage is acceptable even with large
inputs.
25. Performance: Optimization that makes code harder to read
should only be implemented if a profiler or other tool has indicated
that the routine stands to gain from optimization.
These kinds of optimizations should be well-documented and
code that performs the same task simply should be preserved
somewhere.
