---
title: "Define the Deployment Technology Registration File "
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
ms.assetid: 928c176d-79ea-4dcc-a746-d36819c2d1a1searchScope: - ConfigMgr SDK
caps.latest.revision: 22
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Define the Deployment Technology Registration File
To define a deployment technology registration file, create an XML file based on the `http://schemas.microsoft.com/SystemCenterConfigurationManager/2009/AppMgmtDigest` schema. Used in the installation process, the registration file registers the custom deployment technology with Configuration Manager.  The deployment technology registration file is required for the installation of the custom deployment technology.  See [Installing the Application Management Extension](../../develop/apps/installing-the-application-management-extension.md) for additional details.  

### To define the deployment technology registration file  

1.  Create a deployment technology registration file.  

     The following example from the RDP sample project demonstrates how to define a deployment technology registration file.  

    ```  
    <AppMgmtDigest xmlns="http://schemas.microsoft.com/SystemCenterConfigurationManager/2009/AppMgmtDigest" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <DeploymentTechnology AuthoringScopeId="GLOBAL" LogicalName="RdpDeploymentTechnology" TechnologyId="Rdp" AssemblySuffix="Rdp" Version="1">  
        <HostingTechnology>GLOBAL/RdpHostingTechnology</HostingTechnology>  
        <InstallerTechnology>GLOBAL/RdpInstallerTechnology</InstallerTechnology>  
      </DeploymentTechnology>  
    </AppMgmtDigest>  
    ```  

|Attributes|Description|  
|----------------|-----------------|  
|AuthoringScopeID|AuthoringScopeId will always be “GLOBAL��?.|  
|LogicalName|LogicalName must match the name of the SDK class created in the SDK assembly.|  
|TechnologyId|Technology must match the constant declared and used in the SDK assembly.|  
|AssemblySuffix|AssemblySuffix must match the filename of the SDK assembly (Microsoft.ConfigurationManagement.ApplicationManagement.<`AssemblySuffix`>.dll).|  
|Version|Version is the version number for the release of the deployment type extension. This version number is used for in-place revisions.|  

|Element|Description|  
|-------------|-----------------|  
|HostingTechnology|The HostingTechnology element must be “GLOBAL/<`ClassNameForHostingTechnology`>��?.|  
|InstallerTechnology|The InstallerTechnology element must be “GLOBAL/<`ClassNameForInstallerTechnology`>��?.|  

## See Also  
 [How to Define the Hosting Technology Registration File](../../develop/apps/how-to-define-the-hosting-technology-registration-file.md)   
 [How to Define the Installer Technology Registration File](../../develop/apps/how-to-define-the-installer-technology-registration-file.md)   
 [Installing the Application Management Extension](../../develop/apps/installing-the-application-management-extension.md)   
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
