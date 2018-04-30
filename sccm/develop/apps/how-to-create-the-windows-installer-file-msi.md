---
title: "How to Create the Windows Installer File "
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cd6cf0d2-ff17-4d58-a7d5-244c88307b17
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create the Windows Installer File (*.msi)
After the Deployment Type Extension file (*.cmdtx) is created, you are expected to generate a Windows Installer file (\*.msi) which contains the \*.cmdtx file and the UX files. The Windows Installer needs to copy the files into the correct locations and register the custom extension with the site server.  

 The basic contents of the Windows Installer file are shown below:  

 ![Windows Installer package with embedded files](../../develop/apps/media/appmanwindowsinstallerpackage.gif "AppManWindowsInstallerPackage")  

### To Create the Windows Installer File (*.msi)  

1.  Generate a Windows Installer file which contains the *.cmdtx file, and UX files. The Windows Installer file will be responsible for installing the UX files in the correct locations, using the standards defined by the Admin Console team. Basically, this will involve including the following files:  

    1.  UX Assembly, e.g. AdminUI.DeploymentType.\<*AssemblySuffix*>.dll  

         This file is required and contains the UX implementation, which is then bound to the Configuration Manager console using the below XML files.  

         The Installer should copy this file to sms\AdminConsole\bin.  

    2.  CreateApp_\<*TechnologyID*>.xml  

         This file is required and provides the console extension for the Create Application Wizard.  

         The Installer should copy this file to sms\AdminConsole\XmlStorage\Extensions\Forms.  

    3.  CreateDeploymentWizard_\<*TechnologyID*>.xml  

         This file is required and provides the console extension for the Create Deployment Type Wizard.  

         The Installer should copy this file to sms\AdminConsole\XmlStorage\Extensions\Forms.  

    4.  \<*TechnologyID*>DeploymentTypePropertySheet.xml  

         This file is required and provides the Deployment Type property page.  

         The Installer should copy this file to sms\AdminConsole\XmlStorage\Forms.  

2.  The Windows Installer file should contain code to invoke the DeploymentTypeExtender.Extend method, which is located in the Microsoft.ConfigurationManagement.ApplicationManagement namespace. This will then register the extension files for a given site server computer. For an administrator console computer, this will initialize the cache for that user. The Extend method call requires the *.cmdtx file created earlier.  

    1.  Make a standard WqlConnectionManager connection to the site server.  

    2.  Call the Extend method, passing the *cmdtx file, the ConnectionManagerBase object through an instance of ConsoleDcmConnection for the method connection parameter, and the connection path (example below).  

    > [!WARNING]
    >  In order to use ConsoleDcmConnection, you will need to add an assembly reference to AdminUI.DcmObjectWrapper.dll.  

    ```  
    using DCM = Microsoft.ConfigurationManagement.AdminConsole.DesiredConfigurationManagement;   

    [...]  

        ConnectionManagerBase connectionManager = new WqlConnectionManager();  
        connectionManager.Connect("SiteServerName");  

        DeploymentTypeExtender.Extend(@"C:\RdpTechnology.cmdtx", new  DCM.ConsoleDcmConnection(connectionManager, null), @"\\SiteServerName\root\sms\site_ABC");  
    ```  

3.  Client Installation (HandlerApplication.zip)  

     To install the client extension files, either as part of the HandlerApplication or as a separate installation:  

    1.  Compile the AppSynclet MOF file. On the client, compile the custom synclet MOF file to create the necessary instance of the CCM_AppHandler class and the corresponding instances of the CCM_HandlerSynclet classes.  

        ```  
        C:\> mofcomp appsynclet_<technologyid>   
        ```  

    2.  Copy the handler .dll to the Configuration Manager client directory and register the .dll on the system.  

        ```  
        C:\> regsvr32 <technologyid>handler.dll  
        ```  

    > [!NOTE]
    >  The handler .dll must be compiled to match the operating system – either 32-bit or 64-bit.  

#### Namespaces  
 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

#### Assemblies  
 AdminUI.DcmObjectWrapper.dll  

 AdminUI.WqlQueryEngine.dll  

 DcmObjectModel.dll  

 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

 Microsoft.ConfigurationManagement.ApplicationManagement.Extender.dll  

 Microsoft.ConfigurationManagement.ManagementProvider.dll  

## See Also  
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
