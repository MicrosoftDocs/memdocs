---
title: "Connecting with Windows PowerShell"
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
ms.assetid: 1d466a0b-bb4a-4648-8f16-9b6c897934f5searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Connecting to Configuration Manager with Windows PowerShell
In the [Configuration Manager Windows PowerShell Basics](../../../develop/core/understand/windows-powershell-basics.md) topic, you tried a few basic Windows PowerShell cmdlets. This topic helps you connect to Configuration Manager from your Windows PowerShell environment.  

## Loading Windows PowerShell from the Configuration Manager Console  
 The easiest method to load Windows PowerShell is directly from the Configuration Manager console.  

1.  Start by launching the Configuration Manager console. In the upper left corner, there’s a blue rectangle. Click the white arrow in the blue rectangle, and choose **Connect via Windows PowerShell**.  

     ![PowerShell Menu](../../../develop/core/understand/media/cmpowershellmenucb.PNG "CMPowerShellMenuCB")  

2.  Once Windows PowerShell loads, you’ll see a prompt that contains your site code. For example, if the site code is “ABC��?, the prompt looks like:  

    ```  
    PS ABC:\>  
    ```  

3.  Let’s just verify everything is working fine. The first cmdlet you’ll try is `Get-CMSite`. This cmdlet will return information about the Configuration Manager site we’re currently connected to.  

     Go to your Windows PowerShell window, and type in `Get-CMSite`:  

    ```  
    PS ABC:\> get-cmsite  

    BuildNumber       : 7958  
    Features          : 0000000000000000000000000000000000000000000000000000000000000000  
    InstallDir        : C:\Program Files\Microsoft Configuration Manager  
    Mode              : 0  
    ReportingSiteCode :  
    RequestedStatus   : 110  
    ServerName        : SDKTESTLAB.test.lab  
    SiteCode          : ABC  
    SiteName          : ABC Test Site  
    Status            : 1  
    TimeZoneInfo      : 000001E0 0000 000B 0000 0001 0002 0000 0000 0000 00000000 0000 0003 0000 0002 0002 0000 0000 0000  
                        FFFFFFC4  
    Type              : 2  
    Version           : 5.00.7958.1000  

    ```  

## Importing the Configuration Manager PowerShell Module  
 Another method of connecting to Configuration Manager from your Windows PowerShell environment is to load the Configuration Manager module manually.  

1.  Hit your Windows Key and type “PowerShell��? – then right-click **Windows PowerShell** and choose “Run as administrator��?.  

     You should now see your PowerShell environment.  

    ```  
    Windows PowerShell  
    Copyright (C) 2016 Microsoft Corporation. All rights reserved.  

    PS C:\WINDOWS\system32>  
    ```  

2.  Now, you’ll need to import the Configuration Manager module using the built-in Windows PowerShell cmdlet `Import-Module`. To import the Configuration Manager module, you will have to specify the path to the Configuration Manager module or change to the directory that contains the module.  

     Go to your Windows PowerShell window, and type in `CD ‘C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin’`:  

    ```  
    PS C:\>  
    PS C:\> CD ‘C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin’  
    PS C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin>  

    ```  

     Go to your Windows PowerShell window, and type in `import-module .\ConfigurationManager.psd1 -verbose`:  

    ```  
    PS C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin>  
    PS C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin> import-module .\ConfigurationManager.psd1 -verbose  

    Note: The ‘-verbose’ switch displays a list of the cmdlets being imported (quite a long list in the case of Configuration Manager).  

    ```  

3.  Confirm that the Configuration Manager module has been loaded using the `Get-CMSite` cmdlet.  

     Go to your Windows PowerShell window, and type in `Get-CMSite`:  

    ```  
    PS C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin>Get-CMSite  
    get-cmsite : This command cannot be run from the current drive. To run this command you must first connect to a Configuration Manager drive.  
    at line:1 char:1  
     get-cmsite  
     ~~~~~~~~~~  
       + CategoryInfo          : NotSpecified: (:) [Get-CMSite], InvalidOperationException  
       + FullyQualifiedErrorId : System.InvalidOperationException,Microsoft.ConfigurationManagement.Cmdlets.HS.Commands.GetSiteCommand  

    PS C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin>  
    ```  

     The error was caused by our current path pointing to the local hard drive (our Configuration Manager Console path) not the Configuration Manager site.  

    > [!IMPORTANT]
    >  To run the Configuration Manager cmdlets, you need to switch the path to the Configuration Manager site.  

4.  Go to your Windows PowerShell window, and type in `CD <site code>:`, replacing \<site code> with your site code (the site code “ABC��? is used below):  

    ```  
    PS C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin> CD ABC:   
    PS ABC:\>  
    ```  

5.  Now, try to again to confirm that the Configuration Manager module has been loaded using the `Get-CMSite` cmdlet.  

     Go to your Windows PowerShell window, and type in `Get-CMSite`:  

    ```  
    PS ABC:\> Get-CMSite  

    BuildNumber       : 7958  
    Features          : 0000000000000000000000000000000000000000000000000000000000000000  
    InstallDir        : C:\Program Files\Microsoft Configuration Manager  
    Mode              : 0  
    ReportingSiteCode :  
    RequestedStatus   : 110  
    ServerName        : SDKTESTLAB.test.lab  
    SiteCode          : ABC  
    SiteName          : ABC Test Site  
    Status            : 1  
    TimeZoneInfo      : 000001E0 0000 000B 0000 0001 0002 0000 0000 0000 00000000 0000 0003 0000 0002 0002 0000 0000 0000  
                        FFFFFFC4  
    Type              : 2  
    Version           : 5.00.7958.1000  

    ```  

6.  Success! You are connected to the Configuration Manager site and the Configuration Manager module is loaded.  

## Update Help!  
 PowerShell 3.0 introduced a new feature to update your Windows PowerShell help over the Internet.  

1.  You can update Windows PowerShell help (and specifically the help for the Configuration Manager cmdlets) using the `Update-Help` cmdlet.  

     If your computer is connected to the Internet, go to your Windows PowerShell window, and type in `Update-Help –Module configurationmanager`.  

    ```  
    PS ABC:\> Update-Help –Module configurationmanager  
    PS ABC:\>  
    ```  

2.  You can get help about Windows PowerShell cmdlets by using the `Get-Help` cmdlet.  

     Go to your Windows PowerShell window, and type in `Get-Help Get-CMSite`:  

    ```  
    PS ABC:\> Get-Help Get-CMSite  

    NAME  
        Get-CMSite  

    SYNOPSIS  
        Gets one or more Configuration Manager sites.  

    SYNTAX  
        Get-CMSite [-Name <string>]  [<CommonParameters>]  

        Get-CMSite -SiteCode <string>  [<CommonParameters>]  

    DESCRIPTION  
        The Get-CMSite cmdlet gets one or more Microsoft System Center Configuration Manager sites. A SystemCenter  
        Configuration Manager site is a server that has clients assigned to it and that processes client-generated data.  
        You can get a Configuration Manager site by using either a site name or a site code.  

    RELATED LINKS  
        Online Version: http://go.microsoft.com/fwlink/?LinkID=263855  
        Set-CMSite  

    REMARKS  
        To see the examples, type: "get-help Get-CMSite -examples".  
        For more information, type: "get-help Get-CMSite -detailed".  
        For technical information, type: "get-help Get-CMSite -full".  
        For online help, type: "get-help Get-CMSite -online"  

    ```  

## See Also  
 [Getting Started with Configuration Manager Windows PowerShell](../../../develop/core/understand/getting-started-with-configuration-manager-and-windows-powershell.md)
