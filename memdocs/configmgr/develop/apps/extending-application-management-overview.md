---
title: Extending Application Management Overview
titleSuffix: Configuration Manager
description: Partners that must continue to use a specific deployment technology not natively supported by Configuration Manager, can extend the Application Management model to support a custom deployment type.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: b12131ec-cbe0-4c93-9729-e78d904a1a11
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Extending Application Management Overview
By default, Application Management supports creating numerous deployment types such as Windows Installer, Script Installer, Microsoft Application Virtualization, Nokia SIS files and Windows Mobile Cabinet file deployment technologies. Partners that must continue to use a specific deployment technology not natively supported by Configuration Manager, can extend the Application Management model to support a custom deployment type.  

 In Application Management, the application object is the high-level object that Configuration Manager Administrators will create, deploy and monitor. The deployment type object represents the technology that will be detected, installed and uninstalled on the end-user systems. The Application Management model can be extended by creating an instance of deployment type with a custom deployment technology.  

 The deployment type object is composed of multiple objects: deployment technology, hosting technology, installer technology, content importer and the installer. The installer object is a key extension point, as it provides the properties for a technology, as well as the logic for detection, installation and uninstallation of the technology on the client system.  

 Extending the application model requires extending the Configuration Manager consoles and Configuration Manager clients that will leverage the custom deployment type. On the server, the extension is accomplished through creating and registering a custom deployment technology assembly and by extending Configuration Manager console (adding custom property sheets and wizards). The client extension is accomplished through extending WMI and adding a custom handler (a public COM class and methods). It should be noted that the client extension closely maps to the installer object, defined as part of the deployment type. The properties and methods defined in the installer object map directly to the property values are stored in WMI and the public COM methods defined in the custom handler.  

 In conceptualizing a custom deployment type, it might be useful to consider the in-product handling of Windows Installer files (*.msi).  

> [!TIP]
>  A complete sample project implementing a custom deployment type for Remote Desktop Protocol (*.rdp) files is provided separately for reference. The discussion throughout the Extending Application Management section leverages the Remote Desktop Protocol sample project for examples and illustration.  

## Overview  

### Server  

1.  Create a Custom SDK Assembly  

     The custom SDK assembly contains an interface implementation of both the Hosting Technology and Installer Technology.  The AssemblySuffix should correspond to whatever is specified for AssemblySuffix attribute in the DeploymentTechnology.xml file, for example Microsoft.ConfigurationManagement.ApplicationManagement.\<*AssemblySuffix*>.dll.  

    1.  Deployment Technology - The DeploymentTechnology class is the object that is registered with the Configuration Manager Application Model SDK. When implementing a new deployment technology you must implement a class that derives from this class. The new class instance will define the deployment technology used to deploy a specific application to devices.  

    2.  Hosting Technology - The HostingTechnology class is used to define run time interaction and configuration for technologies.  

    3.  Installer Technology – The InstallerTechnology class is used to define specific metadata about the detection, installation and uninstallation of the application.  

    4.  Installer – The Installer class is used to define properties and methods used on the client to actually detect, install and uninstall the application.  

    5.  Content Importer - The ContentImporter class is used to allow custom technologies to be able to read a specific content file and create the corresponding DeploymentType object using information obtained from the content file.  For example, the Windows Installer content importer reads Windows Installer files (*.msi) and is able to populate Title, Description properties of the Installer DeploymentType object and create the Detect, Install and Uninstall actions for the Installer.  

    6.  Resources – To support the Installer, a custom XML schema should be included as part of the assembly. The schema file (XSD) file must be included as a resource in the assembly.  

2.  Create the Registration XML Files  

     As part of defining a custom application management deployment technology, create three registration files/digests. These registration files/digests are used to register the Deployment Technology with Configuration Manager.  

    1.  DeploymentTechnology.xml - Digest of the Deployment Technology.  

    2.  HostingTechnology.xml - Digest of the Hosting Technology.  

    3.  InstallerTechnology.xml - Digest of the Installer Technology.  

3.  Create the UI Extension  

     To extend the Configuration Manager console, create a UX assembly, custom property sheets and wizards.  

     The assembly should correspond to following naming convention: AdminUI.DeploymentType.\<*AssemblySuffix*>.dll.  

    1.  AdminUI.DeploymentType.\<*AssemblySuffix*>.dll  

         Required – Contains UX implementation, which is then bound to the Configuration Manager console using the following XML files:  

    2.  CreateApp_\<*TechnologyId*>.xml  

         Required – Extension XML for the Create Application Wizard.  

    3.  CreateDeploymentWizard_\<*TechnologyId*>.xml  

         Required - Extension XML for the Deployment Type Wizard.  

    4.  \<*TechnologyId*>DeploymentTypePropertySheet.xml  

         Required - Standard Property Page XML for the Deployment Type property page.  

