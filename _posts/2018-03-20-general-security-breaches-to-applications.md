---
layout: post
title: General Encryption & Security breaches to applications
date: 2018-03-20 14:21
author: tmasabari
comments: true
categories: [Security]
---
<h1><a class="question-hyperlink" href="https://stackoverflow.com/questions/549/the-definitive-guide-to-form-based-website-authentication">The definitive guide to form-based website authentication [closed]</a></h1>
<h2>MUST-READ LINKS About Web Authentication</h2>
<ol>
 	<li><a href="https://www.owasp.org/index.php/Authentication_Cheat_Sheet" rel="noreferrer">OWASP Guide To Authentication</a> / <a href="https://www.owasp.org/index.php/Authentication_Cheat_Sheet" rel="noreferrer">OWASP Authentication Cheat Sheet</a></li>
 	<li><a href="https://pdos.csail.mit.edu/papers/webauth:sec10.pdf" rel="noreferrer">Dos and Don’ts of Client Authentication on the Web (very readable MIT research paper)</a></li>
 	<li><a href="http://en.wikipedia.org/wiki/HTTP_cookie#Drawbacks_of_cookies" rel="noreferrer">Wikipedia: HTTP cookie</a></li>
 	<li><a href="http://cups.cs.cmu.edu/soups/2008/proceedings/p13Rabkin.pdf" rel="noreferrer">Personal knowledge questions for fallback authentication: Security questions in the era of Facebook (very readable Berkeley research paper)</a></li>
</ol>
&nbsp;
<ol>
 	<li>In essence, the only <strong>practical</strong> way to protect against wiretapping / packet sniffing during login is by using HTTPS or another certificate-based encryption scheme (for example, <a href="https://en.wikipedia.org/wiki/Transport_Layer_Security" rel="noreferrer">TLS</a>) or a proven &amp; tested challenge-response scheme (for example, the <a href="http://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange" rel="noreferrer">Diffie-Hellman</a>-based SRP). <em>Any other method can be easily circumvented</em> by an eavesdropping attacker.</li>
 	<li><strong>(Do not) </strong>Roll-your-own JavaScript encryption/hashing</li>
 	<li><strong>CAPTCHAS against humanity</strong>
<ol>
 	<li>If you must use a CAPTCHA, use Google's <a href="http://en.wikipedia.org/wiki/ReCAPTCHA" rel="noreferrer">reCAPTCHA</a>, since it is OCR-hard by definition (since it uses already OCR-misclassified book scans) and tries very hard to be user-friendly.</li>
 	<li>Personally, I tend to find CAPTCHAS annoying, and use them only as a last resort when a user has failed to login a number of times and throttling delays are maxxed out. This will happen rarely enough to be acceptable, and it strengthens the system as a whole.</li>
</ol>
</li>
 	<li><strong>Storing Passwords / Verifying logins</strong>
<ol>
 	<li>Do not store passwords in cleartext in your database. User databases are routinely hacked, leaked or gleaned through SQL injection, and if you are storing raw, plaintext passwords, that is instant game over for your login security.</li>
 	<li>So if you can't store the password, how do you check that the login+password combination POSTed from the login form is correct? The answer is hashing using a <a href="https://en.wikipedia.org/wiki/Key_derivation_function" rel="noreferrer">key derivation function</a>. Whenever a new user is created or a password is changed, you take the password and run it through a KDF, such as Argon2, bcrypt, scrypt or PBKDF2, turning the cleartext password ("correcthorsebatterystaple") into a long, random-looking string, which is a lot safer to store in your database.</li>
 	<li>To verify a login, you run the same hash function on the entered password, this time passing in the salt and compare the resulting hash string to the value stored in your database. Argon2, bcrypt and scrypt store the salt with the hash already. Check out this <a href="https://security.stackexchange.com/a/31846/8340">article</a> on sec.stackexchange for more detailed information.</li>
 	<li>A salt effectively prevents two passwords that exactly match from being stored as the same hash value, preventing the whole database being scanned in one run if an attacker is executing a password guessing attack.</li>
</ol>
</li>
 	<li><strong>Session data</strong>
