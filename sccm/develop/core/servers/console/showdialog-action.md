---
title: "Configuration Manager ShowDialog Action"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f5912944-21ac-40d2-a026-f9b2ea69d9c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration Manager ShowDialog Action
The `ShowDialog` action, in System Center Configuration Manager, opens a property sheet or regular dialog box in the Configuration Manager console. With the `ShowDialog` action, you can display existing dialog boxes or extension dialog boxes that you create.  

 The following attributes and elements are specific to an action that opens a dialog box:  

-   The `ActionDescription` element `Class` attribute is set to `ShowDialog`.  

-   The `DialogID` element is the identifier for a property sheet or dialog box displayed in a dialog. It matches the name of the form XML file in the *%ProgramFiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Extensions\Forms folder.  

## Sample ShowDialog Action XML  
 The following XML shows how to show a dialog box with the identifier **PrototypeForm**:  

```  
<ActionDescription Class="ShowDialog" DisplayName="Test Action (dialog)" MnemonicDisplayName="Mnemonic" Description="Description"> <ShowOn>              <string>DefaultHomeTab</string>      <string>ContextMenu</string>           </ShowOn>  
 <DialogId>PrototypeForm</DialogId>  
</ActionDescription>  
```  

## Sample Properties ShowDialog Action XML  
 The following attributes and elements are specific to an action that adds a property page to a properties property sheet:  

-   The `ActionDescription` element `ActionVerb` attribute is set to `Properties`.  

-   The `DialogID` element identifies a property sheet containing the property page to be displayed in the `Properties` dialog.  

 The following XML shows how to integrate a property page (`PrototypeForm`) into a properties context menu option:  

```  
<ActionDescription ActionVerb="Properties" Class="ShowDialog">  <ShowOn>    <string>DefaultHomeTab</string>    <string>ContextMenu</string>  </ShowOn>  <DialogId>PrototypeForm</DialogId>  
</ActionDescription>  
```  

 For more information about creating and showing dialog boxes, see [Configuration Manager Console Dialog Boxes](../../../../develop/core/servers/console/console-forms.md).  

## See Also  
 [About Configuration Manager Dialog Boxes](../../../../develop/core/servers/console/about-configuration-manager-console-forms.md)   
 [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md)   
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [How to Create Form XML for a Configuration Manager Property Sheet](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-property-sheet.md)   
 [How to Create Form XML for a Configuration Manager Dialog Box](../../../../develop/core/servers/console/how-to-create-form-xml-for-a-configuration-manager-dialog-box.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
