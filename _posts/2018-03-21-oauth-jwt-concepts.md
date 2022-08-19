---
layout: post
title: OAuth, JWT concepts
date: 2018-03-21 12:11
author: tmasabari
comments: true
categories: [JWT, OAuth, Security, Todo]
---
<h2 id="aspnet-identity" class="heading-with-anchor">OAuth</h2>
<ol>
 	<li>Imp todo <a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki">https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki</a></li>
 	<li><a href="https://developer.salesforce.com/page/Using_OAuth_to_Authorize_External_Applications">https://developer.salesforce.com/page/Using_OAuth_to_Authorize_External_Applications</a></li>
</ol>
<ul>
 	<li>
<p class="lf-text-block lf-block" data-lf-anchor-id="dbb668d31401b863b32ec71b4d044e7a:0"><a class="external text" href="http://oauth.net/" rel="nofollow">OAuth</a> (Open Authorization) is <i>an open protocol to allow secure API authorization in a simple and standardized way from desktop and web applications</i>.</p>
</li>
 	<li>OAuth 2.0 is the industry-standard protocol for authorization. OAuth 2.0 supersedes the work done on the original OAuth protocol created in 2006.</li>
 	<li>OAuth 2.0 focuses on client developer simplicity while <strong>providing specific authorization flows for web applications, desktop applications, mobile phones, and living room devices</strong>.</li>
 	<li>This specification and its extensions are being developed within the <a href="https://www.ietf.org/mailman/listinfo/oauth">IETF OAuth Working Group</a>.</li>
 	<li>A large and ever-growing number of websites support OAuth including Google, Twitter, SmugMug, Yahoo!, Evernote and OpenSocial.</li>
 	<li><strong>VS OpenID</strong>
<ul>
 	<li>Don't confuse OAuth with OpenID. The two protocols do vaguely similar things but serve totally differently purposes.</li>
 	<li>While OAuth is used for authorization, OpenID is used for authentication.</li>
 	<li>To authorize a consumer with OAuth you will still need to log into your service provider. OAuth doesn't care how you authenticate against the provider, just that you do.</li>
</ul>
</li>
</ul>
<strong>Need</strong>
<ul>
 	<li>OAuth is all about <strong>sharing</strong>. The OAuth protocol enables a website (the consumer) to access protected resources from another web service (the service provider) through an API.</li>
 	<li>For your end users the major benefit of OAuth is <strong>security</strong>.</li>
 	<li>Users gain the added security of not having to hand out their credentials to yet another website, while developers no longer need to store or maintain credentials in their code, database or memory.</li>
 	<li>The benefit of OAuth is that the API does not require users to disclose their provider credentials to consumers, and they can revoke the consumer's access to the service provider at any time.</li>
 	<li>Restricted access instead of exact credentials (username &amp; password)</li>
 	<li>The <a class="external text" href="http://tools.ietf.org/html/rfc6749" rel="nofollow">OAuth 2.0 RFC</a> uses the example of a photo sharing website (for example, Flickr) as the resource server and a printing service (for example, Snapfish) as the client. You <strong>might authorize the printing service (client) for read-only access to some subset of your photos for a limited period of time, after which the authorization becomes invalid.</strong> You can even instruct the authorization server to revoke an access token if you decide you no longer wish the client to have access and don't trust it to discontinue on its own.

&nbsp;</li>
 	<li>Contrast this with giving your credentials (username and password) to a client app so it can access a resource server on your behalf, <strong>effectively impersonating you directly.</strong> That application now has <strong>exactly the same access as you have, to all of your data.</strong></li>
 	<li>Worse, <strong>if you decide you no longer trust the client app, your only recourse is to change your password at the resource server <i>and</i> at all the similar client apps</strong> you wish to continue using - a major inconvenience!</li>
</ul>
<ul>
 	<li>To enable users to log in using <a class="" href="http://oauth.net/2/" data-linktype="external">OAuth 2.0</a> with credentials from an <strong>external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google</strong>.</li>
</ul>
<ul>
 	<li><strong>Pros of 3rd Party authentication:</strong>
<ul>
 	<li>No code for users to signup or reset their password.</li>
 	<li>No code to send an email with a validation link and then validate the address.</li>
 	<li>Users do not need to learn/write-down another username and password.</li>
</ul>
</li>
 	<li><strong>Cons of 3rd Party authentication:</strong>
