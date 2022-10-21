---
description: Learn how to define the installer technology used to install a specific application to devices in Configuration Management.
title: How To Define the Installer Technology
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c47f7a79-62de-4afa-a901-a25789329f32
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How To Define the Installer Technology
To define the application management installer technology, implement the `Microsoft.ConfigurationManagement.ApplicationManagement.DeploymentTechnology.InstallerTechnology` class. The new class instance will define the installer technology used to install a specific application to devices.  

 The installer technology is a key extension point for extending the application model.  This class is used to define specific metadata about the installation and detection of the technology on client systems concepts such as Detect, Install, and Uninstall.  

 In the Remote Desktop Protocol (RDP) sample project, a new installer technology is required for Remote Desktop Protocol (RDP) files.  Deployment support for RDP files is not built-in to Configuration Manager, so a custom installer technology is required.  

> [!IMPORTANT]
>  The InstallerTechnology class name must match the class specified in the InstallerTechnology.xml file.  

### To define a custom installer technology  

1.  Implement the `InstallerTechnology` class using the `Microsoft.ConfigurationManagement.ApplicationManagement.InstallerTechnology` constructor.  

     The following example from the RDP sample project demonstrates how to define an installer technology.  

    ```  
    namespace RdpTechnology  
    {  
        //   Installer technology for RDP.   
        public class RdpInstallerTechnology : InstallerTechnology  
        {  
            // Initializes a new instance of the "RdpInstallerTechnology" class.   
             public RdpInstallerTechnology()  
                : base(Common.TechnologyId, typeof(RdpInstaller), typeof(RdpContentImporter))   
            {  
            }  
        }  
    }   
    ```  

     In the RDP sample project, the string parameter is defined in the Common class.  The RdpInstaller and RdpContentImporter classes are also defined in the RDP sample project.  

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
 [How to Define the Hosting Technology](../../develop/apps/how-to-define-the-hosting-technology.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
