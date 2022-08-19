---
layout: post
title: Authentication Latest Basics - Select mechanism
date: 2018-07-25 17:33
author: tmasabari
comments: true
categories: [Architecture, Security]
---
<h2 id="firstHeading" class="firstHeading" lang="en"><a href="https://www.owasp.org/index.php/Authentication_Cheat_Sheet" target="_blank" rel="nofollow noopener">Authentication Cheat Sheet</a></h2>
&nbsp;
<h2 id="68f1" class="graf graf--p graf-after--p"><a href="https://medium.com/@pavithraranathunga/the-most-common-authentication-methods-in-web-application-development-35845ecb1da0" target="_blank" rel="nofollow noopener"><strong class="markup--strong markup--p-strong">Cookie vs Token Authentication</strong></a></h2>
<p id="d760" class="graf graf--p graf-after--p">Cookie based authentication is considered as stateful authentication method (Server based authentication). In here, it is needed to store authentication records in client side and server side both. Server basically keeps and maintains active session details in the data storage and front end cookie will be created to hold session identifier.</p>
<p id="ff1b" class="graf graf--p graf-after--p">When considering about the flow of the cookie based authentication, we can summarize them as follows.</p>
<p id="0cea" class="graf graf--p graf-after--p">Ø Enter login credentials</p>
<p id="778e" class="graf graf--p graf-after--p">Ø Server verifies given credentials, creates a session and stores in database.</p>
<p id="59c8" class="graf graf--p graf-after--p">Ø Cookie + Session ID will be kept in client side(User browser)</p>
<p id="7b00" class="graf graf--p graf-after--p">Ø For consequent requests, session ID will be verified against database.</p>
<p id="3d90" class="graf graf--p graf-after--p">Ø Session will be destroyed from client and server side once the use logs out.</p>
<p id="0e4b" class="graf graf--p graf-after--p"><span style="background-color: #ff99cc;">The main disadvantage of using this authentication method is, server has to store all the session data for each and every user and increases the overhead in the server.</span></p>
<p id="816c" class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Token Based Authentication</strong></p>
<p id="7787" class="graf graf--p graf-after--p">This is the mostly used authentication methods which is suitable for<strong class="markup--strong markup--p-strong"> single page applications, web APIs and for IOT development (JSON web tokens are mostly used-</strong><em class="markup--em markup--p-em">hope to discuss about it later</em><strong class="markup--strong markup--p-strong">)</strong>. Token based authentication is defined as stateless and server does not keep records about the user logged in. But the token will be generated using credentials provided. The main advantage of token based authentication is client side and server side is decoupled for the authentication mechanism which can provide an uninterrupted workflow. No session information stored means simply your application can scale and add more machines as necessary without worrying about where the user logged in. The flow of the token based authentication can be concluded as follows,</p>
<p id="4c79" class="graf graf--p graf-after--p">Ø User provides credentials</p>
<p id="a115" class="graf graf--p graf-after--p">Ø Server verifies credentials and returns a signed token.</p>
<p id="4569" class="graf graf--p graf-after--p">Ø Token is stored in client side</p>
<p id="ce91" class="graf graf--p graf-after--p">Ø Subsequent requests to the server will be sent with the token as authentication header (HTTP header).</p>
<p id="67f1" class="graf graf--p graf-after--p">Ø Server verifies the token (JSON web token) and return required data.</p>
<p id="8449" class="graf graf--p graf-after--p">Ø Token is destroyed in client, once the user logs out.</p>
<p id="cb6a" class="graf graf--p graf-after--p graf--trailing">Token Based Authentication can be applied for Web API2 via OWIN (Owin — standard interface between .net web app and server which is used to decouple server and client).</p>

<h2><a href="https://www.paladion.net/blogs/evolution-of-authentication-in-web-applications" target="_blank" rel="nofollow noopener">Evolution-of-authentication</a></h2>
<h3>Form-based Authentication</h3>
Form-based Authentication gives the developer freedom to build a more secure authentication scheme. This type evolved over time. Basically, form-based authentication refers to any mechanism that relies on factors external to the HTTP protocol for authenticating the user. The application is left to deal with taking the user credentials, verifying them and deciding their authenticity.

