---
layout: post
title: Windows authentication & Impersonation -ASP.NET
date: 2018-03-20 14:48
author: tmasabari
comments: true
categories: [Impersonation, Security, Windows authentication]
---
&nbsp;
<h2><strong>Windows authentication &amp; authorization</strong></h2>
<u><a href="https://msdn.microsoft.com/en-us/library/ff647405.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/ff647405.aspx</a></u>

<u><a href="http://stackoverflow.com/questions/9443888/windows-authentication-vs-forms-authentication" target="_blank" rel="noopener">http://stackoverflow.com/questions/9443888/windows-authentication-vs-forms-authentication</a></u><strong> </strong>

<strong>Windows Authentication</strong> provider is the default authentication provider for ASP.NET applications. When a user using this authentication logs in to an application, the credentials are matched with the Windows domain through IIS.

There are 4 types of Windows Authentication methods:
<p style="padding-left: 30px;">1) Anonymous Authentication - IIS allows any user</p>
<p style="padding-left: 30px;">2) Basic Authentication - A windows username and password has to be sent across the network (in plain text format, hence not very secure).</p>
<p style="padding-left: 30px;">3) Digest Authentication - Same as Basic Authentication, but the credentials are encrypted. Works only on IE 5 or above</p>
<p style="padding-left: 30px;">4) Integrated Windows Authentication - Relies on Kerberos technology, with strong credential encryption</p>
<strong>Forms Authentication</strong> - This authentication relies on code written by a developer, where credentials are matched against a database. Credentials are entered on web forms, and are matched with the database table that contains the user information.

Windows

<strong>How does Windows Authentication work?</strong>

In this mode, User.Identity (as in HttpContext.Current.User.Identity) is populated by the underlying web server. This might be IIS Express, or full blown IIS.

Specifically, User.Identity is a WindowsIdentity object. E.g. the following cast will work:

WindowsIdentity clientId = (WindowsIdentity)HttpContext.Current.User.Identity;

<strong>How do I test if the Windows Authentication really works for my ASP.NET MVC 4 web site? In other words, how do I test it on my local development PC with local IIS (version 8), and on my company real web server with IIS version 7?</strong>

First, change the ASP.NET authorization to exclude the current user. E.g.
<pre class="EnlighterJSRAW" data-enlighter-language="null">&lt;system.web&gt;

&lt;authentication mode="Windows" /&gt;

&lt;authorization&gt;

&lt;allow users="yourdomainsomeotheruser" /&gt;

&lt;deny users="*" /&gt;

&lt;/authorization&gt;</pre>
&nbsp;

Second, enable Windows Authentication for your site using IIS Manager. It's under the 'Authentication' feature. <em>And</em> disable anonymous authentication.

Note that older explanation will suggest you make changes under element of your site's web.config. However, recent IIS implementations prevent this for security reasons.

Three, point your browser at the webpage. The browser should ask you to provide credentials, because the current user is not allowed access to the website. Provide the ones that are authorized for the site, and your MVC code should run.

Four, check the user identity. E.g.

WindowsIdentity clientId = (WindowsIdentity)HttpContext.Current.User.Identity;
<h2><strong>Forms Authentication Against AD</strong></h2>
<u><a href="http://www.schiffhauer.com/mvc-5-and-active-directory-authentication/" target="_blank" rel="noopener">http://www.schiffhauer.com/mvc-5-and-active-directory-authentication/</a></u> <u><a href="http://stackoverflow.com/questions/10279140/configure-asp-net-mvc-for-authentication-against-ad" target="_blank" rel="noopener">http://stackoverflow.com/questions/10279140/configure-asp-net-mvc-for-authentication-against-ad</a></u>

You can use the normal forms authentication to authenticate a user against an Active Directory, for that you just need you AD connection string:
<pre class="EnlighterJSRAW" data-enlighter-language="null">&lt;connectionStrings&gt;

&lt;add name="ADConn" connectionString="LDAP://YourConnection" /&gt;

&lt;/connectionStrings&gt;

