---
title: "CreateSMSStatusMessage Function"
description: Learn how the CreateSMSStatusMessage function allocates a status message object, initializes it, and retrieves a handle to it.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b7c7accc-d687-4cfa-ac67-611f3d5d23c4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CreateSMSStatusMessage Function
In Configuration Manager, the `CreateSMSStatusMessage` function allocates a status message object, initializes it, and retrieves a handle to it.  

## Syntax  

```  
[C/C++]  
typedef DWORD (WINAPI *PROC_CREATESMSSTATUSMESSAGE)  
(  
      PHANDLE phStatusMessageObject,  
      LPCSTR  pszModuleName,  
      DWORD   dwID,  
      DWORD   dwWin32Error,  
      LPCSTR  pszInsStr1,  
      LPCSTR  pszInsStr2,  
      LPCSTR  pszInsStr3,  
      LPCSTR  pszInsStr4,  
      LPCSTR  pszInsStr5,  
      LPCSTR  pszInsStr6,  
      LPCSTR  pszInsStr7,  
      LPCSTR  pszInsStr8,  
      LPCSTR  pszInsStr9,  
      LPCSTR  pszInsStr10   
);  
```  

#### Parameters  
 `phStatusMessageObject`  
 Data type: `PHANDLE`  

 Qualifiers: [in, out]  

 Pointer to the object handle. On input, supply a handle for the status message to create. On successful return from this function, the parameter indicates the created object. If the function does not succeed, the input value is left unchanged.  

 `pszModuleName`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to the status message module name, a null-terminated ASCII string representing the DLL that contains the display string for your application messages. The module name is displayed in Status Message Viewer and Windows NT Event Viewer as the source of the status message.  

 `dwID`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 Status message ID.  

 `dwWin32Error`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 Optional. Win32 error code returned by the Win32 function `GetLastError.`  

 `pszInsStr1`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 1, or to `null` for no string.  

 `pszInsStr2`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 2, or to `null` for no string.  

 `pszInsStr3`  
 Data type: `LPCSTR`  

 Qualifiers: `[in]`  

 Pointer to status message insertion string 3, or to `null` for no string.  

 `pszInsStr4`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 4, or to `null` for no string.  

 `pszInsStr5`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 5, or to `null` for no string.  

 `pszInsStr6`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 6, or to `null` for no string.  

 `pszInsStr7`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 7, or to `null` for no string.  

 `pszInsStr8`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 8, or to `null` for no string.  

 `pszInsStr9`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 9, or to `null` for no string.  

 `pszInsStr10`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to status message insertion string 10, or to `null` for no string.  

## Return Values  
 This function returns one of the values in the following table.  

|Value|Description|  
|-----------|-----------------|  
|SMSSTATMSG_SUCCESS|The object was successfully created.|  
|SMSSTATMSG_OUT_OF_MEMORY|The function failed to allocate enough memory to create the object.|  
|SMSSTATMSG_ERROR_INVALID_MODULE_NAME|The caller supplied `null` or a string that exceeded SMSSTATMSG_MAX_MODULE_NAME_LENGTH characters in length for the `pszModuleName` parameter.|  
|STATMSG_ERROR_INVALID_INSSTR|The caller supplied a string that exceeded SMSSTATMSG_MAX_INSSTR_LENGTH characters in length for one of the insertion string parameters.|  
|SMSSTATMSG_ERROR_UNKNOWN|The function encountered an unknown error while trying to create the object.|  

## Remarks  
 Smscstat.h includes the following #define for calling `CreateSMSStatusMessage` by using the Win32 function `GetProcAddress`.  

```  
#define PROCNAME_CREATESMSSTATUSMESSAGE "CreateSMSStatusMessage"  
```  

 Administrator privileges are required to call this function.  

 You should call `CreateSMSStatusMessage` only at the exact moment when reporting a status message is necessary. The reason for this rule is that the status message contains a timestamp that is set at creation time.  

 When calling this function, use the `phStatusMessageObject` to supply an object that you will use when calling the other status message reporting functions. Note that the only way to de-allocate the object associated with the handle is to call the [ReportSMSStatusMessage](../../../../../develop/reference/core/servers/manage/reportsmsstatusmessage-function.md) function, which submits the status message to the Configuration Manager status system. You should not pass this handle to the Win32 function `CloseHandle` or any other similar function.  

 The module name that you supply for the `pszModuleName` parameter is not the name of the DLL, but the name of a Configuration Manager module. The Configuration Manager site server contains a mapping of module names to DLL names. For example, the client components report status messages by using the Configuration Manager client module name. The site server is aware that the Configuration Manager client corresponds to the file Climsgs.dll.  

 The module name cannot be localized to other languages, because the Configuration Manager administrator creates queries and filter rules that are based on the component name. This assists the administrator in quickly retrieving your particular status messages and in configuring Configuration Manager to handle these status messages in special ways.  

 In your calls to this function, use the `dwID` parameter to furnish a status message ID. As part of the procedure for preparing your application to report Configuration Manager status messages, you create an .mc file that defines all the messages. Compiling this file produces an .h file containing a #define for each defined status message. You should supply the #define symbol as the message ID. When Status Message Viewer or Windows NT Event Viewer displays your message, it uses the message ID that you supply to look up the message text in the related DLL.  

 In the `dwWin32Error` parameter, you can provide an optional Win32 error code returned by a call to Win32 `GetLastError`. When Status Message Viewer or Windows NT Event Viewer displays the status message, it replaces insertion string 12 (%12) in the status message with the following text: The operating system reported error X: Y. Where X is the error code supplied here and Y is the Win32 error text associated with that error code. For example, error code 5 is "Access is denied."  

 You will typically supply a Win32 error code when reporting a status message immediately following a Win32 function failure. Supply 0 to indicate to the status system that no Win32 error code is associated with the status message, in which case insertion string 12 is blank.  

 Your call to `CreateSMSStatusMessage` can supply between zero and 10 null-terminated ASCII insertion strings. These strings correspond to the %1, %2, %3, and so forth, escape sequences in the status message definition. When Status Message Viewer or Windows NT Event Viewer displays the status message, it replaces the escape sequences with the values supplied to this function.  

## Requirements  
 Smscstat.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSCSTAT.DLL Status Message Functions](../../../../../develop/reference/core/servers/manage/smscstat.dll-status-message-functions.md)
