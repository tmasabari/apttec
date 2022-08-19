---
layout: post
title: Federated Identities: OpenID Connect, SAML v2.0, and OAuth 2.0
date: 2018-08-06 20:16
author: tmasabari
comments: true
categories: [Security]
---
<ul>
 	<li>Single sign-on (SSO), a forerunner to identity federation, was an effective solution which could manage a single set of user credentials for applications and resources which existed within a single domain (enterprise network).</li>
 	<li>Organizations wanted to open APIs in their software so partners and independent developers could use them. Managing authentication and authorization for entities looking to consume these APIs was obviously a challenge.</li>
 	<li>Social media moved things even further. Various platforms spread far and wide on a plethora of devices, and many applications were built on top of those platforms. Now we have countless apps and services hooked into Twitter, Facebook, and LinkedIn.</li>
 	<li>The problem? How to bring together user login information across many applications and platforms to simplify sign-on and increase security. The solution? Federated identities…</li>
 	<li>Federated identities offered organizations the opportunity to preserve the benefits of SSO while extending the reach of a user’s credentials to include external resources which reduces costs and when implemented correctly, can increase security.</li>
</ul>
&nbsp;
<h2><strong>AT A GLANCE</strong></h2>
<h3><strong>Summary</strong></h3>
<ul>
 	<li>OIDC and OAuth 2.0 are protocols. They don't dictate which or how your federation will work. OAuth2 takes place at the authorization stage and OpenID Connect at authentication and federation phases. Any company can, with the public key exposed by OpenID Provider validate the ID Token and, therefore, be part of the Federation.</li>
 	<li>ADFS is as product that allows federation based on SAML protocol (secure but heavier than OIDC)</li>
</ul>
<ul>
 	<li style="list-style-type: none;">
<ul>
 	<li>SSO is a concept. One time authenticated in one domain, this authentication​ remains valid in others​ domains​. You can use a LDAP as user registry and its authentication generate an OIDC token. ADFS extends the LDAP for federation, but targeting Windows network, not applications.</li>
 	<li>Behind ADFS there is a LDAP, that can be thought as a database optimized for read operations.</li>
 	<li>ADSF is a Federated server that issues SAML assertions. There is a OAuth 2 profile to translate a SAML in a Access Token. Consequently, you can use ADSF to do the authentication of the resource owner, before the recording​ of the OIDC or OAuth permission.</li>
 	<li>ADFS 4.0 (Server 2016) is the only ADFS that has full OpenID Connect / OAuth support (i.e. all four profiles).</li>
 	<li>Only ADFS 4.0 can use LDAP v3.0 and above for authentication. On earlier versions you have to use AD.</li>
 	<li>Also SAML and WS-Fed normally use SAML tokens not JWT ones.</li>
 	<li>Just to point out, ADFS also supports WS-Federation.</li>
</ul>
</li>
</ul>
<ul>
 	<li>Claim based is used both in OIDC and SAML protocols. The tokens have information that the issuers claim to be correct about some entity. If you rely on token issued by a third part you became a relying party.</li>
</ul>
&nbsp;

&nbsp;
<h3><strong>Which protocol, when?</strong></h3>
So when should SAML be used, and when should OAuth 2.0 or OpenID Connect be used instead?
<ul>
 	<li>Mobile applications: no question–use OpenID Connect.</li>
 	<li>If the application already supports SAML: use SAML.</li>
 	<li>If you are writing a new application, use OpenID Connect–skate to where the puck is going!</li>
 	<li>If you need to protect API’s, or you need to create an API Gateway… that’s a topic for another blog. Short answer: use OAuth 2.0 or the <a href="https://www.gluu.org/resources/documents/standards/uma/">User Managed Access (“UMA”)</a> protocol.</li>
</ul>
&nbsp;