and add the Membership Provider to use this connection:

&lt;membership defaultProvider="ADMembership"&gt;

&lt;providers&gt;

&lt;add name="ADMembership"

type="System.Web.Security.ActiveDirectoryMembershipProvider,

System.Web,

Version=2.0.0.0,

Culture=neutral,

PublicToken=b03f5f7f11d50a3a"

connectionStringName="ADConn"

connectionUsername="domain/user"

connectionPassword="pwd" /&gt;

&lt;/providers&gt;

&lt;/membership&gt;</pre>
&nbsp;

you will need to use <strong>username@domain</strong> to successfully authenticate the user.

<em>Here is something to get you start</em>
<ul>
 	<li><u><a href="http://helios.ca/2009/05/04/aspnet-mvc-forms-authentication-with-active-directory/" target="_blank" rel="noopener">http://helios.ca/2009/05/04/aspnet-mvc-forms-authentication-with-active-directory/</a></u></li>
</ul>
<h2><strong>Impersonation Setting up for IIS</strong></h2>
If you need to access resources by using the authenticated caller's identity or by using a specific Windows identity other than the process identity, you can configure your ASP.NET application to use impersonation. If you need to impersonate at the method level to perform specific operations or access particular resources, then you can use programmatic impersonation by using the <strong>WindowsIdentity.Impersonate</strong> method.
<h2><strong>Impersonation Scenarios</strong></h2>
The most common situations where you might require impersonation and delegation are:
<ul>
 	<li><strong>Impersonating the original caller.</strong> You want to access Windows resources that are protected with ACLs configured for your application's domain user accounts.</li>
 	<li><strong>Impersonating the original caller programmatically. </strong>You want to access resources predominantly by using the application's process identity, but specific methods need to use the original caller's identity.</li>
 	<li><strong>Impersonating a specific Windows identity.</strong> You need to use a specific identity or several Windows identities to access particular resources.</li>
 	<li><strong>Using delegation to access network resources by using an impersonated identity.</strong> You need to use an impersonated identity to access remote resources.</li>
</ul>
<h3><strong>Always Impersonating the Original Caller</strong></h3>
&lt;authentication mode="Windows" /&gt;

&lt;identity impersonate="true" /&gt;

// Stop impersonation on specific scenarios

WindowsImpersonationContext ctx = WindowsIdentity.Impersonate(IntPtr.Zero);

try

{

// Thread is now running under the process identity.

// Any resource access here uses the process identity.

}

finally

{

// Resume impersonation

ctx.Undo();

}
<h3><strong>Impersonating the Original Caller Temporarily</strong></h3>
<pre class="EnlighterJSRAW" data-enlighter-language="null">&lt;authentication mode="Windows" /&gt;

&lt;identity impersonate="false" /&gt;

using System.Security.Principal;

...

// Obtain the authenticated user's Identity

WindowsIdentity winId = (WindowsIdentity)HttpContext.Current.User.Identity;

WindowsImpersonationContext ctx = null;

try

{

// Start impersonating

ctx = winId.Impersonate();

// Now impersonating

// Access resources using the identity of the authenticated user

}

// Prevent exceptions from propagating

catch

{

}

finally

{

// Revert impersonation

if (ctx != null)

ctx.Undo();

}

// Back to running under the default ASP.NET process identity</pre>
&nbsp;

<strong>Impersonating a specific Windows identity on specific scenario.</strong>

WindowsIdentity wi = new WindowsIdentity(userName@fullyqualifieddomainName);

Just use above line in above example instead of // Obtain the authenticated user's Identity

This <strong>WindowsIdentity</strong> constructor relies on a Windows Server 2003 extension to the Kerberos protocol called Service for User to Self (S4U2Self).

The advantage of this approach is that you do not have to store credentials as you do for<strong>LogonUser</strong>. However, the disadvantage is that if your code needs to access local resources, you must grant the <strong>Act as part of the operating system</strong> privilege to your Web application process account to get an impersonation-level token.

