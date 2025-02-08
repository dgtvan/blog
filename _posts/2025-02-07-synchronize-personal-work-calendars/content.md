---
layout:	post
title:	"Synchronize Personal and Work calendars"
date:	2025-02-07
---

![📅](calendar.png)  
I have two calendars, one is a company-managed Outlook calendar, another is a Google calendar for personal work.

I choose Google calendar for personal use because I own an iPhone and a Windows PC, I need something can work smoothly on both. It is not convinient to use Apple Calendar on Windows PC, Outlook is great but I also use Gmail as a primary mailbox. Therefore, Google calendar is my best choice.

![📅](problem.png)  
I can neither access the company-managed Outlook calendar from my personal phone nor computer. However, I want to be able to view all my schedules at any time. Time conflict is terrible.

![📅](solution.png)  
There are 3rd party service providers which can combine all calendars into a single one. However, it sounds complicated to me, and I don't prefer 3rd party services in this case.

Instead of that, I found that both Google calendar and Outlook allow me to subscribe to calendars of each other.
- Subscribe Google calendar in Outlook calendar - https://support.microsoft.com/en-us/office/see-your-google-calendar-in-outlook-c1dab514-0ad4-4811-824a-7d02c5e77126  
- Subscribe Outlook calendar in Google calendar - https://support.google.com/calendar/answer/37100?hl=en&co=GENIE.Platform%3DDesktop&sjid=8918504672457931033-NC

The outcome is now I have all schedules in both two personal and work calendars, and be able to access them from any devices.
![](combine-calendar.png)


![](warning.png)  
There is a delay in calendar synchronization, it is around 24 hours for Google calendar, there is no setting to change that - https://support.google.com/calendar/thread/225477597/increase-calendar-sync-frequency?hl=en. If we want the synchronization happens more frenquently, we will need more setup with Google App Script - https://github.com/derekantrican/GAS-ICS-Sync.