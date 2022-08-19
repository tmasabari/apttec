---
layout: post
title: Authentication flows in OAuth2 and OpenID Connect
date: 2018-08-06 21:18
author: tmasabari
comments: true
categories: [OAuth, Security]
---
OpenIddict is an OAuth2/OpenID Connect server. As such, it implements all the classical core flows defined by these two specifications.

Here's a quick table to help you:
<table style="height: 196px;">
<thead>
<tr style="height: 56px;">
<th style="height: 56px;">Flow/grant</th>
<th style="height: 56px;">Requires user interaction?</th>
<th style="height: 56px;">For server-side apps?</th>
<th style="height: 56px;">For public apps (JS/mobile)?</th>
<th style="height: 56px;">For third-party apps?</th>
</tr>
</thead>
<tbody>
<tr style="height: 56px;">
<td style="height: 56px;"><strong>ROPC- Resource owner password credentials</strong></td>
<td style="height: 56px;"><strong>No</strong></td>
<td style="height: 56px;">Yes</td>
<td style="height: 56px;">Yes</td>
<td style="height: 56px;">No</td>
</tr>
<tr style="height: 28px;">
<td style="height: 28px;"><strong>Client credentials</strong></td>
<td style="height: 28px;"><strong>No</strong></td>
<td style="height: 28px;">Yes</td>
<td style="height: 28px;">No</td>
<td style="height: 28px;">Yes</td>
</tr>
<tr style="height: 28px;">
<td style="height: 28px;">Authorization code</td>
<td style="height: 28px;">Yes</td>
<td style="height: 28px;">Yes</td>
<td style="height: 28px;">Yes</td>
<td style="height: 28px;">Yes</td>
</tr>
<tr style="height: 28px;">
<td style="height: 28px;">Implicit</td>
<td style="height: 28px;">Yes</td>
<td style="height: 28px;">No</td>
<td style="height: 28px;">Yes</td>
<td style="height: 28px;">Yes</td>
</tr>
</tbody>
</table>
As you figured out, each flow has a different use case:

<strong>1. The resource owner password credentials grant</strong> is the <strong>simplest</strong> OAuth2 flow:<img src="https://kevinchalet.com/2016/07/13/creating-your-own-openid-connect-server-with-asos-choosing-the-right-flows/resource-owner-password-flow.png" />
<ul>
 	<li>the client application sends a token request with the username and the password of the user and it gets back an access token.</li>
 	<li>This flow is sometimes considered as a "<strong>legacy</strong>" flow and <strong>you SHOULD NEVER use it with third-party applications</strong> you don't manage yourself (because it's the only flow where the client knows the user credentials).</li>
 	<li>It is is particularly appreciated by SPA writers as it's trivial to implement in vanilla JavaScript,</li>
 	<li>doesn't involve any redirection or consent form and,</li>
 	<li>unlike interactive flows, doesn't require implementing token validation or cross-site request forgery (XSRF) countermeasures to prevent session fixation attacks.</li>
 	<li><strong>far less vulnerable than a client using interactive flows without implementing the appropriate security checks</strong></li>
</ul>
<strong>2. The client credentials grant</strong>
<ul>
 	<li>is used when a headless client application needs to access its own resources. No user is involved in this flow, which is basically a <strong><strong><strong>server-to-server scenario.</strong></strong></strong></li>
</ul>
&nbsp;
<p id="JCUzEfp"><img class="alignnone size-full wp-image-1665 " src="/wp-content/uploads/2018/08/img_5b686d6f6fdee.png" alt="" /></p>

<ul>
 	<li>This means that <strong>you CAN'T use the client credentials grant with public applications</strong> like JS, mobile or desktop applications, as they are <strong>not able to keep their credentials secret</strong>.</li>
</ul>
<h3 id="Authorization-code-flow">3. Authorization code flow</h3>
&nbsp;
<p id="mEjzzps"><img class="size-full wp-image-1669 aligncenter" src="/wp-content/uploads/2018/08/img_5b698ff72c339.png" alt="" /></p>
&nbsp;
<ul>
 	<li>is the most complex OAuth2/OpenID Connect flow that uses redirections and allows creating consent pages where the user can decide whether he wants to grant an access to the client application without ever sharing his credentials with the app.</li>
 	<li>There are basically 2 steps in the authorization code flow:
<ol>
 	<li>the authorization request/response and</li>
 	<li>the token request/response.</li>
</ol>
</li>
 	<li><strong>Step 1: the authorization request</strong></li>
 	<li>In this flow, the client application always initiates the authentication process by generating an authorization request including the mandatory <code>response_type=code</code> parameter, its <code>client_id</code>, its <code>redirect_uri</code> and optionally, a <code>scope</code> and a <code>state</code> parameter <a href="http://openid.net/specs/openid-connect-core-1_0.html#AuthRequest" target="_blank" rel="external noopener">that allows flowing custom data and helps mitigate XSRF attacks</a>.
<div class="note tip">