<ul>
 	<li>You depend on the third party in order for your users to use your service. If their service goes down or they discontinue it then you need to figure something else out. Eg: how do you migrate the user's account data if their identity changes from "foo@a.com" to "bar@b.com"?</li>
 	<li>Usually you have to write code for each provider. eg Google, Facebook, Twitter.</li>
 	<li>You or your users might have privacy concerns. The providers know which of their users use your service.</li>
 	<li>You are trusting the provider. It is possible for a provider to issue tokens that are valid for one user to someone else. This could be for lawful purposes or not.</li>
</ul>
</li>
 	<li>
<h4><a href="https://www.ibuildings.nl/blog/2013/07/secure-your-rest-api-oauth2-implicit-grant">Controversies</a></h4>
</li>
 	<li><strong>Not a protocol, it's a framework to make protocols</strong></li>
 	<li><strong>Relies on proper SSL / TLS implementation in clients TLS <a href="http://www.theregister.co.uk/2011/04/11/state_of_ssl_analysis/">is hardly perfect</a>.</strong></li>
 	<li><strong>Don't use OAuth2 on Native mobile clients</strong></li>
 	<li><strong>Your access token may not actually come from the Authenticator</strong>

There is <strong>nothing stopping a user from copy-and-pasting an access token from another application / client into your application</strong>. So while the server is still correct in the user that's authenticated, there is a mismatch between who the server thinks it's talking to and who it's actually talking to. Example: I grant access to Facebook to use my Twitter, then I am redirected back to Facebook with an <strong>Access Token</strong> in the URL. I can then take this access token, and hand it to OAT. Now Twitter will think Facebook is requesting the data, when in fact OAT is. In practice this probably won't be an issue unless you're using client specific code (a code smell in its self) or relying on the '<strong>scope</strong>' feature too much (hint: don't!). The scope feature allows you to give a specific client access to only a specific part of your API. For instance if you have a website that always has a scope 'all' and an admin environment where you can have a scope 'editor' or 'all'. The scope 'editor'  would allow the user to only place tweets, the scope 'all' might also allow the user to block tweets. Simply copying the <strong>Access Token</strong> from the website to the admin environment would grant the user extra rights! A simple solution would be to, in the client, <strong>check the Client ID of the access token received with the Authentication Server.</strong> However I would generally advise to <strong>not abuse 'scope' for authorization or write client specific code</strong>, in which case this is a non-issue.</li>
</ul>
<div class="panel-heading">
<h3 class="panel-title">Quick refresher - OAuth 2.0 terminology</h3>
</div>
<div class="panel-body">
<ul>
 	<li><strong>Resource Owner</strong>: the entity that can grant access to a protected resource. Typically this is the end-user.</li>
 	<li><strong>Application</strong>: an application requesting access to a protected resource on behalf of the Resource Owner.</li>
 	<li><strong>Resource Server</strong>: the server hosting the protected resources. This is the API you want to access.</li>
 	<li><strong>Authorization Server</strong>: the server that authenticates the Resource Owner, and issues Access Tokens after getting proper authorization. In this case, Auth0.</li>
 	<li><strong>User Agent</strong>: the agent used by the Resource Owner to interact with the Application, for example a browser or a native application.</li>
</ul>
</div>
<h3>Authentication flows:</h3>
<ul>
 	<li><a href="https://www.ibuildings.nl/blog/2013/07/secure-your-rest-api-oauth2-implicit-grant">Sample flow</a></li>
</ul>
&nbsp;

<img class="alignnone size-full wp-image-1522 " src="/wp-content/uploads/2018/04/img_5ae07638260ed.png" alt="" />

