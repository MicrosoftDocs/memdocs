---
title: Troubleshoot Endpoint Protection
titleSuffix: Configuration Manager
description: Learn how to troubleshoot problems with Windows Defender and Endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Troubleshoot Windows Defender or Endpoint Protection client

*Applies to: Configuration Manager (current branch)*

If you come across problems with Windows Defender or Endpoint Protection, use this article to troubleshoot the following problems:  

- [Update Windows Defender or Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [Starting Windows Defender or Endpoint Protection service](#starting-windows-defender-or-endpoint-protection-service)  
- [Internet connection issues](#internet-connection-issues)  
- [Detected threat can't be remediated](#detected-threat-cant-be-remediated)  

## Update Windows Defender or Endpoint Protection

### Symptoms

Windows Defender or Endpoint Protection works automatically with Microsoft Update to make sure that your virus and spyware definitions are kept up-to-date.  

This section addresses common issues with automatic updates, including the following situations:  

- You see error messages indicating that updates have failed.  

- When you check for updates, you receive an error message that the virus and spyware definition updates can't be checked, downloaded, or installed.  

- Even though your device is connected to the internet, the updates fail.  

- Updates aren't automatically installing as scheduled.  

### Causes

The most common causes for update issues are problems with internet connectivity. If you know your device is connected to the internet because you can browse to other Web sites, the issue might be caused by conflicts with your internet settings in Windows.  

### Options to resolve

#### Step 1: Reset your internet settings  

1. Exit all open programs, including the web browser.  

    > [!NOTE]  
    > When you reset these internet settings, it may delete your browser temporary files, cookies, browsing history, and online passwords. It doesn't delete your favorites.  

2. Go to the **Start** menu, and open `inetcpl.cpl`.  

3. Switch to the **Advanced** tab.  

4. In the section to **Reset Internet Explorer settings**, select **Reset**, and then select **Reset** again to confirm.  

5. Select **OK** when the settings are reset.

6. Try to update Windows Defender again.

If the issue persists, continue to the next step.  

#### Step 2: Make sure that the date and time are set correctly on your computer  

If the error message contains the code 0x80072f8f, the problem is most likely caused by an incorrect date or time setting on your computer. Go to the **Start** menu, select **Settings**, select **Time & language**, and select **Date & time**.

#### Step 3: Rename the Software Distribution folder on your computer  

1. Stop the **Windows Update** service.  

    1. Go to **Start**, and open **services.msc**.  

    2. Select the **Windows Update** service. Go to the **Action** menu, and select **Stop**.

2. Rename the **SoftwareDistribution** directory.  

    1. Open a command prompt as an administrator.  

    2. Enter the following commands:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Restart the **Windows Update** service.

    1. Switch back to the **Services** window.  

    2. Select the **Windows Update** service. Go to the **Action** menu, and select **Start**.

    3. Close the Services window.  

#### Step 4: Reset the Microsoft antivirus update engine on your computer  

1. Open a command prompt as an administrator.

2. Enter the following commands:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Restart the computer.  

4. Try to update Windows Defender again.

If the issue persists, continue to the next step.  

#### Step 5: Manually install the definition updates  

[Manually download the latest updates](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### Step 6: Contact Microsoft support  

If these steps didn't resolve the issue, contact Microsoft support. For more information, see [Support options and community resources](../../core/understand/find-help.md#support-options-and-community-resources).  

## Starting Windows Defender or Endpoint Protection service

### Symptom

You receive a message notifying you that **Windows Defender or Endpoint Protection isn't monitoring your computer because the program's service stopped. You should restart it now.**

### Solution

#### Step 1: Restart your computer

Close all applications and restart your computer.  

#### Step 2: Check the Windows service

1. Go to **Start**, and open **services.msc**.  

2. Select the **Windows Defender Antivirus Service**.  

3. Make sure that the **Startup Type** is set to **Automatic**.

4. Go to the **Action** menu and select **Start**.

    1. If this action isn't available, select **Stop**. Wait for the service to stop, and then select the **Start** action to restart the service.  

Note any errors that may appear during this process. [Contact Microsoft Support](../../core/understand/find-help.md#support-options-and-community-resources) and provide the error information.  

#### Step 3: Remove any third-party security programs  

> [!NOTE]  
> Some security applications don't uninstall completely. You may need to download and run a cleanup utility for your previous security application to completely remove it.  

1. Go to **Start** and open **appwiz.cpl**.  

2. In the list of installed programs, uninstall any third-party security programs.

3. Restart your computer.  

> [!CAUTION]  
> When you remove security programs, your computer may be unprotected. If you have problems installing Windows Defender after you remove existing security programs, contact [Microsoft Support](https://support.microsoft.com/supportforbusiness/productselection). Select the **Security** product family, and then the **Windows Defender** product.

## Internet connection issues

For your computer to receive the latest updates from Windows Update, connect it to the internet.  

1. Go to **Start** and open **ncpa.cpl**.  

2. Open the connection name to view the connection **Status**.  

3. If your computer is connected, the **IPv4 connectivity** and/or **IPv6 connectivity** status is **Internet**.  

4. If your computer doesn't appear to be connected, select the connection name, and select **Diagnose this connection**.

Close any open programs and restart your computer.  

## Detected threat can't be remediated

When Windows Defender or Endpoint Protection detects a potential threat, it tries to mitigate the threat by quarantining or removing the threat. These threats can hide inside a compressed archive (`.zip`) or in a network share.

### Remove or scan the file  

- If the detected threat was in a compressed archive file, browse to the file. Delete the file, or manually scan it. Right-click the file and select **Scan with Windows Defender**. If Windows Defender detects additional threats in the file, it notifies you. Then you can choose an appropriate action.  

- If the detected threat was in a network share, open the share, and manually scan it. Right-click the file and select **Scan with Windows Defender**. If Windows Defender detects additional threats in the network share, it notifies you. Then you can choose an appropriate action.  

- If you're not sure of the file's origin, run a full scan on your computer. A full scan may take some time to complete.  

## See also

[Endpoint Protection client frequently asked questions](endpoint-protection-client-faq.yml)

[Endpoint Protection client help](endpoint-protection-client-help.md)
