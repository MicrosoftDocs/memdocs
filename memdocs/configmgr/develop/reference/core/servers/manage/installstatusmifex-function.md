---
title: "InstallStatusMIFEx Function"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c7f89ba4-eaf4-4755-bc4d-90064d1ad918
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# InstallStatusMIFEx Function
The `InstallStatusMIFEx` function, in Configuration Manager, enhances the functionality of [InstallStatusMIF](../../../../../develop/reference/core/servers/manage/installstatusmif-function.md).  

## Syntax  

```  
DWORD InstallStatusMIFEx(  
     char* pszFileName,  
     char* pszCompany,  
     char* pszProduct,  
     char* pszVersion,  
     char* pszLocale,  
     char* pszSerialNo,  
     char* pszMessage,  
     BOOL bStatus,  
     BOOL bProgramReboots  
);  
```  

#### Parameters  
 `pszFileName`  
 Pointer to a unique name for the Management Information Format (MIF) file. A file name extension must be .mif. The function writes the file to the %*TEMP*% directory.  

 `pszCompany`  
 Pointer to the manufacturer or publisher of the product, for example, Microsoft. This parameter is limited to 64 characters.  

 `pszProduct`  
 Pointer to the product or program name, for example, Microsoft Office 2000. This parameter is limited to 64 characters.  

 `pszVersion`  
 Pointer to the version of the product, for example, 8.0a. This parameter is limited to 64 characters.  

 `pszLocale`  
 Pointer to the country/region or language code, for example, ENU. This parameter is optional and limited to 16 characters.  

 `pszSerialNo`  
 Pointer to the serial number of the product. This parameter is optional and limited to 64 characters.  

 `pszMessage`  
 Pointer to a descriptive message about the status of the installation, which is added to the program status message. This parameter is limited to 128 characters.  

 `bStatus`  
 `true` if the install status is success.  

 `bProgramReboots`  
 `true` if the program will reboot the computer.  

## Return Values  
 A non-zero value to indicate success.  

## Remarks  
 `InstallStatusMIFEx` is functionally equivalent to `InstallStatusMIF`, except for the addition of the `bProgramReboot`parameter. Using `bProgramReboot`is the most reliable way of passing this information to Configuration Manager, because during reboot Configuration Manager might not be able to get the correct exit code from the process. If, after completing program execution, the program sets this flag in the MIF file and a reboot has not happened, Configuration Manager waits for one minute before launching any other program. This allows enough time for the reboot to finish. This flag also enables Configuration Manager to send a preliminary success status message for the program and then a final success status message after the reboot has occurred.  

 Your installation (setup) application must create only one install status MIF file for the package. The file name that you specify must be unique.  

 Installations that run on localized versions of Configuration Manager must specify values in the appropriate format: ANSI format for European languages; DBCS format for East Asia languages.  

 Your application must call `InstallStatusMIFEx` before the installation exits. The MIF file is not reported to Configuration Manager if the installation creates another process that calls `InstallStatusMIFEx`.  

 Note that the parameters `pszFilename`, `pszCompany`, `pszProduct`, and `pszVersion` are directly related to the [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) properties `MIFFileName`, `MIFPublisher`, `MIFName`, and `MIFVersion`, respectively. These parameters and properties must contain the same values.  

## Requirements  
 **Windows NT/2000**: Requires Windows 2000 or later.  

 **Version**: Requires SMS 2003 Advanced Client.  

 **Library**: Included as a resource in IsMIF32.dll (C/C++).  

## See Also  
 [Status MIF Functions](../../../../../develop/reference/core/servers/manage/status-mif-functions.md)   
 [InstallStatusMIF](../../../../../develop/reference/core/servers/manage/installstatusmif-function.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