&nbsp;
<ol>
 	<li><b><a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki#Obtaining_an_Access_Token_in_a_Web_Application_.28Web_Server_Flow.29">Web Server</a></b> - users can authorize your web application to access their data, as described with Flickr and print services. This is the OAuth 2.0 <strong><a class="external text" href="http://tools.ietf.org/html/rfc6749#section-4.1" rel="nofollow"><i>authorization code</i></a> grant type</strong>.</li>
 	<li><b><a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki#Obtaining_an_Access_Token_in_a_Browser_or_Native_Application_.28User-Agent_Flow.29">User-Agent</a></b> - users can authorize your desktop or mobile application to access their data, leveraging an external or embedded browser (or <i>user-agent</i>) for authentication - the <strong>OAuth 2.0 <a class="external text" href="http://tools.ietf.org/html/rfc6749#section-4.2" rel="nofollow"><i>implicit</i></a> grant type</strong>.</li>
 	<li><b><a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki#Obtaining_an_Access_Token_using_a_JWT_Bearer_Token">JWT Bearer Token Flow</a></b> - your app can re-use an existing authorization by supplying a signed <a class="external text" href="http://tools.ietf.org/html/draft-ietf-oauth-json-web-token" rel="nofollow">JSON Web Token</a> (JWT) as described in <a class="external text" href="http://tools.ietf.org/html/draft-ietf-oauth-jwt-bearer" rel="nofollow">JSON Web Token (JWT) Profile for OAuth 2.0 Client Authentication and Authorization Grants</a>.</li>
 	<li><b><a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki#Obtaining_an_Access_Token_using_a_SAML_Bearer_Assertion">SAML Bearer Assertion Flow</a></b> - your app can also re-use an existing authorization by supplying a signed <a class="external text" href="http://en.wikipedia.org/wiki/SAML_2.0" rel="nofollow">SAML 2.0</a>Assertion, as specified in the <a class="external text" href="http://tools.ietf.org/html/draft-ietf-oauth-saml2-bearer" rel="nofollow">SAML 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants</a>.</li>
 	<li><b><a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki#Obtaining_an_Access_Token_using_a_Web_SSO_SAML_Assertion">SAML Assertion Flow</a></b> - your app can federate with the API using a SAML Assertion, in much the same way as you would configure federation with Salesforce for Web single sign-on.</li>
 	<li><b><a href="https://developer.salesforce.com/page//index.php%3Ftitle%3DDigging_Deeper_into_OAuth_2.0_on_Force.com%26oldid%3D50717Wiki#Obtaining_a_Token_in_an_Autonomous_Client_.28Username_and_Password_Flow.29">Username and Password</a></b> - your application can authenticate directly to Force.com using an 'API user's credentials - the OAuth 2.0 <a class="external text" href="http://tools.ietf.org/html/rfc6749#section-4.3" rel="nofollow"><i>resource owner password credentials</i></a> grant type.</li>
</ol>
<h2></h2>
https://auth0.com/docs/api-auth/which-oauth-flow-to-use

http://www.bubblecode.net/en/2016/01/22/understanding-oauth2/

OAuth 2.0 supports several different <strong>grants</strong>. By grants we mean ways of retrieving an Access Token. Deciding which one is suited for your case depends mostly on your Application's type, but other parameters weigh in as well, like the level of trust for the Application, or the experience you want your users to have.<img class="size-full wp-image-1520 aligncenter" src="/wp-content/uploads/2018/04/img_5ae07477ec106.png" alt="" />
<ol>
 	<li><span id="Client_Credentials_Grant">Client Credentials Grant
This type of authorization is used when the client is himself the resource owner. Here, the end-user does not have to give its authorization for accessing the resource server.</span>
<p id="iMSQsTP"><img class="alignnone size-full wp-image-1526 " src="/wp-content/uploads/2018/04/img_5ae07ce0e8591.png" alt="" /></p>
</li>
 	<li><img class="size-full wp-image-1523 aligncenter" src="/wp-content/uploads/2018/04/img_5ae078ba5c0f2.png" alt="" /></li>
 	<li>
<p id="XYEYIGi"><img class="alignnone size-full wp-image-1525 " src="/wp-content/uploads/2018/04/img_5ae07ccb657ba.png" alt="" /></p>
<p id="TNYWtlD"><img class="alignnone size-full wp-image-1524 " src="/wp-content/uploads/2018/04/img_5ae07ca3d5332.png" alt="" /></p>
</li>
</ol>
<strong>The Third-Party Application: "Client"- </strong>The client is the application that is attempting to get access to the user's account. It needs to get permission from the user before it can do so.

<strong>The API: "Resource Server" </strong>The resource server is the API server used to access the user's information.

<strong>The Authorization Server- </strong>This is the server that presents the interface where the user approves or denies the request. In smaller implementations, this <strong>may be the same server as the API server</strong>, but larger scale deployments will often build this as a separate component.

<strong>The User: "Resource Owner"</strong> The resource owner is the person who is giving access to some portion of their account.
<p id="creating-an-app">Creating an App</p>
Before you can begin the OAuth process, you must first register a new app with the service. When registering a new app, you usually register basic information such as application name, website, a logo, etc. In addition, you must register a redirect URI to be used for redirecting users to for web server, browser-based, or mobile apps.