<strong>Current version</strong> OpenID Connect (2014) OAuth 2.0 SAML 2.0
<table>
<tbody>
<tr>
<td></td>
<td><strong>OAuth</strong></td>
<td><strong>OpenID Connect</strong></td>
<td><strong>SAML</strong></td>
</tr>
<tr>
<td><strong>Dates from</strong></td>
<td>2006</td>
<td>2005</td>
<td>2001</td>
</tr>
<tr>
<td><strong>Main purpose</strong></td>
<td>API authorization between applications</td>
<td>Single sign-on for consumers
+
Identity/Auth Services</td>
<td>Single sign-on for enterprise users</td>
</tr>
<tr>
<td><strong>Protocols</strong></td>
<td>JSON, HTTP</td>
<td>XRDS, HTTP, JSON</td>
<td>SAM, XML, HTTP, SOAP</td>
</tr>
<tr>
<td><strong>Current version</strong></td>
<td>OAuth 2.0</td>
<td>OpenID Connect</td>
<td>SAML 2.0</td>
</tr>
<tr>
<td>No. of related CVEs</td>
<td>3</td>
<td>24</td>
<td>17</td>
</tr>
</tbody>
</table>
&nbsp;
<table width="100%">
<tbody>
<tr>
<td></td>
<td><strong>OAuth2</strong></td>
<td><strong>OpenId</strong></td>
<td><strong>SAML</strong></td>
</tr>
<tr>
<td><strong>Token (or assertion) format</strong></td>
<td>JSON or SAML2</td>
<td>JSON</td>
<td>XML</td>
</tr>
<tr>
<td><strong>Authorization?</strong></td>
<td>Yes</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td><strong>Authentication?</strong></td>
<td>Pseudo-authentication</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td><strong>Year created</strong></td>
<td>2005</td>
<td>2006</td>
<td>2001</td>
</tr>
<tr>
<td><strong>Current version</strong></td>
<td>OAuth2</td>
<td>OpenID Connect</td>
<td>SAML 2.0</td>
</tr>
<tr>
<td><strong>Transport</strong></td>
<td>HTTP</td>
<td>HTTP GET and HTTP POST</td>
<td>HTTP Redirect (GET) binding, SAML SOAP binding, HTTP POST binding, and others</td>
</tr>
<tr>
<td><strong>Security Risks</strong></td>
<td>Phishing

OAuth 2.0 does not support signature, encryption, channel binding, or client verification.  Instead, it relies completely on TLS for confidentiality.</td>
<td>Phishing

Identity providers have a log of OpenID logins, making a compromised account a bigger privacy breach</td>
<td><a href="https://www.usenix.org/system/files/conference/usenixsecurity12/sec12-final91.pdf">XML Signature Wrapping</a> to impersonate any user</td>
</tr>
<tr>
<td><strong>Best suited for</strong></td>
<td>API authorization</td>
<td>Single sign-on for consumer apps</td>
<td>Single sign-on for enterprise

Note:  not well suited for mobile</td>
</tr>
</tbody>
</table>
&nbsp;
<h2><strong>OPENID CONNECT</strong></h2>
OpenID is an open standard sponsored by Facebook, Microsoft, Google, PayPal, Ping Identity, Symantec, and Yahoo.

OpenID Connect allows users to employ a <strong>single set of credentials</strong>, managed by a preferred 3rd party OpenID Connect identity provider (IDP) such as Google, Microsoft, and PayPal, to <strong>authenticate with numerous online services and websites that accept the OpenID authentication scheme.</strong>
<ul>
 	<li>OpenID Connect has been built on top of the OAuth 2.0 protocol and employs REST/JSON for messaging.</li>
 	<li>For developers, OpenID allows developers to authenticate users without creating and maintaining a local authentication system.</li>
 	<li>Instead, developers can rely on the expertise of an organization committed to the secure implementation of an identity protocol capable of ensuring identities they manage are authentic and to the best of their abilities, authentic.</li>
