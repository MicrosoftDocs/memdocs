---
title: Client health checks
titleSuffix: Configuration Manager
description: The checks that the Configuration Manager client runs regularly to keep healthy.
ms.date: 11/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Client health checks

*Applies to: Configuration Manager (current branch)*

The Configuration Manager client regularly runs the following checks and remediations to keep healthy.

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
|Verify that the Microsoft SQL Server Compact Edition database is healthy|Reinstall the Configuration Manager client|No additional information|
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
