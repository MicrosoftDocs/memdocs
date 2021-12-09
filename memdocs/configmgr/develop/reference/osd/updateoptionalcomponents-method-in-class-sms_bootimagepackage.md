---
title: "UpdateOptionalComponents Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1563c3a6-5850-404f-9638-090c7bd3c4e5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# UpdateOptionalComponents Method in Class SMS_BootImagePackage
The `UpdateOptionalComponents` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates all specified optional components to the boot image package.  

> [!NOTE]
>  It is necessary to refresh the distribution points when using this method.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 UpdateOptionalComponents(  
      String ComponentIds[],  
);  
```  

#### Parameters  
 `ComponentIds`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Component identifiers. The following are possible values:  

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
|23|Not used.|  
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
|49|Not used.|  
|50|WinPE-WDS-Tools.cab|  
|51|WinPE-WinReCfg.cab|  
|52|WinPE-WMI.cab|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 It is not necessary to refresh the distribution points when using this method.  

 For more information about NAL paths, see [SMS_NAL_Methods Server WMI Class](../../../develop/reference/misc/sms_nal_methods-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)   
 [SMS_NAL_Methods Server WMI Class](../../../develop/reference/misc/sms_nal_methods-server-wmi-class.md)
