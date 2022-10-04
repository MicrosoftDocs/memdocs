---
title: Executable action
titleSuffix: Configuration Manager
description: The executable action runs a program or opens a file by using the program registered with Windows for that file type.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configuration Manager Executable Action
In Configuration Manager, the executable action runs a program or opens a file by using the program registered with Windows for that file type.  

 The following attributes and elements are specific to an action that runs a program:  

-   The `ActionDescription` element `Class` attribute is set to `Executable`.  

-   The `Executable` element is parent to `FilePath``,` the path to the program, and to `Parameters`, the parameters passed to the executable.  

## Sample Executable Action XML  

```  
<ActionDescription Class="Executable" DisplayName="Test Action (execute)" MnemonicDisplayName="A test item" Description="A test item Description">
  <ShowOn>
    <string>DefaultHomeTab</string>
    <string>ContextMenu</string>
  </ShowOn>
  <!--<ResourceAssembly>
    <Assembly>Microsoft.ConfigurationManagement.dll</Assembly>
    <Type>Microsoft.ConfigurationManagement.AdminConsole.Properties.Resources.resources</Type>
  </ResourceAssembly>-->
  <!--<ImagesDescription>
    <ExternalImage>
      <Assembly>AdminUI.Package.dll</Assembly>
      <Type>Microsoft.ConfigurationManagement.AdminConsole.Package.SmsPackageUtils</Type>
      <Method>ShowPackageLockedIcon</Method>
    </ExternalImage>
    <ResourceAssembly>
      <Assembly>AdminUI.UIResources.dll</Assembly>
      <Type>Microsoft.ConfigurationManagement.AdminConsole.UIResources.Properties.Resources.resources</Type>
    </ResourceAssembly>
    <ImageResourceName>New</ImageResourceName>
  </ImagesDescription>-->
  <!--<ImagesDescription AliasProperty="OwnedByThisSite">
    <ResourceAssembly>
      <Assembly>AdminUI.UIResources.dll</Assembly>
      <Type>Microsoft.ConfigurationManagement.AdminConsole.UIResources.Properties.Resources.resources</Type>
    </ResourceAssembly>
    <AliasResourceAssembly>
      <Assembly>AdminUI.UIResources.dll</Assembly>
      <Type>Microsoft.ConfigurationManagement.AdminConsole.UIResources.SMS_Collection-OwnedByThisSite.resources</Type>
    </AliasResourceAssembly>
    <ImageResourceName>CollectionsIcon</ImageResourceName>
  </ImagesDescription>-->
  <!--<ActionStateAssembly>
    <Assembly>AdminUI.Report.dll</Assembly>
    <Type>Microsoft.ConfigurationManagement.AdminConsole.Report.ReportsUtilityClass</Type>
    <Method>EnableReportMenu</Method>
    -->
  <!--Method signature: public static bool EnableMenu(object sender, ScopeNode scopeNode, ActionDescription action, ResultObjectBase resultObject)-->
  <!--
  </ActionStateAssembly>-->
  <!--<InstancePermissions>
    <SecurityFlagsDetailDescription BitName="Delete" BitValue="4" DependsOn="1" />
  </InstancePermissions>-->
  <!--<MatchPattern>[^1]</MatchPattern>
  <MatchValueToTest>##SUB:Order##</MatchValueToTest>-->
  <Executable>
    <FilePath>https://go.microsoft.com/fwlink/?LinkId=67307</FilePath>
  </Executable>
</ActionDescription>
```  

 Other elements and attributes are documented in [ActionDescription](/previous-versions/system-center/developer/cc147252(v=msdn.10)).  

## See Also  
 [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md)   
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