<ol>
 	<li>A single randomly-generated string is stored in an expiring cookie and used to reference a collection of data - the session data - which is stored on the server. If you are using an MVC framework, this is undoubtedly handled already.</li>
 	<li>If at all possible, make sure the session cookie has the secure and HTTP Only flags set when sent to the browser.
<ol>
 	<li>The httponly flag provides some protection against the cookie being read by a XSS attack.</li>
 	<li>The secure flag ensures that the cookie is only sent back via HTTPS, and therefore protects against network sniffing attacks. The value of the cookie should not be predictable.</li>
</ol>
</li>
 	<li>Where a cookie referencing a non-existent session is presented, its value should be replaced immediately to prevent <a href="https://www.owasp.org/index.php/Session_fixation" rel="noreferrer">session fixation</a>.</li>
</ol>
</li>
 	<li><strong>Don't implement 'secret questions'</strong>. The 'secret questions' feature is a security anti-pattern. <strong>In conclusion, security questions are inherently insecure in virtually all their forms and variations, and should not be employed in an authentication scheme for any reason.</strong>
<ol>
 	<li>The true reason why security questions even exist in the wild is that they conveniently save the cost of a few support calls from users who can't access their email to get to a reactivation code. This at the expense of security and Sarah Palin's reputation. Worth it? Probably not.</li>
</ol>
</li>
 	<li>Forgotten Password Functionality
<ol>
 	<li><strong>never use security questions</strong> for handling forgotten/lost user passwords;</li>
 	<li>it also goes without saying that you should never e-mail users their actual passwords</li>
 	<li>Don't <em>reset</em> a forgotten password to an autogenerated strong password - such passwords are notoriously hard to remember, which means the user must either change it or write it down - say, on a bright yellow Post-It on the edge of their monitor. Instead of setting a new password, just let users pick a new one right away - which is what they want to do anyway.</li>
 	<li>Always hash the lost password code/token in the database. <strong><em>AGAIN</em></strong>, this code is another example of a Password Equivalent, so it MUST be hashed in case an attacker got their hands on your database. When a lost password code is requested, send the plaintext code to the user's email address, then hash it, save the hash in your database -- and <em>throw away the original</em>. Just like a password or a persistent login token.</li>
</ol>
</li>
 	<li>Checking Password Strength
<ol>
 	<li><a href="http://www.whatsmypass.com/?p=415" rel="noreferrer">The 500 most common passwords</a></li>
 	<li>The National Institute of Standards and Technology (NIST) <a href="http://en.wikipedia.org/wiki/Password_strength#NIST_Special_Publication_800-63" rel="noreferrer">Special Publication 800-63</a> has a set of very good suggestions.</li>
 	<li>And for a refreshing take on user-friendliness of high-entropy passwords, Randall Munroe's <a href="https://xkcd.com/936/" rel="noreferrer">Password Strength xkcd</a> is highly recommended.</li>
</ol>
</li>
 	<li>Preventing Rapid-Fire Login Attempts
<ol>
 	<li>It takes <em>virtually no time</em> to crack a
<ol>
 	<li>weak password,</li>
 	<li>alphanumeric 9-character password, if it is <strong>case insensitive</strong></li>
 	<li>an intricate, symbols-and-letters-and-numbers, upper-and-lowercase password, if it is <strong>less than 8 characters long</strong></li>
</ol>
</li>
 	<li>It would, however, take an<strong> inordinate amount of time to crack even a 6-</strong>character password, <em>if you were limited to </em><strong><em>one attempt per second</em></strong>
