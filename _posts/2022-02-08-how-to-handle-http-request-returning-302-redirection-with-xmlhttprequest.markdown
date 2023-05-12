---
layout:	post
title:	"How to handle HTTP Request returning 302 Redirection with XMLHttpRequest?"
date:	2022-02-08
---

  Recently, I have jumped into Javascript to make a few tiny scripts for fun. Soon after beginning, I had a problem with an HTTP Request returning status code 302 Redirection.

I used jQuery.ajax() to make HttpRequest and wanted to know whether a request was redirected and where it was redirected to.

With jQuery itself, there is no way. However, Vanilla Javascript can help me out.

#### **Vanilla Javascript**

The XMLHttpRequest’s implementation exposes a property named ResponseURL. The property stores the redirection destination of a request.

It is enough to solve my problem.

![]({{ site.baseurl }}/images/1omCTLTpCgUKLmNXY9SlRXg_2.png)Example of using ResponseURLFor compatibility, reference <https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseURL>

#### **jQuery**

Unfortunately, the property ResponseURL has not been available on jQuery yet. People raised [an issue ](https://github.com/jquery/jquery/issues/4339)and even created [a pull request](https://github.com/jquery/jquery/pull/4405) in May 2019.

It is 2022 now but the pull request is still under review.

For now, I have to make use of Vanilla Javascript.

**What if I want to cancel the redirection or force the redirection to go through a proxy?**

I have done a lot of looking up an answer. It all goes to the same endpoint that it is impossible. The status code 302 Redirection is managed automatically internally by browsers.

Given a situation where it becomes an issue, a separate service running as a request proxy will be necessary.

  