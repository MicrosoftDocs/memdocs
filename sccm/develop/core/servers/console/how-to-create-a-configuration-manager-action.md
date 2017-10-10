---
title: "Create a Configuration Manager Action"
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
ms.assetid: affca54f-bebb-44f8-9c94-58598670770esearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a Configuration Manager Action
To create a Configuration Manager console action, in System Center Configuration Manager, you create an XML file that populates an [ActionDescription](https://msdn.microsoft.com/library/microsoft.configurationmanagement.adminconsole.schema.actiondescription.aspx) XML element for the action. You must then copy the XML file to the %*ProgramFiles*%\Microsoft Configuration Manager\AdminConsole\XmlStorage\Extensions\Actions\GUID folder.  

 For sample XML for each action type, see the following:  

-   [Configuration Manager Executable Action](../../../../develop/core/servers/console/executable-action.md)  

-   [Configuration Manager ShowDialog Action](../../../../develop/core/servers/console/showdialog-action.md)  

-   [Configuration Manager Report Action](../../../../develop/core/servers/console/report-action.md)  

-   [Configuration Manager AssemblyType Action](../../../../develop/core/servers/console/assemblytype-action.md)  

-   [Configuration Manager Group Action](../../../../develop/core/servers/console/group-action.md)  

 For information about deploying the action XML, see [Configuration Manager Console Extension Deployment](../../../../develop/core/servers/console/console-extension-deployment.md).  

### To add an executable action to the Configuration Manager console  

1.  If the Configuration Manager console is open, close it.  

2.  In Notepad, create an empty text file named MyConfigurationManagerNote.txt and save it to C:\\.  

3.  In Notepad, create an XML file that contains the following XML:  

    ```  
    <ActionDescription Class="Executable" DisplayName="Make a Note" MnemonicDisplayName="Note" Description = "Make a note about software updates">    <ShowOn>      <string>DefaultContextualTab</string> <!-- RIBBON -->     <string>ContextMenu</string> <!-- Context Menu -->   </ShowOn>       <Executable>  
      <FilePath>Notepad.exe</FilePath>  
      <Parameters>C:\MyConfigurationManagerNote.txt</Parameters>  
     </Executable>  
    </ActionDescription>  
    ```  

4.  Save the XML file in the folder \<%*Program Files*%> Microsoft Configuration Manager\AdminConsole\XmlStorage\Extensions\Actions\f5445252-da1d-450f-a772-7c3d3cb929fb. The GUID identifies the software updates folder. The file name can be anything with an .xml extension, but it does alphabetically affect the ordering of actions in the context-sensitive menu and in the actions pane. If it is not already created, you must create the Extensions\Actions\f5445252-da1d-450f-a772-7c3d3cb929fb folder structure. Be sure to save the file as type `All Files`.  

5.  Start the Configuration Manager console.  

     In the Configuration Manager console, right-click the **Software Updates** node under **Computer Management**, and then click **Make a Note**. Notepad opens the text file.  

## See Also  
 [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md)   
 [Configuration Manager Action XML](../../../../develop/core/servers/console/configuration-manager-action-xml.md)   
 [Configuration Manager Executable Action](../../../../develop/core/servers/console/executable-action.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
