---
layout:	post
title:	"Is interface implementation that difficult to understand?"
date:	2022-04-26
---

  Once I was asked what do you know about interface? It was an interview for .NET Developer position. After I gave my answer, the interviewer said “Did you just read it from SOLID principle? (laughing)”.

I do not understand why he asked me that. The way he asked me took all my energy for the interview. I was so stupid so it seemed ridiculously that I was able to understand interface implementation?. I did not even want to clarify and want to know what he was thinking, which I usually do.

What was my answer?


> In short, an interface is to decouple the dependency between classes.In the interview, I tried to express my knowledge surrounding interface so the answer was a bit longer but what I wanted to say is the same.

![](/img/1uQYpcPWXqdv6NDgOaS8yQw_2.png)Is it not enough? I do not know but that is what I understand and actually put into practice.

For a simple explanation of interface, the article below is a good simple one.

[Dependency Inversion Principle: How Google Developers write code | by KD Knowledge Diet | Apr, 2022 | Medium](https://paigeshin1991.medium.com/dependency-inversion-principle-how-google-developers-write-code-f6cbd3b530a6)

For my actual implementation using interface to decouple dependencies, take a look at the way I implement and apply unit test in my tiny library below.

[VanDng/UniversalForumClient (github.com)](https://github.com/VanDng/UniversalForumClient)

Here I intend to decouple the HttpRequest from my core implementation.

  