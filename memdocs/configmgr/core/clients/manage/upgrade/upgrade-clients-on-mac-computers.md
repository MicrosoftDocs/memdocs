---
title: Upgrade macOS clients
titleSuffix: Configuration Manager
description: Upgrade the Configuration Manager client on Mac computers.
ms.date: 01/05/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to upgrade clients on Mac computers in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in January 2022, this feature of Configuration Manager is deprecated.<!-- 12927803 --> For more information, see [Mac computers](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

Follow the high-level steps in this article to upgrade the client for Mac computers by using a Configuration Manager application. You can also download the Mac client installation file, copy it to a shared network location or a local folder on the Mac computer, and then instruct users to manually run the installation.  

> [!NOTE]  
> Before you do these steps, make sure that your Mac computer meets the prerequisites. For more information, see [Supported operating systems for Mac computers](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

## Download the latest Mac client

The Mac client for Configuration Manager isn't supplied on the Configuration Manager installation media. The Mac client installation files are contained in a Windows Installer file named **ConfigmgrMacClient.msi**.

> [!NOTE]
> The macOS client installation package isn't available for new deployments, but existing deployments are supported until December 31, 2022.<!-- 12927803 -->

## Create the Mac client installation file

On a computer that runs Windows, run **ConfigmgrMacClient.msi**. This installer unpacks the Mac client installation file, named **Macclient.dmg**. By default, you can find this file in the following folder: **C:\Program Files\Microsoft\System Center Configuration Manager for Mac client**.  

## Extract the client installation files

Copy **Macclient.dmg** to a Mac computer. Mount the Macclient.dmg file in macOS, and then copy the contents to a folder on the Mac computer.  

## Create a .cmmac file

1. Open the **Tools** folder of the Mac client installation files. Use the **CMAppUtil** tool to create a .cmmac file from the client installation package. You'll use this file to create the Configuration Manager application.  

2. Copy the new **CMClient.pkg.cmmac** file to a network location that's available to the computer running the Configuration Manager console.  

    For more information, see the [Supplemental procedures to create and deploy applications for Mac computers](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## Create and deploy the app

1. In the Configuration Manager console, [create an application](../../../../apps/get-started/creating-mac-computer-applications.md) from the **CMClient.pkg.cmmac** file.  

2. [Deploy this application](../../../../apps/deploy-use/deploy-applications.md) to Mac computers in your hierarchy.  

## Install the updated client

The existing Configuration Manager client on Mac computers will prompt the user that an update is available to install. After users install the client, they must restart their Mac computer.  

After the computer restarts, the **Computer Enrollment** wizard automatically runs to request a new user certificate.

If you don't use Configuration Manager enrollment, but install the client certificate independently from Configuration Manager, see [Configure clients to use an existing certificate](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure clients to use an existing certificate

Use this procedure to prevent the Computer Enrollment Wizard from running, and to configure the upgraded client to use an existing client certificate.  

1. In the Configuration Manager console, [create a configuration item](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) of the type **Mac OS X**.  

1. Add a setting to this configuration item with the setting type **Script**.  

1. Add the following script to the setting:  

    ``` Shell
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  
    ```  

1. Add the configuration item to a [configuration baseline](../../../../compliance/deploy-use/create-configuration-baselines.md). Then [deploy the configuration baseline](../../../../compliance/deploy-use/deploy-configuration-baselines.md) to all Mac computers that install a certificate independently from Configuration Manager.  
