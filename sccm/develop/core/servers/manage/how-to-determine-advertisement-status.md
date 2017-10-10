---
title: "Determine Advertisement Status"
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
ms.assetid: 6ec6a9fd-0f61-4ad5-b7ec-4c5c877a3a27searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Determine Advertisement Status
To determine advertisement status in System Center Configuration Manager, you can use the queries described in this section.  

> [!NOTE]
>  These queries query the status messages directly and might take some time to complete because there can be many status messages.  
>   
>  For more information about using these queries, see [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md) and [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md).  
>   
>  For more queries about advertisement status and summarization, you can use [SMS_ClientAdvertisementStatus Server WMI Class](../../../../develop/reference/core/servers/configure/sms_clientadvertisementstatus-server-wmi-class.md) and [SMS_ClientAdvertisementSummary Server WMI Class](../../../../develop/reference/core/servers/configure/sms_clientadvertisementsummary-server-wmi-class.md).  

## Queries  

### Client Program Install  
 The following query returns the clients that have successfully installed a program. You need to check for both message identifiers because the program can report status with an exit code (10008) or an install status MIF file (10009).  

```  
' Returns clients that have successful installed a program  
SELECT msg.MachineName, msg.SiteCode, ad.ProgramName  
FROM SMS_StatusMessage msg  
     JOIN SMS_StatMsgAttributes attr ON msg.RecordID = attr.RecordID  
     JOIN SMS_Advertisement ad ON attr.AttributeValue = ad.AdvertisementID  
WHERE msg.Component = "Software Distribution"  
AND   (msg.MessageID = 10008 or msg.MessageID = 10009)  
AND   attr.AttributeID = 401  
ORDER BY ad.ProgramName  
```  

### Clients That Have Installed a Specific Advertised Program  
 This query returns the clients that have successfully installed a specific advertised program.  

```  
' Returns clients that have successfully installed a specific advertised program  
SELECT msg.MachineName, msg.SiteCode  
FROM SMS_StatusMessage msg  
     JOIN SMS_StatMsgAttributes attr ON msg.RecordID = attr.RecordID  
WHERE msg.Component = "Software Distribution"  
and   (msg.MessageID = 10008 or msg.MessageID = 10009)  
and   attr.AttributeID = 401  
and   attr.AttributeValue = "<AdvertisementID>"  
```  

### Clients That Have Not Installed a Specific Advertised Program  
 The previous queries show which clients successfully installed an advertised program. Determining which collection members have not installed the advertised program can be more involved if the advertisement specified subcollections. The following query determines which clients of the **All Systems** (SMS00001) collection (substitute your collection member class for SMS_CM_RES_COLL_SMS00001) have not installed the advertised program. If the advertisement specified subcollections, the query must be run for each subcollection.  

```  
' Returns which clients of a collection have not installed the advertised program  
SELECT Name  
FROM SMS_CM_RES_COLL_SMS00001  
WHERE NOT Name IN (SELECT msg.MachineName   
FROM SMS_StatusMessage msg  
     JOIN SMS_StatMsgAttributes attr ON msg.RecordID = attr.RecordID  
WHERE msg.Component = "Software Distribution"  
AND   (msg.MessageID = 10008 or msg.MessageID = 10009)  
AND   attr.AttributeID = 401  
AND   attr.AttributeValue = "<AdvertisementID>")  
```  

## See Also  
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using WMI](../../../../develop/core/understand/how-to-perform-an-asynchronous-configuration-manager-query-by-using-wmi.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md)   
 [SMS_StatusMessage Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)   
 [SMS_StatMsgAttributes Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md)   
 [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md)
