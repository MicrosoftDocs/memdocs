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
ms.topicc: troubleshooting-general
---

# Troubleshooting dashboard

*Applies to: Configuration Manager (current branch)*

<!--17668422 -->

The Troubleshooting dashboard gives you information about different scenarios, which needs administrator's attention in your environment at a single glance.

In the Configuration Manager console, go to the **Monitoring** workspace. Expand **Troubleshooting dashboard** node.

:::image type="content" source="media/17668422-Troubleshooting-dashboard.png" alt-text="Screenshot of an example of the updated Troubleshooting Dashboard in version 2403 or later." lightbox="media/17668422-Troubleshooting-dashboard.png":::

## Software update health dashboard

You deploy software updates to help secure your environment, but these deployments only reach healthy error free clients. Configuration Manager update errors adversely affect overall compliance. Determining software update errors can be challenging depending upon the error details.

Configuration Manager provides a dashboard with information about the software update deployment status health and common top errors, which most of the devices have in their environment. View your overall software update errors, common errors. 

In the Configuration Manager console, go to the **Monitoring** workspace. Expand **Troubleshooting dashboard**, and select the **software update health** node.

:::image type="content" source="media/17668422-software-update-health.png" alt-text="Screenshot of an example of the updated Software update Health Dashboard in version 2403 or later." lightbox="media/17668422-software-update-health.png":::

### Overall software update health

You can browse the **update group** in the dashboard:

When you set the update group, the total number of devices in the collection, active software update success percentage is updated. This shows current percentage compliance for the update group at the run time.

### Error details for overall clients

The various top error details are covered in this dashboard, If the number is 0 then your environments doesn't have any of these errors:

- Software Distribution - File not Found       -(80070002, C80003F3) 
- File or folder not accessible                -(80004005, 87D00692, 8024402C, 80070005)  
- Access denied for opening a file or registry -(80070005) 
- No space available for installation          -(80091007, 80070070) 
- Missing or damaged file                      -(8007000D, 800B0100)  
- Not connected to Windows Update Servers      -(8024401B) 
- Unable to get content location               -(87D00662) 
- Update content not available on DP           -(80004002, 87D00605)  
- Update files missing or corrupted            -(8007000E) 
- Applications with Multiple Versions          -(8007066F) 
- Missing / Conflicting Boundary               -(800705B4, 87D00200)
- WUA Not responding                           -(87D00600, 87D00662)
- Disable Branch Cache                         -(87D00314, 87D0027C) 

### Lets discuss the possible solutions for these errors.

