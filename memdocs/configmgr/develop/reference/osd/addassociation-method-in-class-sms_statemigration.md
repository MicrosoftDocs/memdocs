---
title: "AddAssociation Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fa65a143-b6f7-4951-9e0b-2ff874509483
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# AddAssociation Method in Class SMS_StateMigration
The `AddAssociation` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds the computer association between two system resources used in state migration.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddAssociation(  
      UInt32 SourceClientResourceID,  
      UInt32 RestoreClientResourceID,  
      SMS_StateMigrationUserNames UserNames[]  
);  
```  

#### Parameters  
 `SourceClientResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Resource ID for the source client.  

 `RestoreClientResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Resource ID for the destination client.  

 `UserNames`  
 Data type: `SMS_StateMigrationUserNames` Array  

 Qualifiers: [in]  

 [SMS_StateMigrationUserNames Server WMI Class](../../../develop/reference/osd/sms_statemigrationusernames-server-wmi-class.md) objects representing the names of users with profiles to be migrated. These objects are defined by the `UserNames` property of [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md).  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 For an example of the use of this method, see [How to Create an Association Between Two Computers in Configuration Manager](../../../develop/osd/how-to-create-an-association-between-two-computers-in-configuration-manager.md). To remove an association, your application can call the [DeleteAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/deleteassociation-method-in-class-sms_statemigration.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md)   
 [SMS_StateMigrationUserNames Server WMI Class](../../../develop/reference/osd/sms_statemigrationusernames-server-wmi-class.md)   
 [DeleteAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/deleteassociation-method-in-class-sms_statemigration.md)   
 [How to Create an Association Between Two Computers in Configuration Manager](../../../develop/osd/how-to-create-an-association-between-two-computers-in-configuration-manager.md)
