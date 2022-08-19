---
layout: post
title: Authentications ASP.NET legacy / IIS
date: 2018-03-21 22:13
author: tmasabari
comments: true
categories: [Interview Preparation, Security]
---
<img src="https://www.codeproject.com/KB/aspnet/ASPDOTNETauthentication/1.jpg" />
<p id="bGsErqb"><img class="alignnone size-full wp-image-1225 " src="/wp-content/uploads/2018/03/img_5ab2856c463d1.png" alt="" /></p>
<img src="https://www.codeproject.com/KB/aspnet/ASPDOTNETauthentication/2.jpg" />
<p id="kSXzmHF"><img class="alignnone size-full wp-image-1226 " src="/wp-content/uploads/2018/03/img_5ab2858670ab7.png" alt="" /></p>
GenericPrincipal and GenericIdentity objects represent users who have been authenticated using Forms authentication or other custom authentication mechanisms. With these objects, the role list is obtained in a custom manner, typically from a database.
FormsIdentity and PassportIdentity objects represent users who have been authenticated with Forms and Passport authentication respectively.

&nbsp;
<h2><a name="Types of authentication and authorization in ASP.NET"></a>Types of authentication and authorization in IIS</h2>
There are three ways of doing authentication and authorization in ASP.NET:-
• <strong>Windows authentication: -</strong> In this methodology ASP.NET web pages will use local windows users and groups to authenticate and authorize resources.

•<strong> Forms Authentication: -</strong> This is a cookie based authentication where username and password are stored on client machines as cookie files or they are sent through URL for every request. Form-based authentication presents the user with an HTML-based Web page that prompts the user for credentials.

<strong>• Passport authentication :- </strong>Passport authentication is based on the <strong>passport website provided</strong>
<strong>by the Microsoft</strong> .So when user logins with credentials it will be reached to the passport website ( i.e. hotmail,devhood,windows live etc) where authentication will happen. <strong>If Authentication is successful it will return a token to your website. </strong>

• <strong>Anonymous access: -</strong> If you do not want any kind of authentication then you will go for Anonymous access.

&nbsp;

There are three different way of passing the windows username and password to IIS:-
• Basic
• Digest
• Windows
In the coming session we will understand in depth what these 3 options are.
<ul>
 	<li>When basic authentication is selected the ‘userid’ and ‘password’ are passed by using Base64 encoded format . i.e. why the name is basic authentication. ‘Base64’ is a encoding and not encryption. So it’s very easy to crack. You can read more about ‘Base64’ encoding at http://en.wikipedia.org/wiki/Base64 . Its a very weak form of protection.</li>
 	<li>The problem associated with basic authentication is solved by using digest authentication. Digest authentication transfers data over wire as MD5 hash or message digest. This hash or digest is difficult to dechiper. one of the big problems of digest authentication is it’s not supported on some browsers.</li>
 	<li>Integrated Windows authentication (formerly called NTLM, and also known as Windows NT Challenge/Response authentication) uses either Kerberos v5 authentication or NTLM authentication, depending upon the client and server configuration.
<ul>
 	<li>NTLM is a challenge response authentication protocol. Below is how the sequence of events happens:-
• Client sends the username and password to the server.
• Server sends a challenge.
• Client responds to the challenge with 24 byte result.
• Servers checks if the response is properly computed by contacting the domain controller.
• If everything is proper it grants the request.</li>
 	<li>
<p id="UcliGjp"><img class="alignnone wp-image-1227 " src="/wp-content/uploads/2018/03/img_5ab2874257639.png" alt="" width="493" height="399" /></p>
</li>
 	<li>Kerberos is a multi-hounded (3 heads) who guards the gates of hades. In the same way Kerberos security has 3 participants authenticating service, service server and ticket granting server.Kerberos uses symmetric key for authentication and authorization. Below is how the things work for Kerberos:-• In step 1 client sends the username and password to AS (Authenticating service).
• AS authenticates the user and ensures that he is an authenticated user.
• AS then asks the TGT (Ticket granting service) to create a ticket for the user.
• This ticket will be used to verify if the user is authenticated or not. In other words in further client interaction no password will be sent during interaction.
<p id="bpFzyUG"><img class="alignnone wp-image-1228 " src="/wp-content/uploads/2018/03/img_5ab2877674166.png" alt="" width="342" height="246" /></p>
</li>
 	<li>
<p id="jvSFpQd"><img class="alignnone wp-image-1229 " src="/wp-content/uploads/2018/03/img_5ab287ee90d05.png" alt="" width="374" height="282" /></p>
</li>
</ul>
</li>
</ul>
<h2><a name="Order of Precedence"></a>Order of Precedence</h2>
In order words the precedence is:-

1. Windows NT challenge ( Integrated security)
2. Digest
3. Basic

• Browser makes a request; it sends the first request as Anonymous. In other words it does not send any credentials.

• If the server does not accept Anonymous IIS responds with an "Access Denied" error message and sends a list of the authentication types that are supported by the browser.