The simplest way to do so is to have a login form that asks the user for the username and password. These values are then compared with the username and the password already present in the database. The password is protected during transmission by either using an SSL connection or encrypting the password. SSL protects the password during transmission but it can still be stolen by a local adversary from the browser's memory. This problem can be fixed by using a salted hash technique to transmit the password.
<h4>Advantages</h4>
<ul>
 	<li>The developer is free to implement the Login page in a desired manner.</li>
 	<li>All development frameworks and languages support form authentication.</li>
</ul>
<h4>Disadvantages</h4>
<ul>
 	<li>Encryption or security is not enforced by default. The responsibility to implement a safe solution belongs to the developer.</li>
</ul>
<h3>CAPTCHAs and Key Loggers</h3>
As attackers became smarter, applications had to defend themselves against newer threats like automated password guessing and key loggers. Attackers made their job easy by writing scripts that would keep on trying passwords on the Login page till a match was found.

CAPTCHA is an effective method used to address the problem of automated password-guessing attacks. Generally, CAPTCHAs comprise randomly generated text that is displayed in a distorted manner. The text can be read by a human, but not an automated program. CAPTCHAs also prevent an automated script from flooding the web server with a large number of requests. CAPTCHAs are typically used in User Registration pages, Login pages and Forgot Password pages.
<h4>Advantages</h4>
<ul>
 	<li>They prevent automated password-guessing attacks.</li>
 	<li>They prevent automated DoS attacks.</li>
 	<li>They are simple and convenient for a user.</li>
</ul>
<h4>Disadvantages</h4>
<ul>
 	<li>A CAPTCHA that is not implemented properly can make the application vulnerable to attacks.</li>
 	<li>A visual CAPTCHA (distorted text) is not very user friendly for the visually weak.</li>
</ul>
The threat of key loggers was addressed by a number of sites using a virtual keyboard. Since key-logging programs would reside on the client machine and capture all the keystrokes and mail them to the attacker, virtual keyboards eliminate the need to key in the password. A graphical representation of the keyboard is displayed on the screen and the user uses the mouse to click on the respective characters.
<h4>Advantages</h4>
<ul>
 	<li>It is a simple method that can be implemented easily.</li>
 	<li>A virtual keyboard can also be used in pages with sensitive information like credit card details, etc.</li>
</ul>
<h4>Disadvantages</h4>
<ul>
 	<li>Shoulder surfing becomes a more plausible threat.</li>
 	<li>There are advanced malicious software that capture the mouse clicks and based on the pixels, compute the characters entered.</li>
</ul>
The next generation of authentication schemes involved 2 factors for authentication. The 2 factors in authentication are defined as something we know (i.e. password) and something we have (i.e. hardware token/card, etc.). The user is required to provide both to prove their identity.
<h3>One-Time Passwords (OTP)</h3>
One-time passwords are a form of two-factor authentication. They emulate the sharing of a secret on-the-fly between two digital entities using an out-of-band communication model (SMS, email or paper passwords).

The user provides his/her username and/or password during the authentication process. The server validates the username and generates the OTP, which is sent across to the out-of-band communication media (SMS, email, etc.). In certain cases, a pre-generated set of OTPs are generated on paper and physically delivered to the user by hand or through post. Any of these pre-generated OTPs can be used only once.
<h4>Advantages</h4>
<ul>
 	<li>Increased difficulty for the attacker – needs to compromise SMSs/emails apart from the application.</li>
 	<li>Authentication depends on secrets from two disparate systems (2 factors i.e. the human brain and the SMS).</li>
 	<li>The duration of the validity of the OTP limits the continued compromise of the user account.</li>
 	<li>Extended access for the attacker is limited since OTP can be used only once for the specific transaction.</li>
</ul>
<h4>Disadvantages</h4>
<ul>
 	<li>The scheme depends on the availability of the additional (server) and the external infrastructure (SMSs/emails).</li>
 	<li>There can be delays in the delivery of the password, which is outside the application’s control.</li>
 	<li>There can be geographical limitations for a person who is traveling.</li>
</ul>
A number of sensitive sites resorted to various 2nd factors in authentication like hardware tokens and passwords being sent via email.
<h3>Hardware Tokens</h3>
Certain banks and owners of other critical applications provide hardware tokens to their users.

