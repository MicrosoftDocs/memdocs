---
title: Windows Autopilot user-driven Azure AD join - Step 4 of 5 - Create and assign user-driven Azure AD join Autopilot profile
description: Howe to - Windows Autopilot user-driven Azure AD join - Step 4 of 5 - Create and assign user-driven Azure AD join Autopilot profile.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Windows Autopilot user-driven Azure AD join - Step 4 of 5: Create and assign user-driven Azure AD join Autopilot profile

While the ESP controls what is shown during device and user setup and specifies how soon a user can use their device, the Autopilot profile specifies how the device is configured during Windows Setup, or during OOBE.

When creating an Autopilot profile for the user-driven scenario, devices with this Autopilot profile are associated with the user enrolling the device. User credentials are required to enroll the device.

To create an user-driven Azure AD join Autopilot profile, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select > **Windows enrollment**

5. Under **Windows Autopilot Deployment Program**, select **Deployment Profiles**

6. In the **Windows Autopilot deployment profiles** screen, select  **Create Profile** > **Windows PC**.

7. In the **Basics** page of the **Create profile** screen, type a **Name** and optional **Description** for the Autopilot profile, and then select **Next**.

    > [!NOTE]
    >
    > For the purposes of this tutorial, leave the option **Convert all targeted devices to Autopilot** set to **No**. This tutorial is mainly concentrating on new devices while this option mainly covers existing devices.

8. In the **Out-of-box experience (OOBE)** page:

      - For **Deployment mode**, select **User-driven**.

      - For **Join to Azure AD as**, select **Azure AD joined**.

      - For **Microsoft Software License Terms**, select **Hide** to skip the EULA page.

      - For **Privacy settings**, select **Hide** to skip the privacy settings.

      - For **Hide change account options**: Choose **Hide**.

      - For **User account type**, choose the desired account type for the user (**Administrator** or **Standard** user). If **Administrator** is chosen, the user will added to the local Admin group.

      - For **Allow pre-provisioned deployment**, select **No**..

      - For **Language (Region)**, select **Operating system default** to use the default language for the operating system being configured. If another language is desired, select the desired language from the drop down list.

      - For **Automatically configure keyboard**, select **Yes** to skip the keyboard selection page.

      - For **Apply device name template**, select **No**. Alternatively, **Yes** can be chosen to apply a device name templated. Be aware of the following if the name template is selected to **Yes**:

        - Names must be 15 characters or less, and can have letters, numbers, and hyphens.
        - Names can't be all numbers.
        - Use the [%SERIAL% macro](/windows/client-management/mdm/accounts-csp) to add a hardware-specific serial number.
        - Use the [%RAND:x% macro](/windows/client-management/mdm/accounts-csp) to add a random string of numbers, where x equals the number of digits to add.

        > [!NOTE]
        >
        > The above settings have been selected to minimize needed user interaction during device setup. However, some of the settings that are hidden can instead be shown as desired.
        >
        > Also note that if language and keyboard settings are shown instead of hidden, they require ethernet connectivity. Wi-fi connectivity isn't supported because of the requirement to choose a language, locale, and keyboard to initiate the Wi-fi connection.

9. Once the options in the **Out-of-box experience (OOBE)** page are configured as desired, select **Next**.

10. On the **Assignments** page, under **Included groups**, choose **Add groups**.

11. In the **Select groups to include** page, choose the device group(s) to assign this Autopilot profile to. This is normally the device group created in the step [Create device group](#create-device-group) above. Once done, select **Select**.

12. In the **Create profile** page, select **Next**.

13. On the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the Autopilot profile.

For more information on creating and assigning Autopilot profiles, see the following articles:

- [Configure Autopilot profiles](/mem/autopilot/profiles)

## Verify device has an Autopilot profile assigned to it

[!INCLUDE [How to verify a device has an Autopilot profile assigned to it in Intune](includes/verify-autopilot-profile-assignment.md)]

## Next step - Step 5: Assign Autopilot device to a user (optional)

> [!div class="nextstepaction"]
> [Step 5: Assign Autopilot device to a user (optional)](autopilot-user-driven-aadj-5-assign-autopilot-device-to-user.md)

## Previous step - Step 3: Configure and assign the Enrollment Status Page (ESP)

> [!div class="nextstepaction"]
> [Step 3: Configure and assign the Enrollment Status Page (ESP)](autopilot-user-driven-aadj-3-configure-and-assign-esp.md)

## Back to Windows Autopilot user-driven Azure AD join overview

> [!div class="nextstepaction"]
> [Windows Autopilot user-driven Azure AD join overview](autopilot-user-driven-aadj-workflow.md)