<strong>To grant the Act as part of the operating system privilege</strong>
<ol>
 	<li>On the <strong>Start</strong> menu, click <strong>Control Panel</strong>.</li>
 	<li>Click <strong>Administrative Tools</strong>.</li>
 	<li>Click <strong>Local Security Policy</strong>.</li>
 	<li>Expand <strong>Local Policies</strong>, and then click <strong>User Rights Assignments</strong>.</li>
 	<li>In the right pane, right-click <strong>Act as part of the operating system</strong>, and then click <strong>Properties</strong>.</li>
 	<li>Click the <strong>Add User or Group</strong> button, then enter the account used to run your ASP.NET application (<strong>Network Service </strong>by default).</li>
</ol>
<strong>Note</strong>   This places your process within the trusted computing base (TCB) of the Web server, which <u>makes your Web server process very highly privileged. Where possible, you should avoid this approach</u> because an attacker who manages to inject code and compromise your Web application will have almost unrestricted capabilities on the local computer.

<strong>Impersonating a specific Windows identity throughout the application</strong>

&lt;identity impersonate="true" username="TestUser" password="P@ssw0rd" /&gt;

you can specify credentials on the &lt;<strong>identity</strong>&gt; element in your Web.config file. If you use this approach, you should encrypt the credentials. With ASP.NET version 2.0, you can use the Aspnet_regiis.exe tool. With ASP.NET version 1.1, you can use the Aspnet_setreg.exe tool.

<strong>To encrypt the </strong>&lt;<strong>identity</strong>&gt;<strong> element by using Aspnet_regiis</strong>
<ul>
 	<li>Run the following command to encrypt the &lt;<strong>identity</strong>&gt; element in the Web.config file.</li>
</ul>
<strong>aspnet_regiis -pef "system.web/identity" " C:SitesIntranetSite"</strong>

<strong>To decrypt the </strong>&lt;<strong>identity</strong>&gt;<strong> element</strong>
<ul>
 	<li>Run the following command to revert the &lt;<strong>identity</strong>&gt; element to plain text.</li>
</ul>
<strong>aspnet_regiis -pdf "system.web/identity" " C:/Sites/IntranetSite "</strong>
<h2><strong>IIS Authentication Types and Delegation Capability</strong></h2>
<table>
<tbody>
<tr>
<td>Authentication Type</td>
<td>Can Delegate</td>
<td>Notes</td>
</tr>
<tr>
<td>Anonymous</td>
<td>Depends</td>
<td>If the anonymous account (by default IUSR_MACHINE) is configured in IIS as a local account, it cannot be delegated unless the local (Web server) and remote computer have identical local accounts (with matching user names and passwords).
If the anonymous account is a domain account it can be delegated.</td>
</tr>
<tr>
<td>Basic</td>
<td>Yes</td>
<td>If Basic authentication is used with local accounts, it can be delegated if the local accounts on the local and remote computers are identical. Domain accounts can also be delegated.</td>
</tr>
<tr>
<td>Digest</td>
<td>No</td>
<td></td>
</tr>
<tr>
<td>Integrated Windows</td>
<td>Depends</td>
<td>Integrated Windows authentication either results in NTLM or Kerberos (depending upon the version of operating system on client and server computer).
NTLM does not support delegation.
Kerberos supports delegation with the appropriate Active Directory configuration.</td>
</tr>
<tr>
<td>Client Certificates</td>
<td>Depends</td>
<td>Can be delegated if used with IIS certificate mapping and the certificate is mapped to a local account that is duplicated on the remote computer or is mapped to a domain account. This works because the credentials for the mapped account are stored on the local server and are used to create an Interactive logon session (which has network credentials).
Active Directory certificate mapping does not support delegation.</td>
</tr>
</tbody>
</table>
<h2><strong>Kerberos Setting up for IIS</strong></h2>
<u><a href="https://msdn.microsoft.com/en-us/library/ff647404.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/ff647404.aspx</a></u>

<u><a href="https://technet.microsoft.com/library/cc758557(v=WS.10).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/library/cc758557(v=WS.10).aspx</a></u>