There are a number of types of hardware tokens in use, but the most common is the disconnected token. The user has to enter the number displayed on the token along with the password in the application. If both the values entered are correct, the user gains access to the application. The token contains an algorithm, a clock and a seed or a unique number. Taking the time and the seed as the input, the algorithm generates the number displayed.

The application using 2-factor authentication is connected to the server dealing with the tokens. The server would have the seed and using the current time and the same algorithm computes the same number as the token at any point in time. Therefore, the server is able to authenticate with the user. To accommodate for any mismatch in the number entered due to any delay in the clock, the server allows the token to be valid for a time window.
<h4>Advantages</h4>
<ul>
 	<li>Very secure as you need the number generated by the token to log in.</li>
 	<li>The token is easy to use.</li>
</ul>
<h4>Disadvantages</h4>
<ul>
 	<li>A chance of mismatch in the time leading to authentication failure is possible.</li>
 	<li>The token is a small physical entity and can be easily lost.</li>
 	<li>The infrastructure required is a cost overhead.</li>
 	<li>The distribution and maintenance of the tokens is an overhead.</li>
</ul>
&nbsp;
<h2><a href="https://www.pingidentity.com/en/company/blog/2016/02/04/the_top_6_authentication_mechanisms.html" target="_blank" rel="nofollow noopener">Top mechanisms</a></h2>
<span style="background-color: #ffff99;">The days of one-step authentication with a username and password are gone.</span> The digital enterprise requires you to know where they are, what network they're coming from and what application they're accessing. MFA provides enhanced security and control, and moves organizations away from a high-risk password-based security model.

Multi-factor authentication (MFA) requires users to provide multiple proofs of their claimed identity before being granted access to some set of resources. The premise of MFA is that, if one mechanism is compromised, others are unlikely to be, so there's still some level of confidence in the user's authentication.

Historically, MFA has demanded a choice of authentication mechanisms from at least two of the following categories:
<ul>
 	<li>Knowledge (something the user knows)</li>
 	<li>Possession (something the user has)</li>
 	<li>Inherence (some physical characteristic of the user)</li>
</ul>
<ol>
 	<li><strong>Passwords</strong>A password is a shared secret known by the user and presented to the server to authenticate the user. Passwords are the default authentication mechanism on the web today. However, poor usability and vulnerability to large scale breaches and phishing attacks make passwords an unacceptable authentication mechanism in isolation. To a large extent, the value of MFA is that additional authentication mechanisms serve to mitigate the risks associated with passwords.</li>
 	<li><strong>Hard Tokens</strong>These are small hardware devices that the owner carries to authorize access to a network service. The device may be in the form of a smart card, or it may be embedded in an easily-carried object such as a key fob or USB drive. The device itself contains an algorithm (a clock or a counter), and a seed record used to calculate the pseudo-random number. Users enter this number to prove that they have the token. The server that's authenticating the user must also have a copy of each key fob's seed record, the algorithm used and the correct time. The historical challenge of relying on hardware tokens for MFA has been the requirement that users always carry these tokens with them.

A new form factor for hard tokens has emerged. Small tokens are inserted into the PC's USB slot. When the user needs to authenticate, they press a key on the device, which generates a one-time passcode (OTP) and sends it to the server as if the user had entered it by hand. Because these hard tokens can be left in the PC's USB drive, the users aren't pressured to remember to bring the token.</li>
 	<li><strong>Soft Tokens</strong>These software-based security token applications typically run on a smartphone and generate an OTP for signing on. Software tokens have some significant advantages over hardware tokens. Users are less likely to forget their phones at home than lose a single-use hardware token. When they do lose a phone, users are more likely to report the loss, and the soft token can be disabled. Soft tokens are less expensive and easier to distribute than hardware tokens, which need to be shipped.

Soft tokens leverage mobile phones' ability to generate an OTP and, possibly, their communication network. A user can demonstrate possession of his/her previously registered phone by receiving a message sent to that device. An OTP can be sent to the phone by SMS, voice call, or with an app that receives an authentication prompt via the mobile OS notification services, which is then entered by the user into a sign-on screen.

The SMS OTP option doesn't require a user to own a modern smartphone that supports mobile applications, but it has several disadvantages:
<ul>
 	<li>It was never designed for security.</li>
 	<li>It relies on operator practices around number porting, among other things.
