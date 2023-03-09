---
title: Windows Autopilot self-deploying mode - Step 5 of 5 - Create and assign self-deploying mode Autopilot profile
description: How to - Windows Autopilot self-deploying mode - Step 5 of 5 - Create and assign self-deploying mode Autopilot profile.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/09/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Self-deploying mode: Create and assign self-deploying Autopilot profile

Autopilot self-deploying mode steps:
- Step 1: [Set up Windows automatic Intune enrollment](self-deploying-automatic-enrollment.md)
- Step 2: [Register devices as Autopilot devices](self-deploying-register-device.md)
- Step 3: [Create a device group](self-deploying-device-group.md)
- Step 4: [Configure and assign Autopilot Enrollment Status Page (ESP)](self-deploying-esp.md)
> [!div class="checklist"]
> - **Step 5: Create and assign Autopilot profile**

For an overview of the Windows Autopilot self-deploying mode workflow, see [Windows Autopilot self-deploying overview](self-deploying-workflow.md)

## Create and assign self-deploying Autopilot profile

While the ESP controls what is shown during device and user setup and specifies how soon a user can use their device, the Autopilot profile specifies how the device is configured during Windows Setup, or during OOBE.

> [!TIP]
>
> For Configuration Manager admins, the Autopilot profile is similar to some of the configuration that takes place during a task sequence via an unattend.xml file. The unattend.xml file is configured during the **Apply Windows Settings** and **Apply Network Settings** steps. Note however that Autopilot does not use unattend.xml files.

To create a self-deploying mode Autopilot profile, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select > **Windows enrollment**

5. Under **Windows Autopilot Deployment Program**, select **Deployment Profiles**

6. In the **Windows Autopilot deployment profiles** screen, select **Create Profile** > **Windows PC**.

7. In the **Basics** page of the **Create profile** screen, type a **Name** and optional **Description** for the Autopilot profile, and then select **Next**.

    > [!NOTE]
    >
    > For the purposes of this tutorial, leave the option **Convert all targeted devices to Autopilot** set to **No**. This tutorial is mainly concentrating on new devices while this option mainly covers existing devices.

8. In the **Out-of-box experience (OOBE)** page:

      - For **Deployment mode**, select **Self-Deploying (preview)**.

      - **Join to Azure AD as** defaults to **Azure AD joined**, is greyed out, and can't be changed. Only **Azure AD joined** is available because self-deploying mode only supports Azure AD join. Self-deploying modes doesn't support hybrid Azure AD join.

      - **Microsoft Software License Terms** defaults to **Hide**, is greyed out, and can't be changed.

      - **Privacy settings** defaults to **Hide**, is greyed out, and can't be changed.

      - **Hide change account options** defaults to **Hide**, is greyed out, and can't be changed.

      - **User account type**  defaults to **Standard**, is greyed out, and can't be changed..

      - For **Language (Region)**, select **Operating system default** to use the default language for the operating system being configured. If another language is desired, select the desired language from the drop-down list.

      - For **Automatically configure keyboard**, select **Yes** to skip the keyboard selection page.

        > [!NOTE]
        >
        > If you want users to be able to select their keyboard layout, then select **No** instead. However, be aware that the purpose of Autopilot self-deploying mode is to deploy a device with minimal to no user interaction. Setting **Automatically configure keyboard** to **No** will require additional user interaction.

      - For **Apply device name template**, select **No**. Alternatively, **Yes** can be chosen to apply a device name template. Be aware of the following if the name template is selected to **Yes**:

        - Names must be 15 characters or less, and can have letters, numbers, and hyphens.
        - Names can't be all numbers.
        - Use the [%SERIAL% macro](/windows/client-management/mdm/accounts-csp) to add a hardware-specific serial number.
        - Use the [%RAND:x% macro](/windows/client-management/mdm/accounts-csp) to add a random string of numbers, where x equals the number of digits to add.

9. Once the options in the **Out-of-box experience (OOBE)** page are configured as desired, select **Next**.

10. On the **Assignments** page, under **Included groups**, choose **Add groups**.

11. In the **Select groups to include** page, choose the device group(s) to assign this Autopilot profile to. This device group(s) is normally the device group(s) created in the step [Create device group](self-deploying-device-group.md). Once done, select **Select**.

    > [!NOTE]
    >
    > Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** will result in those devices being excluded and they won't receive the Autopilot profile.

12. In the **Assignments** page, verify the correct device group(s) appear under **Included groups** > **Groups** and then select **Next**.

13. On the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the Autopilot profile.

For more information on creating and assigning Autopilot profiles, see the following articles:

- [Configure Autopilot profiles](/mem/autopilot/profiles)

## Verify device has an Autopilot profile assigned to it

[!INCLUDE [How to verify a device has an Autopilot profile assigned to it in Intune](../includes/verify-autopilot-profile-assignment.md)]

## More information

[!INCLUDE [More information Autopilot profile](../includes/more-info-autopilot-profile.md)]
