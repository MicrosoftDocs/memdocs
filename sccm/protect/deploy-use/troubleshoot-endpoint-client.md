---
title: "Troubleshooting Windows Defender or Endpoint Protection client"
description: "Learn how to troubleshoot problems with Windows Defender and Endpoint Protection."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: 7
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe

---
# Troubleshooting Windows Defender or Endpoint Protection client

*Applies to: System Center Configuration Manager (Current Branch)*


If you encounter problems with Windows Defender or Endpoint Protection, contact your security administrator for support. You can also try to troubleshoot the following problems:  

-   [Update Windows Defender or Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [Starting Windows Defender or Endpoint Protection service](#starting-windows-defender-or-endpoint-protection-service)  
-   [Internet connection issues](#internet-connection-issues)  
-   [Detected threat can't be remediated](#detected-threat-cant-be-remediated)  
-   [Install the Endpoint Protection client](#install-the-endpoint-protection-client)  

##  Update Windows Defender or Endpoint Protection  
 Windows Defender or Endpoint Protection works automatically with Microsoft Update to ensure that your virus and spyware definitions are kept up to date.  

 **Symptoms**  

 This article addresses common issues with automatic updates, including the following situations:  

-   You see error messages indicating that updates have failed.  

-   When you check for updates, you receive an error message that the virus and spyware definition updates cannot be checked, downloaded, or installed.  

-   Even though you are connected to the Internet, the updates fail.  

-   Updates are not automatically installing as scheduled.  

 **Cause**  

 The most common causes for update issues are problems with Internet connectivity. However, if you know you are connected to the Internet because you can browse to other Web sites, the issue might be caused by conflicts with your settings in Windows Internet Explorer.  

> [!IMPORTANT]  
>  You have to exit Internet Explorer to complete these steps. Therefore, print them, write them down, or copy them to another file, and then bookmark this topic for future access.  

### Step 1: Reset your Internet Explorer settings  

1.  Exit all open programs, including Internet Explorer.  

    > [!NOTE]  
    >  Resetting these settings in Internet Explorer deletes your temporary files, cookies, browsing history, and your online passwords. But, your favorites are not deleted.  

2.  Click **Start** and search for **inetcpl.cpl**, and then press **Enter**.  

3.  In the **Internet Options** dialog box, click the **Advanced** tab.  

4.  Under the **Reset Internet Explorer settings**, click **Reset**, and then click **Reset** again.  

5.  Wait until Internet Explorer finishes resetting the settings, and then click **OK**.  

6.  Open Internet Explorer.  

7.  Open Microsoft Security Essentials, click the **Update** tab, and then click **Update**.  

8.  If the issue persists, proceed to the next step.  

### Step 2: Set Internet Explorer as the default browser  

1.  Exit all open programs, including Internet Explorer.  

2.  Click **Start** and search for **inetcpl.cpl**, and then press **Enter**.  

3.  In the **Internet Options** dialog box, click the **Programs** tab.  

4.  Under **Default Web browser**, click **Make default**.  

5.  Click **OK**.  

6.  Open Windows Defender or Endpoint Protection. Click the **Update** tab, and then click **Update**.  

7.  If the issue persists, proceed to the next step.  

### Step 3: Ensure that the date and time are set correctly on your computer  

1.  Open Windows Defender or Endpoint Protection.  

2.  If the error message that you received contains the code 0x80072f8f, the problem is most likely caused by an incorrect date or time setting on your computer.  

3.  To reset your computer's date or time setting, follow the steps in [Fix broken desktop shortcuts and common system maintenance tasks](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579).  

### Step 4: Rename the Software Distribution folder on your computer  

1. Stop the Automatic Updates service  

    1.  Click **Start** and search for **services.msc**, and then click **OK**.  

    2.  Right-click the **Automatic Updates service**, and then click **Stop**.  

    3.  Minimize the Services snap-in.  

2.  Rename the **SoftwareDistribution** directory as follows:  

    1.  Click **Start** and search for  **cmd**, and then click **OK**.  

    2.  Type **cd %windir%**, and then press **Enter**.  

    3.  Type **ren SoftwareDistribution SDTemp**, and then press **Enter**.  

    4.  Type **exit**, and then press **Enter**.  

3.  Start the Automatic Updates service as follows:  

    1.  Maximize the Services snap-in.  

    2.  Right-click **Automatic Updates service**, and then click **Start**.  

    3.  Close the Services snap-in window.  

### Step 5: Reset the Microsoft antivirus update engine on your computer  

1.  Click **Start** and search for  **cmd**, and then click **OK**and then right-click **Command Prompt**, and then select **Run as administrator**.  

2.  In the **Command Prompt** window, type the following commands and press **Enter** after each command:  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Exit**  

3.  Restart your computer.  

4.  Open Windows Defender or  
          Endpoint Protection, click the **Update** tab, and then click **Update**.  

5.  If the issue persists, proceed to the next step.  

### Step 6: Manually install the virus and spyware definition updates  

-   If you are running a 32-bit Windows operating system, download the latest updates manually at [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342).  

-   If you are running a 64-bit Windows operating system, download the latest updates manually at [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341).  

-   Click **Run**. The latest updates are manually installed on your computer.  


### Step 7: Contact Support  

-   If the steps did not resolve the issue, contact support. For more information, see [Customer Support](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174).  

##  Starting Windows Defender or Endpoint Protection service  
 **Symptom**  

 You receive a message notifying you that **Windows Defender or Endpoint Protection isn't monitoring your computer because the program's service stopped. You should restart it now.** 

 **Solution**  

### Step 1: Restart your computer.  

-   Close all applications and restart your computer.  

### Step 2: Make sure the "Windows Defender" or "Endpoint Protection service" is set to automatic and is started  

1.  Click **Start** and search for **services.msc**, and then press **Enter**.  

2.  Search for **Microsoft Antimalware Service**. Right click it and select **Properties** or double-click it to open the service.  

3.  Check to make sure that the "**Startup Type**" is set to "**Automatic**".  

4.  Click the **Start** button to start the service. If the **Start** button is not available, click the **Stop** button, and then click the **Start** button to restart the service.  

5.  Make sure you note any errors that may appear during this process, submit a case online, and include the error information.  

### Step 3: Remove any existing Internet security programs  

1.  Click **Start** and search for **appwiz.cpl**, and then press **Enter**.  

2.  In the list of installed programs, uninstall any third-party Internet security programs.*  

3.  Restart your computer, and then try to install Windows Defender or  
          Endpoint Protection again.  

> [!NOTE]  
>  Some Internet security applications do not uninstall completely. You may need to download and run a cleanup utility for your previous security application in order for it to be completely removed.  

> [!CAUTION]  
>  When you remove Internet security programs, your computer is unprotected. If you have problems installing   
>       Endpoint Protection after you remove existing Internet security programs, contact Windows Defender or  
>       Endpoint Protection support by submitting a case online (for more information, see [How to Submit a Case Online](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx)).  

### Step 4: Uninstall/reinstall Endpoint Protection  

1.  Click **Start** and search for **appwiz.cpl**, and then press **Enter**.  

2.  In the list of installed programs, click **Endpoint Protection**, and then uninstall it.  

3.  If prompted, restart your computer, and then try to install Endpoint Protection again.  

##  Internet connection issues  
 In order to make sure that your computer receives the latest updates from Windows Update, you must be connected to the Internet.  

### Step 1: Verify that your computer is connected to the Internet  

1.  Click **Start**and search for **ncpa.cpl**, and then press **Enter**.  

2.  Right-click the connection name and then click **Status**.  

3.  If your computer is connected, in Windows XP the connection status will appear as **Connected**, **Enabled**, or **Authentication** succeeded. In Windows Vista and Windows 7, the **IPv4** status will appear as **Internet**.  

4.  If your computer doesn't appear to be connected, right-click the connection name, and then click **Connect**, **Enable**, **Authenticate**, or **Repair**.  

### Step 3: Restart your computer  

-   Close any open programs and restart your computer.  

### Step 4: If you still can't connect to the Internet, check your connections  

1.  If you use a dial-up connection, make sure the telephone cord connection in the wall jack and in your modem are firmly connected.  

2.  If you use a cable modem, make sure the cable connection to the modem and the connection from the modem to your computer are firmly connected.  

3.  If you use a cable modem or DSL router, make sure the connections to the router and to the computer are firmly connected. Try unplugging and turning off the router and modem. Wait a few minutes, plug in the modem in first, wait one minute, then plug in the router, and restart your computer.  

##  Detected threat can't be remediated  
 When Windows Defender or  
      Endpoint Protection detects a potential threat that's hiding inside a compressed file with a .zip file name extension or within a network share, it tries to deal with the threat by quarantining or removing the threat.  

### Remove or scan the file  

-   If the detected threat was in a .zip file, browse to the .zip file, and then either remove the file or scan it by right-clicking the file and selecting **Scan with Windows Defender** or **Scan with Endpoint Protection**. If Windows Defender or Endpoint Protection detects additional threats in the file, it notifies you about these threats and enables you to choose an appropriate action.  

-   If the detected threat was in a network share, browse to the network share and scan it by right-clicking the file and selecting **Scan with Windows Defender** or **Scan with Endpoint Protection**. If Windows Defender or Endpoint Protection detects additional threats in the network share, it notifies you about these threats and enables you to choose an appropriate action.  

-   If you're not sure of the file's origin, one of the best solutions is to run a full scan on your computer. A full scan may take some time to complete, but it makes it possible for Windows Defender or Endpoint Protection to look for the source of the infection and clean it.  

##  Install the Endpoint Protection client  

> [!NOTE]  
>  Windows Defender is installed with the operating system on Windows 10 PC's.  

 **Symptoms**  

 Installation fails for an unknown reason, or you receive an error message with error code, such as 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E, or 0x8007007E.  

 If your computer is running Windows XP Service Pack 2 (SP2), you might see one or more of the following error messages:  

-   Installation Wizard is missing a filter manager rollup package needed to complete the installation.  

-   KB914882 Setup Error, Setup cannot update your Windows XP files because the language installed on your system is different from the update language.  

 **Cause**  

 Endpoint Protection cannot be installed on a computer that is running other security programs. Sometimes, even if you remove other security programs, they do not completely uninstall. You must be running a genuine version of the Windows operating system to install Endpoint Protection.  

 **Solution**  

> [!IMPORTANT]  
>  You will need to restart your computer while resolving this issue. Bookmark this page (mark it as a Favorite) to make it easier to find this topic again or print it for easy reference.  

### Step 1: Remove any existing security programs  
**Endpoint Protection only**

1.  Completely uninstall any existing Internet security programs.  

2.  Restart your computer.  

3.  Install Endpoint Protection again. If this does not resolve the issue, continue to the next step.  

### Step 2: Ensure that the Windows Installer service is running  

1.  Click **Start** and search for **services.msc**, and then press **Enter**.  

2.  Right-click **Windows Installer**, and then click **Start**. If **Start** is unavailable and the **Stop** and **Restart** options are available, this tells you that the service is already started.  

3.  On the **Services** page, on the **File** menu, click **Exit**.  

4.  Click **Start** and search for **command prompt**. Right-click **Command Prompt**, and then click **Run as administrator**.  

5.  Type **MSIEXEC /REGSERVER**, and then press **Enter**.  

    > [!NOTE]  
    >  There is no indication that this command has succeeded or failed.  

6.  Install Endpoint Protection again. If this does not resolve the issue, continue to the next step.  

### Step 3: Start Windows in Selective Startup mode  

1.  Click **Start** and search for **msconfig**, and then press **Enter**.  

2.  On the **General** tab, click **Selective Startup**, and then clear the **Load Startup Items** check box.  

3.  On the **Services** tab, select the **Hide All Microsoft Services** check box, and then clear all the check boxes for the services that remain in the list.  

4.  Click **OK**, and then click **Restart** to restart the computer.  

5.  Try to install Endpoint Protection again.  



### See also  
 [Endpoint Protection client frequently asked questions](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Endpoint Protection Client Help](../../protect/deploy-use/endpoint-protection-client-help.md)
