---
layout: post
title: .NET core - code analysis
date: 2018-11-14 15:39
author: tmasabari
comments: true
categories: [Uncategorized]
---
<!-- wp:paragraph -->
<p>

Apparently the right way to do this is to install the&nbsp;<a href="https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers">Microsoft.CodeAnalysis.FxCopAnalyzers</a>&nbsp;NuGet package. This works great, even on ASP.NET Core projects, and doesn't require the&nbsp;<code>&lt;RunCodeAnalysis&gt;</code>&nbsp;flag at all.

</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The flavor of Code Analysis (FxCopCmd.exe) isn't supported for .NET Core 2.0 because it's a legacy tool. The new tool to be used going forward for .NET Core 2.0 is FxCopAnalyzers.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://stackoverflow.com/questions/46617261/enabling-code-analysis-for-net-core-2-0-project-results-ca0055-and-ca0052-error">https://stackoverflow.com/questions/46617261/enabling-code-analysis-for-net-core-2-0-project-results-ca0055-and-ca0052-error</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This error is caused by using an old version of Code Analysis with .NET Core. This old version is only for non-.NET Core applications.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The solution is to disable the old Code Analysis for .NET Core projects and install the new version of Code Analysis, which is now a NuGet package. (The reason you probably want to disable the old Code Analysis tool for your project and NOT uninstall it is so that you can still use the old Code Analysis with old .NET applications, such as .NET 4.5.)</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Install the Code Analysis NuGet package in one of your projects in your solution:<code>Microsoft.CodeAnalysis.FxCopAnalyzers</code>Refer to&nbsp;<a href="https://github.com/dotnet/roslyn-analyzers#recommended-version-of-analyzer-packages">https://github.com/dotnet/roslyn-analyzers#recommended-version-of-analyzer-packages</a>&nbsp;to chose the right package version based upon your Visual Studio version.</li><li>Remove the&nbsp;<code>RunCodeAnalysis</code>&nbsp;element from your .csproj files (if it exists). This is done to disable the old legacy version of Code Analysis. The new version that you installed will still function.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Additional details are described here: <a href="https://github.com/dotnet/roslyn-analyzers/issues/1313">https://github.com/dotnet/roslyn-analyzers/issues/1313</a></p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>  &lt;PropertyGroup Condition="'$(Configuration)|$(TargetFramework)|$(Platform)' == 'Debug|net40|AnyCPU'">
    &lt;DebugType>full&lt;/DebugType>
    &lt;RunCodeAnalysis>true&lt;/RunCodeAnalysis>
    &lt;CodeAnalysisRuleSet>AllRules.ruleset&lt;/CodeAnalysisRuleSet>
  &lt;/PropertyGroup>
  &lt;PropertyGroup Condition="'$(Configuration)|$(TargetFramework)|$(Platform)' == 'Release|net40|AnyCPU'">
    &lt;DebugType>pdbonly&lt;/DebugType>
    &lt;RunCodeAnalysis>true&lt;/RunCodeAnalysis>
    &lt;CodeAnalysisRuleSet>AllRules.ruleset&lt;/CodeAnalysisRuleSet>
  &lt;/PropertyGroup>
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>The disadvantage to this is that it will not catch any code that is not .NET Framework compliant (i.e. #if !NET40).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Suppress warning</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://docs.microsoft.com/en-us/visualstudio/ide/how-to-suppress-compiler-warnings?view=vs-2017">https://docs.microsoft.com/en-us/visualstudio/ide/how-to-suppress-compiler-warnings?view=vs-2017</a></p>
<!-- /wp:paragraph -->
