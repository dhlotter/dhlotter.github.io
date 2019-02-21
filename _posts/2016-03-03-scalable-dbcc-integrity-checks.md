---
title: Scalable DBCC Integrity Checks
date: '2016-03-03T16:03:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">I've recently started a new job and have been struggling getting 
all the Redgate SQL Monitor alerts to a happy place. Currently focusing on the 
integrity checks of about 100 servers, many which have multiple databases 
bigger than 1Tb in size. Running integrity checks on these can take well over 
a couple of days and this causes havoc with the underlying storage and 
business logic running during this period. 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;"> 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">I've been a big van of [Ola 
Hallengren's](https://ola.hallengren.com/) Maintenance solution for years. One 
can split the DBCC work into the following: (CHECKDB, CHECKFILEGROUP, 
CHECKTABLE, CHECKALLOC, CHECKCATALOG). In my searches I also came across 
Cus[tomDBCC by Mike 
Eastland](https://www.mssqltips.com/sqlservertip/3485/sql-server-dbcc-checkdb-checkcatalog-and-checkalloc-for-vldbs), 
which as a matter of fact was already implemented on some of these servers by 
fellow team members. Mike's solution hits the sweet spot, you can schedule the 
CHECKTABLE commands independently and provide it with a time limit. In 
essence, it lists all table objects from the list of databases passed into the 
proc and then starts iterating through these tables, updating the start time, 
end time and processed flag. Once the time limit has been exceeded, the 
commands will stop, and when you run the same proc again, it will continue 
where it left off. Nice yes, but I am so invested in the Ola solution and the 
one universal table (CommandLog) where one can query basically all maintenance 
history. So either I update Mike's solution to write to the CommandLog table 
or I update Ola's solution to accept a time limit. I could theoretically 
monitor the running time of and existing job and stop it once it reached a 
certain time, but hat means on my monitoring the job flags as failed. Therefor 
I would like for this logic to reside in the stored proc. 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;"> 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">Lets look at the requirements again: 
1. <span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">Perform integrity checks on all databases 
1. <span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">Schedule CHECKALLOC and CHECKCATALOG in one job and execute 
weekly. 
1. <span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">Schedule second job to perform CHECKTABLE on all tables in all 
databases and execute daily. 
1. <span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">**BONUS!** have the daily CHECKTABLE stop after 3 hours and 
resume the next day where it left off. 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">At the moment I am unable to achieve #4 using Ola's maintenance 
plans, but this is okay and we can work around that (for the time being). We 
can use the OUTPUT parameter from the below proc to get all databases on the 
current instance which can be updated. The reason for doing it this way was to 
account for multiple AlwaysOn availability groups which might or might not be 
read-intent on the current instance. 
<script 
src="https://gist.github.com/dhlotter/ce575e8feedd023bb57737b6f372efac.js"></script> 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">The second proc will cycle through Ola's CommandLog table and 
create a parameter to exclude all tables which have already been checked in 
the last x days. 

<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">And an execution example would like this: 

<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">It is a very neat approach to the issue I have been experiencing. 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;"> 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">Please note, by performing the integrity checks this way the 
dbi_dbccLastKnownGood date is not updated and monitoring solutions like 
RedGate SQL Monitor will report integrity checks overdue. [Only a CHECKDB or 
CHECKFILEGROUP will update this 
date.](http://www.sqlsoldier.com/wp/sqlserver/day22of31daysofdisasterrecoverywhichdbcccheckcommandsupdatelastknowngooddbcc) 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;"> 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">I plan to roll my solution out to the majority of our servers, 
disabling the Redgate monitor and then create a custom alert which will read 
through the CommandLog table and report on any database which have note had 
all tables scanned along with CHECKCATALOG/CHECKALLOC in the last 9 days. 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;"> 
<span style="font-family: &quot;arial&quot; , &quot;helvetica&quot; , 
sans-serif;">Cheers 