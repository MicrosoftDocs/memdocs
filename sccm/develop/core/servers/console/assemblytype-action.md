---
title: "AssemblyType Action"
titleSuffix: "Configuration Manager"
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
ms.assetid: 0a910d9f-9064-4295-b286-01a6d809702bsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager AssemblyType Action
The `AssemblyType` action defines the type and assembly for a method that is called by the System Center Configuration Manager console.  

> [!NOTE]
>  The XML and C# code in this topic is available in the Dialog Prototype sample in the Configuration Manager SDK.  

 The following attributes and elements are specific to an action that calls a method in an assembly:  

-   The `Class` attribute of the `ActionDescription` element is set to `AssemblyType`.  

-   The `ActionAssembly` element has a number of child elements that are used to define the method and assembly.  

-   The `Assembly` element identifies the assembly that contains the method. If the assembly is in a folder other than %*ProgramFiles*%\Microsoft Configuration Manager\AdminConsole\bin folder then the `Assembly` element should include the assembly filename and the full path to the file.  

-   The `Type` element contains the namespace and class for the method.  

-   The `Method` element contains the name of the method to be called.  

## Method  
 The method signature is:  

```  
public static void Method(object, ScopeNode, ActionDescription, IResultObject, PropertyDataUpdated, Status)  
```  

 Where the parameters are as follows:  

 `object`  
 The object calling the method.  

 `ScopeNode`  
 The Configuration Manager console node that was active when the action was called.  

 `ActionDescription`  
 The `ActionDescription` class instance that initiated the action.  

 `IResultObject`  
 The selected object, or `null` if there is no selected object.  

 `PropertyDataUpdated`  
 The delegate to open to provide update information for the Configuration Manager console view.  

 `Status`  
 Allows control of the Configuration Manager console busy status indicator.  

### Example Implementation  
 The following is an example implementation of the method.  

```  
public static void Method(object sender, ScopeNode scopeNode, ActionDescription action, IResultObject resultObject, PropertyDataUpdated dataUpdatedDelegate, Status status)   
{  
    if (resultObject != null)   
    {  
        MessageBox.Show(string.Format("The {0} package was selected", resultObject["Name"].StringValue));   
    }  
    else  
    {  
        MessageBox.Show("No package was selected");  
    }  
}  

```  

## AssemblyType Action XML  
 The following XML example demonstrates how to call a method, `Method`, in a class, `SampleClass`. The method is in the assembly `AdminUI.PrototypeDialog.dll`.  

```  
<ActionDescription Class="AssemblyType" DisplayName="Test Action (method)" MnemonicDisplayName="Mnemonic" Description="Description">  
  <ShowOn>  
    <string>DefaultHomeTab</string>  
    <string>ContextMenu</string>  
  </ShowOn>  
  <ActionAssembly>  
    <Assembly>AdminUI.PrototypeDialog.dll</Assembly>  
    <Type>Microsoft.ConfigurationManagement.AdminConsole.PrototypeDialog.ExampleClass</Type>  
    <Method>Method</Method>  
    <!--Method signature: public static void Method(object sender, ScopeNode scopeNode, ActionDescription action, IResultObject resultObject, PropertyDataUpdated dataUpdatedDelegate, Status status)-->   
  </ActionAssembly>  
</ActionDescription>  

```  

## See Also  
 [How to Create a Configuration Manager Action](../../../../develop/core/servers/console/how-to-create-a-configuration-manager-action.md)   
 [Configuration Manager Actions](../../../../develop/core/servers/console/configuration-manager-actions.md)   
 [Configuration Manager Action XML](../../../../develop/core/servers/console/configuration-manager-action-xml.md)   
 [How to Find a Configuration Manager Node GUID](../../../../develop/core/servers/console/how-to-find-a-configuration-manager-console-node-guid.md)
