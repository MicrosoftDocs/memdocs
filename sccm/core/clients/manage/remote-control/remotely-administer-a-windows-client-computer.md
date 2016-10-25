---
title: "Remotely administer Windows computer | System Center Configuration Manager"
description: "Administer a remote Windows client computer by using System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigmanms.author: nbigmanmanager: angrobe

---
# How to remotely administer a Windows client computer by using System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Use the following procedure to remotely administer a computer in System Center Configuration Manager.  

 Before you begin to use remote control, ensure that you have reviewed the information in the following topics:  

-   [Planning for remote control in System Center Configuration Manager](../../../../core/clients/manage/remote-control/planning-for-remote-control.md)  

-   [Configuring remote control in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

 You can start the Configuration Manager remote control viewer by using one of three methods:  

-   By using the Configuration Manager console.  

-   At the Windows command prompt.  

-   On the Windows **Start** menu on a computer that runs the Configuration Manager console from the **Microsoft System Center 2012** program group.  

### To remotely administer a client computer from the Configuration Manager console  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Devices** or **Device Collections**.  

3.  Select the computer that you want to remotely administer and then, in the **Home** tab, in the **Device** group, click **Start**, and then click **Remote Control**.  

    > [!IMPORTANT]  
    >  If the client setting **Prompt user for Remote Control** permission is set to **True**, the connection does not initiate until the user at the remote computer agrees to the remote control prompt. For more information, see [Configuring remote control in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  After the **Configuration Manager Remote Control** window opens, you can remotely administer the client computer. Use the following options to configure the connection.  

    > [!NOTE]  
    >  If the computer that you connect to has multiple monitors, the display from all these monitors is shown in the remote control window.  

    -   **File - Connect** - Connect to another computer. This option is unavailable when a remote control session is active.  

    -   **File - Disconnect** - Disconnects the active remote control session but does not close the **Configuration Manager Remote Control** window.  

    -   **File - Exit** - Disconnects the active remote control session and closes the **Configuration Manager Remote Control** window.  

        > [!NOTE]  
        >  When you disconnect a remote control session, the contents of the Windows Clipboard on the computer that you are viewing is deleted.  

    -   **View - Full Screen** - Maximizes the **Configuration Manager Remote Control** window to fill all the available display space.  

        > [!NOTE]  
        >  To exit full screen mode, press Ctrl+Alt+Break.  

    -   **View - Scale to Fit** - Scales the display of the remote computer to fit the size of the **Configuration Manager Remote Control** window.  

    -   **View - Status Bar** - Toggles the display of the **Configuration Manager Remote Control** window status bar.  

    -   **Action - Send Ctrl+Alt+Del Key** - Sends a Ctrl+Alt+Del key combination to the remote computer.  

    -   **Action - Enable Clipboard Sharing** - Lets you copy and paste items to and from the remote computer. If you change this value, you must restart the remote control session for the change to take effect.  

        > [!NOTE]  
        >  If you do not want clipboard sharing to be enabled in the Configuration Manager console, on the computer running the console, set the value of the registry key, **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** to **0**.  

    -   **Action - Lock Remote Keyboard and Mouse** - Locks the remote keyboard and mouse to prevent the user from operating the remote computer.  

    -   **Help - About Remote Control** - Displays information about the current version of the remote control viewer.  

5.  Users at the remote computer can view more information about the remote control session when they click the Configuration Manager**Remote Control** icon in the Windows notification area or the icon on the remote control session bar.  

6.  When you no longer require the remote control session, use one of the methods detailed earlier to end the remote control session.  

### To start the remote control viewer from the Windows command line  

-   At the Windows command prompt, type *<Configuration Manager Installation Folder\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

    > [!NOTE]  
    >  CmRcViewer.exe supports the following command-line options:  
    >   
    >  -   *<Address\>* - Specifies the NetBIOS name, the fully qualified domain name (FQDN), or the IP address of the client computer that you want to connect to.  
    > -   *<Site Server Name\>* - Specifies the name of the System Center 2012 Configuration Manager site server to which you want to send status messages that are related to the remote control session.  
    > -   **/?** - Displays the command-line options for the remote control viewer.  
    >   
    >  **Example:CmRcViewer.exe** *<Address\>* *<\\\Site Server Name>*  