| Error details | Possible solution |
|---------|---------|
| Software Distribution - File not Found -(80070002, C80003F3)                                | 1.  Type CMD in Start Menu and right click the result & run as administrator. <br> 2. Type cmd and press enter. <br> 3. Type net stop wuauserv and press enter.<br> 4. Type rename c:\windows\SoftwareDistribution softwaredistribution.old and press enter.<br> 5. Type net start wuauserv and press enter.<br> 6. Type exit and press enter.<br> 7. Restart the ConfigMgr Agent Service.<br> 8. Start the Software Update Scan and Deployment Cycles.<br> |
| File or folder not accessible - (80004005 87D00692 8024402C 80070005)                       | 1. Check the WUAHandler.log for Group policy settings were overwritten by a higher authority Error Code 0x87d00692.<br> 2. Rename C:\Windows\System32\GroupPolicy\Machine\registry.pol<br> 3. Restart the ConfigMgr Agent Service.<br> 4. Start the Software Update Scan and Deployment Cycles.<br> |
| Access denied for opening a file or registry - (80070005)                                   | 1. Check the WUAHandler.log for Group policy settings were overwritten by a higher authority Error Code 0x87d00692.<br> 2. Rename C:\Windows\System32\GroupPolicy\Machine\registry.pol<br> 3. Restart the ConfigMgr Agent Service.<br> 4. Start the Software Update Scan and Deployment Cycles.<br> |
| No space available for installation -(80091007, 80070070)                                   | 1. Check whether UpdateDeployment.log has "Update (Site_*/SUM_*) Progress: Status = ciStateError, PercentComplete = *, DownloadSize = *, Result = 0x80091007".<br> 2. Check whether CAS.log has "Successfully raised SoftDistHashMismatchEvent event. ContentAccess * Error: DeleteDirectory:- Failed to delete Directory with Error 0x00000003. ContentAccess * Releasing content request * ContentAccess * There are 0 files in the directory compared to * expected files ContentAccess *<br> 3. If the above conditions are true, then the issue can be because of space issue Check the space available in the disk.<br> 4. If the Space is less try clearing the temporary files to free up space.<br> 5.  Once you complete get free space or you already have space available Start the Software Update Scan and Deployment Cycles.<br> Note:- the "*" in the log references are variables.<br> |
| Missing or damaged file -(8007000D, 800B0100)                                    | Issue may be related to the windows update agent. Run the Update readiness tool to verify the same.  https://support.microsoft.com/en-in/help/971058/how-do-i-reset-windows-update-components |
| Not connected to Windows Update Servers -(8024401B)                              | 1. Check whether the Windows update log has Proxy specified. If yes continue.<br> 2. Type CMD in Start Menu and right click the result & run as administrator.<br> 3. Type  netsh winhttp reset proxy.<br> 4. Type net stop wuauserv and press enter.<br> 5. Type rename c:\windows\SoftwareDistribution softwaredistribution.old and press enter.<br> 6. Type net start wuauserv and press enter.<br> 7. Type exit and press enter.<br> 8. Restart the ConfigMgr Agent Service.<br> 9. Start the Software Update Scan and Deployment Cycles.<br> |
| Unable to get content location -(87D00662)                                       | 1. Restart Windows Update Agent.<br> 2. Restart SMS Agent.<br> 3. Initiate the Update Evaluation Cycle.<br> |
| Update content not available on DP -(80004002, 87D00605)                         | 1.  Check whether the UpdatesHandler.log has the following entries. WSUS update (689c410a-44d7-45c7-ae51-9806fcb177f5) installation result = 0x80004002, Reboot State = NoReboot Update execution failed.<br> 2. Check whether the WUAHandler.log has the following entries Failed to get final installation result of updates. Error = 0x80004002. Update 1 (unique update id) finished installing (0x80004002). Update 2 (unique update ID) finished installing (0x80004002). Installation of updates completed.<br> 3. Check whether the WUAHandler.log has "WARNING: WU client failed to install updates with error 0x80004002"<br> 4. The WUA installation on the client might be missing files or be corrupt. Reinstall WUA (https://blogs.technet.microsoft.com/enterprisemobility/2014/07/14/how-to-install-the-windows-update-agent-on-client-computers/)<br> 5. Restart the ConfigMgr Agent Service.<br> 6. Start the Software Update Scan and Deployment Cycles. <br> |
| Update files missing or corrupted -(8007000E)                                    | 1. Open Command prompt as administrator execute the commands on the given sequence.<br>  a. Net stop wuauserv <br> b. Sc config wuauserv type= own<br>  c. Net start wuauser<br> |
| Applications with Multiple Versions -(8007066F)                                  | 1. Find the update getting failed and check the client has different versions of the application getting updated.<br> 2. If the client has different versions of the application Open the Registry editor.<br> 3. Navigate to the following registry keys HKEY_USERS\.DEFAULT\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders.<br> 4. The correct and default value for AppData should be: %USERPROFILE%\AppData\Roaming<br> 5. Close the Registry editor, and try again Windows Update again. (A reboot shouldn't be required.)<br> 6. If the problem persists, repeat the steps 3 through 5 with the following registry keys: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\ HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\<br>  | 
| Missing / Conflicting Boundary -(800705B4, 87D00200)                             | 1. Add Missing IP Subnets to Boundary |
| WUA Not responding -(87D00600, 87D00662)                                         | 1. Restart Windows Update Agent.<br> 2. Restart SMS Agent.<br> 3. Initiate the Update Evaluation Cycle.'<br> |
| Disable Branch Cache -(87D00314, 87D0027C)                                       | 1. Restart BITS.<br> 2. Disable Branch Cache(HKLM\Software\Policies\Microsoft\PeerDist\Service.<br> 3. Start the Update Evaluation cycle'<br> |

In the Configuration Manager console, go to the **Monitoring** workspace. Expand **Troubleshooting dashboard**, select the **software update health** node and select the **Software Distribution - File not Found -80070002, C80003F3**.

:::image type="content" source="media/17668422-error-software-dist-file-error.png" alt-text="Screenshot of an example of the error devices in version 2403 or later." lightbox="media/17668422-error-software-dist-file-error.png":::

You can export the devices or create collection to perform manual remediation to these devices.

### Next steps

In future releases, we add remediation for few issues. 
