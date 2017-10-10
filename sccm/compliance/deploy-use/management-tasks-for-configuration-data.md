---
title: "Manage configuration data"
description: "After you create configuration items and baselines in System Center Configuration Manager, you can use other commands to perform various actions."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
caps.latest.revision: 7
caps.handback.revision: 0
author: andredm7ms.author: andredmmanager: angrobe

---
# Manage configuration data in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
After you have created configuration items and configuration baselines in System Center Configuration Manager, further commands are available to help you perform various actions.  

## Manage configuration items  

-   In the **Assets and Compliance** workspace, expand **Compliance Settings** > **Configuration Items**, select the configuration item to manage, and then select a management task.  

|Management task|Details|  
|---------------------|-------------|  
|**Create Child Configuration Item**|Opens the **Create Child Configuration Item Wizard** where you can create a child configuration item from the selected configuration item.<br /><br /> You cannot create a child configuration item from a mobile device configuration item.<br /><br /> For details, see [Create child configuration items](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Revision History**|Opens the **Configuration Item Revision History** dialog box where you can view and manage previous revisions of the selected configuration item.|  
|**View XML Definition**|Displays the XML definition file for the selected configuration item in a new window. This information can be useful when you want to author configuration data manually.|  
|**Export**|Exports a configuration item in a cabinet (.cab) file format, providing that it was created at that site. You can then import it to the same or a different Configuration Manager site. Configuration data is converted to DCM Digest.|  
|**Copy**|Creates a copy of the selected configuration item with a name you specify. The new configuration item does not retain any relationship to the original configuration item. This means that the duplicate configuration item does not continue to inherit configuration information from the original configuration item.|  
|**Delete**|Opens the **Delete Configuration Item** dialog box where you can review any references to this configuration item.<br /><br /> You must remove all references to a configuration item before you can delete the configuration item.|  

## Manage configuration baselines  

-   In the **Assets and Compliance** workspace, expand **Compliance Settings** > **Configuration Baselines**, select the configuration baseline to manage, and then select a management task.  


|Management task|Details|  
|---------------------|-------------|  
|**Show Members**|Displays all of the configuration items that are referenced by the configuration baseline.|  
|**Schedule Summarization**|Configures the schedule by which the data shown in the **Configuration Baselines** node in the Configuration Manager console is updated with the latest information from the site database.|  
|**Run Summarization**|Summarization causes the data in the **Configuration Baselines** node to be refreshed with the latest data from the site database. This action might take several minutes to complete. You might have to click **Refresh** before you can see the latest data in the console.|  
|**View XML Definition**|Displays the XML definition file for the selected configuration baseline in a new window. This information can be useful when you want to author configuration data manually.|  
|**Enable**|Enables a configuration baseline for compliance monitoring.|  
|**Disable**|Disables a configuration baseline so it is no longer evaluated for compliance on client computers. Configuration baselines that reference this configuration baseline will also be disabled.|  
|**Export**|Exports a configuration baseline in a cabinet (.cab) file format, providing that it was created at that site. You can then import it to the same or a different Configuration Manager site. Configuration data is converted to DCM Digest.<br /><br /> For information about how to import configuration data, see [Import configuration data](../../compliance/deploy-use/import-configuration-data.md).|  
|**Copy**|Creates a copy of the selected configuration baseline with a name that you specify. The new configuration baseline does not retain any relationship to the original configuration baseline.|  
|**Delete**|Opens the **Delete Configuration Baseline** dialog box where you can review any references to this configuration baseline.<br /><br /> You must remove all references to a configuration baseline before you can delete the configuration baseline.|  
|**Deploy**|Opens the **Deploy Configuration Baseline** dialog box where you can deploy one or more configuration baselines to devices in your hierarchy.<br /><br /> For details, see [Deploy configuration baselines](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
