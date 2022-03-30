---
title: "Interpret Bitfield Properties"
titleSuffix: "Configuration Manager"
description: "Some SMS object properties are implemented as bit fields, where individual binary bits of an integer (usually a **uint32** data type) are used as Boolean flags to store information. These properties can be difficult to interpret at the user interface because the bit field is often displayed as a decimal number."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3abf009f-13f8-4baf-a548-648777a4e2b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Interpreting Bitfield Properties
Some SMS object properties are implemented as bit fields, where individual binary bits of an integer (usually a **uint32** data type) are used as Boolean flags to store information. These properties can be difficult to interpret at the user interface because the bit field is often displayed as a decimal number.  

 For example, the Security User Class Permissions object (**SMS_UserClassPermissions**) contains an integer property called **ClassPermissions**, which is defined as an **int32** data type with the following bit flags:  

|Bit|Flag|  
|---------|----------|  
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

 The difficulty arises when the binary number 10100000111 appears as the decimal number 1287 in an SMS Administrator console display and how you interpret the bits. The solution is to open the Windows Calculator application (Calc.exe, in the Accessories group). Use the Scientific view, set the calculator for decimal mode, and enter 1287. Use the radio buttons of the calculator to convert to a binary display. The binary bit field 10100000111 appears. You can read the selected bit flags from this display.  

> [!NOTE]
>  In a typical bit field property, many of the bits are unused and have no defined meaning.
