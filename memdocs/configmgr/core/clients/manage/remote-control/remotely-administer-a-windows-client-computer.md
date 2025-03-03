---
title: Remotely administer Windows computer
titleSuffix: Configuration Manager
description: Administer a remote Windows client computer by using Configuration Manager.
ms.date: 10/08/2020
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to remotely administer a Windows client computer by using Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager allows you to connect to client computers using **Configuration Manager Remote Control**. Before you begin to use remote control, ensure that you review the information in the following articles:  

- [Prerequisites for remote control](prerequisites-for-remote-control.md)  

- [Configuring remote control](configuring-remote-control.md)  

Here are three ways to start the remote control viewer:  

- In the Configuration Manager console.  

- In a Windows command prompt.  

- From the Windows **Start** menu, on a computer that runs the Configuration Manager console, in the **Microsoft Endpoint Manager** program group.  

    > [!NOTE]
    > The above Start menu path is for versions from November 2019 (version 1910) or later. In earlier versions, the folder name is **Microsoft System Center**.

## To remotely administer a client computer from the Configuration Manager console  

1. In the Configuration Manager console, choose **Assets and Compliance** > **Devices** or **Device Collections**.  

1. Select the computer that you want to remotely administer and then, in the **Home** tab, in the **Device** group, choose **Start** > **Remote Control**.  

    > [!IMPORTANT]  
    >  If the client setting **Prompt user for Remote Control** permission is set to **True**, the connection does not initiate until the user at the remote computer agrees to the remote control prompt. For more information, see [Configuring remote control](configuring-remote-control.md).  

1. After the **Configuration Manager Remote Control** window opens, you can remotely administer the client computer. Use the following options to configure the connection.  

    > [!NOTE]  
    >  If the computer that you connect to has multiple monitors, the display from all the monitors is shown in the remote control window.  

    - **File**
        - **Connect** - Connect to another computer. This option is unavailable when a remote control session is active.  
        - **Disconnect** - Disconnects the active remote control session but doesn't close the **Configuration Manager Remote Control** window.  
        - **Exit** - Disconnects the active remote control session and closes the **Configuration Manager Remote Control** window.  

        > [!NOTE]  
        >  When you disconnect a remote control session, the contents of the Windows Clipboard on the computer that you are viewing is deleted.

    - **View**
      - **Color depth**  - Choose either 16 bits or 32 bits per pixel.
      - **Full Screen** - Maximizes the **Configuration Manager Remote Control** window. To exit full screen mode, press Ctrl+Alt+Break.  
      - **Optimize for low bandwidth connection** - Choose this option if the connection is low bandwidth.
      - **Display:**
        - **All Screens** - If the computer that you connect to has multiple monitors, the display from all the monitors is shown in the remote control window.
        - **First Screen** - The *first screen* is at the top and far left as shown in Windows display settings. You can't select a specific screen. When you switch the configuration of the viewer, reconnect the remote session. The viewer saves your preference for future connections.
        - **Scale to Fit** - Scales the display of the remote computer to fit the size of the **Configuration Manager Remote Control** window.
        - **Status Bar** - Toggles the display of the **Configuration Manager Remote Control** window status bar.  

       > [!NOTE]  
       >  The viewer saves your preference for future connections.

    - **Action**
        - **Send Ctrl+Alt+Del Key** - Sends a Ctrl+Alt+Del key combination to the remote computer.
        - **Enable Clipboard Sharing** - Lets you copy and paste items to and from the remote computer. If you change this value, you must restart the remote control session for the change to take effect.
          - If you don't want clipboard sharing to be enabled in the Configuration Manager console, on the computer running the console, set the value of the registry key **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** to **0**.
        - **Enable Keyboard Translation** - Translates the keyboard layout of the computer running the console to the connected device's layout.
        - **Lock Remote Keyboard and Mouse** - Locks the remote keyboard and mouse to prevent the user from operating the remote computer.  

    - **Help**
        - **About Remote Control** - Displays the current version of the viewer.  

1. Users at the remote computer can view more information about the remote control session when they click the Configuration Manager **Remote Control** icon. The icon is in the Windows notification area or the icon on the remote control session bar.  

## To start the remote control viewer from the Windows command line  

- At the Windows command prompt, type _<Configuration Manager Installation Folder\>_**\AdminConsole\Bin\i386\CmRcViewer.exe**  

CmRcViewer.exe supports the following command-line options:  

- `Address` - Specifies the NetBIOS name, the fully qualified domain name (FQDN), or the IP address of the client computer that you want to connect to.
- `Site Server Name` - Specifies the name of the Configuration Manager site server to which you want to send status messages that are related to the remote control session.
- `/?` - Displays the command-line options for the remote control viewer.  

**Example:** `CmRcViewer.exe <Address> <\\Site Server Name>`

> [!NOTE]  
> The remote control viewer is supported on all operating systems that are supported for the Configuration Manager console. For more information, see [Supported configurations for Configuration Manager consoles](../../../plan-design/configs/supported-operating-systems-consoles.md) and [Prerequisites for remote control](prerequisites-for-remote-control.md).

## Next steps

[Audit remote control usage](audit-remote-control-usage.md)
