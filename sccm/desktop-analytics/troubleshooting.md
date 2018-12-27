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

If you think some devices aren't showing in Desktop Analytics, first check the percentage of **Connected devices**. If it's less than 100%, make sure the missing devices are included in your targeted collection. For more information on configuring the target collection, see [Connect Configuration Manager](/sccm/desktop-analytics/connect-configmgr).

Next review the **Connection health** chart. It displays the number of devices in the following health categories:  
<!--need details of what these mean from Bryan-->
- **Properly enrolled**: 

- **Configuration issues**: 

- **Client not installed**: 

- **Waiting for enrollment**: 

- **Missing prerequisites**: 

- **Missing data**: 

Select the category name to remove or add it from the chart. This action helps to zoom the chart so you can see the relative sizes of smaller segments. 

Select one of the chart segments to drill down to a list of devices in this category. This custom device view displays the following Desktop Analytics columns by default:
- Commercial ID configuration
- Minimum compatibility update
- Windows diagnostic data opt-in
- Windows commercial data opt-in
- Windows diagnostic endpoint connectivity
- Office diagnostic endpoint connectivity

These columns correspond to the key [prerequisites](/sccm/desktop-analytics/overview#prerequisites) for devices to communicate with Desktop Analytics. 

![Screenshot of Properly Enrolled device list](media/sccm-device-list-properly-enrolled.png)

Select a device to see the full list of available properties in the detail pane. You can also add any of these properties as columns to the device list. 

### Desktop Analytics device properties in Configuration Manager
<!--need more details from Bryan-->
- Appraiser configuration
- Minimum compatibility update
- Appraiser version
- Appraiser run status
- Last successful full run of Appraiser
- Appraiser data collection
- Census run status
- Last successful full run of Census
- Census data collection
- Windows diagnostic endpoint connectivity
- Check end-user diagnostic data
- Check User Proxy
- Commercial ID configuration
- Windows commercial data opt-in
- Check device name in diagnostic data
- DiagTrack service configuration
- DiagTrack version
- SQM ID retrieval
- Windows diagnostic data opt-in
- Office diagnostic endpoint connectivity



## Log files

Use the following log files to help troubleshoot issues with Desktop Analytics integrated with Configuration Manager. 


### Service connection point

The following log files are on the service connection point in the following directory: `C:\Program Files\Configuration Manager\Logs\M365A`:
<!--waiting details from Bryan-->

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
    DELETE FROM M365AProperties WHERE Name = ‘M365ATenantUpdateInfo_LastUpdateTime’
    ```
4. Restart the **SMS_EXECUTIVE** service on the site server

