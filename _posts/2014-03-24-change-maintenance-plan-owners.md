---
title: "Change Maintenance Plan Owners"
date: "2014-03-24T12:46:00.000+02:00"
search: true
comments: true
published: true
tags:
- sql
- imported-post
---

Every now and then I happen upon a maintenance plan which was created under user credentials. As part of the maintenance plan, SQL agent jobs are created which then runs under the plan owner's credentials. To give you context, if I log onto a SQL instance with a username [backupuser] and create a maintenance plan, the SQL agent jobs will all have [backupuser] as their owner as well. Now this can easily be changed in the job, but whenever a change is made to the originating maintenance plan, the SQL agent job owner (that and every other change made to the agent job) will be replaced to the original. 

This is mildly frustrating and can be even more dangerous if the account used was an active directory account and becomes disabled. 

To prevent this from happening, always create maintenance plans with a SQL user which will never be changed/disabled. Sounds familiar? In the below example I show you how to identify maintenance plans created with the indicated user and then subsequently how to update them. I use user [sa] as the owner. 

```sql
-- identify maintenance plans not having sa as the owner
SELECT SUSER_SNAME([ownersid]) AS 'owner', [ownersid], *
FROM [msdb].[dbo].[sysssispackages] 
WHERE [packagetype] = 6 AND [ownersid] <> SUSER_SID('sa') 
   
-- updating these plans
UPDATE [msdb].[dbo].[sysssispackages] 
SET [ownersid] = SUSER_SID('sa') 
WHERE [packagetype] = 6 AND [ownersid] <> SUSER_SID('sa') 

```