---
title: "Create Function"
titleSuffix: "Configuration Manager"
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
ms.assetid: 09542d06-6ab2-4835-b4d4-9388d1563369searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Create Function
The `Create` function creates a status MIF file that System Center Configuration Manager uses to correlate the install status for an advertisement.  

## Syntax  

```  
StatusMIF.Create(  
     ByVal bstrFileName As String _  
     ByVal bstrCompany As String _  
     ByVal bstrProduct As String _  
     ByVal bstrVersion As String _  
     ByVal bstrLocale As String _  
     ByVal bstrSerialNo As String _  
     ByVal bstrMessage As String _  
     ByVal bStatus As Long _  
);  
```  

#### Parameters  
 `bstrFileName`  
 Unique name for the MIF file. A file name extension must be .mif. The function writes the file to the %TEMP% directory.  

 `bstrCompany`  
 Manufacturer or publisher of the product, for example, Microsoft. This parameter is limited to 64 characters.  

 `bstrProduct`  
 Product or program name, for example, Office 2000. This parameter is limited to 64 characters.  

 `bstrVersion`  
 Version of the product, for example, 8.0a. This parameter is limited to 64 characters.  

 `bstrLocale`  
 Country/region or language code, for example, ENU. This parameter is optional and is limited to 16 characters.  

 `bstrSerialNo`  
 Serial number of the product. This parameter is optional and is limited to 64 characters.  

 `bstrMessage`  
 Descriptive message about the status of the installation, added to the program status message. This parameter is limited to 128 characters.  

 `bStatus`  
 `true` if the install status is success.  

## Return Values  
 None.  

## Remarks  
 Your installation (setup) application must create only one install status MIF file for the package. The file name must be unique so that multiple installations in a single session can report status without a conflict.  

 Installations that run on localized versions of Configuration Manager must specify values in the appropriate format: ANSI format for European languages; DBCS format for East Asia languages.  

 Your application must call `InstallStatusMIF` before the installation exits. The MIF file is not reported to Configuration Manager if the installation creates another process that calls `InstallStatusMIF`.  

 Note that the parameters `bstrFilename`, `bstrCompany`, `bstrProduct`, and `bstrVersion` are directly related to the [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) properties `MIFFileName`, `MIFPublisher`, `MIFName`, and `MIFVersion`, respectively. These parameters and properties must contain the same values.  

 The example in the next section shows how to call the `Create` method.  

## Example  

```  
[VisualBasic]  
   Dim MIFStatus As New InstallStatusMIF  

   MIFStatus.Create "MyStatusFile", _  
                    "MyCompany", _  
                    "MyProduct", _  
                    "1.00.000", _  
                    "ENU", _  
                    " ", _  
                    "Installation Successful", _  
                    True  
```  

## Requirements  
 **Windows NT/2000**: Requires Windows NT 4.0 or later.  

 **Windows 95/98**: Requires Windows 95 or later.  

 **Version**: Requires SMS 2.0.  

 **Library**: Included as a resource in IsMIFCom.dll (Visual Basic).  

## See Also  
 [Status MIF Functions](../../../../../develop/reference/core/servers/manage/status-mif-functions.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
