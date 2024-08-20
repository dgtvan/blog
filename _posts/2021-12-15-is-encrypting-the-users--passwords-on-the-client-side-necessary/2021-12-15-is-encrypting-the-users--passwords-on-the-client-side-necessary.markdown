---
layout:	post
title:	"Is encrypting the users’ passwords on the client-side necessary?"
date:	2021-12-15
---

  This is the question I got on a day in November 2021. This article is about where the question comes from, and my answer.

Even though I am neither a security consultant nor a security expert, by working as a back-end developer I do have awareness of vulnerabilities in my implementation as well as security fundamental knowledge. That said, I can make decisions on some simple cases whether an additional implementation for security purposes is necessary.

#### Context

Back then, I was in charge of maintaining an authentication module for my customer’s system.

The authentication module had a public API “/Login” where end-users submitted their username and password to authenticate.

HTTPS was in use.

![](1xa9QVocoKr-sHWuUmocxPQ_2.png)

The development had several phases, it was going to the end of the first phase at the time. Before that end, a security audit had to be established, the customer hired another security audit company to do that.

My story is a security auditor reported an issue that I do not agree to.

#### Begin

There was a day, a security auditor reported a critical issue with our customer and my development team via an email.

The issue was the end-users password was sent to the login endpoint in plain text. It was a high vulnerability. And an image, which is similar to the one I made below, is attached to the email.

![](1WNnun0Ds1nuHqZK9G7y5cg_2.png)He suggested a solution to the issue. It was to encrypt passwords on the client-side (the browser) with a strong algorithm such as RSA 2048 bits.

#### Discussion between me and the auditor

When I first looked at the issue, I instantly got the idea and understood what the auditor was concerned about.

Generally, yes, it is reasonable to encrypt the end-user's password. Because it prevents a problem that passwords can be read during transmitting by hackers, somehow.

In the given situation, however, HTTPS was in use so the end-user's password was encrypted by the secure connection already. Obviously, encryption on passwords was not necessary here.

I shared my above opinion with the auditor, he said something like **“If the connection was secured, why I was able to capture the password in plain text as I shared it with you?”.**

Well, I did not know how he set up everything to audit and capture the issue. I could only think of two possibilities:

1/ HTTPS did not work properly. If that was the case, he had to ask DevOps or someone else, I was not in charge of that stuff.

2/ Basically, he was inside the secured connection. For example, while accessing Google, Facebook,… with a secured connection established, I can open Google Chrome Inspector (F12) and able to view what is inside Request/Response Payload.

#### Final

I had to do it as he suggested, that was to encrypt passwords on the client-side anyway.

The implementation was to generate a pair of public/private RSA keys. The front-end always encrypts the end-user's passwords with the public key, the back-end decrypts them with the private key.

**Personally, I do not agree with the issue as well as the solution.**

#### Side notes

Here are some of my opinions along with the discussion.

1/ Making connection secured is the reason for the existence of TLS. If there is something that went wrong, let's make it work properly again. Do not try to do something, not of your expertise. Things can even get worse.

2/ If somehow TLS is broken, the encrypted passwords are sniffed. Hackers can relay these encrypted passwords to the server in order to impersonate users. In that case, encryption has no meaning.

If I am not wrong, TLS has a mechanism to authenticate parties involved in a connection via certificates. It helps to prevent sort of attacks like the man in the middle attack. I can not go deeper because it will be going out of my knowledge.

3/ Given a situation where we value the end-user’s passwords, we do not want the end-users’s plain text passwords to be exposed to any party including the server itself, then we should perform **hashing **on the client-side, then **hashing **it one more time on the server-side.

If you have an opposite opinion or something to comment on, please respond so that I have a chance to sharpen my knowledge.

Thank you.