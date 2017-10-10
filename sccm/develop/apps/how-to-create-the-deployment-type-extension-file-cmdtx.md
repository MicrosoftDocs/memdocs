---
title: "How to Create the Deployment Type Extension File "
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
ms.assetid: c576b3fd-5eb3-4e57-9c20-3158f8d0b7cbsearchScope: - ConfigMgr SDK
caps.latest.revision: 19
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create the Deployment Type Extension File (*.cmdtx)
The application management extension must be installed on each Configuration Manager administrator console computer that will create a custom deployment technology. The first step in installing the application management extension files is to create a deployment type extension file (*.cmdtx).  

### To Create the ConfigMgr Deployment Type Extension File (*.cmdtx)  

1.  Create an empty directory to stage the contents.  

2.  Create and copy the following files previously created into the empty directory:  

    1.  DeploymentTechnology.xml  

         Required. A digest of the Deployment Technology  

    2.  HostingTechnology.xml  

         Required. A digest of the Hosting Technology  

    3.  InstallerTechnology.xml  

         Required. A digest of the Installer Technology  

    4.  The custom SDK Assembly (Microsoft.ConfigurationManagement.ApplicationManagement.{AssemblySuffix}.dll)  

         Required. Contains interface implementation of both the Hosting Technology and Installer Technology Note: the AssemblySuffix should correspond to whatever is specified for AssemblySuffix attribute in the DeploymentTechnology.xml file.  

    5.  HostingApplication.zip  

         Optional. Importable application that represents the Hosting Application, which includes content (if any). This should be created using the Export feature on the Applications node, in the Admin Console.  

    6.  HandlerApplication.zip  

         Optional. Importable application that represents the Handler Application for the client, which includes content (if any). This should be created using the Export feature on the Applications node, in the Admin Console.  

3.  Use the method DeploymentTypeExtender.CreateExtension, which is located in Microsoft.ConfigurationManagement.ApplicationManagement namespace, to create the Deployment Type Extension (*.cmdtx) file based on the content in the staging directory.  

    ```  
    // Summarizes progress from CreateExtension method to a log file or the console.   
    // <param name="summaryText">Summary text to be presented</param>  
    public void Summarize(string summaryText)   
    {  
          System.Console.WriteLine(summaryText);   
          return;   
    }  
    // Creates a new Deployment Type Extension using the specified source path  
    // <param name="sourcePath">Source path used to create the Deployment Type Extension</param>  
    // <param name="deploymentTypeExtensionFilePath">Resulting Deployment Type Extension file</param>  
    private void CreateDeploymentTypeExtensionFile(string sourcePath, string deploymentTypeExtensionFilePath)   
    {  
          DeploymentTypeExtender.CreateExtension(sourcePath, deploymentTypeExtensionFilePath, this.Summarize);   
          return;   
    }  
    ```  

#### Namespaces  
 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement.Serialization  

#### Assemblies  
 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

 Microsoft.ConfigurationManagement.ApplicationManagement.Extender.dll  

## See Also  
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
