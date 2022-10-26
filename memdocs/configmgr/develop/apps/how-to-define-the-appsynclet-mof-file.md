---
title: How to Define the AppSynclet MOF File
description: To define a custom synclet MOF file, create an instance of the CCM_AppHandlers class.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: ac9193e8-f6c8-4acf-ba1f-95e95d54d4ad
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Define the AppSynclet MOF File
To define a custom synclet MOF file, create an instance of the CCM_AppHandlers class. The new class instance will identify the custom client-side handler.  Also, create instances of the CCM_HandlerSynclet class to store, detect, install and uninstall property values.  

 The client extension maps closely to the Installer object, defined as part of the DeploymentType. Property values are stored in WMI and the public COM methods in the client-side handler map to detection, installation and uninstallation.  

 In this example, a new custom synclet MOF file is required for Remote Desktop Protocol (RDP) files.  Support for RDP files isn't built-in to Configuration Manager, so a custom synclet MOF file is required.  

### To define a custom synclet MOF file  

1.  Create an instance of the `CCM_AppHandlers` class. This class associates the synclet with the custom client-side handler. The HandlerCLSID value is the globally unique identifier that identifies the custom client-side handler's COM object.  This, and the other class instances will be stored in WMI under root\ccm\cimodels.  

     The following example from the RDP sample project demonstrates how to define a custom synclet MOF file.  

    ```  
    //******************************************************************************  
    //  
    // The following are the registrations of the Rdp handler  
    //  
    //******************************************************************************  
    instance of CCM_AppHandlers  
    {  
        HandlerName     = "Rdp";  
        HandlerCLSID    = "{4A1FFE05-FEF1-41E3-8DE1-732474E5983D}";  
    };  
    ```  

2.  Creates custom instance of the `CCM_HandlerSynclet` class to store the Detect action property values.  

     The following example from the RDP sample project demonstrates how to define a custom synclet MOF file.  

    ```  
    //******************************************************************************  
    //  
    // Rdp_Detect_Synclet  
    //  
    //******************************************************************************  
    class Rdp_Detect_Synclet : CCM_HandlerSynclet  
    {  
        [ Not_Null ]   
        string      FileName;   

        [ Not_Null ]   
        string      InstallFolder;   

        [ Not_Null ]   
        string      FullAddress;   

        string      RemoteApplication;   
        boolean     RemoteApplicationMode;   
    };  
    ```  

3.  Create a custom instance of the `CCM_HandlerSynclet` class to store the Install action property values.  

     The following example from the RDP sample project demonstrates how to define a custom synclet MOF file.  

    ```  
    //******************************************************************************  
    //  
    // Rdp_Install_Synclet  
    //  
    //******************************************************************************  
    class Rdp_Install_Synclet : CCM_HandlerSynclet  
    {  
        [ Not_Null ]   
        string  Filename;   

        [ Not_Null ]   
        string  InstallFolder;   
        sint32  FullScreen;   
        sint32  DesktopWidth;   
        sint32  DesktopHeight;   
        sint32  AudioMode;   
        string  FullAddress;   
        string  RemoteServerName;   
        sint32  RemoteServerPort;   
        string  RemoteApplication;   
        boolean RemoteApplicationMode;   
        boolean ConstructRdpOnClient;   
        sint32  KeyboardMode;   
        sint32  RedirectPrinters;   
        sint32  RedirectSmartCards;   
        string  Username;   
        string  ContentFilename;   
    };  
    ```  

4.  Create a custom instance of the `CCM_HandlerSynclet` class to store the Uninstall action property values.  

     The following example from the RDP sample project demonstrates how to define a custom synclet MOF file.  

    ```  
    //******************************************************************************  
    //  
    // Rdp_Uninstall_Synclet  
    //  
    //******************************************************************************  
    class Rdp_Uninstall_Synclet : CCM_HandlerSynclet  
    {  
        [ Not_Null ]   
        string  FileName;   

        [ Not_Null ]   
        string  InstallFolder;   
    };  
    ```  

## See Also  
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