IIS uses the <u><a href="https://technet.microsoft.com/en-gb/library/cc778008(v=ws.10).aspx" target="_blank" rel="noopener">NTAuthenticationProviders Metabase Property</a></u> to pass the Negotiate header when Integrated Windows authentication is used to authenticate client requests. The Negotiate header permits clients to choose either Kerberos or NTLM. Negotiate uses Kerberos, unless Kerberos cannot be used by one of the systems involved in the authentication, or unless the calling application does not provide sufficient information to use Kerberos.

By default, Active Directory allows the Network Service and Local System accounts to use Kerberos. If <strong>NtAuthenticationProviders</strong> is set to <strong>Negotiate,NTLM</strong> for an application pool, Kerberos works correctly with Network Service as the worker process identity, because this is the default worker process identity for IIS 6.0 in worker process isolation mode. However, suppose you isolate applications on a Web site by configuring each application to run in a separate application pool under a separate process identity that is a domain account. If you attempt to use Integrated Windows authentication with the isolated applications, because you want to use Kerberos authentication, Kerberos fails.

Unless Kerberos authentication is configured correctly, it fails with a 401.1 error in the following situations:
<ul>
 	<li>The Fully Qualified Domain Name (FQDN) is different from the NetBIOS name. For example, the IIS server might host a Web site called www.contoso.com on a server named web01.</li>
 	<li>The process—for example, Dllhost.exe or W3wp.exe—that is performing the underlying authentication runs under an identity other than System, and no SPN is registered for that identity.</li>
 	<li>Applications are hosted across multiple servers that use the same computer name. Only one user can be registered per computer name.</li>
 	<li>If all servers in a Web farm use one computer name, but load balancing distributes requests to multiple servers, and no server in the Web farm has a unique SPN.</li>
</ul>
For Kerberos authentication to work correctly, you must configure isolation at the site level, not at the application pool level. All application pools in your Web site that use Kerberos must run with the same application pool process identity. You must then register that process identity as an SPN with Kerberos by using the Setspn.exe command-line tool. The Setspn.exe tool is included in Resource Kit Tools for Windows Server 2003 Deployment Kit companion CD, or on the Web at <u><a href="https://www.microsoft.com/reskit" target="_blank" rel="noopener">http://www.microsoft.com/reskit</a></u>. You must be a domain administrator to set an SPN. For more information about registering a service principal name by using Setspn.exe, see <u><a href="https://technet.microsoft.com/en-gb/library/cc786828(v=ws.10).aspx" target="_blank" rel="noopener">Configuring Constrained Delegation for Kerberos</a></u>.

&nbsp;
<h3>References How To</h3>
<ul>
 	<li><u><a href="http://msdn2.microsoft.com/en-us/library/ms998351.aspx" target="_blank" rel="noopener">How To: Use Impersonation and Delegation in ASP.NET 2.0</a></u></li>
 	<li><u><a href="http://wiki.asp.net/ControlPanel/How%20to%20implement%20impersonation%20in%20an%20ASP.NET%20application" target="_blank" rel="noopener">How to implement impersonation in an ASP.NET application</a></u></li>
 	<li><u><a href="http://msdn.microsoft.com/library/en-us/dnnetsec/html/SecNetHT05.asp" target="_blank" rel="noopener">How To: Implement Kerberos Delegation for Windows 2000</a></u></li>
 	<li><u><a href="http://msdn.microsoft.com/library/en-us/dnpag2/html/paght000024.asp" target="_blank" rel="noopener">How To: Use Protocol Transition and Constrained Delegation in ASP.NET 2.0</a></u></li>
 	<li><u><a href="http://aspalliance.com/articleViewer.aspx?aId=650&amp;pId=2" target="_blank" rel="noopener">CodeSnip: Impersonation in ThreadPool Worker Threads</a></u></li>
</ul>
<u><a href="https://msdn.microsoft.com/en-us/library/aa302415.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/aa302415.aspx</a></u>
