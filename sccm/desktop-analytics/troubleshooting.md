---
title: Troubleshooting Desktop Analytics
titleSuffix: Configuration Manager
description: Technical details to help you troubleshoot issues with Desktop Analytics.
ms.date: 12/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Troubleshooting Desktop Analytics

Use the details in this article to help you troubleshoot issues with Desktop Analytics integrated with Configuration Manager.



## Confirm prerequisites

Many common issues are caused by missing prerequisites. First confirm the following configurations:

- [Prerequisites](/sccm/desktop-analytics/overview#prerequisites)  

- [Compatibility updates](/sccm/desktop-analytics/set-up#compatibility-updates)  

- [How to enable data sharing](/sccm/desktop-analytics/enable-data-sharing), which covers the following topics:  

    - Internet endpoints to which clients need to connect  

    - Proxy server authentication  

    - Diagnostic data levels  



## Monitor connection health

Use the **Connection Health** dashboard in Configuration Manager to drill down into categories by device health. In the Configuration Manager console, go to the **Software Library** workspace, expand the **Microsoft 365 Servicing** node, and select the **Connection Health** dashboard.  

![Screenshot of the Configuration Manager Connection Health dashboard](media/connection-health-dashboard.png)

If you think some devices aren't showing in Desktop Analytics, first check the percentage of **Connected devices**. If it's less than 100%, make sure the devices are supported by Desktop Analytics. For more information, see [Prerequisites](/sccm/desktop-analytics/overview#prerequisites).


### Connection health states

Next review the **Connection health** chart. It displays the number of devices in the following health categories:  

- [Properly enrolled](#properly-enrolled)  
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
- [Missing data](#missing-data)  

Select the category name to remove or add it from the chart. This action helps to zoom the chart so you can see the relative sizes of smaller segments. 

#### Properly enrolled
The device has the following attributes:  
- A Configuration Manager client version 1810 or later  
- There are no configuration errors  
- Desktop Analytics received complete diagnostic data from this device in the past 28 days  
- Desktop Analytics has a complete inventory of the device's configuration and installed apps  

#### Configuration issues
Configuration Manager detects one or more issues with the configuration required for Desktop Analytics. For more information, see the list of [Desktop Analytics device properties in Configuration Manager](#bkmk_config-issues).  

#### Client not installed
The device is targeted for Desktop Analytics, but isn't a Configuration Manager client. 

The Configuration Manager client is required to configure and manage the device for Desktop Analytics. For more information, see [Client installation methods](/sccm/core/clients/deploy/plan/client-installation-methods).  

#### Waiting for enrollment
Desktop Analytics doesn't have diagnostic data for this device. This issue can be because the device was recently added to the target collection and hasn't yet sent data. It can also mean the device isn't properly communicating with the service, and the latest diagnostic data is more than 28 days old. 

Make sure the device is able to communicate with the service. For more information, see [Endpoints](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### Missing prerequisites
The Configuration Manager client isn't at least version 1806 (5.0.8740). 

Update the client to the latest version. Consider enabling automatic client upgrade for the Configuration Manager site. For more information, see [Upgrade clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

#### Missing data
Desktop Analytics can't create a compatibility assessment. It doesn't have a complete data set for the device's configuration (census) or installed apps (inventory). 

This issue is often fixed automatically when the device retries. If it persists, make sure the device is able to communicate with the service. For more information, see [Endpoints](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


### Device list

To see a specific list of devices by status, start with the **Connection Health** dashboard. Select one of the segments of the **Connection health** tile and drill down to a list of devices in this category. This custom device view displays the following Desktop Analytics columns by default:
- Commercial ID configuration
- Minimum compatibility update
- Windows diagnostic data opt-in
- Windows commercial data opt-in
- Windows diagnostic endpoint connectivity
- Office diagnostic endpoint connectivity

These columns correspond to the key [prerequisites](/sccm/desktop-analytics/overview#prerequisites) for devices to communicate with Desktop Analytics. 

![Screenshot of Properly Enrolled device list](media/sccm-device-list-properly-enrolled.png)

Select a device to see the full list of available properties in the detail pane. You can also add any of these properties as columns to the device list. 

### <a name="bkmk_config-issues"></a> Desktop Analytics device properties in Configuration Manager

#### Appraiser configuration
<!--not sure which checks this covers-->


#### Minimum compatibility update
<!--32-->
The compatibility update (appraiser.dll) is out of date on the device. It's older than the minimum requirement for Desktop Analytics. 

Install the latest compatibility update. For more information, see [Compatibility updates](/sccm/desktop-analytics/set-up#compatibility-updates).


#### Appraiser version
This property displays the current version of the Appraiser component on the device. It shows the file version on `%windir%\System32\appraiser.dll`, without the decimal points. For example, file version 10.0.17763 displays as 10017763. 


#### Appraiser run status
<!--22-->
This property shows the latest result from the appraiser component. It might show one of the following entries:
- Successful
- Error
- Can't collect app compatibility data (RunAppraiser). Check the logs for details

Check the logs<!--which ones?--> for the exception message and HResult. 

Check for the following file: `%windir%\System32\CompatTelRunner.exe`. If it doesn't exist, reinstall the required [compatibility updates](/sccm/desktop-analytics/set-up#compatibility-updates). Make sure no other system component is removing this file, such as group policy or an antimalware service. 


#### Last successful full run of Appraiser
This property displays the date and time that the device last successfully ran Appraiser.


#### Appraiser data collection
<!--what's the difference between this and Appraiser run status, which seems to have the same errors?-->

#### Census run status
<!--51? 52?-->


#### Last successful full run of Census
This property displays the date and time that the device last successfully ran Census. 

#### Census data collection
<!--what's the difference between this and Census run status? How can this be successful is Census run status shows error?-->


#### Windows diagnostic endpoint connectivity
<!--12, 15-->
If this check is successful, then the device is able to connect to the connected user experience and telemetry endpoint (Vortex). 

Otherwise, it may show one of the following errors:
- Can't connect to the connected user experience and telemetry endpoint (Vortex). Check your network/proxy settings  
- Can't check connectivity to the connected user experience and telemetry endpoint (CheckVortexConnectivity). Check the logs for the exception details<!--which specific logs?-->  

Windows 10 devices verify connectivity with a GET request to `https://v10.vortex-win.data.microsoft.com/health/keepalive`. Windows 7 and Windows 8.1 devices verify connectivity with a GET request to `https://vortex-win.data.microsoft.com/health/keepalive`. 

Make sure the device is able to communicate with the service. For more information, see [Endpoints](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


#### Check end-user diagnostic data
<!--1004?-->

<!-- End user disabled Windows diagnostic data on the device -->


#### Check User Proxy
<!--30, 35?-->

<!-- 
Authentication proxy is enabled. Set DisableEnterpriseAuthProxy to 0 in HKLM\Software\Policies\Microsoft\Windows\DataCollection 

Can't check for the Authentication proxy status. Check the logs for the exception details

-->


#### Commercial ID configuration
<!--9, 11, 53, 64 -->

<!-- 
Failed to write Commercial Id to registry. Error creating or updating registry key: CommercialId at HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection	Can't write the CommercialId to registry key HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection. Check permissions

Function SetupCommercialId failed with an unexpected exception	Can't update the CommercialId in registry key HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection. Check the logs for the exception details

There is a different CommercialID present at the GPO path: HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection. This will take precedence over the CommercialID provided in the script.	Provide the correct CommercialId value at HKLM:\SOFTWARE\Policies\Microsoft \Windows\DataCollection

An error occurred when creating or updating the registry key CommercialDataOptIn at HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection	Can't write CommercialDataOptIn to registry key HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection. Check permissions 
-->


#### Windows commercial data opt-in
<!--?-->


#### Check device name in diagnostic data
<!--58-->

Can't check for the device name to be sent to Microsoft as part of the Windows diagnostic data. Check the logs for the exception details<!-- which specific log? -->


#### DiagTrack service configuration
<!--44, 45, 50-->

- Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements
- Can't find the Connected User Experience and telemetry (diagtrack.dll) component. Check requirements
- Enable and start the Connected User Experiences and Telemetry service to send data to Microsoft
- An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements


#### DiagTrack version
This property displays the current version of the Connected User Experience and Telemetry component on the device. It shows the file version on `%windir%\System32\diagtrack.dll`, without the decimal points. For example, file version 10.0.10242 displays as 10010242. 

#### SQM ID retrieval
<!--38-->

- Can't retrieve the legacy device telemetry identifier (SQM ID)


#### Windows diagnostic data opt-in
<!-- ? -->

#### Office diagnostic endpoint connectivity
<!-- 1001,1002,1003 -->

- Can't connect to the Office diagnostic endpoint (Aria). Check your network/proxy settings
- Can't connect to the Office diagnostic endpoint (Nexusrules). Check your network/proxy settings
- Can't connect to the Office diagnostic endpoint (Nexus). Check your network/proxy settings

Make sure the device is able to communicate with the service. For more information, see [Endpoints](/sccm/desktop-analytics/enable-data-sharing#endpoints).  



## Log files

Use the following log files to help troubleshoot issues with Desktop Analytics integrated with Configuration Manager. 


### Service connection point

The following log files are on the service connection point in the following directory: `C:\Program Files\Configuration Manager\Logs\M365A`:

| Log | Description |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Information about deployment plan sync from Desktop Analytics cloud service to on-premises Configuration Manager |
| **M365ADeviceHealthWorker.log** | Information about device health upload from Configuration Manager to Microsoft cloud |
| **M365AUploadWorker.log** | Information about collection and device upload from Configuration Manager to Microsoft cloud |


### Configuration Manager client

The following log files are on the Configuration Manager client in the following directory: `C:\Windows\CCM\logs`:

| Log | Description |
|---------|---------|
| **M365Handler.log** | Information about the Desktop Analytics settings policy |


### Enable verbose logging 

1. On the service connection point, go to the following registry key: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Set the **LogLevel** value to `0`  
3. Run the following SQL command on the site database:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Restart the **SMS_EXECUTIVE** service on the site server

