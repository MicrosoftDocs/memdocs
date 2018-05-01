---
title: "Bit Field Properties"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b2e8a746-7b57-4381-87a1-c49d9434811a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration Manager Bit Field Properties
Some System Center Configuration Manager object properties are implemented as bit fields, where individual binary bits of an integer (usually a `uint32` data type) are used as `Boolean` flags to store information. These properties can be difficult to interpret at the user interface because the bit field is often displayed as a decimal number.  

 For example, the Security User Class Permissions object (`SMS_UserClassPermissions`) contains an integer property called `ClassPermissions`, which is defined as an `int32` data type with the following bit flags:  

|Bit|Value|  
|---------|-----------|  
|0|READ|  
|1|MODIFY|  
|2|DELETE|  
|3|DISTRIBUTE|  
|4|CREATE_CHILD|  
|5|REMOTE_CONTROL|  
|6|ADVERTISE|  
|7|MODIFY_RESOURCE|  
|8|ADMINISTER|  
|9|DELETE_RESOURCE|  
|10|CREATE|  
|11|VIEW_COLL_FILE|  
|12|READ_RESOURCE|  
|13|DELEGATE|  
|14|METER|  
|15|MANAGESQLCOMMAND|  
|16|MANAGESTATUSFILTER|  

 A typical value of this bit field might be 10100000111. Bit 0 is the least significant bit (on the right) and the other bits are counted right to left. Therefore, in this example, the available class permissions include READ, MODIFY, DELETE, ADMINISTER, and CREATE, corresponding to bit fields 0, 1, 2, 8, and 10, respectively.  

 The difficulty arises when the binary number 10100000111 appears as the decimal number 1287 in an Configuration Manager console display and in how you interpret the bits. The solution is to open the Windows Calculator application (Calc.exe, in the Accessories group). Use the Scientific view, set the calculator for decimal mode, and enter 1287. Use the radio buttons of the calculator to convert to a binary display. The binary bit field 10100000111 appears. You can read the selected bit flags from this display.  

> [!NOTE]
>  In a typical bit field property, many of the bits are unused and have no defined meaning.  

## See Also  
 [Configuration Manager Association Classes](../../../develop/core/understand/association-classes.md)   
 [Configuration Manager Date and Time Formats](../../../develop/core/understand/date-and-time-formats.md)   
 [Configuration Manager Embedded Objects](../../../develop/core/understand/embedded-objects.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [Configuration Manager Errors](../../../develop/core/understand/configuration-manager-errors.md)   
 [Configuration Manager Object Security](../../../develop/core/understand/configuration-manager-object-security.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)
