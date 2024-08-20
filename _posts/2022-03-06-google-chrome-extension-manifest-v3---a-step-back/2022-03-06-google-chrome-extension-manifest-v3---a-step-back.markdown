---
layout:	post
title:	"Google Chrome Extension Manifest V3 — A Step back?"
date:	2022-03-06
---

I have a personal project developing a Chrome extension. Along the way I research to develop it, I find that I joined the party at the wrong time frame. It’s both interesting and frustrating at the same time.

According to an [official announcement](https://developer.chrome.com/docs/extensions/mv3/mv2-sunset/), Manifest V2 will be going to an end by 2023. Everyone is on their way to upgrade their extensions to Manifest V3.

![](18wpbad9oyhAouUelHMzFUA_2.png)

At first, I had no idea about Manifest V2 and V3, I found a sample and kicked it started, later I knew that I was working on Manifest V2 and realized Manifest V2 is going to be deprecated soon.

So, I started to work on Manifest V3 migration. Well, gradually, it was more like developing everything all over again, not migrating.

Between Manifest V2 and V3, there are minor changes as well as[ breaking changes](https://developer.chrome.com/docs/extensions/mv3/intro/mv3-overview/). Correct, breaking changes means no backward compatibility.

In case you did not know where people are discussing these changes, let's [check it out](https://groups.google.com/a/chromium.org/g/chromium-extensions). Manifest V3 comes out with lots of issues and limitations.

Developers are sharing their workaround to overcome their migration obstacles, complaining every single day.

Here is a simple one [MV3 changes/decisions (google.com)](https://groups.google.com/a/chromium.org/g/chromium-extensions/c/l-V2OR4a7j8).

My project is about [a javascript injector](https://github.com/VanDng/Page-Editor), it supports injecting my own javascript to specific websites I want.

There’re a few things I have to deal with Manifest V3 limitations.

#### Background page is replaced by Service worker

The main fundamental difference is that the service worker is neither intended to be persistent nor worked in a DOM context.

**No more persistency**

The service worker gets woken up by an event it registered then it goes back to sleep when it is done.

Even though the Chrome Extension team lets a small door open that can help to [extend the life span of the service worker](https://stackoverflow.com/questions/66618136/persistent-service-worker-in-chrome-extension), it is not really helpful and reasonable for all cases.

For now, I have to maintain one tab at least and inject a timer that periodically sends an event to the service worker in order to keep it up. Alright, not a big problem.

**No more DOM Context**

Any library requires window do not work with the service worker.

I can not use any DOM-based functions or libraries such as document.getElementById or jQuery any more.

How do I parse HTML? Hmm, I do not need that ability at present. However, my idea is that I will have to pass my HTML source to the content script, it is parsed here and be sent back to the service worker.

#### Content security policy is more strict

As a Chrome browser end-user, it is a security improvement that is good. However, it coincidentally prevents my extension from working properly.

My extension aims to inject custom javascript scripts to target websites. In some scenarios, I need my scripts to be injected as soon as the DOM of target websites is loaded, DOMContentLoaded.

There are two ways to inject scripts: Extension API, Content Script.

**Extension API**

There is an API chrome.scripting.executeScript() that support executing scripts at the runtime. The downside is that it executes scripts at [document\_idle](https://developer.chrome.com/docs/extensions/reference/scripting/#method-executeScript) which means scripts are injected after the event window.onloadevent.

It is too late. I want my scripts to be injected and loaded as soon as DOMContentLoaded.

**Content script**

With the [new content security policy](https://developer.chrome.com/docs/extensions/mv3/intro/mv3-migration/#content-security-policy), I can not append an in-line script tag in the content script’s context anymore.

It still allows a script tag with the source coming from localhost. However, this way, I have to establish a localhost serving script files. Then I have to push all my script files to that localhost and my script tag references to the localhost. It’s too complicated. Moreover, [there’s a bug causing it does work](https://bugs.chromium.org/p/chromium/issues/detail?id=1301301)!

Fortunately, there is still another way. Yes, that’s why I said it’s also interesting. By finding that this way does not work but that way works, I learned a lot during the progress.

I prepare a web\_accessible\_resources script dynamically fetching my custom scripts from the content script via CustomEvent. It works. However, all my scripts are now run in the MAIN world, not the content script's [isolated world](https://developer.chrome.com/docs/extensions/mv3/content_scripts/#:~:text=Content%20scripts%20live%20in%20an,the%20page%20or%20other%20extensions.).

It solved my issue, so far no problem.

  