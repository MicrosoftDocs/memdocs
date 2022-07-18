---
description: Learn how to register the custom installer technology with Configuration Manager using an XML file.
title: "Define the Installer Technology Registration File"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: a86bf770-7386-4655-b264-a543fe954afa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Define the Installer Technology Registration File
To define an installer technology registration file, create an XML file based on the `http://schemas.microsoft.com/SystemCenterConfigurationManager/2009/AppMgmtDigest` schema. Used in the installation process, the registration file registers the custom installer technology with Configuration Manager.  The deployment technology registration file is required for the installation of the custom installer technology.

### To define the installer technology registration file  

1.  Create an installer technology registration file.  

     The following example from the RPC sample project demonstrates how to define an installer technology registration file.  

    ```  
    <AppMgmtDigest xmlns="http://schemas.microsoft.com/SystemCenterConfigurationManager/2009/AppMgmtDigest" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <InstallerTechnology AuthoringScopeId="GLOBAL" LogicalName="RdpInstallerTechnology" InstallerId="Rdp" AssemblySuffix="Rdp" Version="1" />  
    </AppMgmtDigest>  
    ```  

|Attributes|Description|  
|----------------|-----------------|  
|AuthoringScopeID|AuthoringScopeId will always be "GLOBAL".|  
|LogicalName|LogicalName must match the name of the SDK class created in the SDK assembly for InstallerTechnology.|  
|HostingId|HostingId must match the constant declared and used in the SDK assembly for InstallerTechnolgy.|  
|AssemblySuffix|AssemblySuffix must match the filename of the SDK assembly (Microsoft.ConfigurationManagement.ApplicationManagement.<`AssemblySuffix`>.dll).|  
|Version|Version is the version number for the release of the deployment type extension. This version number is used for in-place revisions.|  

## See Also  
 [How to Define the Deployment Technology Registration File](../../develop/apps/how-to-define-the-deployment-technology-registration-file.md)   
 [How to Define the Hosting Technology Registration File](../../develop/apps/how-to-define-the-hosting-technology-registration-file.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
