---
title: Refresh method in class SMS_SiteInstallMap
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 13db1af5-84b4-4242-b1f3-98bd282766a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Refresh Method in Class SMS_SiteInstallMap
The `Refresh` Windows Management Instrumentation (WMI) class method, in Configuration Manager, reloads the install map from the database, which repopulates the classes.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Refresh( );  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method is used in the rare case when a new component is added by Configuration Manager site setup and the SMS Provider is located on a remote SQL Server computer that might not be restarted. Generally it is not necessary for your application to call this method because the SMS Provider copy of the install map will be up to date.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteInstallMap Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallmap-server-wmi-class.md)
