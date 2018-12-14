---
title: "Use SMSCSTAT.DLL to Create Status Messages"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4149481d-d78d-422a-b342-cf7ddcf2962c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About Using SMSCSTAT.DLL to Create Status Messages
Smscstat.dll is a library of 32-bit C APIs for reporting System Center Configuration Manager status messages from an application that is running on either client computer. Smscstat.dll is only present and only functions properly on Windows 95, Windows 98, Windows NT, Windows 2000, Windows Server 2003, Windows XP, and Windows Vista computers that have the client software installed on them.  

## Loading Smscstat.dll  
 Applications need to explicitly load Smscstat.dll by using the Win32 **LoadLibrary()** API. **LoadLibrary** requires the full path to Smscstat.dll.  

|||  
|-|-|  
|SMS 2003 Advanced Client|%*windir*%\system32\ccm|  
|System Center Configuration Manager client|%*windir*%\system32\ccm|  

 The logic for finding the path on a given client is as follows:  

1.  Read the registry value Local SMS Path in key HKEY_LOCAL_MACHINE\Software\Microsoft\SMS\Client\Configuration\ClientProperties.  

2.  If last three characters of this path are **ccm**, then this is the Advanced Client or System Center Configuration Manager client and Smscstat.dll resides in the path retrieved.  

## Accessing the Functions in Smscstat.dll  
 When Smscstat.dll has been loaded, call the Win32 API `GetProcAddress()` to retrieve function pointers to the status message functions. The three status message functions are:  

- `CreateSMSStatusMessage()`  

- `AddAttributeToSMSStatusMessage()`  

- `ReportSMSStatusMessage`  

  `GetProcAddress()` returns a pointer of type `FARPROC`. For convenience, `Smscstat.h` (provided with the SMS 2003 SDK) defines C function prototypes for the status message APIs. The application should cast the pointer returned by`GetProcAddress()` to the appropriate prototype and then call the function through the pointer.  

  If Smscstat.dll does not exist, as in the case of SMS 2.0 Legacy Clients that do not have Service Pack 1 or a later service pack installed, `LoadLibrary()` fails. A subsequent call to the Win32 API `GetLastError()` returns an error code indicating that the file does not exist. Most likely this will be error 126: "The specified module could not be found."  

  The Win32 API `FreeLibrary` should be called when access to the functions is no longer need.  

## Using the Status Message Functions in Smscstat.dll  
 There are three steps to using the status message functions.  

1.  Create a status message object by calling the `CreateSMSStatusMessage()` function. This function allocates an object and returns a handle to the caller.  

2.  Add any needed status message attributes to the object by using the `AddAttributeToSMSStatusMessage()` function. Status message attributes are optional and are required only if the application needs to integrate with a particular Configuration Manager feature. Most applications will not do this.  

3.  Call `ReportSMSStatusMessage` to submit the status message to the Configuration Manager status system and deallocate the object.
