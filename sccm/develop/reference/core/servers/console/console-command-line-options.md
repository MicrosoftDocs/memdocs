---
title: "Console Command-Line Options"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3461eb99-928f-4290-9c18-29a7d73f0e5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration Manager Console Command-Line Options
The Microsoft System Center Configuration Manager console has the following command-line options that are useful to developers.  

|Option|Description|  
|------------|-----------------|  
|**/sms:debugview=1**|A DebugView is included in all ResultViews that specify a view. DebugView shows raw properties (names and values).|  
|**/sms:NamespaceView=1**|Shows namespace view in the System Center Configuration Manager console.|  
|**/sms:ResetSettings**|The System Center Configuration Manager console ignores user persisted connection and view states (Microsoft Management Console window size is not reset).|  
|**/sms:IgnoreExtensions**|Disables any System Center Configuration Manager extensions.|  
|**/sms:NoRestore**|The System Center Configuration Manager console ignores previous persisted node navigation.|  

## See Also  
 [Configuration Manager Console Extension](../../../../../develop/core/servers/console/console-extension.md)   
 [Configuration Manager Programming Fundamentals](../../../../../develop/core/understand/configuration-manager-programming-fundamentals.md)