</ul>
The OpenID Connect protocol, launched in February of 2014, can be used
<ul>
 	<li>across numerous platforms including mobile</li>
 	<li>in addition to a varied array of clients such as JavaScript to produce confirmable identity assertions. (Source: http://openid.net/connect/faq/)</li>
</ul>
The OpenID Connect specification defines three roles:
<ul>
 	<li>The end user or the entity that is looking to verify its identity</li>
 	<li>The relying party (RP), which is the entity looking to verify the identity of the end user</li>
 	<li>The OpenID Connect provider (OP), which is the entity that registers the OpenID URL and can verify the end user’s identity</li>
</ul>
<h2><strong>SAML V2.0</strong></h2>
Security Assertion Markup Language (SAML) is an XML-based open standard for exchanging authentication and authorization data between parties. SAML was launched in 2001 and is managed by the OASIS Security Services Technical Committee.

The SAML specification defines three roles,
<ul>
 	<li>The principal, which is typically the user looking to verify his or her identity</li>
 	<li>The identity provider (idP), which is the entity that is capable of verifying the identity of the end user</li>
 	<li>The service provider (SP), which is the entity looking to use the identity provider to verify the identity of the end user</li>
</ul>
<h2><strong>OAUTH 2.0</strong></h2>
OAuth2 is also the basis for OpenID Connect, which provides OpenID (authentication) on top of OAuth2 (authorization) for a more complete security solution. OpenID Connect (OIDC) was created in early 2014. This primer will instead focus on OAuth2 by itself, not as a part of OIDC.

Yet Twitter’s <a href="https://dev.twitter.com/oauth/overview/faq">OAuth guide</a> says that OAuth2 is an authentication standard. So what gives? As it turns out, authorization can be used as a form of pseudo-authentication.

&nbsp;

OAuth 2.0 is an open standard launched in 2006 focusing exclusively on authorization, differentiating itself from OpenID and SAML which were created for the purposes of authentication.

The OAuth 2.0 specifications define the following roles,
<ul>
 	<li>The end user or the entity that owns the resource in question</li>
 	<li>The resource server (OAuth Provider), which is the entity hosting the resource</li>
 	<li>The client (OAuth Consumer), which is the entity that is looking to consume the resource after getting authorization from the client</li>
</ul>
&nbsp;

OpenId VS OAuth

https://security.stackexchange.com/questions/44611/difference-between-oauth-openid-and-openid-connect-in-very-simple-term/130411#130411

<a href="http://en.wikipedia.org/wiki/OpenID">OpenID</a> is a protocol for <strong>authentication</strong> while <a href="http://en.wikipedia.org/wiki/OAuth">OAuth</a> is for <strong>authorization</strong>. Authentication is about making sure that the guy you are talking to is indeed who he claims to be. Authorization is about deciding what that guy should be allowed to do.

In OpenID, authentication is delegated: server A wants to authenticate user U, but U's credentials (e.g. U's name and password) are sent to another server, B, that A trusts (at least, trusts for authenticating users). Indeed, server B makes sure that U is indeed U, and then tells to A: "ok, that's the genuine U".

In OAuth, authorization is delegated: entity A obtains from entity B an "access right" which A can show to server S to be granted access; B can thus deliver temporary, specific access keys to A without giving them too much power. You can imagine an OAuth server as the key master in a big hotel; he gives to employees keys which open the doors of the rooms that they are supposed to enter, but each key is limited (it does not give access to all rooms); furthermore, the keys self-destruct after a few hours.

To some extent, authorization can be abused into some pseudo-authentication, on the basis that if entity A obtains from B an access key through OAuth, and shows it to server S, then server S may <em>infer</em> that B authenticated A before granting the access key. So some people use OAuth where they should be using OpenID. <a href="http://en.wikipedia.org/wiki/OpenID#OpenID_vs._pseudo-authentication_using_OAuth">This schema</a> may or may not be enlightening; but I think this pseudo-authentication is more confusing than anything. <a href="http://openid.net/connect/">OpenID Connect</a> does just that: it abuses OAuth into an authentication protocol. In the hotel analogy: if I encounter a purported employee and that person shows me that he has a key which opens my room, then I <em>suppose</em> that this is a true employee, on the basis that the key master would not have given him a key which opens my room if he was not.

References
<ul>
 	<li>https://spin.atomicobject.com/2016/05/30/openid-oauth-saml/</li>
 	<li>https://www.softwaresecured.com/federated-identities-openid-vs-saml-vs-oauth/</li>
 	<li>https://www.softwaresecured.com/differentiating-federated-identities-openid-connect-saml-v2-0-and-oauth-2-0/</li>
 	<li>https://www.gluu.org/resources/documents/articles/oauth-vs-saml-vs-openid-connect/</li>
</ul>
