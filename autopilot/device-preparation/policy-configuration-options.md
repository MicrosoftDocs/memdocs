---
title: Windows Autopilot device preparation policy configuration options
description: Describes the available configuration options in a Windows Autopilot device preparation policy.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/03/2024
ms.topic: article
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
  - essentials-overview
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation policy configuration options


The **Configuration settings** page has several configuration options. The following section describes each option in the **Configuration settings** page and what each option should be set to for a Microsoft Entra join Windows Autopilot device preparation deployment.

In the **Configuration settings** page:

1. Expand the **Out-of-box experience settings** section by selecting it.

   1. **Minutes allowed before showing installation error** - enter the number of minutes allowed before failing a deployment.

      The value entered is for the whole deployment and not for an individual application install or PowerShell script. The acceptable value is an integer between 15 and 720.

   2. **Custom error message** - enter a custom message to display to the end-user if the deployment fails.

   3. **Allow users to skip setup after multiple attempts** - select either **Yes** or **No** as desired by toggling the switch.

      Normally after a deployment failure, a **Retry** button is displayed allowing the end-user to retry the deployment. Setting this option as **Yes** also adds a **Continue anyway** button that allows the deployment to just fail, signs the end-user in, and lets them continue to the Desktop.

   4. **Show link to diagnostics** - select either **Yes** or **No** as desired by toggling the switch.

      If there's a deployment failure, setting this option to **Yes** displays a link at the deployment failure page allowing the end-user to retrieve diagnostic logs.

2. Expand the **Apps** section by selecting it:

   The **Apps** section allows selection of up to 10 managed applications reference with the deployment. The applications specified here should be the essential applications that should be installed on the device before the end-user can start using the device.

   > [!IMPORTANT]
   >
   > The applications selected in this setting should be assigned to the device security group previously specified in the **Device group** page. If applicable, the applications should also be configured to install in the **System** context since it's installed during OOBE when no user is signed in.

   1. Under **Allowed Applications**, select **Add**. The **Select Apps** pane opens.

   2. In the **Select Apps** pane:

      1. Scroll through the list of applications or use the **Search** box to search for desired applications.

      2. Once a desired application is found, select the **Add** button next to the application. The application is added to the list under **Selected Apps**.

      3. Once all of the desired applications are selected, select the **Save** button.

    All of the selected applications should display under **Allowed Applications**.

    > [!NOTE]
    >
    > The following types of applications are supported for use with Windows Autopilot device preparation:
    >
    > - [Line-of-business (LOB)](/mem/intune/apps/lob-apps-windows).
    > - [Win32](/mem/intune/apps/apps-win32-prepare).
    > - [Microsoft Store](/mem/intune/apps/store-apps-microsoft) - only Microsoft Store apps that support WinGet are supported.
    > - [Microsoft 365](/mem/intune/apps/apps-add-office365).
    >
    > In addition, Windows Autopilot device preparation supports deploying both Win32 and line-of-business (LOB) applications in the same deployment.

3. Expand the **Deployment settings** section by selecting it:

   1. **Deployment mode** - select **Single user** in the drop-down menu.

   2. **Deployment type** - select **User driven** in the drop-down menu.

   3. **Join type** - select **Microsoft Entra joined** in the drop-down menu.

   4. **User account type** - select either **Standard User** or **Administrator** as desired by toggling the switch.

    > [!IMPORTANT]
    >
    > By default, when a device is enrolled in Microsoft Entra ID, the user is automatically added to the **Administrator** group on the device. If this setting is set to **Standard User**, the Windows Autopilot device preparation deployment ensures that the user is removed from the **Administrator** group before the deployment completes, the user is signed in, and the user reaches the Desktop.

4. Expand the **Scripts** section by selecting it:

    The **Scripts** section allows selection of up to 10 PowerShell scripts to install during the deployment. The PowerShell scripts specified here should be the essential PowerShell scripts that should run on the device before the end-user can start using the device.

    > [!IMPORTANT]
    >
    > The PowerShell scripts selected in this setting should be assigned to the device security group previously specified in the **Device group** page. The PowerShell script should also be configured to run in the **System** context since the PowerShell scripts run during OOBE when no user is signed in. The PowerShell script can be set to run in the **System** context by setting the option **Run this script using the logged on credentials** to **No** in the properties of the PowerShell script.

   1. Under **Allowed Scripts**, select **Add**. The **Select Scripts** pane opens.

   2. In the **Select Scripts** pane:

      1. Scroll through the list of PowerShell scripts or use the **Search** box to search for desired PowerShell scripts.

      2. Once a desired PowerShell script is found, select the **Add** button next to the PowerShell script. The PowerShell script is added to the list under **Selected Scripts**.

      3. Once all of the desired PowerShell scripts are selected, select the **Save** button.

    All of the selected PowerShell scripts should display under **Allowed Scripts**.

