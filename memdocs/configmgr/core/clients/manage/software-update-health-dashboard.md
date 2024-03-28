---
title: Troubleshooting dashboard
titleSuffix: Configuration Manager
description: Use a dashboard in the console to view information about the software update health status of clients in your environment.
ms.date: 04/04/2024
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Troubleshooting dashboard

*Applies to: Configuration Manager (current branch)*

<!--17668422 -->

The Troubleshooting dashboard gives you information about different scenarios which needs administrator's attention in your environment at a single glance.

In the Configuration Manager console, go to the **Monitoring** workspace. Expand **Troubleshooting dashboard** node.

# software update health dashboard

You deploy software updates to help secure your environment, but these deployments only reach healthy error free clients. Configuration Manager update errors adversely effect overall compliance. Determining software update errors can be challenging depending upon the error details.

Configuration Manager provides a dashboard with information about the software update deployment status health and common top errors which most of the devices have in every environment. View your overall software update errors, common errors. 

In the Configuration Manager console, go to the **Monitoring** workspace. Expand **Troubleshooting dashboard**, and select the **software udpate health** node.

:::image type="content" source="media/5728069-client-health-dashboard-small.png" alt-text="An example of the updated Client Health Dashboard in version 2111 or later." lightbox="media/5728069-client-health-dashboard.png":::

## Overall software update health

You can browse the **update group** in the dashboard:

:::image type="content" source="media/client-health-dashboard-ribbon.png" alt-text="Browse the update group.":::

When you set the update group, the total number of devices in the collection will be updated, active software update success percentage will be updated. This shows current percentage at the run time.

## Error details for overall clients

The various top error details are covered in this dashboard, If the number is 0 then your environments doesn't have any of these errors:

- Software Distribution - File not Found - 80070002 C80003F3 
- File or folder not accessible --80004005 87D00692 8024402C 80070005  
- Access denied for opening a file or registry - 80070005 
- No space available for installation - 80091007 80070070 
- Missing or damaged file - 8007000D  800B0100  
- Not connected to Windows Update Servers - 8024401B 
- Unable to get content location - 87D00662 
- Update content not available on DP - 80004002 87D00605  
- Update files missing or corrupted - 8007000E 
- Applications with Multiple Versions - 8007066F 
- Missing / Conflicting Boundary - 800705B4 87D00200 
- WUA Not responding - 87D00600  87D00662 
- Disable Branch Cache - 87D00314   87D0027C 

Lets discuss the possible solutions for these errors.

Software Distribution - File not Found - 80070002 C80003F3

```solution
1.  Type CMD in Start Menu and right click the result & run as administrator
2.  Type cmd and press enter
3.  Type net stop wuauserv and press enter
4.  Type rename c:\windows\SoftwareDistribution softwaredistribution.old and press enter
5.  Type net start wuauserv and press enter
6.  Type exit and press enter
7.  Restart the ConfigMgr Agent Service.
8.  Start the Software Update Scan and Deployment Cycles. 
```          

File or folder not accessible --80004005 87D00692 8024402C 80070005  

```solution
1.  Check the WUAHandler.log for Group policy settings were overwritten by a higher authority Error Code 0x87d00692/80004005/8024402C 80070005
2.  Rename C:\Windows\System32\GroupPolicy\Machine\registry.pol
3.  Restart the ConfigMgr Agent Service.
4.  Start the Software Update Scan and Deployment Cycles.
```

Access denied for opening a file or registry - 80070005

```solution
1.  Check the WUAHandler.log for Group policy settings were overwritten by a higher authority Error Code 0x87d00692/80004005/8024402C 80070005
2.  Rename C:\Windows\System32\GroupPolicy\Machine\registry.pol
3.  Restart the ConfigMgr Agent Service.
4.  Start the Software Update Scan and Deployment Cycles.
```

No space available for installation - 80091007 80070070 

```solution
1.  Check whether UpdateDeployment.log has "Update (Site_*/SUM_*) Progress: Status = ciStateError, PercentComplete = *, DownloadSize = *, Result = 0x80091007" .
2.  Check whether CAS.log has "Successfully raised SoftDistHashMismatchEvent event. ContentAccess *
Error: DeleteDirectory:- Failed to delete Directory with Error 0x00000003. ContentAccess *
Releasing content request * ContentAccess *
There are 0 files in the directory compared to * expected files ContentAccess *
3.  If the above conditions are true then the issue can be because of space issue Check the space available in the disk.
4.  If the Space is less try clearing the temporay files to free up space.
5.  Once you complete get free space or you already have space available Start the Software Update Scan and Deployment Cycles.
PS:- the "*" in the log references are variables.
```

Missing or damaged file - 8007000D  800B0100 

```solution
Issue may be related to the windows update agent. Run the Update rediness tool to verify the same.  https://support.microsoft.com/en-in/help/971058/how-do-i-reset-windows-update-components
```

Not connected to Windows Update Servers - 8024401B 

```solution
1.  Check wheether the Windows update log has Proxy specified. If yes continue.
2.  Type CMD in Start Menu and right click the result & run as administrator
3.  Type  netsh winhttp reset proxy
4.  Type net stop wuauserv and press enter
5.  Type rename c:\windows\SoftwareDistribution softwaredistribution.old and press enter
6.  Type net start wuauserv and press enter
7.  Type exit and press enter
8.  Restart the ConfigMgr Agent Service.
9.  Start the Software Update Scan and Deployment Cycles. 
```


## Version tiles

| error details | possible solution |
|---------|---------|
| Software Distribution - File not Found - 80070002 C80003F3 | ```Issue may be related to the windows update agent. Run the Update rediness tool to verify the same.  https://support.microsoft.com/en-in/help/971058/how-do-i-reset-windows-update-components``` |
| :::image type="content" source="media/client-health-dashboard-client-versions-chart.png" alt-text="Client Versions tile with chart on Client health dashboard."::: | :::image type="content" source="media/client-health-dashboard-os-versions.png" alt-text="OS Versions tile with chart on Client health dashboard."::: |


## Next steps

For more information on the client's regular checks to keep healthy, see [Client health checks](client-health-checks.md).

Use the [Surface device dashboard](surface-device-dashboard.md) to see the use of Surface devices in your environment.

