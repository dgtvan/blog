---
layout:	post
title:	"GoCD does not seem to work with Apps having GUI ?"
date:	2022-04-01
---

  Once I integrated my small app with GoCD on my personal computer. There was nothing special, I make GoCD to build and execute the app when there is new changes from repository.

My app had a window, the window should have been shown up right away when the app started. GoCD did not show any error, everything was completely fine, unfortunately, the window was not shown up as expected even though the app was running.

I spent 2 days to looking for a fix on Google, I literally visited every page but I had no luck. Eventually, I had to create an issue on the GoCD’s github to seek help.

Finally, I got an answer from one of the project’s developers. The app’s window was not shown up due to GoCD was running as SYSTEM, so I had to run GoCD as User to fix the problem.

Visit the link below for the detail of the issue as well as related information  
[UI-based programs are not shown up after executed by a Custom Command task on Windows Agents](https://github.com/gocd/gocd/issues/9990)

  