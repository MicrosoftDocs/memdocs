---
title: Monitor clients
titleSuffix: Configuration Manager
description: Get detailed guidance on how to monitor clients in Configuration Manager
ms.date: 05/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# How to monitor clients in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Once you install the Configuration Manager client on the Windows devices in your site, monitor their health and activity in the Configuration Manager console.  


## <a name="bkmk_about"></a> About client status

Configuration Manager provides the following types of information as client status:  

- **Client online status**: The site considers a device as **online** if it's connected to its assigned management point. To indicate that the client is online, it sends ping-like messages to the management point. If the management point doesn't receive a message in five minutes, the site considers the client as **offline**.  

- **Client activity**: The site considers the client as **active** if it has communicated with Configuration Manager in the past seven days. The site considers the client **inactive** if it hasn't requested done the following actions in seven days:  

    - Requested policy update  
    - Sent a heartbeat message  
    - Sent hardware inventory  

- **Client check**: The state of the periodic evaluation that the Configuration Manager client runs on the device. The evaluation checks the device and can remediate some of the problems it finds. For more information, see [Client health checks](#BKMK_ClientHealth).  

     On devices that run Windows 7, client check runs as a scheduled task. On later OS versions, client check runs automatically during the Windows maintenance window.  

     You can configure remediation not to run on specific devices, for example, a business-critical server. If there are additional items that you want to evaluate, use Configuration Manager compliance settings to monitor additional configurations. For more information about compliance settings, see [Plan for and configure compliance settings](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

- **Decommissioned**: The site has marked the device record for deletion. This behavior can happen when a new registration for same device assigns to the same or a different primary site in a hierarchy. The site deletes these devices the next time it runs the site maintenance task **Delete Aged Discovery Data**.<!-- SCCMDocs issue #1418 -->  

- **Obsolete**: The site has discovered a new device record with the same hardware ID, so it marks the old record as obsolete. Reports don't count obsolete records of the same device multiple times. You can still target policies to obsolete devices. If the site doesn't get a heartbeat for an obsolete record after 90 days of inactivity, it removes the obsolete device when it runs the site maintenance task **Delete Obsolete Client Discovery Data**.


## <a name="bkmk_indStatus"></a> Monitor individual clients

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select either the **Devices** node or choose a collection under **Device Collections**.  

    The icons at the beginning of each row indicate the online status of the device:  

    |||  
    |-|-|  
    |![online status icon for clients](../../../core/clients/manage/media/online-status-icon.png)|Device is online|  
    |![offline status icon for clients](../../../core/clients/manage/media/offline-status-icon.png)|Device is offline|  
    |![unknown status icon for clients](../../../core/clients/manage/media/unknown-status-icon.png)|Online status is unknown|  
    |![client not installed](../../../core/clients/manage/media/client-not-installed.png)|Client isn't installed on the device|  

2. For more detailed online status, add the client online status information to the device view. Right-click the column header and select the online status fields you want to add:

    - **Device Online Status**: Indicates whether the client is currently online or offline. (This status is the same information given by the icons.)  

    - **Last Online Time**: Indicates when the client online status changed to online  

    - **Last Offline Time** indicates when the status changed to offline  

3. Select an individual client in the list pane to see more status in the detail pane. This information includes client activity and client check status.  


## <a name="bkmk_allStatus"></a> Monitor the status of all clients

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Client Status** node. Review the overall statistics for client activity and client checks across the site. Change the scope of the information by choosing a different collection.  

2. To drill down into detail about the reported statistics, choose the name of the reported information. For example, **Active clients that have passed client check or no results**. Then review the information about the individual clients.  

3. Select **Client Activity** to see charts showing the client activity in your Configuration Manager site.  

4. Select **Client Check** to see charts showing the status of client checks in your Configuration Manager site.  

    Configure alerts to notify you when client check results or client activity drops below a specified percentage. The site can also alert you when remediation fails on a specified percentage of clients. For more information, see [How to configure client status](/sccm/core/clients/deploy/configure-client-status).  


## <a name="BKMK_ClientHealth"></a> Client health checks

Client check runs the following checks and remediations:  

|Client check|Remediation action|More information|  
|------------------|------------------------|----------------------|  
|Verify that client check has recently run|Run client check|Checks that client check has run at least one time in the past three days.|  
|Verify that client prerequisites are installed|Install the client prerequisites|Checks that client prerequisites are installed. Reads the file ccmsetup.xml in the client installation folder to discover the prerequisites.|  
|WMI repository integrity test|Reinstall the Configuration Manager client|Checks that Configuration Manager client entries are present in WMI.|  
|Verify that the client service is running|Start the client (SMS Agent Host) service|No additional information|  
|WMI Event Sink Test.|Restart the client service|Check whether the Configuration Manager related WMI event sink is lost|  
|Verify that the Windows Management Instrumentation (WMI) service exists|No remediation|No additional information|  
|Verify that the client was installed correctly|Reinstall the client|No additional information|  
|Verify that the antimalware service startup type is automatic|Reset the service startup type to automatic|No additional information|  
|Verify that the antimalware service is running|Start the antimalware service|No additional information|  
|Verify that the Windows Update service startup type is automatic or manual|Reset the service startup type to automatic|No additional information|  
|Verify that the client service (SMS Agent Host) startup type is automatic|Reset the service startup type to automatic|No additional information|  
|Verify that the Windows Management Instrumentation (WMI) service is running.|Start the Windows Management Instrumentation service|No additional information|  
|Verify that the Microsoft SQL CE database is healthy|Reinstall the Configuration Manager client|No additional information|  
|Microsoft Policy Platform WMI Integrity Test|Repair the Microsoft Policy Platform|No additional information|  
|Verify that the Microsoft Policy Platform Service exists|Repair the Microsoft Policy Platform|No additional information|  
|Verify that the Microsoft Policy Platform service startup type is manual|Reset the service startup type to manual|No additional information|  
|Verify that the Background Intelligent Transfer Service exists|No Remediation|No additional information|  
|Verify that the Background Intelligent Transfer Service startup type is automatic or manual|Reset the service startup type to automatic|No additional information|  
|Verify that the Network Inspection Service startup type is manual|Reset the service startup type to manual if installed|No additional information|  
|Verify that the Windows Management Instrumentation (WMI) service startup type is automatic|Reset the service startup type to automatic|No additional information|  
|Verify that the Windows Update service startup type on Windows 8 devices is automatic or manual|Reset the service startup type to manual|No additional information|  
|Verify that the client (SMS Agent Host) service exists.|No Remediation|No additional information|  
|Verify that the Configuration Manager Remote Control service startup type is automatic or manual|Reset the service startup type to automatic|No additional information|  
|Verify that the Configuration Manager Remote Control service is running|Start the remote control service|No additional information|  
|Verify that the wake-up proxy service (ConfigMgr Wake-up Proxy) is running|Start the ConfigMgr Wakeup Proxy service|This client check is made only if the **Power Management**: **Enable wake-up proxy** client setting is set to **Yes** on supported client operating systems.|  
|Verify that the wake-up proxy service (ConfigMgr Wake-up Proxy) startup type is automatic|Reset the ConfigMgr Wakeup Proxy service startup type to automatic|This client check is made only if the **Power Management**: **Enable wake-up proxy** client setting is set to **Yes** on supported client operating systems.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## Client deployment log files

For more information about the log files used by client deployment and management operations, see [Log files](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
