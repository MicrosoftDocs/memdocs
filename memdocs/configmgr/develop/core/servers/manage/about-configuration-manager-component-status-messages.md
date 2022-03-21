---
title: "About Component Status Messages"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fb0d7f0c-a341-4c41-a84f-16c027433e2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Configuration Manager Component Status Messages
The message text for both the Configuration Manager components and the raw user-defined messages is contained in message DLLs. The [SMS_StatMsgInsStrings Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsginsstrings-server-wmi-class.md) class contains the insertion strings for those messages that use insertion strings. To read the SMS component and raw user-defined messages, you must know the message DLL that contains the message text.  

> [!NOTE]
>  If the status message is in Srvmsgs.dll, Provmsgs.dll, or Climmsgs.dll, you can use [FormatModuleMessage Method](../../../../develop/reference/core/servers/manage/formatmodulemessage-method.md) to resolve the message.  

 You can get the DLL name from the [SMS_StatMsgModuleNames Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsgmodulenames-server-wmi-class.md). The [SMS_StatMsgModuleNames Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsgmodulenames-server-wmi-class.md) class contains the **ModuleName** and **MsgDLLName** properties. You can use **ModuleName** to join the `SMS_StatMsgModuleNames` class with the `SMS_StatusMessage` class, as the following example shows.  

```  
// Note that this query returns all the instances found in the SMS_Status_Message   
// class. This query can return several thousand instances. If you test this   
// query, you should add a where clause to limit its scope, or set the   
// InstanceCount context qualifier to limit the number of instances returned.  
SELECT B.Severity, B.MessageID, B.MessageType,  
       B.Win32Error, B.SiteCode, B.MachineName,  
       B.Component, C.MsgDLLName, D.InsStrValue   
FROM SMS_StatusMessage AS B  
     INNER JOIN SMS_StatMsgModuleNames AS C   
     ON B.ModuleName = C.ModuleName  
     LEFT OUTER JOIN SMS_StatMsgInsStrings AS D  
     ON B.RecordID = D.RecordID   
ORDER BY B.Sitecode, B.RecordID, B.MessageID, D.InsStrIndex  
```  

 You can use the **MessageID** and **Component** names from the list to limit your status message query. For example, you can add a WHERE clause to limit the status messages to the SMS_Distribution_Manager component.  

 After you have the DLL name, you can use the Microsoft Win32 API function **FormatMessage** to retrieve the message text from the component's message DLL. This requires you to get the module handle for the DLL by using the Win32 API function **GetModuleHandle**. The *dwMessageId* parameter is the OR'd result of the **MessageID** and the **Severity** properties. You should set the FORMAT_MESSAGE_ARGUMENT_ARRAY flag and pass the insertion strings as an array.  

 The following code shows how to call **FormatMessage** to retrieve the message text from a DLL.  

```  
// Get the module handle for the component's message DLL. This assumes the  
// message DLL is loaded. If the DLL is not loaded, then load the DLL by using  
// the Win32 API LoadLibrary.  
hmodMessageDLL = GetModuleHandle(MsgDLLName);  

// The flags tell FormatMessage to allocate the memory needed for the message,  
// to get the message text from a message DLL, and that the insertion strings are  
// stored in an array, instead of a variable length argument list. The last  
// parameter, apInsertStrings, is the array of insertion strings returned by the  
// query.  
dwMsgLen = FormatMessage(FORMAT_MESSAGE_ALLOCATE_BUFFER |  
                         FORMAT_MESSAGE_FROM_HMODULE |  
                         FORMAT_MESSAGE_ARGUMENT_ARRAY,  
                         hmodMessageDLL,  
                         Severity | MessageID,  
                         0,  
                         lpBuffer,  
                         nSize,  
                         apInsertStrings);  

// Free the memory after you use the message text.  
LocalFree(lpBuffer);  
```  

## See Also  
 [About Configuration Manager Status Messages](../../../../develop/core/servers/manage/about-configuration-manager-status-messages.md)   
 [SMS_StatMsgInsStrings Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsginsstrings-server-wmi-class.md)   
 [SMS_StatMsgModuleNames Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsgmodulenames-server-wmi-class.md)
