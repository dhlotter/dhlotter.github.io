---
title: "SQL 2012 install fails with Microsoft .NET Framework error"
date: "2013-08-30T13:51:00.000+02:00"
search: true
comments: true
published: true
tags:
- sql
---

This happened to me again today, this time with a SQL 2012 install on Windows Server 2012. I did not make a note of the solution last time and as a result forgot what to do. After tons of Star Trek-like deep brain memory recovery, I finally remembered what was required and this time around I'm making a note. 

All we need to do is manually browse to below directory and remove the Microsoft_Corporation folder 
> c:\users\%username%\appdata\local

Or just open an elevated command prompt and execute below. Make sure you [know](http://technet.microsoft.com/en-us/library/bb490990.aspx) what the code do before you execute. 
> rd /S C:\Users\%username%\appdata\local\Microsoft_Corporation

See below error message and dump. 

> Unhandled exception has occurred in your application. If you click Continue, the application will ignore this error and attempt to continue. If you click Quit, the  application will close immediately. 

> An error occurred creating the configuration section handler for userSettings/Microsoft.SqlServer.Configuration.LandingPage.Properties.Settings: Could not load file or assembly 'System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot find the file specified.


And the JIT debug. 
``` See the end of this message for details on invoking  just-in-time (JIT) debugging instead of this dialog box. 
## ********** Exception Text ************** 
 System.Configuration.ConfigurationErrorsException: An error occurred creating the configuration section handler for userSettings/Microsoft.SqlServer.Configuration.LandingPage.Properties.Settings: Could not load file or assembly 'System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot find the file specified. 
(C:Usershermann.lotterAppDataLocalMicrosoft_CorporationLandingPage.exe_StrongName_ryspccglaxmt4nhllj5z3thycltsvyyx11.0.0.0user.config line 5) --->; System.IO.FileNotFoundException: Could not load file or assembly 'System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot find the file specified.  File name: 'System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'  at System.Configuration.TypeUtil.GetTypeWithReflectionPermission(IInternalConfigHost 
host, String typeString, Boolean throwOnError)  at System.Configuration.RuntimeConfigurationRecord.RuntimeConfigurationFactory.Init(RuntimeConfigurationRecord configRecord, FactoryRecord factoryRecord) at 
System.Configuration.RuntimeConfigurationRecord.RuntimeConfigurationFactory.InitWithRestrictedPermissions(RuntimeConfigurationRecord 
configRecord, FactoryRecord factoryRecord) at System.Configuration.RuntimeConfigurationRecord.CreateSectionFactory(FactoryRecord 
factoryRecord) at System.Configuration.BaseConfigurationRecord.FindAndEnsureFactoryRecord(String configKey, Boolean&; isRootDeclaredHere) 
WRN: Assembly binding logging is turned OFF. 
 To enable assembly bind failure logging, set the registry value 
[HKLMSoftwareMicrosoftFusion!EnableLog] (DWORD) to 1. Note: There is some performance penalty associated with assembly bind failure logging. To turn this feature off, remove the registry value [HKLMSoftwareMicrosoftFusion!EnableLog]. 
--- End of inner exception stack trace --- 
```