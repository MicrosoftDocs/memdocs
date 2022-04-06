---
description: The InstallStatusMIF function creates a status Management Information Format (MIF) file that Configuration Manager uses to correlate the install status for an advertisement.
title: "InstallStatusMIF Function"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5ad7cfc6-4112-41ab-94fe-c0a125564e28
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# InstallStatusMIF Function
The `InstallStatusMIF` function creates a status Management Information Format (MIF) file that Configuration Manager uses to correlate the install status for an advertisement.  

## Syntax  

```  
DWORD InstallStatusMIF(  
     char* pszFileName,  
     char* pszCompany,  
     char* pszProduct,  
     char* pszVersion,  
     char* pszLocale,  
     char* pszSerialNo,  
     char* pszMessage,  
     BOOL bStatus  
);  
```  

#### Parameters  
 `pszFileName`  
 Pointer to a unique name for the MIF file. A file name extension must be .mif. The function writes the file to the %*TEMP*% directory.  

 `pszCompany`  
 Pointer to the manufacturer or publisher of the product, for example, Microsoft. This parameter is limited to 64 characters.  

 `pszProduct`  
 Pointer to the product or program name, for example, Microsoft Office 2000. This parameter is limited to 64 characters.  

 `pszVersion`  
 Pointer to the version of the product, for example, 8.0a. This parameter is limited to 64 characters.  

 `pszLocale`  
 Pointer to the country/region or language code, for example, ENU. This parameter is optional and is limited to 16 characters.  

 `pszSerialNo`  
 Pointer to the serial number of the product. This parameter is optional and is limited to 64 characters.  

 `pszMessage`  
 Pointer to a descriptive message about the status of the installation, added to the program status message. This parameter is limited to 128 characters.  

 `bStatus`  
 `true` if the install status is success.  

## Return Values  
 A non-zero value to indicate success.  

## Remarks  
 Your installation (setup) application must create only one install status MIF file for the package. The file name that you specify must be unique.  

 Installations that run on localized versions of Configuration Manager must specify values in the appropriate format: ANSI format for European languages; DBCS format for East Asia languages.  

 Your application must call `InstallStatusMIF` before the installation exits. The MIF file is not reported to Configuration Manager if the installation creates another process that calls `InstallStatusMIF`.  

 Note that the parameters `pszFilename`, `pszCompany`, `pszProduct`, and `pszVersion` are directly related to the [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) properties `MIFFileName`, `MIFPublisher`, `MIFName`, and `MIFVersion`, respectively. These parameters and properties must contain the same values.  

 The `InstallStatusMIF` function is provided in a 32-bit version (Ismif32.dll) and a 16-bit version (Ismif16.dll). The appropriate DLL is installed on the client computer during the Configuration Manager client installation process.  

 The example in the next section shows how to call the `InstallStatusMIF` function by using the Ismif32.dll file directly. A failure to load the Ismif32.dll file might indicate that the system is not a Configuration Manager client.  

## Example  

```  
[C/C++]  
DWORD (WINAPI *InstallStatusMIF)(char *, char *, char *, char *, char *, char *, char *, BOOL);  

#define PROCSIGNATURE DWORD (WINAPI *)(char *, char *, char *, char *, char *, char *, char *, BOOL)  

    HINSTANCE  hinst;  
    int  RetCode;  

    hinst = LoadLibrary("ismif32.dll");  

    InstallStatusMIF = (PROCSIGNATURE) GetProcAddress(hinst, "InstallStatusMIF");  

    if (InstallStatusMIF)  
    {  
        RetCode = InstallStatusMIF("Status",  
                                   "Microsoft",  
                                   "Microsoft SQL Server 7.0",  
                                   "7.00.000",  
                                   "ENU",  
                                   NULL,  
                                   "Installation Successful",  
                                   true);  
    }  
    FreeLibrary(hinst);   
```  

## Requirements  
 **Windows NT/2000**: Requires Windows NT 4.0 or later.  

 **Windows 95/98**: Requires Windows 95 or later.  

 **Version**: Requires SMS 2.0.  

 **Library**: Included as a resource in Ismif32.dll (C/C++); Ismif16.dll (C/C++).  

## See Also  
 [Status MIF Functions](../../../../../develop/reference/core/servers/manage/status-mif-functions.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