### Client  
 The client extension is accomplished through extending WMI and adding a custom handler (public COM class and methods). It should be noted that the client extension closely maps to the Installer object, defined as part of the DeploymentType. Property values are stored in WMI and the public COM methods map to detection, installation and uninstallation.  

1.  Create an AppSynclet MOF File  

     To define a custom synclet MOF file, create an instance of the CCM_AppHandlers class. The new class instance will identify the custom client-side handler. Additionally, create instances of the CCM_HandlerSynclet class which will store install, uninstall and detect property values which can be used by the corresponding client-side handler methods.  

2.  Create a Client-side Handler  

     The custom client-side handler needs to implement a public COM interface and methods (InstallApp, UninstallApp and DiscoveryApp). The methods will be called by the Configuration Manager client framework. However, the actual functionality of the methods is defined by the client-side handler developer.  

### Installation  

1.  How to Create the Configuration Manager Deployment Type Extension File (*.cmdtx)  

    1.  Create an empty directory to stage its contents  

    2.  Create and copy the following files into this directory:  

        1.  DeploymentTechnology.xml - A digest of the Deployment Technology  

        2.  HostingTechnology.xml - A digest of the Hosting Technology  

        3.  InstallerTechnology.xml - A digest of the Installer Technology  

        4.  The custom SDK Assembly (Microsoft.ConfigurationManagement.ApplicationManagement.\<*AssemblySuffix*>.dll) - Contains interface implementation of both the Hosting Technology and Installer Technology Note: the AssemblySuffix should correspond to whatever is specified for AssemblySuffix attribute in the DeploymentTechnology.xml file.  

        5.  HostingApplication.zip - Optional. Importable application that represents the Hosting Application, which includes content (if any). This should be created using the Export feature on the Applications node, in the Configuration Manager console.  

        6.  HandlerApplication.zip - Optional. Importable application that represents the Handler Application for the client, which includes content (if any). This should be created using the Export feature on the Applications node, in the Configuration Manager console.  

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

2.  How to Create the Windows Installer File (*.msi)  

     After the *.cmdtx is created, create a Windows Installer file (\*.msi) which contains the \*.cmdtx file and UX files. The Installer will be responsible for installing the UX files in the correct locations.  

    1.  Install the UX files in the correct locations. Basically, this will involve including the following files (with respect to Deployment Type Extensions):  

        1.  AdminUI.DeploymentType.\<AssemblySuffix>.dll  

             Required – Contains UX implementation, which is then bound to the Configuration Manager console using the following XML files:  

        2.  CreateApp_\<*TechnologyId*>.xml  

             Required – Extension XML for the Create Application Wizard.  

        3.  CreateDeploymentWizard_\<*TechnologyId*>.xml  

             Required - Extension XML for the Deployment Type Wizard.  

        4.  \<*TechnologyId*>DeploymentTypePropertySheet.xml  

             Required - Standard Property Page XML for the Deployment Type property page.  

    2.  Register the *.cmdtx  

         The Windows Installer file (*.msi) should contain code/script to invoke the DeploymentTypeExtender.Extend method, which is located in the Microsoft.ConfigurationManagement.ApplicationManagement namespace. This will then register the extension files for a given site server computer. For a Configuration Manager administrator console computer, this will initialize the cache for that user.  

        ```  
        using DCM = Microsoft.ConfigurationManagement.AdminConsole.DesiredConfigurationManagement;   
         [...]  
            ConnectionManagerBase connectionManager = new WqlConnectionManager();  
            connectionManager.Connect("SiteServerName");  
            DeploymentTypeExtender.Extend(@"C:\PartnerTechnology.cmdtx", new  DCM.ConsoleDcmConnection(connectionManager, null), @"\\SiteServerName\root\sms\site_SITECODE");  
        ```  

## Namespaces  
 Microsoft.ConfigurationManagement.AdminConsole  

 Microsoft.ConfigurationManagement.AdminConsole.AppManFoundation  

 Microsoft.ConfigurationManagement.AdminConsole.CreateDT  

 Microsoft.ConfigurationManagement.AdminConsole.DesiredConfigurationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement.Serialization  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.ConnectionManagerBase  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

## Assemblies  
 AdminUI.AppManFoundation  

 AdminUI.CreateDT  

 AdminUI.DcmObjectWrapper.dll  

 AdminUI.WqlQueryEngine.dll  

 Microsoft.ConfigurationManagement.exe  

 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

 Microsoft.ConfigurationManagement.ApplicationManagement.Extender.dll  

 Microsoft.ConfigurationManagement.ManagementProvider.dll  

## See Also  
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
