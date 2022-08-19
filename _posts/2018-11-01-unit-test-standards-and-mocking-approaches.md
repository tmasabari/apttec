---
layout: post
title: Xunit test standards and Nsubstitute approaches
date: 2018-11-01 21:08
author: tmasabari
comments: true
categories: [mock, Nsubstitute, Unit Test, Unit Test]
---
<!-- wp:heading -->
<h2>Naming conventions</h2>
<p>MethodName_Expectedbehaviour_conditions</p>
<p><a href="https://dzone.com/articles/7-popular-unit-test-naming">https://dzone.com/articles/7-popular-unit-test-naming</a></p>
<h2>Parameterized unit test</h2>
<p><a href="https://andrewlock.net/creating-parameterised-tests-in-xunit-with-inlinedata-classdata-and-memberdata/">https://andrewlock.net/creating-parameterised-tests-in-xunit-with-inlinedata-classdata-and-memberdata/</a></p>
<p>xUnit uses the <code>[Fact]</code> attribute to denote a parameterless unit test, which tests invariants in your code.</p>
<p>In contrast, the <code>[Theory]</code> attribute denotes a parameterised test that is true for a subset of data. That data can be supplied in a number of ways, but the most common is with an <code>[InlineData]</code> attribute.</p>
<pre class="language-csharp"><code class="language-csharp"><span class="token punctuation">[</span><span class="token class-name">Theory</span><span class="token punctuation">]</span>
<span class="token punctuation">[</span><span class="token class-name">InlineData</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
<span class="token punctuation">[</span><span class="token class-name">InlineData</span><span class="token punctuation">(</span><span class="token operator">-</span><span class="token number">4</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">6</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">10</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
<span class="token punctuation">[</span><span class="token class-name">InlineData</span><span class="token punctuation">(</span><span class="token keyword">int</span><span class="token punctuation">.</span>MinValue<span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MaxValue<span class="token punctuation">)</span><span class="token punctuation">]</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">CanAddTheory</span><span class="token punctuation">(</span><span class="token keyword">int</span> value1<span class="token punctuation">,</span> <span class="token keyword">int</span> value2<span class="token punctuation">,</span> <span class="token keyword">int</span> expected<span class="token punctuation">)</span></code></pre>
<p>&nbsp;</p>
<p>If the values you need to pass to your <code>[Theory]</code> test aren't constants, then you can use an alternative attribute, <code>[ClassData]</code>, to provide the parameters. This attribute takes a <code>Type</code> which xUnit will use to obtain the data:</p>
<pre class="language-csharp"><code class="language-csharp"><span class="token punctuation">[</span><span class="token class-name">Theory</span><span class="token punctuation">]</span>
<span class="token punctuation">[</span><span class="token class-name">ClassData</span><span class="token punctuation">(</span><span class="token keyword">typeof</span><span class="token punctuation">(</span>CalculatorTestData<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">CanAddTheoryClassData</span><span class="token punctuation">(</span><span class="token keyword">int</span> value1<span class="token punctuation">,</span> <span class="token keyword">int</span> value2<span class="token punctuation">,</span> <span class="token keyword">int</span> expected<span class="token punctuation">)</span></code></pre>
<pre class="language-csharp"><code class="language-csharp"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">CalculatorTestData</span> <span class="token punctuation">:</span> <span class="token class-name">IEnumerable</span><span class="token operator">&lt;</span><span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span>
<span class="token punctuation">{</span>
    <span class="token keyword">public</span> IEnumerator<span class="token operator">&lt;</span><span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span> <span class="token function">GetEnumerator</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
    <span class="token punctuation">{</span>
        <span class="token keyword">yield</span> <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
        <span class="token keyword">yield</span> <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token operator">-</span><span class="token number">4</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">6</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">10</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
        <span class="token keyword">yield</span> <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token operator">-</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">0</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
        <span class="token keyword">yield</span> <span class="token keyword">return</span> <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MinValue<span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MaxValue <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token class-name">IEnumerator</span> IEnumerable<span class="token punctuation">.</span><span class="token function">GetEnumerator</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">GetEnumerator</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}<br /></span></code></pre>
<p>&nbsp;</p>
<p>The <code>[MemberData]</code> attribute can be used to fetch data for a <code>[Theory]</code> from a <code>static</code> property or method of a type. This attribute has quite a lot options, </p>
<p>The <code>[MemberData]</code> attribute can load data from an <code>IEnnumerable&lt;object[]&gt;</code> property on the test class. </p>
<pre class="language-csharp"><code class="language-csharp">    <span class="token punctuation">[</span><span class="token class-name">Theory</span><span class="token punctuation">]</span>
    <span class="token punctuation">[</span><span class="token class-name">MemberData</span><span class="token punctuation">(</span><span class="token function">nameof</span><span class="token punctuation">(</span>Data<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">CanAddTheoryMemberDataProperty</span><span class="token punctuation">(</span><span class="token keyword">int</span> value1<span class="token punctuation">,</span> <span class="token keyword">int</span> value2<span class="token punctuation">,</span> <span class="token keyword">int</span> expected<span class="token punctuation">)</span></code><br /><br /></pre>
<pre class="language-csharp"><code class="language-csharp">    <span class="token keyword">public</span> <span class="token keyword">static</span> IEnumerable<span class="token operator">&lt;</span><span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span> Data <span class="token operator">=</span><span class="token operator">&gt;</span>
        <span class="token keyword">new</span> <span class="token class-name">List</span><span class="token operator">&lt;</span><span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span>
        <span class="token punctuation">{</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token operator">-</span><span class="token number">4</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">6</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">10</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token operator">-</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">0</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MinValue<span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MaxValue <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token punctuation">}</span><span class="token punctuation">;</span></code></pre>
<pre class="language-csharp"><code class="language-csharp">    <span class="token keyword">public</span> <span class="token keyword">static</span> IEnumerable<span class="token operator">&lt;</span><span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span> <span class="token function">GetData</span><span class="token punctuation">(</span><span class="token keyword">int</span> numTests<span class="token punctuation">)</span>
    <span class="token punctuation">{</span>
        <span class="token keyword">var</span> allData <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">List</span><span class="token operator">&lt;</span><span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token operator">&gt;</span>
        <span class="token punctuation">{</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">3</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token operator">-</span><span class="token number">4</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">6</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">10</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token operator">-</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">0</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token keyword">new</span> <span class="token keyword">object</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MinValue<span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token keyword">int</span><span class="token punctuation">.</span>MaxValue <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token punctuation">}</span><span class="token punctuation">;</span>

        <span class="token keyword">return</span> allData<span class="token punctuation">.</span><span class="token function">Take</span><span class="token punctuation">(</span>numTests<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span></code></pre>
<h2 class="language-csharp"><br /><br />Throw exceptions</h2>
<p class="language-csharp"><a href="http://nsubstitute.github.io/help/callbacks">Callbacks</a> can be used to throw exceptions when a member is called.</p>
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="code">
<div class="container">
<div class="line number1 index0 alt2"><code class="csharp comments">//For non-voids:</code></div>
<div class="line number2 index1 alt1"><code class="csharp plain">calculator.Add(-1, -1).Returns(x =&gt; { </code><code class="csharp keyword">throw</code> <code class="csharp keyword">new</code> <code class="csharp plain">Exception(); });</code></div>
<div class="line number3 index2 alt2"> </div>
<div class="line number4 index3 alt1"><code class="csharp comments">//For voids and non-voids:</code></div>
<div class="line number5 index4 alt2"><code class="csharp plain">calculator</code></div>
<div class="line number6 index5 alt1"><code class="csharp spaces">    </code><code class="csharp plain">.When(x =&gt; x.Add(-2, -2))</code></div>
<div class="line number7 index6 alt2"><code class="csharp spaces">    </code><code class="csharp plain">.Do(x =&gt; { </code><code class="csharp keyword">throw</code> <code class="csharp keyword">new</code> <code class="csharp plain">Exception(); });</code></div>
</div>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>Assert received method calls, properties, indexer, event subscriptions, event invocation</h2>
<p><a href="http://nsubstitute.github.io/help/received-calls/">http://nsubstitute.github.io/help/received-calls/</a></p>
<div class="line number1 index0 alt2"><code class="csharp plain">var command = Substitute.For&lt;ICommand&gt;();</code></div>
<div> </div>
<div class="line number4 index3 alt1"><code class="csharp comments">//Check received with second arg of 2 and any first arg:</code></div>
<div class="line number5 index4 alt2"><code class="csharp plain">calculator.Received().Add(Arg.Any&lt;</code><code class="csharp keyword">int</code><code class="csharp plain">&gt;(), 2);</code></div>
<div> </div>
<div> </div>
<div> </div>
<div>
<div class="line number8 index7 alt1"><code class="csharp comments">//Check did not receive a call where second arg is &gt;= 500 and any first arg:</code></div>
<div class="line number9 index8 alt2"><code class="csharp plain">calculator</code></div>
<div class="line number10 index9 alt1"><code class="csharp plain">.DidNotReceive()</code></div>
<div class="line number11 index10 alt2"><code class="csharp plain">.Add(Arg.Any&lt;</code><code class="csharp keyword">int</code><code class="csharp plain">&gt;(), Arg.Is&lt;</code><code class="csharp keyword">int</code><code class="csharp plain">&gt;(x =&gt; x &gt;= 500));</code></div>
<div> </div>
</div>
<div>//Number of times</div>
<div><code class="csharp plain">command.Received(3).Execute(); </code><code class="csharp comments">// &lt;&lt; This will fail if 2 or 4 calls were received</code></div>
<div> </div>
<div>//ignore arguments</div>
<div>calculator.ReceivedWithAnyArgs().Add(1,1);</div>
<div> </div>
<div>
<div>Check for strings and other data</div>
<div><a href="https://www.clearlyagileinc.com/agile-blog/using-nsubstitute-to-check-if-method-called-with-particular-object">https://www.clearlyagileinc.com/agile-blog/using-nsubstitute-to-check-if-method-called-with-particular-object</a></div>
</div>
<div> </div>
<div>
<h2>Logger</h2>
<p><a href="https://stackoverflow.com/questions/39604198/how-to-test-asp-net-core-built-in-ilogger">https://stackoverflow.com/questions/39604198/how-to-test-asp-net-core-built-in-ilogger</a></p>
<p><a href="https://ardalis.com/testing-logging-in-aspnet-core">https://ardalis.com/testing-logging-in-aspnet-core</a></p>
</div>
<p>Can't mock an LogError extension method. What you <em>should</em> mock, is <a href="https://github.com/aspnet/Logging/blob/dev/src/Microsoft.Extensions.Logging.Abstractions/ILogger.cs#L22" rel="noreferrer">the <code>ILogger.Log</code> method</a>, which <a href="https://github.com/aspnet/Logging/blob/dev/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs#L280" rel="noreferrer"><code>LogError</code> calls into</a>. It makes the verification code a bit clunky, but it should work</p>
<div>
<p>public static class MockExtensions<br />{<br />/// &lt;summary&gt;<br />/// Checks the given logger received a message which contains given 'ExpectedLogMessage'<br />/// Throws exception in case given log message is not received<br />//https://stackoverflow.com/questions/39604198/how-to-test-asp-net-core-built-in-ilogger<br />//https://www.clearlyagileinc.com/agile-blog/using-nsubstitute-to-check-if-method-called-with-particular-object<br />//If LogInformation() has not been received NSubstitute will throw a ReceivedCallsException <br />//and let you know what call was expected and with which arguments, as well as <br />//listing actual calls to that method and which the arguments differed.<br />//Log&lt;Object&gt;(Information, 0, *Xml File or XML folder Path is not Specified in command line arguments or configuration file.*, &lt;null&gt;, Func&lt;Object, Exception, String&gt;)<br />/// &lt;/summary&gt;<br />/// &lt;typeparam name="T"&gt;&lt;/typeparam&gt;<br />/// &lt;param name="logger"&gt;&lt;/param&gt;<br />/// &lt;param name="ExpectedLogLevel"&gt;&lt;/param&gt;<br />/// &lt;param name="LogExpected"&gt;&lt;/param&gt;<br />/// &lt;param name="args"&gt;&lt;/param&gt;<br />public static void AssertLog&lt;T&gt;(this ILogger&lt;T&gt; logger,<br />LogLevel ExpectedLogLevel, string ExpectedLogMessage, params object[] args)<br />{<br /><strong>logger.Received().Log(logLevel: ExpectedLogLevel, eventId: Arg.Any&lt;EventId&gt;()</strong><br /><strong>, state: Arg.Is&lt;FormattedLogValues&gt;(data =&gt;</strong><br /><strong>data.ToString().Contains( string.Format(ExpectedLogMessage, args) ))</strong><br /><strong>, exception: Arg.Any&lt;Exception&gt;(), formatter: Arg.Any&lt;Func&lt;Object, Exception, String&gt;&gt;());</strong><br />}</p>
<p>}</p>
</div>
<div> </div>
<div> </div>
<h2>HTTP / API mocking</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>I find the unit testing approach as broadly practiced to be way too granular and it's not obvious that the strategy of mocking and faking and tickling every method and property singly yields higher coverage for the code you care about.</li>
<li>What we in our team generally aim for internally is not to wedge ourselves into parts of the framework our team doesn't own (we don't use the source code of HttpWebRequest, we use what you use) but rather create an environment in the small that can give us the answers we're looking for to achieve maximum coverage during build-verification testing.</li>
<li>That means that if we need one, we'll have a mock HTTP service that can run on every developer box (self-hosted in the same process, even) and spews out the right set of errors and we run that as we execute the unit tests.</li>
</ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Database mocking</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>If tests have a dependency on a database we'll have a little local one that's just capable enough and prepopulated for predictable results in order to exercise the scenario.</li>
</ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li><a href="http://rtigger.com/blog/2013/02/19/testing-without-interfaces">http://rtigger.com/blog/2013/02/19/testing-without-interfaces</a></li>
</ul>
<!-- /wp:list -->
