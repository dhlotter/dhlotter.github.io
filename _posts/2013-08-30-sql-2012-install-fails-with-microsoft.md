---
title: SQL 2012 install fails with Microsoft .NET Framework error
date: '2013-08-30T13:51:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

This happened to me again today, this time with a SQL 2012 install on Windows 
Server 2012. I did not make a note of the solution last time and as a result 
forgot what to do. After tons of Star Trek-like deep brain memory recovery, I 
finally remembered what was required and this time around I'm making a note. 

All we need to do is manually browse to below directory and remove the 
Microsoft_Corporation folder 
<pre><span style="font-family: Courier New, Courier, 
monospace;">c:\users\%username%\appdata\local</pre> 
Or just open an elevated command prompt and execute below. Make sure you 
[know](http://technet.microsoft.com/en-us/library/bb490990.aspx) what the code 
do before you execute. 
<pre><span style="font-family: Courier New, Courier, monospace;">rd /S 
C:\Users\%username%\appdata\local\Microsoft_Corporation</pre> 
See below error message and dump. 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://2.bp.blogspot.com/-Opu0dLOqIs8/VHFsl-ZRlsI/AAAAAAABF-E/wDjEgmkJ7y8/s1600/step-1.png" 
height="362" width="400" 
/>](http://2.bp.blogspot.com/-Opu0dLOqIs8/VHFsl-ZRlsI/AAAAAAABF-E/wDjEgmkJ7y8/s1600/step-1.png) 
<pre><span style="font-family: Courier New, Courier, monospace;">Unhandled 
exception has occurred in your application. If you click Continue, the  
application will ignore this error and attempt to continue. If you click Quit, 
the  application will close immediately. 

An error occurred creating the configuration section handler for 
userSettings/Microsoft.SqlServer.Configuration.LandingPage.Properties.Settings: 
Could not load file or assembly 'System, Version=4.0.0.0, Culture=neutral, 
PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot 
find the file specified.</pre> 


And the JIT debug. 
<pre>See the end of this message for details on invoking 
 just-in-time (JIT) debugging instead of this dialog box. 
## ********** Exception Text ************** 
 System.Configuration.ConfigurationErrorsException: An error occurred creating 
the configuration section handler for 
userSettings/Microsoft.SqlServer.Configuration.LandingPage.Properties.Settings: 
Could not load file or assembly 'System, Version=4.0.0.0, Culture=neutral, 
PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot 
find the file specified. 
(C:Usershermann.lotterAppDataLocalMicrosoft_CorporationLandingPage.exe_StrongName_ryspccglaxmt4nhllj5z3thycltsvyyx11.0.0.0user.config 
line 5) ---&gt; System.IO.FileNotFoundException: Could not load file or 
assembly 'System, Version=4.0.0.0, Culture=neutral, 
PublicKeyToken=b77a5c561934e089' or one of its dependencies. The system cannot 
find the file specified. 
 File name: 'System, Version=4.0.0.0, Culture=neutral, 
PublicKeyToken=b77a5c561934e089' 
 at 
System.Configuration.TypeUtil.GetTypeWithReflectionPermission(IInternalConfigHost 
host, String typeString, Boolean throwOnError) 
 at 
System.Configuration.RuntimeConfigurationRecord.RuntimeConfigurationFactory.Init(RuntimeConfigurationRecord 
configRecord, FactoryRecord factoryRecord) 
 at 
System.Configuration.RuntimeConfigurationRecord.RuntimeConfigurationFactory.InitWithRestrictedPermissions(RuntimeConfigurationRecord 
configRecord, FactoryRecord factoryRecord) 
 at 
System.Configuration.RuntimeConfigurationRecord.CreateSectionFactory(FactoryRecord 
factoryRecord) 
 at 
System.Configuration.BaseConfigurationRecord.FindAndEnsureFactoryRecord(String 
configKey, Boolean&amp; isRootDeclaredHere) 
WRN: Assembly binding logging is turned OFF. 
 To enable assembly bind failure logging, set the registry value 
[HKLMSoftwareMicrosoftFusion!EnableLog] (DWORD) to 1. 
 Note: There is some performance penalty associated with assembly bind failure 
logging. 
 To turn this feature off, remove the registry value 
[HKLMSoftwareMicrosoftFusion!EnableLog]. 
--- End of inner exception stack trace --- 
 at 
System.Configuration.BaseConfigurationRecord.FindAndEnsureFactoryRecord(String 
configKey, Boolean&amp; isRootDeclaredHere) 
 at System.Configuration.BaseConfigurationRecord.GetSectionRecursive(String 
configKey, Boolean getLkg, Boolean checkPermission, Boolean getRuntimeObject, 
Boolean requestIsHere, Object&amp; result, Object&amp; resultRuntimeObject) 
 at System.Configuration.BaseConfigurationRecord.GetSection(String configKey) 
 at 
System.Configuration.ClientConfigurationSystem.System.Configuration.Internal.IInternalConfigSystem.GetSection(String 
sectionName) 
 at System.Configuration.ConfigurationManager.GetSection(String sectionName) 
 at System.Configuration.ClientSettingsStore.ReadSettings(String sectionName, 
Boolean isUserScoped) 
 at 
System.Configuration.LocalFileSettingsProvider.GetPropertyValues(SettingsContext 
context, SettingsPropertyCollection properties) 
 at 
System.Configuration.SettingsBase.GetPropertiesFromProvider(SettingsProvider 
provider) 
 at System.Configuration.SettingsBase.GetPropertyValueByName(String 
propertyName) 
 at System.Configuration.SettingsBase.get_Item(String propertyName) 
 at System.Configuration.ApplicationSettingsBase.GetPropertyValue(String 
propertyName) 
 at System.Configuration.ApplicationSettingsBase.get_Item(String propertyName) 
 at 
Microsoft.SqlServer.Configuration.LandingPage.LandingPageForm.OnLoad(EventArgs 
e) 
 at System.Windows.Forms.Control.CreateControl(Boolean fIgnoreVisible) 
 at System.Windows.Forms.Control.CreateControl() 
 at System.Windows.Forms.Control.WmShowWindow(Message&amp; m) 
 at System.Windows.Forms.Control.WndProc(Message&amp; m) 
 at System.Windows.Forms.Control.ControlNativeWindow.WndProc(Message&amp; m) 
 at System.Windows.Forms.NativeWindow.Callback(IntPtr hWnd, Int32 msg, IntPtr 
wparam, IntPtr lparam) 
 ************** Loaded Assemblies ************** 
 mscorlib 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/Microsoft.NET/Framework64/v2.0.50727/mscorlib.dll 
 ---------------------------------------- 
 LandingPage 
 Assembly Version: 11.0.0.0 
 Win32 Version: 11.0.2100.60 ((SQL11_RTM).120210-1917 ) 
 CodeBase: 
file:///C:/Program%20Files/Microsoft%20SQL%20Server/110/Setup%20Bootstrap/SQLServer2012/x64/LandingPage.exe 
 ---------------------------------------- 
 System.Windows.Forms 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/assembly/GAC_MSIL/System.Windows.Forms/2.0.0.0__b77a5c561934e089/System.Windows.Forms.dll 
 ---------------------------------------- 
 System 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/assembly/GAC_MSIL/System/2.0.0.0__b77a5c561934e089/System.dll 
 ---------------------------------------- 
 System.Drawing 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/assembly/GAC_MSIL/System.Drawing/2.0.0.0__b03f5f7f11d50a3a/System.Drawing.dll 
 ---------------------------------------- 
 Microsoft.SqlServer.Configuration.Sco 
 Assembly Version: 11.0.0.0 
 Win32 Version: 11.0.2100.60 ((SQL11_RTM).120210-1917 ) 
 CodeBase: 
file:///C:/Program%20Files/Microsoft%20SQL%20Server/110/Setup%20Bootstrap/SQLServer2012/x64/Microsoft.SqlServer.Configuration.Sco.DLL 
 ---------------------------------------- 
 Microsoft.SqlServer.Chainer.Infrastructure 
 Assembly Version: 11.0.0.0 
 Win32 Version: 11.0.2100.60 ((SQL11_RTM).120210-1917 ) 
 CodeBase: 
file:///C:/Program%20Files/Microsoft%20SQL%20Server/110/Setup%20Bootstrap/SQLServer2012/x64/Microsoft.SqlServer.Chainer.Infrastructure.DLL 
 ---------------------------------------- 
 Microsoft.SqlServer.Deployment 
 Assembly Version: 11.0.0.0 
 Win32 Version: 11.0.2100.60 ((SQL11_RTM).120210-1917 ) 
 CodeBase: 
file:///C:/Program%20Files/Microsoft%20SQL%20Server/110/Setup%20Bootstrap/SQLServer2012/x64/Microsoft.SqlServer.Deployment.DLL 
 ---------------------------------------- 
 System.Xml 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/assembly/GAC_MSIL/System.Xml/2.0.0.0__b77a5c561934e089/System.Xml.dll 
 ---------------------------------------- 
 Accessibility 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/assembly/GAC_MSIL/Accessibility/2.0.0.0__b03f5f7f11d50a3a/Accessibility.dll 
 ---------------------------------------- 
 Microsoft.SqlServer.Management.Controls 
 Assembly Version: 11.0.0.0 
 Win32 Version: 11.0.2100.60 ((SQL11_RTM).120210-1917 ) 
 CodeBase: 
file:///C:/Program%20Files/Microsoft%20SQL%20Server/110/Setup%20Bootstrap/SQLServer2012/x64/Microsoft.SqlServer.Management.Controls.DLL 
 ---------------------------------------- 
 System.Configuration 
 Assembly Version: 2.0.0.0 
 Win32 Version: 2.0.50727.6387 (Win8RTM.050727-6300) 
 CodeBase: 
file:///C:/Windows/assembly/GAC_MSIL/System.Configuration/2.0.0.0__b03f5f7f11d50a3a/System.Configuration.dll 
 ---------------------------------------- 
## ********** JIT Debugging ************** 
 To enable just-in-time (JIT) debugging, the .config file for this 
 application or computer (machine.config) must have the 
 jitDebugging value set in the system.windows.forms section. 
 The application must also be compiled with debugging 
 enabled. 
For example: 
&lt;configuration&gt; 
 &lt;system.windows.forms jitDebugging="true" /&gt; 
 &lt;/configuration&gt; 
When JIT debugging is enabled, any unhandled exception 
 will be sent to the JIT debugger registered on the computer 
 rather than be handled by this dialog box.</pre> 