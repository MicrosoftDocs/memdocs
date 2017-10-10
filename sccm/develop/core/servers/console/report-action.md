---
title: "Configuration Manager Report Action"
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
ms.assetid: 47806f0a-362a-4255-bbd5-af38146a8880searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Report Action
The report action displays a System Center Configuration Manager report in the Configuration Manager console.  

 The following attributes and elements are specific to an action that opens a report box:  

-   The `ActionDescription` element `Class` attribute is set to **Report**.  

-   The `ReportDescription` element `ReportName` attribute is the GUID of the report to be displayed. The GUID maps to the `SMS_Report` class `ReportGUID` property.  

> [!NOTE]
>  An alternative method to load a report is to use the executable action to launch the report's URL. This will display the report in a new window rather than in the Configuration Manager console.  

## Sample Report Action XML  
 The following XML demonstrates how to display a report, identified by its GUID, in the Configuration Manager console:  

```  
<ActionDescription Class="Report" DisplayName="Test Action (report)" MnemonicDisplayName="Mnemonic" Description="Description"> <ShowOn>      <string>DefaultContextualTab</string> <!-- RIBBON -->     <string>ContextMenu</string> <!-- Context Menu -->   </ShowOn>        
 <ReportDescription ReportName="05874720-1D08-4CF7-B182-5F9D065BEAE5">  
 </ReportDescription>  
</ActionDescription>  
```  

## See Also  
 [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md)   
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