Redirect URIs

The service will only redirect users to a registered URI, which helps prevent some attacks. Any HTTP redirect URIs must be protected with TLS security, so the service will only redirect to URIs beginning with "https". This prevents tokens from being intercepted during the authorization process. Native apps may register a redirect URI with a custom URL scheme for the application, which may look like <code>demoapp://redirect</code>.

Client ID and Secret

After registering your app, you will receive a client ID and a client secret. The client ID is considered public information, and is used to build login URLs, or included in Javascript source code on a page. The client secret <strong>must</strong> be kept confidential. If a deployed app cannot keep the secret confidential, such as single-page Javascript apps or native apps, then the secret is not used, and ideally the service shouldn't issue a secret to these types of apps in the first place.

&nbsp;

WEB API Authentication
<ul>
 	<li>Web API assumes that authentication happens in the host.</li>
 	<li>For web-hosting, the host is IIS, which uses HTTP modules for authentication.</li>
 	<li>When the host authenticates the user, it creates a <em>principal</em>, which is an <a href="https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx" data-linktype="external">IPrincipal</a> object that represents the security context under which code is running. The host attaches the principal to the current thread by setting <strong>Thread.CurrentPrincipal</strong>. The principal contains an associated <strong>Identity</strong> object that contains information about the user. If the user is authenticated, the <strong>Identity.IsAuthenticated</strong> property returns <strong>true</strong>. For anonymous requests, <strong>IsAuthenticated</strong> returns <strong>false</strong>.</li>
 	<li>For more information about principals, see <a href="https://msdn.microsoft.com/library/shz8h065.aspx" data-linktype="external">Role-Based Security</a>.</li>
</ul>
<h2><span id="Best_Practices" class="mw-headline">Best Practices for SalesForce</span></h2>
Here are some best practices when building applications that use OAuth:
<ul>
 	<li><strong>Access tokens do not expire</strong> and are useful <strong>until they are revoked by the user.</strong>
<ul>
 	<li>Keep the access token and access secret<strong> in a database and use it for subsequent calls</strong> to create a new Force.com session.</li>
 	<li>Treat your access token and token secret as if they are actual credentials. You should consider <strong>encrypting</strong> them in your database.</li>
</ul>
</li>
 	<li>Name your Remote Access Application the same as your web application to avoid confusion when users authorize it.</li>
 	<li>When testing, use multiple browsers and ensure that you are logged out of all orgs. It is very easy to authorize the wrong user if you have multiple accounts.</li>
 	<li>Use the Firefox plugin <a class="external text" href="https://addons.mozilla.org/en-US/firefox/addon/3829" rel="nofollow">Live HTTP Headers</a> during testing to view the packets being passed back and forth to Force.com. This will make debugging your application much easier.</li>
 	<li>You may want to consider cloning existing users profiles and locking down access to objects not needed by the consumer application.</li>
 	<li>Use a test server if developing your own OAuth client. You can find a list of testing servers at the bottom of <a class="external text" href="http://wiki.oauth.net/ServiceProviders" rel="nofollow">this page</a>. I found <a class="external text" href="http://googlecodesamples.com/oauth_playground/" rel="nofollow">Google's OAuth Playground</a> and <a class="external text" href="http://term.ie/oauth/example/" rel="nofollow">Termie's OAuth Echo Server</a> the easiest to use.</li>
 	<li>Double check the package access controls or security settings for the profiles accessing Force.com via OAuth to ensure they don't have access to unauthorized data.</li>
</ul>
&nbsp;
<h2>OAuth Token</h2>
<h3></h3>
<p id="mqcOKYU"><a style="font-size: 1rem;" href="https://stackoverflow.com/questions/1626575/best-practices-around-generating-oauth-tokens">https://stackoverflow.com/questions/1626575/best-practices-around-generating-oauth-tokens</a></p>
OAuth says nothing about token except that it has a secret associated with it. So all the schemes you mentioned would work. Our token evolved as the sites get bigger. Here are the versions we used before,
<ol>
 	<li>Our first token is an encrypted BLOB with username, token secret and expiration etc. The problem is that we can't revoke tokens without any record on host.</li>
 	<li>So we changed it to store everything in database and the token is simply an random number used as the key to the database. It has an username index so it's easy to list all the tokens for an user and revoke it.</li>
 	<li>We get quite few hacking activities. With random number, we have to go to database to know if the token is valid. So we went back to encrypted BLOB again. This time, the token only contains encrypted value of the key and expiration. So we can detect invalid or expired tokens without going to the database.</li>
