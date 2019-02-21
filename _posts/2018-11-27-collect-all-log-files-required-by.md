---
title: "Collect all log files required by Microsoft FailoverDetector.exe"
date: '2018-11-27T06:49:00.000+02:00'
search: true
comments: true
published: true
tags:
  - SQL
  - PowerShell
---

When Microsoft's TigerTeam recently released their Failover Detection Utility I decided to play around with it as something that could make my life easier diagnosing failovers. I quickly released that there is quite a bunch of preparation required collecting all the required logs. So I turned to trusty PowerShell to assist and the exercise turned out both fun an frustrating at times. Nevertheless, I soon had a solution which reliably copied all relevant and required logs for analysis. I wrapped this in a function and adding it to my office PowerShell module for easy referencing. 

This is how it works: 
![powershell import obfuscated.gif]({{site.baseurl}}/assets/images/powershell import obfuscated.gif)


Below the code snippet, also [on github](https://github.com/dhlotter/dhl-scripts/blob/master/powershell/alwayson_Invoke-FailoverDetector.ps1): 

```powershell
function Invoke-FailoverDetector {
<#
Description 
This will copy all information FailoverDetector to work correctly into required folder structure.
Run on a replica participating in the cluster. 
This will only copy records from the last 30 days 
dbawithbeard did this too. https://sqldbawithabeard.com/2018/11/28/gathering-all-the-logs-and-running-the-availability-group-failover-detection-utility-with-powershell/

#>

    If (-NOT([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator"))
    {
        Write-Warning "You do not have Administrator rights to run this script!`nPlease re-run this script as an Administrator!"
        break
    }
    
    ### parameters
    $PathRoot = 'c:\temp\AlwaysOn'

    ### remove previous collected data 
    if (test-path "$PathRoot\FailoverDetector\Data") {
        if ((Get-ChildItem "$PathRoot\FailoverDetector\Data" -Recurse -Directory | Measure-Object | Select-Object -Expand Count) -gt 0) {
            Write-Host "Clean up previous collections. " -foregroundcolor Green
            remove-item "$PathRoot\FailoverDetector\Data" -Recurse 
        }
    }
    $PathRoot = ($PathRoot).TrimEnd('\')

    ### create new folders for project 
    If(!(test-path $PathRoot)) {
        write-host "Create new directories " -foregroundcolor Green
        New-Item -ItemType Directory -Force -Path $PathRoot > $null
    } 

    ### addressing TLS issues when downloading from github
    Write-Host "Fixing TLS issue" -foregroundcolor Green
    $TLSVersion = [Net.ServicePointManager]::SecurityProtocol
    $TLSSupportedVersion = [Math]::Max($TLSVersion.value__, [Net.SecurityProtocolType]::Tls.value__)
    $TLSAvailable = [enum]::GetValues('Net.SecurityProtocolType') | Where-Object {$_ -gt $TLSSupportedVersion}
    $TLSAvailable | ForEach-Object {[Net.ServicePointManager]::SecurityProtocol = [Net.ServicePointManager]::SecurityProtocol -bor $_ }

    ### downloading required Visual C++ Redist 
    $URLVisualCPPRedist = 'https://download.visualstudio.microsoft.com/download/pr/9fbed7c7-7012-4cc0-a0a3-a541f51981b5/e7eec15278b4473e26d7e32cef53a34c/vc_redist.x64.exe'
    if (!(Test-Path -Path "$PathRoot\vc_redist.x64.exe")) {
        Write-Host "Downloading Visual C++ Redist" -foregroundcolor Green
        Invoke-WebRequest -Uri $URLVisualCPPRedist -OutFile "$PathRoot\vc_redist.x64.exe"
    } 
    ### downloading FailoverDetector
    $URLFailoverDetector = 'https://github.com/Microsoft/tigertoolbox/raw/master/Always-On/FailoverDetection/FailoverDetector.zip'
    if (!(Test-Path -path "$PathRoot\FailoverDetector.zip")) {
        Write-Host "Downloading latest FailoverDetector" -foregroundcolor Green
        Invoke-WebRequest -Uri $URLFailoverDetector -OutFile "$PathRoot\FailoverDetector.zip"
    }
    $FileFailoverDetector = $URLFailoverDetector.Split('/')[-1]
    if (!(Test-Path "$PathRoot\FailoverDetector")) {
        Write-Host "Extracting FailoverDetector" -ForegroundColor Green
        Expand-Archive -Path "$PathRoot\$FileFailoverDetector" -DestinationPath "$PathRoot" -Force
    }

    ### installing required pre-requisites 
    if (!(Get-Module FailoverCluster)) {
        write-host "Enabling failover cluster feature" -foregroundcolor Green
        try {
            Install-WindowsFeature -Name Failover-Clustering -IncludeManagementTools  > $null
        }
        catch {
            Write-Warning -Message "Failover cluster feature was not installed. Manually run: Install-WindowsFeature -Name Failover-Clustering -IncludeManagementTools"
            break
        }
    }

    $software = "Microsoft Visual C++ 2017 X64 Minimum Runtime - 14.16.27012"
    $installed = (Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* | `
        Where-Object { $_.DisplayName -eq $software }).DisplayName
    If(-Not $installed) {
        Write-Host "[$software] NOT is installed" -foregroundcolor Green
        Start-Process -FilePath "$PathRoot\vc_redist.x64.exe" -wait 
    } else {
        Write-Host "[$software] is installed" -foregroundcolor Green
    }

    ### collecting logs
    $HostName = HostName
    $PathData = ("\\$HostName\$PathRoot\FailoverDetector\Data").Replace("/","\").Replace(":","$")
    try {
        $ErrorActionPreference = "Stop"; #Make all errors terminating
        $Replicas = (Get-Cluster).Name
    }
    catch {
        Write-Warning -Message "Cluster service is not running or or this server is not part of a cluster"
        break
    }
    finally{
        $ErrorActionPreference = "Continue"; #Reset the error action pref to default
     }
    
    foreach ($Replica in $Replicas)
    {
    #$StartTime = Get-Date
    Write-Host "[$Replica] - Creating folder(s)"  -foregroundcolor Green
    $PathReplica = join-path $PathData $Replica
    If(!(test-path $PathReplica)) {New-Item -ItemType Directory -Force -Path $PathReplica > $null} 

    ### cluster logs 
    #$StartTime = Get-Date
    Write-Host "[$Replica] - Collecting cluster log(s)"  -foregroundcolor Green
    $DaysAgo = 30
    $TimeSpan = ($DaysAgo*1440)
    Get-ClusterLog -Node $Replica -Destination $PathReplica -TimeSpan $TimeSpan > $null
   
    ### system logs 
    $Date = (Get-Date).AddDays(-$DaysAgo)
    Write-Host "[$Replica] - Collecting system log(s)" -foregroundcolor Green
    Get-WinEvent -FilterHashtable @{LogName = 'System'; StartTime = $Date } -ComputerName $Replica -ErrorAction SilentlyContinue | Export-CSV -Path $PathReplica'\'$Replica'_system2.csv'
    #Write-Output "That took: $((Get-Date).Subtract($StartTime).Seconds) second(s)"

    ### collecting alwayson | system_health | ERRORLOG | SQLDUMPER
    # todo filter this output for files in the last x days as well 
    $Date = (Get-Date).AddDays(-$DaysAgo)
    Write-Host "[$Replica] - Collecting AlwaysOn / system_health / ERRORLOG / SQLDUMPER"  -foregroundcolor Green
    $SQLLogDir = (invoke-sqlcmd -ServerInstance $Replica -Query "declare @rootdir nvarchar(500) exec master.dbo.xp_instance_regread N'HKEY_LOCAL_MACHINE', N'SOFTWARE\Microsoft\MSSQLServer\Setup', N'SQLPath', @rootdir OUTPUT SELECT @rootdir as 'RootDirectoryPath';").RootDirectoryPath + '\LOG'
    Copy-Item ("$SQLLogDir\AlwaysOn_health_*.xel" -replace "c:", "\\$Replica\c$") $PathReplica
    Copy-Item ("$SQLLogDir\system_health*.xel" -replace "c:", "\\$Replica\c$") $PathReplica
    Copy-Item ("$sqllogdir\ERRORLOG*" -replace "c:", "\\$Replica\c$") $PathReplica
    if(Test-Path ("$SQLLogDir\SQLDUMPER_ERRORLOG.log" -replace "c:", "\\$Replica\c$")){Copy-Item ("$SQLLogDir\SQLDUMPER_ERRORLOG.log" -replace "c:", "\\$Replica\c$") $PathReplica}
    #    Write-Output "That took: $((Get-Date).Subtract($StartTime).Seconds) second(s)"
    }


    ### dynamically building configuration file 
    Write-Host "Creating a new configuration file. " -ForegroundColor Green
    $String = ForEach ($Replica in $Replicas) {'"' + $Replica.Split('\')[0].Replace('\', '\\') + '",'}
    $String[-1] = $String[-1].Replace(',', '')
    $PathData = ("$PathRoot\FailoverDetector\Data").Replace('\', '\\')
    $JsonConfig = @"
{
    "Data Source Path": "$PathData",
    "Health Level": 3,
    "Instances": [
		$String
    ]
}
"@
    Set-Content -Path "$PathRoot\FailoverDetector\Configuration.json" -Value $JsonConfig 

    ### registering DLL's
    Write-Host "Registering DLL's to prevent unkown exception. " -ForegroundColor Green
    set-location -Path "$PathRoot\FailoverDetector\"
    .\sn.exe -Vr "$PathRoot\FailoverDetector\Microsoft.SqlServer.XE.Core.dll" > $null
    .\sn.exe -Vr "$PathRoot\FailoverDetector\Microsoft.SqlServer.XEvent.Linq.dll" > $null


    Write-Host "Opening result folder. " -ForegroundColor Green
    Invoke-Item "$PathRoot\FailoverDetector\Result"

    Write-Host "Starting FailoverDetector. " -ForegroundColor Green
    Start-Process -FilePath "$PathRoot\FailoverDetector\FailoverDetector.exe" -ArgumentList "--Analyze --Show"

} 

```

~Update: 
Since me doing this of course [Rob 
Sewell](https://twitter.com/@sqldbawithbeard) has also written a something 
similar which is [available on his 
blog.](https://sqldbawithabeard.com/2018/12/01/sql-server-availability-group-failoverdetection-utility-powershell-function-improvements-named-instances-archiving-data-speed/) 
An issue has also been [added to 
dbatools](https://github.com/sqlcollaborative/dbatools/issues/4601) and will 
likely be included and that module in the near future. Looking forward to 
this!
