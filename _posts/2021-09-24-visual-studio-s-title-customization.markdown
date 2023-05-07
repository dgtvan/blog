---
layout:	post
title:	"Visual Studio’s Title Customization"
date:	2021-09-24
---

  ### I. Problem

I usually open multiple instances of Visual Studio to ease the reference and quickly switch between bug fixes.

There’s a situation where I have different GIT branches checked out, they are from the same repo so the solution name and source code structure are likely the same. At the moment, I want to open a few of them with different Visual Studio instances, after that the problem comes in not too long.

![](/img/1J5tVrwvq6jTXLtGzrr88Qw_2.png)After a few switching between Visual Studio windows, I suddenly get lost. The name of all opening solutions is the same, then I do not know where I am at the moment, I simply can not determine which Visual Studio window belongs to which solution.

![](/img/1Nh_bULRPCP1ra4Y8NzM1ug_2.png)![](/img/1HTdmBykRiZxSkpQ0jdl08g_2.png)How can I get out of this? Two ways:  
(1) Hover to any file opening tab to view the solution path.  
(2) Right-click on the solution and open the solution folder to view the solution path.

![](/img/1HRLPCSWOPtbz1rq7A_mgxw_2.png)The thing in common is that I use the solution’s parent folder name to identify.

### II. Solution

Straight to the point, I want to show the solution’s parent folder name on the Visual Studio’s title.

Follow the steps below:  
**1. Download & install this extension:**  
 — Name: Customize Visual Studio Window Title  
 — Link: <https://marketplace.visualstudio.com/items?itemName=mayerwin.RenameVisualStudioWindowTitle>

**2. Disable the compact title feature on the Visual Studio.**  
It depends on the Visual Studio version you are using, the option might be available or not. If the option is available, you will have to uncheck it.

Here are the steps:  
 — Go to Tools / Options.  
 — Uncheck the option “Use compact menu & search bar…”.  
 — Restart the Visual Studio.

![](/img/1HCg75vATD0doUcmDvamOvw_2.png)**3. Customize your Visual Studio’s title**  
 — Go to Tools / Options again.   
 — Find the option “Customize VS Window Title” (1), and explore its available customizations, it’s quite simple so I do not go into detail.  
 — Here I show you my settings, take a look at the (2) and (3).

![](/img/1OXgGwEfblCRKN5BWIOCkCg_2.png)### III. Demonstration

Here is what you get after all.

— The taskbar:

![](/img/1Ceevf4GbAdLRP0gxUNwaUw_2.png)— The Visual Studio window’s title:

![](/img/1IqVLUkctbuN9Kc30eGYl0g_2.png)  