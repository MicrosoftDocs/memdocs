---
title: Deploy Windows update packages in Intune
titleSuffix: Microsoft Intune
description: Learn how to deploy a Windows update package (.msu file) in Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
ms.custom: 
ms.collection:
- tier2
- M365-identity-device-management
---

# Deploy Windows update packages in Intune

If you want to deploy a specific Windows update package (*.msu* file) to Windows 10/11 devices managed by Intune, you can use the [Intune Win32 app management](../apps/apps-win32-app-management.md) capabilities to deploy an *.msu* file as a Win32 app.

The following steps help you deploy a Windows update package to Intune.

## Step 1: Prepare the update package as Win32 app content

1. Download the  Windows update package by searching on [Microsoft Update Catalog](https://www.catalog.update.microsoft.com/).
2. Use the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) to convert the *.msu* file into the *.intunewin* format. This tool will guide you to input the required parameters in a step-by-step process if you don't specify the parameters in the command-line. For more information about the Microsoft Win32 Content Prep Tool, see [Convert the Win32 app content](../apps/apps-win32-prepare.md#convert-the-win32-app-content).

## Step 2: Create the Win32 app

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under **Other** app types, select **Windows app (Win32)**.
4. Click **Select**, locate the **Add app** pane, and then select **Select app package file**.
5. In the **App package file** pane, select the *.intunewin* file, and then select **OK**.
6. On the **App information** page, add the details for your app.
7. On the **Program** page, specify the following installation and removal commands for the app:

    **Install command:**  

    `wusa.exe <full path of the .msu file> /quiet /norestart -Wait`

    For example, if the *windows10.0-kb4532693-x64_e22f60a077a0ec5896266a18cc3daf26bfc29e16.msu* file is in the current folder, type the following command in **Install command**:

    `wusa.exe .\windows10.0-kb4532693-x64_e22f60a077a0ec5896266a18cc3daf26bfc29e16.msu /quiet /norestart -Wait`

    **Uninstall command:**  

    `wusa.exe /uninstall /kb:<KB number> /quiet`

    The following image provides an example of the **Program** page:

    :::image type="content" source="./media/apps-win32-deploy-update-package/apps-win32-deploy-update-package-01.png" alt-text="Example of editing commands.":::

    Use the `/quiet` switch to run *Wusa.exe* in quiet mode without user interaction. Use the `/norestart` switch to prevent *Wusa.exe* from restarting the computer. For more information about *Wusa.exe*, see [Description of the Windows Update Standalone Installer in Windows](https://support.microsoft.com/help/934307).

    The `-Wait` option is used to make sure that the app installation returns after *Wusa.exe* exits.

8. On the **Requirements** page, specify the [requirements](../apps/apps-win32-add.md#step-3-requirements) that devices must meet before the app is installed.

    **Minimum operating system**: Select the minimum operating system that is required to apply the update.

    To specify additional requirements, such as build number and Update Build Revision (UBR), select **Add** to display the **Add a Requirement rule** pane.

    For example, to install the app on only devices that are running Windows 10, version 1903, build 18362, UBR less than 329, select **Registry** as the **Requirement type**, and then specify the following rules:

    - **Key path**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion`
    - **Value name**: CurrentBuildNumber
    - **Registry key requirement**: String comparison
    - **Operator**: Equals
    - **Value**: 18362
    - **Associated with a 32-bit app on 64-bit clients**: No

    :::image type="content" source="./media/apps-win32-deploy-update-package/apps-win32-deploy-update-package-02.png" alt-text="Screenshot of build 18362 example.":::

    - **Key path**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion`
    - **Value name**: UBR
    - **Registry key requirement**: Integer comparison
    - **Operator**: Less than
    - **Value**: 329
    - **Associated with a 32-bit app on 64-bit clients**: No

    :::image type="content" source="./media/apps-win32-deploy-update-package/apps-win32-deploy-update-package-03.png" alt-text="Screenshot of UBR less than 329 example.":::

9. On the **Detection rules** page, select **Use a custom detection script** as the **Rules format**.

    **Example:**

    :::image type="content" source="./media/apps-win32-deploy-update-package/apps-win32-deploy-update-package-04.png" alt-text="Screenshot of Detection rules example.":::

    **Sample script file (DetectKB.ps1)**:

    ```powershell
    $result = systeminfo.exe | findstr KB<KB number>

    if ($result)
     {
        Write-Output "Found KB<KB number>"
        exit 0
     }
     else
     {
        exit 1
     }
    ```

10. Specify [assignments](../apps/apps-win32-add.md#step-7-assignments) for the app.

11. Review your settings, and then select **Create** to add the app to Intune.

## Step 3: Deploy the app

[Assign the app](../apps/apps-deploy.md) to groups.

## Next steps

- For more information about adding apps to Intune, see [Add apps to Microsoft Intune](apps-add.md).
- For more information about Win32 apps, see [Intune Win32 app management](apps-win32-app-management.md).