</ol>
Some implementation details that may help you,
<ol>
 	<li>Add a version in the token so you can change token format without breaking existing ones. All our token has first byte as version.</li>
 	<li>Use URL-safe version of Base64 to encode the BLOB so you don't have to deal with the URL-encoding issues, which makes debugging more difficult with OAuth signature, because you may see triple encoded basestring.</li>
</ol>
<ul>
 	<li><strong>OAuth token</strong>
<ul>
 	<li>Often people think "<strong>OAuth token</strong>" <em>always</em> implies an opaque token that is granted by a OAuth token dispensary, that can then <strong>be validated only by that same OAuth dispensary system</strong>.</li>
 	<li>Today, the OAuthV2/GenerateAccessToken policy in Apigee Edge generates opaque tokens. It returns a token of <strong>32 seemingly random characters</strong>, and the holder has no idea what the token signifies. Therefore, we call it "<strong>opaque</strong>".</li>
 	<li>To USE the token, the holder must present it back to the token dispensary, because the original dispensary is the only party that can relate the opaque string to meaningful information. You can think of an opaque token as a pointer to information that is held only by the token dispensary.</li>
</ul>
</li>
</ul>
<h3>Session Id/Opaque Vs JWT</h3>
<ul>
 	<li><a href="https://auth0.com/blog/cookies-vs-tokens-definitive-guide/">https://auth0.com/blog/angularjs-authentication-with-cookies-vs-token/</a></li>
 	<li>https://softwareengineering.stackexchange.com/questions/298973/rest-api-security-stored-token-vs-jwt-vs-oauth</li>
</ul>
<p id="QoRGRVP"><img class="alignnone size-full wp-image-1202 " src="/wp-content/uploads/2018/03/img_5ab1f0882f867.png" alt="" /></p>

<table style="width: 782px;">
<tbody>
<tr>
<td style="width: 125px;"></td>
<td style="width: 231.917px;">Cookie based</td>
<td style="width: 385.083px;">JWT Token based</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Cross-domain / CORS</strong></td>
<td style="width: 231.917px;">Cookies work well with singular domains and sub-domains. Don't play well for CORS</td>
<td style="width: 385.083px;">allows you to make AJAX calls to any server, on any domain because you use an HTTP header to transmit the user information.</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Stateless (a.k.a. Server side scalability)</strong></td>
<td style="width: 231.917px;"><strong>stateful</strong>. This means that an authentication record or session must be kept both server and client-side.</td>
<td style="width: 385.083px;">no need to keep a session store, the token is a self-contanined entity that conveys all the user information</td>
</tr>
<tr>
<td style="width: 125px;"><strong>CDN</strong></td>
<td style="width: 231.917px;">Session Id needs to be generated from Server. So a server call is required.</td>
<td style="width: 385.083px;">you can serve all the assets of your app from a CDN (e.g. javascript, HTML, images, etc.), and your server side is just the API</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Performance</strong></td>
<td style="width: 231.917px;">Every HTTP request requires a lookup to the data store <span style="font-family: inherit; font-size: inherit;">RDBMS DB or a NoSQL  DB </span>

