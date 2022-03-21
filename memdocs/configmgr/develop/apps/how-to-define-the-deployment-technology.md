---
title: "How to Define the Deployment Technology"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: afacc3b0-db65-4f10-8410-5a94c27d1ea6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Define the Deployment Technology
To define a custom application management deployment technology, implement the `Microsoft.ConfigurationManagement.ApplicationManagement.DeploymentTechnology` class. The new class instance will define the deployment technology used to deploy a specific application to devices.  

 The DeploymentTechnology class is the object that is registered with the Configuration Manager Application Model SDK. The DeploymentTechnology class contains references to three different types of objects that compose the technology. When implementing a new deployment technology you must implement a class that derives from this class.  

 In the Remote Desktop Protocol (RDP) sample project, a new deployment technology is required for Remote Desktop Protocol (RDP) files. Deployment support for RDP files is not built-in to Configuration Manager, so a custom deployment technology is required.  

> [!IMPORTANT]
>  The DeploymentTechnology class name must match the class specified in the DeploymentTechnology.xml file.  

### To define a custom deployment technology  

1.  Implement the `Microsoft.ConfigurationManagement.ApplicationManagement.DeploymentTechnology` class using the `Microsoft.ConfigurationManagement.ApplicationManagement.DeploymentTechnology` constructor. The string parameters are string values that uniquely identify the RDP Deployment Technology.  

    > [!NOTE]
    >  The class constructor requires multiple instances of the string parameter that identifies the technology.  

     The following example from the RDP sample project demonstrates how to define a deployment technology.  

    ```  
    namespace Microsoft.ConfigurationManagement.ApplicationManagement  
    {  
        //   Deployment technology used by RDP files.   
        public class RdpDeploymentTechnology : DeploymentTechnology  
        {  
            // Initializes a new instance of the "RdpDeploymentTechnology" class.   
             public RdpDeploymentTechnology()  
                : base(Common.TechnologyId, Common.TechnologyId, Common.TechnologyId)   
            {  
            }  
        }  
    }   
    ```  

     In the RDP sample project, the string parameter is defined as a constant in the Common class of the local project.  

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
 [How to Define the Hosting Technology](../../develop/apps/how-to-define-the-hosting-technology.md)   
 [How To Define the Installer Technology](../../develop/apps/how-to-define-the-installer-technology.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