• If Windows NT Challenge/Response is the only one supported method then the browser must support this method to communicate with the server. Otherwise, it cannot negotiate with the server and the user receives an "Access Denied" error message.

• If Basic is the only supported method, then a dialog box appears in the browser to get the credentials, and then passes these credentials to the server. It attempts to send these credentials up to three times. If these all fail, the browser is not connected to the server.

• If both Basic and Windows NT Challenge/Response are supported, the browser determines which method is used. If the browser supports Windows NT Challenge/Response, it uses this method and does not fall back to Basic. If Windows NT Challenge/Response is not supported, the browser uses Basic.
You can read more about precedence from <a href="http://support.microsoft.com/kb/264921">http://support.microsoft.com/kb/264921</a>.

&nbsp;

&nbsp;
<table border="1" width="67%">
<tbody>
<tr>
<td></td>
<td><strong>Browse support</strong></td>
<td><strong>Authentication mechanism</strong></td>
</tr>
<tr>
<td><strong>Basic</strong></td>
<td>Almost all browsers</td>
<td>Weak uses Base64.</td>
</tr>
<tr>
<td><strong>Digest</strong></td>
<td> IE 5 and later version</td>
<td>Strong MD5</td>
</tr>
<tr>
<td><strong>Integrated windows</strong></td>
<td colspan="2"></td>
</tr>
<tr>
<td>
<p align="center"><strong>• Kerberos</strong></p>
</td>
<td> IE5 and above</td>
<td> Ticket encryption using AD , TGT and KDC</td>
</tr>
<tr>
<td>
<p align="center"><strong>• Challenge / response</strong></p>
</td>
<td>IE5 and above</td>
<td>Send a challenge</td>
</tr>
</tbody>
</table>
&nbsp;
<h2><a name="Forms Authentication"></a>Forms Authentication</h2>
Forms authentication is a cookie/URL based authentication where username and password are stored on client machines as cookie files or they are sent encrypted on the URL for every request if cookies are not supported.
<p id="RKrtRdg"><img class="alignnone wp-image-1230 " src="/wp-content/uploads/2018/03/img_5ab28971808b7.png" alt="" width="296" height="298" /></p>
Membership

• Creation of user and roles tables.
• Code level implementation for maintaining those tables.
• User interface for userid and password.
<h2><a name="Forms Authentication using Single Sign on"></a>Forms Authentication using Single Sign on</h2>
Many time we would like to implement single sign on across multiple sites. This can be done using forms authentication. You can implement forms authentication in <strong>both the websites with same machine key.</strong> Once the validation is done in one website a cookie text file will be created. When that user goes to the other website the same cookie file will used to ensure that the user is proper or not.
<img class="alignnone size-full wp-image-1231 " src="/wp-content/uploads/2018/03/img_5ab28a74c8527.png" alt="" />

&nbsp;

References
<ul>
 	<li>https://www.codeproject.com/Articles/98950/ASP-NET-authentication-and-authorization</li>
 	<li>Single sign on in sub domain <a href="https://www.codeproject.com/KB/aspnet/SingleSignon.aspx">SingleSignon.aspx</a></li>
 	<li>Great reference on different authentication mechanism<a href="http://msdn.microsoft.com/en-us/library/ee817643.aspx"> http://msdn.microsoft.com/en-us/library/ee817643.aspx</a></li>
 	<li>MSDN article which explains how to do forms authentication <a href="http://support.microsoft.com/kb/301240">http://support.microsoft.com/kb/301240</a></li>
 	<li>MSND article which explains identity and principal objects <a href="http://msdn.microsoft.com/en-us/library/ftx85f8x(v=VS.85).aspx">http://msdn.microsoft.com/en-us/library/ftx85f8x(v=VS.85).aspx</a></li>
 	<li>Patterns and practices page which provides a table that illustrate range of IIS authentication settings. <a href="http://msdn.microsoft.com/en-us/library/ff649264.aspx">http://msdn.microsoft.com/en-us/library/ff649264.aspx</a></li>
 	<li>Order of precedence for Windows authentication, basic authentication and digest authentication <a href="http://support.microsoft.com/kb/264921">http://support.microsoft.com/kb/264921</a></li>
 	<li>Nice article on Forms authentication which goes in depth <a href="http://www.4guysfromrolla.com/webtech/110701-1.shtml">http://www.4guysfromrolla.com/webtech/110701-1.shtml</a></li>
 	<li>Forms authentication explained with nice sequence diagrams <a href="http://www.asp.net/security/tutorials/an-overview-of-forms-authentication-vb">http://www.asp.net/security/tutorials/an-overview-of-forms-authentication-vb</a></li>
 	<li>Nice PDF of best practices for forms authentication <a href="http://www.foundstone.com/us/resources/whitepapers/aspnetformsauthentication.pdf">http://www.foundstone.com/us/resources/whitepapers/aspnetformsauthentication.pdf</a></li>
</ul>
&nbsp;
