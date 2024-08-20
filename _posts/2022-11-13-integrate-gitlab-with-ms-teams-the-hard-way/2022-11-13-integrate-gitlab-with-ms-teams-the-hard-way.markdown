---
layout:	post
title:	"Integrate Gitlab with MS Teams the hard way"
date:	2022-11-13
---

I was working on a new forming development team, there’s a guy raised a question if there is a way to receive notifications from Gitlab so that we don’t need to remind each other to take action on our merge requests.

It sounds normal, there should be tons of people also have asked the same question somewhere else. I found it interesting so I started to find out how.

### Situation

Here is the given situation I have to deal with.

1/ I have no control on Gitlab configuration, which means I can not enable web hook.

2/ I think a bot can help me on this effectively but I fails deploy my bot to MS Teams because it is not a straight deployment. The bot must be going through a review complicated process and get passed before it can be deployed.

3/ Gitlab is running as self-managed instance and hosted inside the corporate network. It requires connections going through a VPN.

### Solution

I give up trying to ask other teams to help on Gitlab configuration and bot deployment as well.

After some tries, I find out **Power Automate** is the right tool that can help me moving forward. Now, when I look back, it’s all so simple but it takes days to figure out surrounding things and make them work together.

1/ Because Gitlab does not enable web hook. I set Power Automate to actively sends requests to Gitlab for updates.

2/ Power Automate has appropriate actions for sending notifications to MS Teams, they are **Post adaptive card to MS Teams** and **Update adaptive card on MS Teams**. It also has HTTP-based actions for communicating with other services such when necessary.

3/ Power Automate can not communicate directly with the self-managed Gitlab because of network barrier. I have to set up a [gateway](https://learn.microsoft.com/en-us/power-automate/gateway-reference), and enable VPN on that gateway. Power Automate has to communicate with the Gitlab via the gateway.

My words can be summarized by the following diagram.

![](1fMFFJlsbxkuVobOn15i8Ag_2.png)

### **Conclusion**

I made it.

![](1FkrH69esZyU-Q68D9zu9dw_2.png)

There’re lots of rooms to improve and add more features.

This article is for myself and those who are looking for something similar but be stuck.

### Reference

https://learn.microsoft.com/en-us/power-automate/gateway-reference