---
title: "Monitor Endpoint Protection status"
titleSuffix: "Configuration Manager"
description: "Learn how monitor Endpoint Protection in your System Center Configuration Manager hierarchy."
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to monitor Endpoint Protection status

*Applies to: System Center Configuration Manager (Current Branch)*

You can monitor Endpoint Protection in your Microsoft System Center Configuration Manager hierarchy by using the **Endpoint Protection Status** node under **Security** in the **Monitoring** workspace, the **Endpoint Protection** node in the **Assets and Compliance** workspace, and by using reports.  

##  <a name="BKMK_1"></a> How to Monitor Endpoint Protection by Using the Endpoint Protection Status Node  

1. In the Configuration Manager console, click **Monitoring**.  

2. In the **Monitoring** workspace, expand **Security** and then click **Endpoint Protection Status**.  

3. In the **Collection** list, select the collection for which you want to view status information.  

   > [!IMPORTANT]
   >  Collections are available for selection in the following cases:  
   > 
   > - When you select **View this collection in the Endpoint Protection dashboard** on the **Alerts** tab of the <em><collection name\></em>**Properties** dialog box.  
   >   -   When you deploy an Endpoint Protection antimalware policy to the collection.  
   >   -   When you enable and deploy Endpoint Protection client settings to the collection.  

4. Review the information that is displayed in the **Security State** and **Operational State** sections. You can click any status link to create a temporary collection in the **Devices** node in the **Assets and Compliance** workspace. The temporary collection contains the computers with the selected status.  

   > [!IMPORTANT]  
   >  Information that is displayed in the **Endpoint Protection Status** node is based on the last data that was summarized from the Configuration Manager database and might not be current. If you want to retrieve the latest data, on the **Home** tab, click **Run Summarization**, or click **Schedule Summarization** to adjust the summarization interval.  

##  <a name="BKMK_2"></a> How to Monitor Endpoint Protection in the Assets and Compliance Workspace  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, perform one of the following actions:  

    -   Click **Devices**. In the **Devices** list, select a computer, and then click the **Malware Detail** tab.  

    -   Click **Device Collections**. In the **Device Collections** list, select the collection that contains the computer you want to monitor and then, on the **Home** tab, in the **Collection** group, click **Show Members**.  

3.  In the *<collection name\>* list, select a computer, and then click the **Malware Detail** tab.  

##  <a name="BKMK_3"></a> How to Monitor Endpoint Protection by Using Reports  
 Use the following reports to help you view information about Endpoint Protection in your hierarchy. You can also use these reports to help troubleshoot any Endpoint Protection problems. For more information about how to configure reporting in Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) and [Log files in System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md). The Endpoint Protection reports are in the Endpoint Protection folder.  

|Report name|Description|  
|-----------------|-----------------|  
|**Antimalware Activity Report**|Displays an overview of antimalware activity for a specified collection.|  
|**Infected Computers**|Displays a list of computers on which a specified threat is detected.|  
|**Top Users By Threats**|Displays a list of users with the most number of detected threats.|  
|**User Threat List**|Displays a list of threats that were found for a specified user account.|  

## Malware Alert Levels  
 Use the following table to identify the different Endpoint Protection alert levels that might be displayed in reports, or in the Configuration Manager console.  

|Alert level|Description|  
|-----------------|-----------------|  
|**Failed**|Endpoint Protection failed to remediate the malware. Check your logs for details of the error.<br /><br /> **Note:** For a list of Configuration Manager and Endpoint Protection log files, see the "Endpoint Protection" section in the [Log files in System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md) topic.|  
|**Removed**|Endpoint Protection successfully removed the malware.|  
|**Quarantined**|Endpoint Protection moved the malware to a secure location and prevented it from running until you remove it or allow it to run.|  
|**Cleaned**|The malware was cleaned from the infected file.|  
|**Allowed**|An administrative user selected to allow the software that contains the malware to run.|  
|**No Action**|Endpoint Protection took no action on the malware. This might occur if the computer is restarted after malware is detected and the malware is no longer detected; for instance, if a mapped network drive on which malware is detected is not reconnected when the computer restarts.|  
|**Blocked**|Endpoint Protection blocked the malware from running. This might occur if a process on the computer is found to contain malware.|
