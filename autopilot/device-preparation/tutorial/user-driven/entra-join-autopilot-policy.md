---
title: Windows Autopilot device preparation user-driven Microsoft Entra join - Step 6 - Create a Windows Autopilot device preparation policy
description: Create a Windows Autopilot device preparation policy for a user-driven Microsoft Entra join deployment.
ms.date: 08/25/2026
ms.topic: tutorial
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation user-driven Microsoft Entra join: Create a Windows Autopilot device preparation policy

Windows Autopilot device preparation user-driven Microsoft Entra join steps:

- Step 1: [Set up Windows automatic Intune enrollment](entra-join-automatic-enrollment.md)
- Step 2: [Allow users to join devices to Microsoft Entra ID](entra-join-allow-users-to-join.md)
- Step 3: [Create an assigned device group](entra-join-device-group.md)
- Step 4: [Create a user group](entra-join-user-group.md)
- Step 5: [Assign applications and PowerShell scripts to device group](entra-join-assign-apps-scripts.md)

> [!div class="checklist"]
>
> - **Step 6: Create Windows Autopilot device preparation policy**

- Step 7, option 1: [Add Windows corporate identifier to device](entra-join-corporate-identifier.md)
- Step 7, option 2: [Associate devices](entra-join-device-association.md)

For an overview of the Windows Autopilot device preparation user-driven Microsoft Entra join workflow, see [Windows Autopilot device preparation user-driven Microsoft Entra join overview](entra-join-workflow.md#workflow).

## Create user-driven Microsoft Entra join Windows Autopilot device preparation policy

The Windows Autopilot policy specifies how the device is configured during Windows Setup and what is shown during the out-of-box experience (OOBE).

To create a user-driven Microsoft Entra join Windows Autopilot device preparation policy, follow these steps:

1. Sign in to the [Microsoft Intune admin center].

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot device preparation**, select **Device preparation policies**.

1. In the **Device preparation policies** screen, select **Create**, and then select **User Driven**.

1. The **Create profile** screen opens. In the **Introduction** page, select **Next**.

1. In the **Basics** page:

   1. In the **Name** text box, enter a name for the Windows Autopilot device preparation policy.

   1. In the **Description** text box, if desired, enter a description for the Windows Autopilot device preparation policy.

   1. Once a name and description is entered, select **Next**.

1. In the **Device group** page, select the **Search by group name..** box, and then either select or search for the device group created in [Step 3: Create an assigned device group](entra-join-device-group.md). Make sure to select the device group created in [Step 3: Create an assigned device group](entra-join-device-group.md) and not the user group created in [Step 4: Create a user group](entra-join-user-group.md). Once the correct device group is selected, select **Next**.

1. In the **Configuration settings** page, configure the various settings as desired and then select **Next**. For detailed information on the configurations on this page, see the next section [Configuration settings](#configuration-settings).

1. In the **Scope tags** page, select **Next**.

    > [!NOTE]
    >
    > **Scope tags** are optional. For this tutorial, scope tags are being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/intune/fundamentals/role-based-access-control/scope-tags).

1. In the **Assignments** page, select the **Search by group name..** box, and then either select or search for the user group created in [Step 4: Create a user group](entra-join-user-group.md). Make sure to select the user group created in [Step 4: Create a user group](entra-join-user-group.md) and not the device group created in [Step 3: Create an assigned device group](entra-join-device-group.md). Once the correct user group is selected, select **Next**.

1. In the **Review + create** page, review all settings to make sure they're all correct. Once everything is verified, select **Save** to finish creating the Windows Autopilot device preparation policy.

## Configuration settings

The **Configuration settings** page has several configuration options. The following section describes each option in the **Configuration settings** page and what each option should be set to for a Microsoft Entra join Windows Autopilot device preparation deployment.

In the **Configuration settings** page:

1. Expand the **Deployment settings** section by selecting it:

   1. **Deployment mode** - Select **User-driven** in the drop-down menu.

   1. **Deployment type** - Select **Single user** in the drop-down menu.

   1. **Join type** - Select **Microsoft Entra joined** in the drop-down menu.

   1. **User account type** - Select either **Standard User** or **Administrator** as desired by toggling the switch.

    > [!IMPORTANT]
    >
    > By default, when a device is enrolled in Microsoft Entra ID, the user is automatically added to the **Administrator** group on the device. If this setting is set to **Standard User**, the Windows Autopilot device preparation deployment ensures that the user is removed from the **Administrator** group before the deployment completes, the user is signed in, and the user reaches the desktop.

1. Expand the **Out-of-box experience settings** section by selecting it.

   1. **Minutes allowed before showing installation error** - Enter the number of minutes allowed before failing a deployment.

      The value entered is for the whole deployment and not for an individual application install or PowerShell script. The acceptable value is an integer between 15 and 720.

   1. **Custom error message** - Enter a custom message to display to the end-user if the deployment fails.

   1. **Allow users to skip setup after multiple attempts** - Select either **Yes** or **No** as desired by toggling the switch.

      Normally after a deployment failure, a **Retry** button is displayed allowing the end-user to retry the deployment. Setting this option as **Yes** also adds a **Continue anyway** button that allows the deployment to just fail, signs the end-user in, and lets them continue to the desktop.

   1. **Show link to diagnostics** - Select either **Yes** or **No** as desired by toggling the switch.

      If there's a deployment failure, setting this option to **Yes** displays a link at the deployment failure page allowing the end-user to retrieve diagnostic logs.

   > [!IMPORTANT]
   >
   > The out-of-box experience settings that follow—**Language (Region)**, **Automatically configure keyboard**, **Hide Microsoft Software License Terms**, **Hide privacy settings**, **Hide change account options**, and **Apply device name template**—are **only available to associated devices**. They take effect only when the device is bound to your tenant using [device association](entra-join-device-association.md), and they have no effect on devices that aren't associated, such as devices onboarded with corporate identifiers only. This limitation doesn't apply to the **Apps** or **Scripts** sections, which apply to all Windows Autopilot device preparation deployments.

   1. **Language (Region)** - Sets the language and region applied to the device during OOBE.

   1. **Automatically configure keyboard** - Skips the keyboard selection page in OOBE.

      > [!NOTE]
      >
      > When the device uses a Wi-Fi network connection during OOBE, the language and keyboard selection screens aren't hidden.

   1. **Hide Microsoft Software License Terms** - Hides the Microsoft Software License Terms (EULA) page in OOBE.

   1. **Hide privacy settings** - Hides the privacy settings page in OOBE.

   1. **Hide change account options** - Prevents change account options from appearing on the company sign-in and domain error pages. This setting requires company branding to be configured in Microsoft Entra ID.

   1. **Apply device name template** - Renames the device before enrollment using a custom prefix combined with `%RAND:4%` (four random characters) or `%SERIAL%` (the device serial number). The resulting device name can be up to 63 characters long.

1. Expand the **Apps** section by selecting it:

   The **Apps** section lets you select up to 25 managed applications to install during deployment. Select the essential applications that must be installed before the end user can use the device.

   > [!IMPORTANT]
   >
   > The applications selected in this setting should be assigned to the device security group previously specified in the **Device group** page. If applicable, the applications should also be configured to install in the **System** context since it's installed during OOBE when no user is signed in.

   1. Under **Allowed Applications**, select **Add**. The **Select Apps** pane opens.

   1. In the **Select Apps** pane:

      1. Scroll through the list of applications or use the **Search** box to search for desired applications.

      1. Once a desired application is found, select the **Add** button next to the application. The application is added to the list under **Selected Apps**.

      1. Once all of the desired applications are selected, select **Save**.

    All of the selected applications should display under **Allowed Applications**.

    > [!NOTE]
    >
    > The following types of applications are supported for use with Windows Autopilot device preparation:
    >
    > - [Line-of-business (LOB)](/intune/app-management/deployment/add-lob-windows).
    > - [Win32](/intune/app-management/deployment/create-win32-package).
    > - [Microsoft Store](/intune/app-management/deployment/add-microsoft-store) - only Microsoft Store apps that support WinGet are supported.
    > - [Microsoft 365](/intune/app-management/deployment/add-microsoft-365-windows).
    > - [Enterprise App Catalog](/intune/app-management/deployment/add-enterprise-catalog-app).
    >
    > In addition, Windows Autopilot device preparation supports deploying both Win32 and line-of-business (LOB) applications in the same deployment.

1. Expand the **Scripts** section by selecting it:

    The **Scripts** section allows selection of up to 10 PowerShell scripts to install during the deployment. The PowerShell scripts specified here should be the essential PowerShell scripts that should run on the device before the end-user can start using the device.

    > [!IMPORTANT]
    >
    > The PowerShell scripts selected in this setting should be assigned to the device security group previously specified in the **Device group** page. The PowerShell script should also be configured to run in the **System** context since the PowerShell scripts run during OOBE when no user is signed in. The PowerShell script can be set to run in the **System** context by setting the option **Run this script using the logged on credentials** to **No** in the properties of the PowerShell script.

   1. Under **Allowed Scripts**, select **Add**. The **Select Scripts** pane opens.

   1. In the **Select Scripts** pane:

      1. Scroll through the list of PowerShell scripts or use the **Search** box to search for desired PowerShell scripts.

      1. Once a desired PowerShell script is found, select the **Add** button next to the PowerShell script. The PowerShell script is added to the list under **Selected Scripts**.

      1. Once all of the desired PowerShell scripts are selected, select **Save**.

    All of the selected PowerShell scripts should display under **Allowed Scripts**.

> [!IMPORTANT]
>
> If a device is registered as a Windows Autopilot device, whether the Windows Autopilot deployment or the Windows Autopilot device preparation deployment runs depends on the device's association state:
>
> - **The device isn't associated with your tenant.** Windows Autopilot registration takes precedence, and the Windows Autopilot deployment runs instead of the device preparation deployment.
> - **The device is associated with your tenant.** Device association takes precedence, and the Windows Autopilot device preparation deployment runs.
>
> To run device preparation on a registered device without associating it, first remove the device's Windows Autopilot registration. For more information, see [Deregister a device](../../../registration-overview.md#deregister-a-device).

## Policy priority

If multiple Windows Autopilot device preparation policies are assigned to a user, the policy with the highest priority takes precedence. On the **Home** > **Enroll devices | Windows enrollment** > **Device preparation policies** screen, the highest-priority policy appears at the top of the list and has the smallest number in the **Priority** column. To change a policy's priority, drag it to a different position in the list.

A device preparation policy can be assigned to a device or to a user. When a device has both a device-based assignment and a user-based assignment, the **device-based assignment takes precedence**. For example, if you assign a device preparation policy directly to a device when you [pre-associate the device](entra-join-device-association.md), that policy is used instead of any policy assigned to the user who signs in during enrollment.

## Next step: Onboard trusted devices

After you create the device preparation policy, choose **one** of the following methods to make sure only trusted devices are prepared. You don't need to use both:

- **Corporate identifiers** (optional) - Upload device identifiers so only trusted devices can enroll when personal-device enrollment is blocked.
- **Device association** (optional) - Bind devices to your tenant before enrollment. Associated devices are automatically treated as corporate-owned, so you **don't** need to upload corporate identifiers for them. Device association also enables the out-of-box experience settings that are only available to associated devices.

To use corporate identifiers:

> [!div class="nextstepaction"]
> [Step 7, option 1: Add Windows corporate identifier to device](entra-join-corporate-identifier.md)

To use device association instead:

> [!div class="nextstepaction"]
> [Step 7, option 2: Associate devices](entra-join-device-association.md)

> [!NOTE]
>
> Windows Autopilot device preparation only requires [corporate identifiers for Windows](../../overview.md#corporate-identifiers-for-windows) if Intune enrollment restrictions are being used to block personal device enrollments. If enrollment restrictions aren't blocking personal devices and you aren't using device association, then the next step is to deploy the device.

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431