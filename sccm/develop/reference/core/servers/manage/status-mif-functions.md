---
title: "Status MIF Functions"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 57b8ea8c-7cbd-45d1-8b68-a5ff817f2aa1searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Status MIF Functions
In System Center Configuration Manager, status MIF functions are provided in separate libraries to create a status Management Information Format (MIF) file. For more information about how the install status MIF file is used by System Center Configuration Manager, see [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md).  

 Success or failure of an advertisement is determined by using either an install status MIF file or the exit code of the advertised program. Relying on the exit code limits the visibility of events during the installation process and requires interpretation of the various exit codes. However, using the install status MIF file provides an enhanced status indicating whether the installation succeeded or failed, and it includes an appropriate description.  

## Status MIF Functions  

-   [Create Function](../../../../../develop/reference/core/servers/manage/create-function.md)  

-   [InstallStatusMIF Function](../../../../../develop/reference/core/servers/manage/installstatusmif-function.md)  

-   [InstallStatusMIFEx Function](../../../../../develop/reference/core/servers/manage/installstatusmifex-function.md)  

## See Also  
 [Configuration Manager Status](../../../../../develop/reference/core/servers/manage/status-classes.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
