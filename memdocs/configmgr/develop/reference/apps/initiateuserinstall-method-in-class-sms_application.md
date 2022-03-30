---
title: "InitiateUserInstall Method"
titleSuffix: "Configuration Manager"
description: "InitiateUserInstall method is reserved for future use in Configuration Manager."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 955b71e0-6890-4cae-8ce1-9d3e3b5d78fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# InitiateUserInstall Method in Class SMS_Application
> [!WARNING]
>  This method is reserved for future use.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 InitiateUserInstall (  
     String  ModelName,  
     String  Username,  
     String  ClientGUID  
);  

```  

#### Parameters  
 `ModelName`  
 Data type: `String`  

 Qualifiers: [in]  

 Model name of the application.  

 `Username`  
 Data type: `String`  

 Qualifiers: [in]  

 Unique user name.  

 `ClientGUID`  
 Data type: `String`  

 Qualifiers: [in]  

 Unique identifier of a client.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)   