In most cases, the client application will simply return a 302 response with a <code>Location</code> header to redirect the user agent to the authorization endpoint, but depending on the OpenID Connect client you're using, POST requests might also be supported to allow you to send large authorization requests. This feature <a href="https://github.com/aspnet/Security/pull/392" target="_blank" rel="external noopener">is usually implemented using an auto-post HTML form</a>.

</div>
The way the identity provider handles the authorization request is implementation-specific but in most cases, a consent form is displayed to ask the user if he or she agrees to share his/her personal data with the client application.
<p id="DhDIwbA"><img class="alignnone wp-image-1670 " src="/wp-content/uploads/2018/08/img_5b699086a671b.png" alt="" width="470" height="272" /></p>
</li>
 	<li>When the consent is given, the user agent is redirected back to the client application with <strong>a unique and short-lived token</strong> named <em>authorization code</em> that the client will be able to exchange with an access token by sending a token request.</li>
 	<li>To prevent XSRF/session fixation attacks, <strong>the client application MUST ensure that the <code>state</code> parameter returned by the identity provider corresponds to the original <code>state</code></strong> and stop processing the authorization response if the two values don't match. <a href="https://tools.ietf.org/html/rfc6749#section-10.12" target="_blank" rel="external noopener">This is usually done by generating a non-guessable string and a corresponding correlation cookie</a>.</li>
 	<li><strong>Step 2: the token request</strong></li>
 	<li>When the client application gets back an authorization code, it must immediately reedem it for an access token by sending a <code>grant_type=authorization_code</code>token request.
<div class="note tip">

To help the identity provider <a href="https://tools.ietf.org/html/rfc6819#section-4.4.1.7" target="_blank" rel="external noopener">mitigate counterfeit clients attacks</a>, the original <code>redirect_uri</code> must also be sent.

If the client application is a confidential application (i.e an application that has been assigned client credentials), authentication is required.

</div></li>
</ul>
<strong>4. The implicit flow</strong>
<p id="HLxUkBO"><img class="size-full wp-image-1671 aligncenter" src="/wp-content/uploads/2018/08/img_5b6991d7ab2c7.png" alt="" /></p>

<ul>
 	<li>is a simplified code flow, made for browsers-based apps.</li>
 	<li>The implicit flow is similar to the authorization code flow, <strong>except there's no token request/response step</strong>: the access token is directly returned to the client application as part of the authorization response in the URI fragment (or in the request form when using <code>response_mode=form_post</code>).</li>
</ul>
<div class="note info">
<ul>
 	<li>This flow is inherently less secure than the authorization code flow, but is easier to implement and has been specifically <strong>designed for JS applications.</strong> Using it with confidential applications is <strong>not recommended</strong> and authorization servers <strong>SHOULD STRONGLY</strong> consider rejecting implicit flow requests when the <code>client_id</code> corresponds to a confidential application to prevent downgrade attacks and token leakage.</li>
 	<li>To prevent XSRF/session fixation attacks, <strong>the client application MUST ensure that the <code>state</code> parameter returned by the identity provider corresponds to the original <code>state</code></strong> and stop processing the authorization response if the two values don't match. <a href="https://tools.ietf.org/html/rfc6749#section-10.12" target="_blank" rel="external noopener">This is usually done by generating a non-guessable string and a corresponding value stored in the local storage</a>.</li>
</ul>
</div>
<div class="note warn">
<ul>
 	<li>When using the implicit flow, <strong>the client application MUST also ensure that the access token was not issued to another application to prevent <a href="http://stackoverflow.com/a/17439317/542757" target="_blank" rel="external noopener">confused deputy attacks</a>.</strong> With OpenID Connect, this can be done by using <code>response_type=id_token token</code> and checking the <code>aud</code> claim of the JWT identity token, that must correspond or contain the <code>client_id</code> of the client application.</li>
</ul>
<strong>5. Hybrid Flow</strong>
<ul>
 	<li>hybrid flow is essentially a mix between the authorization code flow and the implicit flow (with all the security implications they have).There are mainly 2 cases where it's used: to avoid sending token requests with an invalid code (since the relying party can validate the authorization code using the c_hash claim stored in the identity token if one was returned) and in "hybrid" client-side/server-side apps, where the authorization code can be sent to the server-side part.

This flow is fully supported by both ASOS and OpenIddict but AFAIK, it's rarely used in practice.</li>
</ul>
</div>
<h2>References</h2>
<ul>
 	<li>https://tools.ietf.org/html/rfc6749</li>
 	<li>For more information, you can read this blog post: <a href="http://kevinchalet.com/2016/07/13/creating-your-own-openid-connect-server-with-asos-choosing-the-right-flows/" rel="nofollow noreferrer">http://kevinchalet.com/2016/07/13/creating-your-own-openid-connect-server-with-asos-choosing-the-right-flows/</a>.</li>
 	<li>https://stackoverflow.com/questions/46024665/why-there-are-many-authentication-flows-in-openiddict</li>
</ul>