It doesn't protect against phishing, although it does force attackers to implement a real-time attack.</li>
 	<li>It doesn't have the sort of delivery guarantee that authentication demands--a delay in delivery of minutes can effectively lock the customer out.</li>
</ul>
&nbsp;

In mobile-based solutions, it's more common to rely on an application installed on the mobile device. Instead of sending an SMS to the phone number, the authentication server can send a notification to the mobile app, which prompts the user for some action (e.g., 'Swipe your screen' or 'Apply your fingerprint'). A mobile app can provide useful context to the user to explain why he/she is being asked to authenticate and what he/she may be authorizing. There's a big difference between "sign on to your bank account" versus "empty your bank account."</li>
 	<li><strong>Biometric Authentication</strong>Biometric authentication methods include retina, iris, fingerprint and finger vein scans, facial and voice recognition, and hand or even earlobe geometry. The latest phones are adding hardware support for biometrics, such as TouchID on the iPhone. Biometric factors may demand an explicit operation by the user (e.g., scanning a fingerprint), or they may be implicit (e.g., analyzing the user's voice as they interact with the help desk).

The FIDO Alliance is defining a standardized architecture by which a user's local authentication to the device (e.g., laptop, phone) can be communicated to a server through a secure cryptographic protocol. When that local authentication is biometric (e.g., a scan of the user's fingerprint by a TouchID sensor or a facial scan or a voice print), then the FIDO model's advantage is that the biometric template doesn't have to be stored on the server, with attendant privacy risk.</li>
 	<li><strong>Contextual Authentication</strong>Every time a user interacts with an authentication server, in addition to any explicit credentials they present, they (or their devices) implicitly present a number of different signals. Contextual authentication collects signals like geolocation, IP address and time of day in order to help establish assurance that the user is valid. Typically, a user's current context is compared to previously established context (or blacklists/whitelists) in order to spot inconsistencies and identify potential fraud. These checks are invisible to the authorized user, so there are no usability issues, but they can create a significant barrier to an attacker. As an example, Visa's mobile location confirmation mechanisms determine the location of the user's mobile phone to verify that the user is physically near the location where the credit card is being used. The chances of a fraudulent transaction are higher if the transaction takes place in a different location from the phone. This is an example of comparing the contextual signals of the application channel to the contextual signals of a separate authentication channel (which will typically be similar) to spot potential fraud.

Contextual signals can be collected by:
<ul>
 	<li>The web pages where they authenticate.</li>
 	<li>The mobile devices used for MFA.</li>
 	<li>Other network hardware.</li>
 	<li>The application (or gateways in front).</li>
 	<li>Other sensors in proximity to the user (e.g., wearables, smart watches, etc.).</li>
</ul>
&nbsp;

Once collected and aggregated, the authentication server can analyze these signals to look for anomalous patterns that might indicate an attack or fraudulent behavior. This analysis can be:
<ul>
 	<li><strong>Contextual</strong>, comparing a given signal value to a prescribed list of allowed or prohibited values (e.g., not allowing sign-on for any IP address coming from Uzbekistan).</li>
 	<li><strong>Behavioral</strong>, comparing a given signal value to the expected value based on a previously established pattern (e.g., an employee often travels to Uzbekistan on legitimate business, and therefore is allowed to sign on with MFA, whereas any other employee is prohibited from signing on from Uzbekistan).</li>
 	<li><strong>Correlative</strong>, comparing a given signal value to a different collected signal value and looking for inconsistencies between the two (e.g., according to the laptop IP, an employee is in the United States, but according to their mobile phone, this employee is in Uzbekistan).</li>
</ul>
&nbsp;</li>
 	<li><strong>Device Identification</strong>A specific noteworthy example of contextual authentication is for the authentication server to be able to recognize a particular device over repeated interactions. Device identification establishes a <em>fingerprint</em> that's somewhat unique to that device. Over time, this fingerprint allows the authentication server to recognize that device and determine when the user associated with it attempts to authenticate from a different device, which could indicate fraudulent activity. Device identification solutions create a fingerprint based on characteristics like geolocation, OS version and browser. The simplest mechanism for device identification is a long-lived cookie that is set in the mobile browser by the authentication server. The logic here is that 'I trust this device because I have seen it before and nothing bad happened.'</li>
</ol>
&nbsp;

&nbsp;

&nbsp;

&nbsp;
