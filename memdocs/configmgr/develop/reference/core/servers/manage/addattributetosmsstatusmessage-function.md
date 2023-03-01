---
description: Learn to use AddAttributeToSMSStatusMessage to add a single optional status message attribute id-value pair to a status message object.
title: AddAttributeToSMSStatusMessage Function
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: fe906f97-a669-49aa-9fb3-09920f0d395e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddAttributeToSMSStatusMessage Function
In Configuration Manager, the `AddAttributeToSMSStatusMessage` function adds a single optional status message attribute ID/value pair to a status message object.  

## Syntax  

```  
[C/C++]  
typedef DWORD (WINAPI *PROC_ADDATTRIBUTETOSMSSTATUSMESSAGE)  
(  
      HANDLE hStatusMessageObject,  
      DWORD  dwAttributeID,  
      LPCSTR pszAttributeValue  
);  
```  

#### Parameters  
 `hStatusMessageObject`  
 Data type: `HANDLE`  

 Qualifiers: [in]  

 Handle to the status message object.  

 `dwAttributeID`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 Status message attribute ID.  

 `pszAttributeValue`  
 Data type: `LPCSTR`  

 Qualifiers: [in]  

 Status message attribute value.  

## Return Values  
 One of the values in the following table.  

|Value|Description|  
|-----------|-----------------|  
|SMSSTATMSG_SUCCESS|The attribute ID/value pair was successfully added to the object.|  
|SMSSTATMSG_OUT_OF_MEMORY|This function failed to allocate enough memory to add the attribute ID/value pair to the object.|  
|STATMSG_ERROR_INVALID_ATTR_VALUE|The caller supplied `null` or a string that exceeded SMSSTATMSG_MAX_ATTR_VALUE_LENGTH characters in length for the `pszAttributeValue`parameter.|  
|SMSSTATMSG_ERROR_MAX_ATTR_LIMIT|The object already has SMSSTATMSG_MAX_NUM_ATTRS attribute ID/value pairs associated with it, which is the maximum permitted number.|  
|SMSSTATMSG_ERROR_UNKNOWN|Encountered an unknown error while trying to add the attribute ID/value pair.|  

## Remarks  
 Smscstat.h includes the following #define for calling `AddAttributeToSMSStatusMessage` by using the Win32 function `GetProcAddress`.  

```  
#define PROCNAME_ADDATTRIBUTETOSMSSTATUSMESSAGE "AddAttributeToSMSStatusMessage"  
```  

 All Configuration Manager status messages include a set of mandatory properties, such as the name of the component that reported the message, the message ID, the time the message was reported, and the insertion strings for the message. These mandatory properties are initialized when the status message object is created and by the parameters passed into the status message reporting API functions. In addition to the mandatory properties, a status message has zero or more optional properties associated with it. In the Configuration Manager status system, these optional properties are called attribute ID/value pairs or simply attributes. In Status Message Viewer, these optional properties appear in the **Properties** box when you double-click a status message to open the **Status Message Details** box.  

 Attribute ID/value pairs are associated with status messages to facilitate the construction of efficient status message queries. For example, when any Configuration Manager component reports a status message related to a particular Configuration Manager package (a software distribution object), the status message includes the package ID as an attribute ID/value pair. The administrator can execute a query to retrieve all the status messages associated with the package. The status message tables in the Configuration Manager SQL Server database are indexed to allow messages to be retrieved efficiently by attribute ID/value pairs.  

 An attribute ID/value pair is composed of a `DWORD` type as the attribute ID and a null-terminated ASCII string as the attribute data. The possible attribute IDs are listed in the following table. These IDs currently specify all object identifiers for objects that are specific to Configuration Manager that are associated with the Configuration Manager software distribution features. Unless your application is integrating with the software distribution functionality, it is highly unlikely that you need to associate any attribute ID/value pairs with any of the status messages to report. Therefore, it is highly unlikely that you ever need to call this function from an application.  

|Value|Description|  
|-----------|-----------------|  
|SMSSTATMSG_ATTR_ID_PACKAGE_ID (400)|The attribute value is the eight-character ID of a Configuration Manager package.|  
|SMSSTATMSG_ATTR_ID_ADVERTISEMENT_ID (401)|The attribute value is the eight-character ID of a Configuration Manager advertisement.|  
|SMSSTATMSG_ATTR_ID_COLLECTION_ID (402)|The attribute value is the eight-character ID of a Configuration Manager collection.|  
|SMSSTATMSG_ATTR_ID_USER_NAME (403)|The attribute value is a Windows NT user name and domain of the form domain\user name. In situations where the domain is not available, the attribute value takes the form of user name alone.|  
|SMSSTATMSG_ATTR_ID_DISTRIBUTION_POINT (404)|The attribute value is a Configuration Manager NAL path for a Configuration Manager distribution point.|  

## Requirements  
 Smscstat.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSCSTAT.DLL Status Message Functions](../../../../../develop/reference/core/servers/manage/smscstat.dll-status-message-functions.md)   
 [CreateSMSStatusMessage](../../../../../develop/reference/core/servers/manage/createsmsstatusmessage-function.md)
