---
title: Windows Autopilot self-deploying mode - Step 5 of 5 - Create and assign self-deploying mode Autopilot profile
description: How to - Windows Autopilot self-deploying mode - Step 5 of 5 - Create and assign self-deploying mode Autopilot profile.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Self-deploying mode: Create and assign self-deploying Autopilot profile

Autopilot self-deploying mode steps:
- Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
- Step 2: [Register devices as Autopilot devices](self-deploying-register-device.md)
- Step 3: [Create a device group](self-deploying-device-group.md)
- Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
> [!div class="checklist"]
> - **Step 5: Create and assign Autopilot profile**

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md#workflow)

## Create and assign self-deploying Autopilot profile

The Autopilot profile specifies how the device is configured during Windows Setup and what is shown during the out of box experience (OOBE).

> [!TIP]
>
> For Configuration Manager admins, the Autopilot profile is similar to some of the configuration that takes place during a task sequence via an `unattend.xml` file. The `unattend.xml` file is configured during the **Apply Windows Settings** and **Apply Network Settings** steps. Note however that Autopilot does not use `unattend.xml` files.

To create a self-deploying mode Autopilot profile, follow these steps:

[!INCLUDE [Autopilot profiles before steps](../includes/autopilot-profile-steps-before.md)]

8. In the **Out-of-box experience (OOBE)** page:

      - For **Deployment mode**, select **Self-Deploying (preview)**.

      - **Join to Azure AD as** defaults to **Azure AD joined**, is greyed out, and can't be changed. Only **Azure AD joined** is available because self-deploying mode only supports Azure AD join. Self-deploying modes doesn't support hybrid Azure AD join.

      - **Microsoft Software License Terms** defaults to **Hide**, is greyed out, and can't be changed.

      - **Privacy settings** defaults to **Hide**, is greyed out, and can't be changed.

      - **Hide change account options** defaults to **Hide**, is greyed out, and can't be changed.

      - **User account type**  defaults to **Standard**, is greyed out, and can't be changed.

      - For **Language (Region)**, select **Operating system default** to use the default language for the operating system being configured. If another language is desired, select the desired language from the drop-down list.

      - For **Automatically configure keyboard**, select **Yes** to skip the keyboard selection page.

        > [!NOTE]
        >
        > If you want users to be able to select their keyboard layout, then select **No** instead. However, the purpose of Autopilot self-deploying mode is to deploy a device with minimal to no user interaction. Setting **Automatically configure keyboard** to **No** requires additional user interaction.

      - For **Apply device name template**, select **No**. Alternatively, **Yes** can be chosen to apply a device name template. Be aware of the following if the name template is selected to **Yes**:

        - Names must be 15 characters or less, and can have letters, numbers, and hyphens.
        - Names can't be all numbers.
        - Use the [%SERIAL% macro](/windows/client-management/mdm/accounts-csp) to add a hardware-specific serial number.
        - Use the [%RAND:x% macro](/windows/client-management/mdm/accounts-csp) to add a random string of numbers, where x equals the number of digits to add.

      > [!NOTE]
      >
      > If the language/region and keyboard screens are set to hidden, they may still be displayed if there's no network connectivity at the start of the Autopilot deployment. These screens are displayed because there's no network connectivity at the start of the deployment to download the Autopilot profile where the settings to hide these screens are specified. Once network connectivity is established, the Autopilot profile is downloaded and any additional screen settings should work as expected.

[!INCLUDE [Autopilot profiles after steps](../includes/autopilot-profile-steps-after.md)]

## Verify device has an Autopilot profile assigned to it

[!INCLUDE [How to verify a device has an Autopilot profile assigned to it in Intune](../includes/verify-autopilot-profile-assignment.md)]

## Next step: Deploy the device

At this point, the device is ready to be deployed. If desired, deploy any additional applications, policies, and profiles to the device group that the device is a member of which should run during Autopilot. Boot the device with a fresh install of Windows and the Autopilot deployment should begin.

[!INCLUDE [Assignment tip](../includes/assignment-tip.md)]

> [!NOTE]
>
> Although a user isn't assigned to a device for Windows Autopilot self-deploying mode, for testing purposes, assigning at least one policy and at least one application to users is still recommended since User ESP still runs when a user first signs into the device.

## More information

[!INCLUDE [More information Autopilot profile](../includes/more-info-autopilot-profile.md)]