If there are multiple front end HTTP servers data store becomes a single point of failure and it can become a bottleneck</td>
<td style="width: 385.083px;">network roundtrip (e.g. finding a session on database) is likely to take more time than calculating an <a href="http://en.wikipedia.org/wiki/Hash-based_message_authentication_code" target="_blank" rel="noopener"><code>HMACSHA256</code></a> to validate a token and parsing its contents.
since you can store additional data inside the JWT, such as the users permission level, you can save yourself additional lookup calls to get and process the requested data.In order to revoke a JWT before it expires you need to use a revocation list. This gets you back to the server side storage issues you were trying to avoid.</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Standard-based</strong></td>
<td style="width: 231.917px;"></td>
<td style="width: 385.083px;">JWT s a standard and there are multiple backend libraries (<a href="https://www.nuget.org/packages?q=JWT" target="_blank" rel="noopener">.NET</a>, <a href="http://rubygems.org/search?utf8=%E2%9C%93&amp;query=jwt" target="_blank" rel="noopener">Ruby</a>, <a href="https://code.google.com/p/jsontoken/" target="_blank" rel="noopener">Java</a>, <a href="https://github.com/davedoesdev/python-jwt" target="_blank" rel="noopener">Python</a>, <a href="https://github.com/firebase/php-jwt" target="_blank" rel="noopener">PHP</a>) and companies backing their infrastructure (e.g. <a href="https://www.firebase.com/docs/security/custom-login.html" target="_blank" rel="noopener">Firebase</a>, <a href="https://developers.google.com/accounts/docs/OAuth2ServiceAccount#overview" target="_blank" rel="noopener">Google</a>, <a href="https://github.com/MSOpenTech/AzureAD-Node-Sample/wiki/Windows-Azure-Active-Directory-Graph-API-Access-Using-OAuth-2.0" target="_blank" rel="noopener">Microsoft</a>)</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Data</strong></td>
<td style="width: 231.917px;">simply store the session id in a cookie</td>
<td style="width: 385.083px;">JWT can contain any type of data such as the<strong> user id</strong> and <strong>expiration of the token</strong>, who issued the token, <strong>scopes or permissions</strong> for the user etc</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Mobile Ready -</strong>Modern APIs need to serve both different clients</td>
<td style="width: 231.917px;">Native mobile platforms and cookies do not mix well. IoT applications don't have concept of session</td>
<td style="width: 385.083px;">Tokens on the other hand are much easier to implement on both iOS and Android. Tokens are also easier to implement for Internet of Things applications and services that do not have a concept of a cookie store</td>
</tr>
<tr>
<td style="width: 125px;"><strong>Security</strong></td>
<td style="width: 231.917px;"></td>
<td style="width: 385.083px;">The data stored in the JWT is readable by the client.

Anyone who gets a copy of the signing key can create JWTs.</td>
</tr>
</tbody>
</table>
<h2>JWT</h2>
<ul>
 	<li>JWT is a type of Token, and OAuth is a Framework that describes how to dispense tokens.</li>
 	<li>Most common practice is to use JWT as an OAuth Bearer token.</li>
 	<li>But <strong>opaque toen </strong>is not the only kind of OAuth token. JWT is just a different kind of OAuth token.</li>
 	<li>JWT, in contrast are not opaque.
<ul>
 	<li>The JWT is not a "pointer" or reference to information. It actually contains lots of information, that can be extracted and interpreted by any party that has the token.</li>
 	<li>Because the JWT contains real information, a JWT can be large; 300 bytes or more, depending on the claims contained within it.</li>
 	<li>When people say "<strong>JWT are self-validating</strong>" what they mean is, any holder of the JWT can open it, validate it, and then make authorization decisions based on the claims presented in it. Validating the JWT means: verifying its structure, decoding the base64 encoding, verifying the key is correct, verifying the signature, then verifying the required claims are present in the token, checking the expiry.</li>
</ul>
</li>
 	<li>JSON Web Token (JWT) is an open standard (<a href="https://tools.ietf.org/html/rfc7519">RFC 7519</a>) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the <strong>HMAC</strong>algorithm) or a public/private key pair using <strong>RSA</strong>.</li>
 	<li>To secure our ASP.NET Core application, we are going to rely on JWTs (JSON Web Tokens). JSON Web Token (JWT) is an <a href="https://tools.ietf.org/html/rfc7519" target="_blank" rel="noopener">open standard</a> that defines a compact and <strong>self-contained way for securely transmitting information between parties as a JSON object</strong>.</li>
 	<li>The technology is becoming a<strong> de facto standard for securing microservices and backends for mobile applications and for SPA (Single Page Applications)</strong>. Using JWTs to authenticate requests makes easier to create stateless applications and therefore to scale this applications horizontally. <a href="https://auth0.com/docs/jwt" target="_blank" rel="noopener">If you want to learn more about JWTs, take a look at this resource</a>.</li>
 	<li>This is a stateless authentication mechanism as the <strong>user state is never saved in server memory</strong>.</li>
 	<li><a href="https://www.quora.com/How-do-I-crack-and-Tamper-JWT-requests">Tampering:</a> JWT tokens are signed using, depending on server configuration, RSA-SHA2 or HMAC-SHA2, both of which rely on SHA2. At the time of writing, SHA2 has excellent collision resistance, and combined with RSA/HMAC layer it is almost impossible to change the JWT content and end up with exactly that same signature</li>
