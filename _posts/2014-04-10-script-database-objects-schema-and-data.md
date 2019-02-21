---
title: "Script Database Objects (Schema and Data)"
date: "2014-04-10T15:36:00.000+02:00"
search: true
comments: true
published: true
tags:
- sql
- imported-post
---

Every now and then we need to create a full baseline for our current development environment (which is not a backup). Without looking for tools on Google, the easiest way to accomplish this is to use SSMS. 

Just right click on you database and point to *Tasks* > *Generate Scripts...* 

You are greeted with the trusty introduction page which you can just skip through. 
 
In the [**Choose Objects**] window, you can select the objects you would like to script out. In my case I was interested in the entire database. 
 
The important section in this process is the [**Set Scripting Options**] screen. This is 
where we find the advanced button which let us customize a couple of things. So go on hit the [**Advance**] button. 
 
This is where you can change the type of data to script from schema only, data only or schema and data. 

![results](/images/script-database-objects-001.png)

* Click Next/Finish and pick up your scripts in the folder specified. 

![results](/images/script-database-objects-002.png)

![results](/images/script-database-objects-003.png)
