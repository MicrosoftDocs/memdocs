---
title: "Virtual desktop infrastructure (VDI) client management "
titleSuffix: "Configuration Manager"
description: "Manage System Center Configuration Manager clients in a virtual desktop infrastructure (VDI)."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Considerations for managing System Center Configuration Manager clients  in a Virtual Desktop Infrastructure (VDI)

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager supports installing the Configuration Manager client on the following virtual desktop infrastructure (VDI) scenarios:  

- **Personal virtual machines** - Personal virtual machines are generally used when you want to make sure that user data and settings are maintained on the virtual machine between sessions.  

- **Remote Desktop Services sessions** - Remote Desktop Services enables a server to host multiple, concurrent client sessions. Users can connect to a session and then run applications on that server.  

- **Pooled virtual machines** - Pooled virtual machines are not persisted between sessions. When a session is closed, all data and settings are discarded. Pooled virtual machines are useful when Remote Desktop Services cannot be used because a required business application cannot run on the Windows Server that hosts the client sessions.  

  The following table lists considerations for managing the Configuration Manager client in a virtual desktop infrastructure.  

|Virtual machine type|Considerations|  
|--------------------------|--------------------|  
|Personal virtual machines|Configuration Manager treats personal virtual machines identically to a physical computer. The Configuration Manager client can be preinstalled on the virtual machine image or deployed after the virtual machine is provisioned.|  
|Remote Desktop Services|The Configuration Manager client is not installed for individual Remote Desktop sessions. Instead, the client is only installed one time on the Remote Desktop Services server. All Configuration Manager features can be used on the Remote Desktop Services server.|  
|Pooled virtual machines|When a pooled virtual machine is decommissioned, any changes that you make by using Configuration Manager are lost.<br /><br /> Data returned from Configuration Manager features such as hardware inventory, software inventory and software metering might not be relevant to your needs as the virtual machine might only be operational for a short length of time. Consider excluding pooled virtual machines from inventory tasks.|  

 Because virtualization supports running multiple Configuration Manager clients on the same physical computer, many client operations have a built-in randomized delay for scheduled actions such as hardware and software inventory, antimalware scans, software installations, and software update scans. This delay helps distribute the CPU processing and data transfer for a computer that has multiple virtual machines that run the Configuration Manager client.  

> [!NOTE]  
>  With the exception of Windows Embedded clients that are in servicing mode, Configuration Manager clients that are not running in virtualized environments also use this randomized delay. When you have many deployed clients, this behavior helps avoid peaks in network bandwidth and reduces the CPU processing requirement on the Configuration Manager site systems, such as the management point and site server. The delay interval varies according to the Configuration Manager capability.  
>   
>  The randomization delay is disabled by default for required software updates by using the following client setting: **Computer Agent**: **Disable deadline randomization**.
