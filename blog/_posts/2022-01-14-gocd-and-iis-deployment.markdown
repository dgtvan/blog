---
layout:	post
title:	"GoCD and IIS Deployment"
date:	2022-01-14
---

  Those who have never touched CICD apps or specifically GoCD probably think CDCI is somewhat magic but it is not. Simply put, CICD apps help to automate procedures that you can do using the command line. Given a task you can not complete by the command line, CICD apps do not.

In addition, some apps are categorized as CD only, CI only, or CICD. Do not pay much attention to that now. It does not matter. I usually name them all CICD.

The article begins with my own explanation of CICD because I found there are people who seem not to understand correctly about CICD apps, which leads to problems that they have no clues on how to deal with.

Here is a question of a guy on the internet, he set up a CICD with the GoCD app and got a problem with deployment.

![](/img/1WlFO6Hh_P0q9QbpyyzXhyg_2.png)Cedric asked, “How do I deploy [a website package] to the IIS Web Server [using GoCD]?”.

Aravind gave a great answer but general. I still want to give more details as well as an example for this question.

Before answering that question, he has to answer another question “How do I deploy to the IIS Web Server **using the command line**?”

Supposedly, we have deployment steps and corresponding approaches below:

**1/ Prepare the package.**  
- Without GoCD: For .NET projects, we can build projects with the command line “dotnet build”.  
- With GoCD: We set up a GoCD Agent to checkout source code and execute the command line “dotnet build” to build a package. Then, push the package to the GoCD Server.

**2/ Copy the package to the web server.  
**- Without GoCD: Connect to the web server and transfer the package.  
- With GoCD: We install a GoCD Agent on the web server and set that agent to fetch the package from the GoCD Server.

**3/ Stop IIS on the web server.  
**- Without GoCD: On the web server, we can execute the command line “appcmd stop apppool <AppName>” to stop our app pool.  
- With GoCD: We set up the GoCD Agent on the web server to execute the command line “appcmd stop appool <AppName>”.

**4/ Extract the package to the website’s folder.  
**- Without GoCD: We execute the command line of copying the package to the website’s folder.  
- With GoCD: We set up the GoCD Agent on the web server to execute the command line of copying the package to the website’s folder.

**5/ Start IIS on the web server.  
**- Without GoCD: On the web server, we can execute the command line “appcmd start apppool <AppName>” to stop our app pool.  
- With GoCD: We set up the GoCD Agent on the web server to execute the command line “appcmd start appool <AppName>”.

For each step, I can find a way to do it with a command line, then I configure the GoCD to do the same.

The concept of Server and Agent is fundamental in the world of CICD. You may need to take a little time to play with it to get to understand it.

Clearly, I am only limited by the possibility of doing something with a command line, not the GoCD or any CICD apps in general.

  