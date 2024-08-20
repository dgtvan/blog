---
layout:	post
title:	"IIS Configuration Changes Always Get Reverted"
date:	2021-12-31
---

Once I am asked to config IIS to deny all OPTIONS requests.

Below are steps I take:  
1/ Open IIS.  
2/ Navigate to the target website.  
3/ Open Request Filtering configuration.  
4/ Add a new rule to deny OPTIONS requests.

All OPTIONS requests are now denied. It works as expected, IIS seems to be configured correctly.

Later, after a few deployments, our team recognized that OPTIONS requests are allowed again.

I check my configuration in IIS. The rule I added is not there, it is gone. What happened?

There is a thing I did not know. IIS has two configuration levels:

1/ IIS level  
A configuration set at the IIS level applies to all websites.

![](127kzObVVFie1JBMFw9f2TQ_2.png)

2/ Website level  
- A configuration set at the website level applies only to a certain website.  
- The IIS level configurations will be overwritten by the website level.  
- **Configurations are stored in a web.config file.**

![](1lh3ajWX9xcTBwHaYGWb9tw_2.png)Website level configurationAs you may guess what the problem is.

For each new deployment I manually copy and paste all new files (a web.config file included) to the target website’s deployment folder, all files should be overwritten. Hence, any configuration stored in the web.config file via IIS is removed.

There are a few solutions:

1/ Reflect changes from IIS to the source code’s repository where packages are generated from. It is reasonable but some people do not want to do it. Sometimes, the one who deploys a new package is not a person having the right to access the repository.

Move on.

2/ Configure IIS at the IIS level. It is simple, only do one time and forget.

It is reasonable but I feel we are losing control of something. Personally, I do not like this solution.

Anyway, it is chosen.