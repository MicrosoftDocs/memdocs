---
title: "Console Management Class XML"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 32b5eea0-903b-4b54-92e8-d540973c6321
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Console Management Class XML
The management classes XML for the Configuration Manager console are located %*ProgramFiles*%\Microsoft Endpoint Manager\AdminConsole\XmlStorage\ConsoleRoot\ManagementClassDescriptions.xml file. Your extension management class XML files, however, must be placed in the AdminConsole\XmlStorage\Extensions\ManagementClasses\ folder.  

 The following XML defines an extension management class called "MyClass". The "MyClass" node is a subclass of the `SMS_SiteControlItem` management class, which is defined in the ConsoleRoot\ManagementClassDescriptions.xml.  

```  

<ManagementClassDescription Name="MyClass" SuperclassName="SMS_SiteControlItem" SecurityObjectAlias="SMS_Site"> <Properties>          <ManagementClassPropertyDescription Name="RoleName"/>          <ManagementClassPropertyDescription Name="SiteCode" />     </Properties></ManagementClassDescription>  
```  

 You can also expose your own custom management class that is defined within an assembly. For example, the XML below defines a management class called `_SDK`. The `_SDK` class is defined in a custom assembly. Note that the management class must be defined using .NET from within the referenced assembly.  

```  
<ManagementClassDescription Name="_SDK">       <Properties>          <ManagementClassPropertyDescription Name="MyProperty1"/>         <ManagementClassPropertyDescription Name="MyProperty2"/>           <ManagementClassPropertyDescription Name="MyProperty3"/>      </Properties>       <ResourceAssembly>         <Assembly>UIExtensionsDemo.dll</Assembly>    <Type>UIExtensionsDemo.ConnectionManager._SDK.resources</Type>       </ResourceAssembly>       <ImagesDescription>          <ResourceAssembly>             <Assembly>UIExtensionsDemo.dll</Assembly>        <Type>UIExtensionsDemo.Resources.resources</Type>   </ResourceAssembly>         <ImageResourceName>ViewIcon</ImageResourceName>      </ImagesDescription></ManagementClassDescription>  
```  

## See also

[About console management classes](about-configuration-manager-console-management-classes.md)
