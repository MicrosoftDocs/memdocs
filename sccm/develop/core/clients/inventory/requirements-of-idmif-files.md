---
title: "Requirements of IDMIF files"
ms.custom: ""
ms.date: "2017-1-03"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 089b823d-2532-46da-9d33-1d269a5adf03searchScope: - ConfigMgr SDK
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Requirements of IDMIF files
Two delta header comments are required for an IDMIF file. Other comments are optional. The comments you must include are:

-   The name of the architecture you want to create or modify: //Architecture<*ArchitectureName*>

-   A unique ID for this instance: //UniqueID<*UniqueID*>

The unique ID can be any unique ID. Each architecture has one or more instances within the SMS site database. The unique ID is the key for this specific instance.

Also, although it is not required, you should use the agent name, especially with a large or complicated custom MIF file that might be updated by more than one agent: //AgentID<*AgentName*>

If you do not include this attribute, hardware inventory might overwrite the information your IDMIF file places in the SMS site database.

The agent name enables you to independently create and modify the **System** architecture. Others who modify the architecture can use a different agent name. They can then remove or modify the parts of the architecture that are associated with that agent, independently of the modifications of other agents.

There is another requirement of any IDMIF file. Whenever you create an IDMIF file, you must include a group within the IDMIF file with the same class name as the architecture you are creating or modifying. This group is known as the top-level group.

Also, if you create any class that has more than one instance, you must include at least one key value within the class, to avoid having each instance overwrite previous instances.

> [!IMPORTANT]
> The formatting of the comments must be exactly the same as that given here. The only part that you can change is the part in italics. The < and > characters must be included.

IDMIF files must be stored in the following folder on Advanced Clients: *%Windir%\System32\CCM\Inventory\Idmifs*

IDMIF files must be stored in the following folder on Legacy Clients: *%Windir%\MS\SMS\Idmifs*

The safest method on both clients is to use the folder the following registry key points to:

**HKLM\Software\Microsoft\SMS\Client\Configuration\Client Properties\IDMIF Directory**

The following is an example of a simple IDMIF file:

```

//Architecture<System>
//UniqueID<3b93b13a-afb4-40cf-86d4-3ad1aaaa8414>

Start Component
    Name = "Workstation"
    Start Group
        Name = "System"
        ID = 1
        Class = "System"
        Key = 1,2,3
            Start Attribute
                Name = "Name"
                ID = 1
                Access = READ-ONLY
                Storage = Specific
                Type = String(255)
                Value = "MachineName8d16380a-3928-4ef1-b4f3-fdc557d4af9b"
            End Attribute
            Start Attribute
                Name = "SMSID"
                ID = 2
                Access = READ-ONLY
                Storage = Specific
                Type = String(255)
                Value = "8d16380a-3928-4ef1-b4f3-fdc557d4af9b"
            End Attribute
            Start Attribute
                Name = "SystemType"
                ID = 3
                Access = READ-ONLY
                Storage = Specific
                Type = String(255)
                Value = "Test Type"
            End Attribute
    End Group

```  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Inventory](../../../../develop/core/clients/inventory/inventory.md)   
 [About Configuration Manager Inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md)   
 [How to Configure Hardware Inventory Settings](../../../../develop/core/clients/inventory/how-to-configure-hardware-inventory-settings.md)
