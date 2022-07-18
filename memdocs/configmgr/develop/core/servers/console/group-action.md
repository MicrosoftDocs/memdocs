---
description: Learn how to use the group action in configuration manager to create a submenu for related actions.
title: "Configuration Manager Group Action"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3156b487-c303-47d5-990f-8af010326acd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Group Action
In Configuration Manager, the Group action creates a menu group, also known as a submenu, for related actions.  

 The following attributes and elements are specific to an action that creates a group of context menu items:  

-   The <`ActionDescription`> element `Class` attribute is set to **Group**.  

-   The <`DisplayName`> attribute is the group name displayed in the context menu.  

-   The <`GroupAsRegion`> Boolean attribute specifies whether or not to display this group as a region on the ribbon bar.  

-   The <`ActionGroups`> element is a list of actions (<`ActionDescription`> elements) displayed in the context menu group.  

## Group Action XML  
 The following XML demonstrates a group of actions named New Group Name:  

```  
<ActionDescription Class="Group" GroupAsRegion="true" DisplayName="New Group Name" MnemonicDisplayName="MnemonicNewGroupName" Description="NewGroupNameDescription">  <ShowOn>      <string>DefaultContextualTab</string> <!-- RIBBON -->     <string>ContextMenu</string> <!-- Context Menu -->   </ShowOn>       <ActionGroups>  
    <ActionDescription Class="Executable" DisplayName="Test Action (execute)" MnemonicDisplayName="A test item" Description="A test item Description">          <ShowOn>          <string>DefaultContextualTab</string> <!-- RIBBON -->         <string>ContextMenu</string> <!-- Context Menu -->      </ShowOn>         <Executable>  
      <FilePath>https://go.microsoft.com/fwlink/?LinkId=67307</FilePath>  
    </Executable>  
    </ActionDescription>  
    <ActionDescription Class="Report" DisplayName="Test Action (report)" MnemonicDisplayName="Mnemonic" Description="Description">  
    <ShowOn>         <string>DefaultContextualTab</string> <!-- RIBBON -->        <string>ContextMenu</string> <!-- Context Menu -->      </ShowOn>            <ReportDescription Id="05874720-1D08-4CF7-B182-5F9D065BEAE5">  
      </ReportDescription>  
    </ActionDescription>  
  </ActionGroups>  
</ActionDescription>  
```  

## See Also  
[About Configuration Manager console actions](configuration-manager-actions.md)
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