<ol>
 	<li>Present a <strong>CAPTCHA</strong> after N failed attempts (annoying as hell and often ineffective -- but I'm repeating myself here)</li>
 	<li><strong>Locking accounts</strong> and requiring email verification after N failed attempts (this is a <a href="http://en.wikipedia.org/wiki/Denial-of-service_attack" rel="noreferrer">DoS</a> attack waiting to happen)</li>
 	<li>And finally, <strong>login throttling</strong>: that is, setting a time delay between attempts after N failed attempts (yes, DoS attacks are still possible, but at least they are far less likely and a lot more complicated to pull off).</li>
</ol>
</li>
</ol>
</li>
 	<li>Distributed Brute Force Attacks
<ol>
 	<li><strong>Distributing the attempts on a botnet</strong> to prevent IP address flagging</li>
 	<li>Rather than picking one user and trying the 50.000 most common passwords (which they can't, because of our throttling), they will <strong>pick THE most common password and try it against 50.000 users instead.</strong> That way, not only do they get around maximum-attempts measures like CAPTCHAs and login throttling, their chance of success increases as well, since the number 1 most common password is far more likely than number 49.995</li>
 	<li><strong>Spacing the login requests for each user account,</strong> say, 30 seconds apart, to sneak under the radar</li>
 	<li>Here, the best practice would be <strong>logging the number of failed logins, system-wide</strong>, and using a running average of your site's bad-login frequency as the basis for an upper limit that you then impose on all users.
<ol>
 	<li>Say your site has had an average of 120 bad logins per day over the past 3 months. Using that (running average), your system might set the global limit to 3 times that -- ie. 360 failed attempts over a 24 hour period.</li>
 	<li>Then, if the total number of failed attempts across all accounts exceeds that number within one day (or even better, monitor the rate of acceleration and trigger on a calculated threshold),</li>
 	<li>it <strong>activates system-wide login throttling - meaning short delays for ALL users</strong> (still, with the exception of cookie logins and/or backup CAPTCHA logins).</li>
</ol>
</li>
</ol>
</li>
 	<li>Two-Factor Authentication and Authentication Providers
<ol>
 	<li>Credentials can be compromised, whether by exploits, passwords being written down and lost, laptops with keys being stolen, or users entering logins into phishing sites.</li>
 	<li>Logins can be further protected with two-factor authentication, which use out-of-band factors such as single-use codes received from a phone call, SMS message, app, or dongle. Several providers offer two-factor authentication services.</li>
</ol>
</li>
</ol>
<h1><strong>Encryption</strong></h1>
<h3>The Basic Principles</h3>
<ul>
 	<li>Plaintext - the original message</li>
 	<li>Ciphertext - the coded message</li>
 	<li>Cipher - algorithm for transforming plaintext to<strong> </strong>ciphertext. A cryptographic algorithm, or cipher, is a mathematical function used in the encryption and decryption process</li>
 	<li>key - info used in cipher known only to<strong> </strong>sender/receiver</li>
 	<li>Cryptography is the science of using mathematics to encrypt and decrypt data.
<ul>
 	<li>Cryptography enables you to store sensitive information or transmit it across insecure networks (like the Internet) so that it cannot be read by anyone except the intended recipient.</li>
</ul>
</li>
 	<li>Cryptanalysis (codebreaking) - the study of<strong> </strong>principles/ methods of<strong> </strong>deciphering ciphertext<strong> </strong>without knowing key</li>
 	<li>Cryptology - the field of both cryptography and<strong> C</strong>ryptanalysis</li>
 	<li>Symmetric Encryption– Both Sender/Receiver use the same algorithms/keys for encryption/decryption</li>
 	<li>Asymmetric Encryption- Sender/receiver can employ different keys</li>
 	<li>Block ciphers encrypt block at a time Message is broken into blocks and encrypted</li>
 	<li>Stream ciphers process a bit or byte at a time during encryption/decryption</li>
 	<li>A certificate server, also called a cert server or a key server, is a database that allows users to submit and retrieve digital certificates.</li>
 	<li>Public Key Infrastructures- A PKI contains the certificate storage facilities of a certificate server, but also provides certificate management facilities (the ability to issue, revoke, store, retrieve, and trust certificates). The main feature of a PKI is the introduction of what is known as a Certification Authority, or CA, which is a human entity—a person, group, department, company, or other association—that an organization has authorized to issue certificates to its computer users.</li>
</ul>
<em>“There are two kinds of cryptography in this world: cryptography that will stop your kid sister from reading your files, and cryptography that will stop major governments from reading your files. This book is about the latter.”</em>

--Bruce Schneier, Applied Cryptography: Protocols, Algorithms, and Source Code in C.
<h3>1. Encryption</h3>
In a simplest form, encryption is to convert the data in some unreadable form. This helps in protecting the privacy while sending the data from sender to receiver. On the receiver side, the data can be decrypted and can be brought back to its original form. The reverse of encryption is called as decryption. The concept of encryption and decryption requires some extra information for encrypting and decrypting the data. This information is known as key.
<h3>2. Authentication</h3>
This is another important principle of cryptography. In a layman’s term, authentication ensures that the message was originated from the originator claimed in the message.
<h3>3. Integrity</h3>
Now, one problem that a communication system can face is the loss of integrity of messages being sent from sender to receiver. This means that Cryptography should ensure that the messages that are received by the receiver are not altered anywhere on the communication path. This can be achieved by using the concept of cryptographic hash.
<h3>4. Non Repudiation</h3>
What happens if Alice sends a message to Bob but denies that she has actually sent the message? Cases like these may happen and cryptography should prevent the originator or sender to act this way. One popular way to achieve this is through the use of digital signatures.
<h3>Types of Cryptography</h3>
There are three types of cryptography techniques :
<ul>
 	<li>Secret key Cryptography</li>
 	<li>Public key cryptography</li>
 	<li>Hash Functions</li>
</ul>
<h2><strong>1. Secret Key Cryptography or Conventional cryptography or symmetric-key encryption</strong></h2>
This type of cryptography technique uses just a single key. The sender applies a key to encrypt a message while the receiver applies the same key to decrypt the message. Since only single key is used so we say that this is a symmetric encryption.

<img class="wp-image-1093" src="/wp-content/uploads/2018/03/image10.png" alt="image10" />

The biggest problem with this technique is the distribution of key as this algorithm makes use of single key for encryption or decryption.

Conventional encryption has benefits. It is very fast. It is especially useful for encrypting data that is not going anywhere.
<h2><strong>2. Public Key Cryptography</strong></h2>
This type of cryptography technique involves two key crypto system in which a secure communication can take place between receiver and sender over insecure communication channel. Since a pair of keys is applied here so this technique is also known as asymmetric encryption.

<img class="wp-image-1096" src="/wp-content/uploads/2018/03/image11.png" alt="image11" />

In this method, each party has a private key and a public key. The private is secret and is not revealed while the public key is shared with all those whom you want to communicate with. If Alice wants to send a message to bob, then Alice will encrypt it with Bob’s public key and Bob can decrypt the message with its private key.

This is what we use when we setup <u><a href="http://www.thegeekstuff.com/2008/11/3-steps-to-perform-ssh-login-without-password-using-ssh-keygen-ssh-copy-id/" target="_blank" rel="noopener">public key authentication in openssh</a></u> to login from one server to another server in the backend without having to enter the password.

It is computationally infeasible to deduce the private key from the public key. Anyone who has a public key can encrypt information but cannot decrypt it. Only the person who has the corresponding private key can decrypt the information.

The primary benefit of public key cryptography is that it allows people who have no preexisting security arrangement to exchange messages securely. The need for sender and receiver to share secret keys via some secure channel is eliminated; all communications involve only public keys, and no private key is ever transmitted or shared.

Some examples of public-key cryptosystems are Elgamal (named for its inventor, Taher Elgamal), RSA (named for its inventors, Ron Rivest, Adi Shamir, and Leonard Adleman), Diffie-Hellman (named, you guessed it, for its inventors), and DSA, the Digital Signature Algorithm (invented by David Kravitz).

In public key cryptography, the bigger the key, the more secure the ciphertext. A conventional 80-bit key has the equivalent strength of a 1024-bit public key. A conventional 128-bit key is equivalent to a 3000-bit public key deriving the private key is always possible given enough time and computing power. This makes it very important to pick keys of the right size; large enough to be secure, but small enough to be applied fairly quickly. Additionally, you need to consider who might be trying to read your files, how determined they are, how much time they have, and what their resources might be. Larger keys will be cryptographically secure for a longer period of time.

A digital certificate is data that functions much like a physical certificate. A

digital certificate is information included with a person’s public key that helps

others verify that a key is genuine or valid. Digital certificates are used to

thwart attempts to substitute one person’s key for another.

A digital certificate consists of three things:

• A public key.

• Certificate information. (“Identity” information about the user, such as

name, user ID, and so on.)

• One or more digital signatures.

The purpose of the digital signature on a certificate is to state that the

certificate information has been attested to by some other person or entity
<h3><strong>Digital signatures </strong></h3>
Digital signatures enable the recipient of information to verify the authenticity of the information’s origin, and also verify that the information is intact. Thus, public key digital signatures provide authentication and data integrity. A digital signature also provides non-repudiation, which means that it prevents the sender from claiming that he or she did not actually send the information.
<h2><strong>3. Hash Functions</strong></h2>
<img class="wp-image-1087" src="/wp-content/uploads/2018/03/image9.png" alt="image9" />

This technique does not involve any key. Rather it uses a fixed length hash value that is computed on the basis of the plain text message. Hash functions are used to check the integrity of the message to ensure that the message has not be altered,compromised or affected by virus.
<h1><strong>Security Threads</strong></h1>
<u><a href="http://www.zdnet.com/article/legacy-vulnerabilities-easy-route-for-hackers/" target="_blank" rel="noopener">http://www.zdnet.com/article/legacy-vulnerabilities-easy-route-for-hackers/</a></u>

The work of our threat research and software security research teams revealed vulnerabilities in products and programs that were years old--in a few cases, decades old. Well-known attacks were still distressingly effective, and misconfiguration of core technologies continued to plague systems that should have been far more stable and secure than they in fact proved to be. We are, in other words, still in the middle of old problems and known issues even as the pace of the security world quickens around us.

<img class="wp-image-1089" src="/wp-content/uploads/2018/03/image16.png" alt="image16" />

Among other key items:
<ul>
 	<li>Software as a service and middleware are increasingly being exploited via protocols including HTTP, Simple Object Access Protocol (SOAP) and JSON.</li>
 	<li>Oracle has curtailed exploits in Java. The report noted: "Oracle introduced click to play as a security measure making the execution of unsigned Java more difficult. As a result we did not encounter any serious Java zero days in the malware space. Many Java vulnerabilities were logical or permission-based issues with a nearly 100 percent success rate. In 2014, even without Java vulnerabilities, we still saw high success rate exploits in other areas."</li>
 	<li>The top 10 discovered exploits in 2014 were led by Microsoft Internet Explorer as well as Adobe Flash.</li>
</ul>
<img class="wp-image-1098" src="/wp-content/uploads/2018/03/image15.png" alt="image15" />
<h2>Introduction</h2>
Data breaches are more than a security problem. A significant attack can shake your customer base, partner relations, executive staff, profits, and revenue. Historic data breaches have cost executives their jobs, resulted in major revenue losses and damaged brand reputations.
<ul>
 	<li>“Rogue clouds” (private file sync-and-share options not supported or secured by an enterprise’s IT infrastructure) are creeping into organizations. A 2013 survey by Symantec found that 77% of all businesses experienced rogue cloud situations.³</li>
 	<li>You don’t just need to defend against viruses and malware—19% of security incidents involve malicious insiders.</li>
 	<li>84% of organizations have not implemented a cybersecurity task force.</li>
 	<li>We needed to secure and manage the mobile devices and smartphones used outside the corporate network—as well as the data they contain. The Enterprise Mobility Suite delivers these capabilities in one, cost-effective package.</li>
 	<li>Cybersecurity spending isn’t slowing down. Gartner reported that cybersecurity spending reached a record $75 billion in 2015 and anticipates it reaching $170 billion by 2020.</li>
</ul>
<h2>Background</h2>
In a 2014 study of 700 consumers about brand reputation by Experian and the Ponemon Institute, data breaches were reported as the most damaging occurrence to brand reputation, exceeding environmental disasters and poor customer service.1

Although Chief Security Officers, Chief Information Security Officers, and security analysts are on the front lines fighting hackers, they should not be considered the last and only line of defense. CFOs, typically responsible for managing a corporation’s financial risks, should be inquiring on the enterprise risk of cybersecurity.

&nbsp;

<strong>Insider threats</strong>

Insider threats are commonly thought of as one of the most difficult threats to defend against.

With the growing use of contractors, freelancers, and temporary employees throughout an enterprise, defending against potential internal threats seems next to impossible.

In 2013, the FBI estimated malicious insider threat attacks cost approximately $412,000 per incident.⁴

Although there is no single solution for defending against insider threats, experts recommend a multi-pronged approach that involves action from several members of leadership

Talent acquisition should focus on strong background checks on all employees and contractors, and human relations can help catch red flags stemming from irregular employee behavior (such as missed work or bragging about potential damage they could do).⁵

&nbsp;
