---
title: "ReportSMSStatusMessage Function"
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
ms.assetid: 3fbdfb51-67dc-4409-9e4a-d943e1e0382fsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ReportSMSStatusMessage Function
The `ReportSMSStatusMessage` function, in Configuration Manager, submits a status message object to the Configuration Manager status system and then deallocates the object.  

## Syntax  

```  
[C/C++]  
typedef DWORD (WINAPI *PROC_REPORTSMSSTATUSMESSAGE)  
(  
      HANDLE hStatusMessageObject,  
      LPCSTR pszComponentName,  
      LPCSTR pszSiteCode,  
      LPCSTR pszTopLevelSiteCode  
);  
```  

#### Parameters  
 `hStatusMessageObject`  
 Data type: `HANDLE`  

 Qualifiers: [in, out]  

 Handle to the status message object. On input, supply the handle retrieved by [CreateSMSStatusMessage](../../../../../develop/reference/core/servers/manage/createsmsstatusmessage-function.md). On successful return from the function, this parameter contains the handle to the deallocated object.  

 The behavior of this function is undefined for invalid handles and throws an access violation exception. Therefore, ensure that you supply a valid handle for this parameter. See Remarks.  

 `pszComponentName`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to the name of the component reporting the status message. This name is a null-terminated ASCII component name. It appears in Status Message Viewer in the Component column and in Windows NT Event Viewer in the Category column. For more information , see the Remarks section later in this topic.  

 `pszSiteCode`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to the Configuration Manager site code for the site to which to report the status message. The code is a null-terminated ASCII code that is exactly three characters long. Alternatively you can set this parameter to `null`. For more information, see the Remarks section later in this topic.  

 `pszTopLevelSiteCode`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Pointer to the Configuration Manager site code for the highest site in the hierarchy to which the message can be replicated. The code is a null-terminated ASCII code. Alternatively, you can set this parameter to `null`. For more information, see  the Remarks section later in this topic.  

## Return Values  
 This function returns one of the values in the following table.  

|Value|Description|  
|-----------|-----------------|  
|SMSSTATMSG_SUCCESS|The object was successfully submitted to the Configuration Manager status system.|  
|SMSSTATMSG_OUT_OF_MEMORY|This function failed to allocate enough memory to submit the object to the Configuration Manager status system.|  
|SMSSTATMSG_ERROR_INVALID_COMPONENT_NAME|The caller supplied `null` or a string that exceeded SMSSTATMSG_MAX_COMPONENT_NAME_LENGTH characters in length for the `pszComponentName` parameter.|  
|SMSSTATMSG_ERROR_INVALID_SITE_CODE|The caller supplied a non-NULL invalid string for `pszSiteCode`.|  
|SMSSTATMSG_ERROR_UNKNOWN|The function encountered an unknown error while trying to submit the object to the Configuration Manager status system.|  
|SMSSTATMSG_ERROR_INVALID_TOP_LEVEL_SC|The caller supplied a non-NULL invalid string for `pszTopLevelSiteCode`.|  
|SMSSTATMSG_ERROR_NOT_SMS_CLIENT|This function failed to submit the object to the Configuration Manager status system because the Configuration Manager client software is not properly installed on this computer.|  

## Remarks  
 Smscstat.h includes the following #define for calling `ReportSMSStatusMessage` by using the Win32 function `GetProcAddress`.  

```  
#define PROCNAME_REPORTSMSSTATUSMESSAGE "ReportSMSStatusMessage"  
```  

 When calling this function, use the `hStatusMessageObject` parameter to supply a handle for the status message to report. When this function returns, the retrieved object is guaranteed to be deallocated, regardless of the success of the function. If the function is unsuccessful and you want your application to try again, create a new status message before calling `ReportSMSStatusMessage`.  

 Use the `pszComponentName` parameter of this function to supply a name for the component that is reporting the status message. This name is not localizable to other languages, because the Configuration Manager administrator creates queries and filter rules that are based on the component name. This assists the administrator in quickly retrieving your particular status messages and in configuring Configuration Manager to handle these status messages in special ways.  

 In the `pszSiteCode` parameter, supply the code for the Configuration Manager site to which to submit the message. The code must be for one of the sites to which the Configuration Manager client currently belongs. Generally, you should supply `null` for this parameter, to indicate that the status message should be reported to all Configuration Manager sites to which the Configuration Manager client belongs.  

 The status system stops replication at the site indicated by `pszTopLevelSiteCode` no matter how the administrator has configured the replication rules. Generally, you should specify `null` for this parameter, to indicate that there is no top-level site code and that the message is free to replicate all the way to the top of the hierarchy. However, if there is a reason to prevent the replication past a certain site, you can supply the site code of that site using the `pszTopLevelSiteCode` parameter.  

## Requirements  
 Smscstat.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSCSTAT.DLL Status Message Functions](../../../../../develop/reference/core/servers/manage/smscstat.dll-status-message-functions.md)