</ul>
<h4>Use Cases</h4>
<table style="width: 785px;">
<tbody>
<tr style="height: 27px;">
<td style="width: 498.729px; height: 27px;">JWT</td>
<td style="width: 259.271px; height: 27px;">Opaque token</td>
</tr>
<tr style="height: 108.66px;">
<td style="width: 498.729px; height: 108.66px;">
<ul>
 	<li>Federation is desired. For example, you want to use Azure AD as the token issuer, and then use Apigee Edge as the token validator. With JWT, an app can authenticate to Azure AD, receive a token, and then present that token to Apigee Edge to be verified. (Same works with Google Sign-In. Or Paypal. Or <a href="http://salesforce.com/" target="_blank" rel="noopener">Salesforce.com</a>. etc)</li>
</ul>
</td>
<td style="width: 259.271px; height: 108.66px;">
<ul>
 	<li>There is no federation. The issuer of the token is the same party that validates the token. All API requests bearing the token will go through the token dispensary.</li>
</ul>
</td>
</tr>
<tr style="height: 332px;">
<td style="width: 498.729px; height: 332px;">
<ul>
 	<li>Asynchrony is required. For example, you want the client to send in a request, and then store that request somewhere, to be acted on by a separate system "later". That separate system will not have a synchronous connection to the client, and it may not have a direct connection to a central token dispensary. a JWT can be read by the asynchronous processing system to determine whether the work item can and should be fulfilled at that later time. This is, in a way, related to the Federation idea above. Be careful here, though: JWT expire. If the queue holding the work item does not get processed within the lifetime of the JWT, then the claims should no longer be trusted.</li>
</ul>
</td>
<td style="width: 259.271px; height: 332px;">
<ul>
 	<li>There is no need or desire to allow the holder of the token to examine the claims within the token.</li>
 	<li>When you wish to unilaterally allow token revocation. It is not possible to revoke JWT. They expire when they are marked to expire at creation time.</li>
</ul>
</td>
</tr>
</tbody>
</table>
<h3>Tokens Are Signed, Not Encrypted</h3>
<ul>
 	<li>A JSON Web Token is comprised of three parts: the <strong>header, payload, and signature</strong>. The format of a JWT is <code>header.payload.signature</code>.  Sample payload :
<pre class="EnlighterJSRAW" data-enlighter-language="null">{
  "sub": "1234567890",
  "name": "Ado Kukic",
  "admin": true
}</pre>
</li>
 	<li>The <strong>very</strong> important thing to note here, is that, this token is signed by the HMACSHA256 algorithm, and the header and payload are Base64URL encoded, it is <strong>not</strong> encrypted. Therefore, it should go without saying that <strong>sensitive data, such as passwords, should never be stored in the payload</strong></li>
 	<li></li>
</ul>
<h3 id="how-do-json-web-tokens-work-" class="anchor-heading">How do JSON Web Tokens work?</h3>
<p style="font-size: 16px;"><img class="wp-image-1201 alignleft" src="/wp-content/uploads/2018/03/img_5ab1e937970b5.png" alt="" width="391" height="219" /></p>

<ul>
 	<li>In authentication, when the user successfully logs in using their credentials, a JSON Web Token will be returned and must be saved locally (typically in local storage, but cookies can be also used), instead of the traditional approach of creating a session in the server and returning a cookie.</li>
</ul>
<div class="alert alert-warning alert-with-icon">

&nbsp;
<div class="alert-content">
<blockquote>
<ul>
 	<li>You <strong>must</strong> <a href="https://auth0.com/docs/tokens/id-token#verify-the-signature">verify a JWT's signature</a> before storing and using it.</li>
</ul>
</blockquote>
</div>
</div>
<ul>
 	<li>Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the <strong>Authorization</strong> header using the <strong>Bearer</strong> schema. The content of the header should look like the following: <code>Authorization: Bearer &lt;token&gt; </code></li>
</ul>
&nbsp;
<ul>
 	<li> The server's protected routes will check for a valid JWT in the Authorization header, and if it's present, the user will be allowed to access protected resources. As JWTs are self-contained, all the necessary information is there, reducing the need to query the database multiple times.</li>
 	<li>This allows you to fully rely on data APIs that are stateless and even make requests to downstream services. It doesn't matter which domains are serving your APIs, so Cross-Origin Resource Sharing (CORS) won't be an issue as it doesn't use cookies.</li>
</ul>
&nbsp;
