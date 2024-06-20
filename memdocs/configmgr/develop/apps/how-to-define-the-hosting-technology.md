---
title: How to Define the Hosting Technology
titleSuffix: Configuration Manager
description: The hosting technology is defined by implementing the `Microsoft.ConfigurationManagement.ApplicationManagement.HostingTechnology` class.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 242c1cf6-3cb8-4ed7-89fb-501130832730
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Define the Hosting Technology
To define a custom application management hosting technology, implement the `Microsoft.ConfigurationManagement.ApplicationManagement.HostingTechnology` class. The new class instance will define the hosting technology for a specific file type.  

 The HostingTechnology class supports run time interaction and configuration for technologies. The class contains the hosting rules as defined in the HostingTechnology.xml file. If needed, additional methods and properties can be added to this class, though in most cases the existing base should be sufficient.  

 In the Remote Desktop Protocol (RDP) sample project, a new hosting technology is required to handle Remote Desktop Protocol (RDP) files. Hosting support for RDP files is not built in to Configuration Manager, so a custom hosting technology is required.  

> [!IMPORTANT]
>  The HostingTechnology class name must match the class specified in the HostingTechnology.xml file.  

### To define a custom hosting technology  

1. Implement the `Microsoft.ConfigurationManagement.ApplicationManagement.HostingTechnology` class using the `Microsoft.ConfigurationManagement.ApplicationManagement.HostingTechnology` constructor.  

    In the example, a string constant, defined in the Common class of the local project, is used for the string parameter.  While the boolean parameter (`Microsoft.ConfigurationManagement.ApplicationManagement.HostingTechnology.IsRemote`) is set directly to true.  

   The following example from the RDP sample project demonstrates how to define a hosting technology.  

```  
// Defines the hosting technology for RDP files. Hosting support for RDP files is not built in, so a custom  
// hosting technology is needed on the client.   
public class RdpHostingTechnology : HostingTechnology  
{  
    //   Initializes a new instance of the "RdpHostingTechnology" class.   
    public RdpHostingTechnology()  
       : base(Common.TechnologyId, true)   
    {  
    }  
}  
```  

 In the RDP sample project, a string constant for the TechnologyId is defined in the Common class of the local project.  

```  
//   Internal ID of the technology.   
public const string TechnologyId = "Rdp";  
```  

#### Namespaces  
 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement.Serialization  

#### Assemblies  
 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

## .NET Framework Security  

## See Also  
 [How to Define the Deployment Technology](../../develop/apps/how-to-define-the-deployment-technology.md)   
 [How To Define the Installer Technology](../../develop/apps/how-to-define-the-installer-technology.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
