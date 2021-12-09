---
title: "GetProviderVersion Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ceaf0a5e-83fa-4c59-a6fd-c041e73a030b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetProviderVersion Method in Class SMS_Identification
The `GetProviderVersion` Windows Management Instrumentation (WMI) class method, in Configuration Manager,  gets the product version string from the version resources of the SMS Provider DLL.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetProviderVersion(  
      String VersionString  
);  
```  

#### Parameters  
 `VersionString`  
 Data type: `String`  

 Qualifiers: [out]  

 Product version string from the version resources of the Smsprov.dll file.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 The version that is obtained by this method allows your application to determine whether the SMS Provider has had a hotfix applied.  

## Example Code  
 The following example shows how to call this method to get the version number of the SMS Provider.  

```  
Dim Identification As SWbemObject  
Dim ProviderVersion As String  

Set Identification = GetObject("winmgmts:\root\sms\site_<sitecode>:SMS_Identification")  
Identification.GetProviderVersion ProviderVersion  

MsgBox "Version = " & ProviderVersion  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)
