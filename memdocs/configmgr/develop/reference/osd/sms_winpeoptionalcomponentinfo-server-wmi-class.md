---
title: SMS_WinPEOptionalComponentInfo Class
titleSuffix: Configuration Manager
description: Represents WinPE optional components information.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5b4d124c-2eb3-4e32-9027-c076dc27e91f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_WinPEOptionalComponentInfo Server WMI Class
The `SMS_WinPEOptionalComponentInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents WinPE optional components information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WinPEOptionalComponentInfo : SMS_BaseClass  
{  
    String Architecture;  
    String DependentComponentNames[];  
    UInt32 DependentIds[];  
    Boolean IsRequired;  
    UInt32 LanguageID;  
    String Name;  
    String RelativePath;  
    UInt64 Size;  
    UInt32 UniqueID;  
};  
```  

## Methods  
 The `SMS_WinPEOptionalComponentInfo` class does not define any methods.  

## Properties  
 `Architecture`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The architecture of WinPE optional components. Possible values are:  

|Value|
|-|  
|X86|  
|X64|  

 `DependentComponentNames`  
 Data type: `String` Array  

 Access type: Read  

 Qualifiers: none  

 The name of dependent WinPE optional components.  

 `DependentIds`  
 Data type: `UInt32` Array  

 Access type: Read  

 Qualifiers: none  

 The unique ID of dependent WinPE optional components.  

 `IsRequired`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: none  

 `true` if the WinPE optional component is required.  

 `LanguageID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The language ID of the WinPE optional component.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The name of the WinPE optional component.  

 `RelativePath`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The relative path to the Assessment and Deployment Kit (ADK) installation path of the WinPE optional component.  

 `Size`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 The size of the WinPE optional component.  

 `UniqueID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The unique ID of WinPE optional component. Possible values are:  

| ID value | WinPE component |
| -------- | --------------- |
|X86||  
|1|WinPE-DismCmdlets.cab|  
|2|WinPE-Dot3Svc.cab|  
|3|WinPE-EnhancedStorage.cab|  
|4|WinPE-FMAPI.cab|  
|5|WinPE-FontSupport-JA-JP.cab|  
|6|WinPE-FontSupport-KO-KR.cab|  
|7|WinPE-FontSupport-ZH-CN.cab|  
|8|WinPE-FontSupport-ZH-HK.cab|  
|9|WinPE-FontSupport-ZH-TW.cab|  
|10|WinPE-HTA.cab|  
|11|WinPE-StorageWMI.cab|  
|12|WinPE-LegacySetup.cab|  
|13|WinPE-MDAC.cab|  
|14|WinPE-NetFx4.cab|  
|15|WinPE-PowerShell3.cab|  
|16|WinPE-PPPoE.cab|  
|17|WinPE-RNDIS.cab|  
|18|WinPE-Scripting.cab|  
|19|WinPE-SecureStartup.cab|  
|20|WinPE-Setup.cab|  
|21|WinPE-Setup-Client.cab|  
|22|WinPE-Setup-Server.cab|  
|23|N/A|  
|24|WinPE-WDS-Tools.cab|  
|25|WinPE-WinReCfg.cab|  
|26|WinPE-WMI.cab|  

| ID value | WinPE component |
| -------- | --------------- |
|X64||  
|27|WinPE-DismCmdlets.cab|  
|28|WinPE-Dot3Svc.cab|  
|29|WinPE-EnhancedStorage.cab|  
|30|WinPE-FMAPI.cab|  
|31|WinPE-FontSupport-JA-JP.cab|  
|32|WinPE-FontSupport-KO-KR.cab|  
|33|WinPE-FontSupport-ZH-CN.cab|  
|34|WinPE-FontSupport-ZH-HK.cab|  
|35|WinPE-FontSupport-ZH-TW.cab|  
|36|WinPE-HTA.cab|  
|37|WinPE-StorageWMI.cab|  
|38|WinPE-LegacySetup.cab|  
|39|WinPE-MDAC.cab|  
|40|WinPE-NetFx4.cab|  
|41|WinPE-PowerShell3.cab|  
|42|WinPE-PPPoE.cab|  
|43|WinPE-RNDIS.cab|  
|44|WinPE-Scripting.cab|  
|45|WinPE-SecureStartup.cab|  
|46|WinPE-Setup.cab|  
|47|WinPE-Setup-Client.cab|  
|48|WinPE-Setup-Server.cab|  
|49|N/A|  
|50|WinPE-WDS-Tools.cab|  
|51|WinPE-WinReCfg.cab|  
|52|WinPE-WMI.cab|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
