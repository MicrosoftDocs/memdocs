---
title: Set up local admin account creation and password management for macOS devices
description: Set up macOS account configuration with LAPS through automatic device enrollment for macOS devices in Intune.
ms.date: 11/17/2025
ms.topic: how-to
ms.reviewer: annovich
ms.collection:
- M365-identity-device-management
- highpri
---

# Configure support for macOS ADE local account configuration with LAPS in Microsoft Intune



You can use a macOS automated device enrollment (ADE) profile to configure a newly enrolled macOS device for both admin and user account configuration alongside Microsoft local admin password solution (LAPS). **macOS account configuration with LAPS** is an optional set of configurations you can use in new and existing macOS ADE profiles with and without user device affinity. These configurations for account management only apply to new enrollments.

With *macOS local account configuration with LAPS*, devices are provisioned with a local administrator account that has a strong, encrypted, and randomized admin password, which is stored and encrypted by Intune. Similarly, a local standard user account can also be provisioned within the enrollment profile. After enrollment, Intune automatically rotates the LAPS-managed administrator password every six months. To supplement autorotation, Intune admins with sufficient permissions can use the Intune admin center to view a devices local administrator account password and can manually rotate that password at need with remote device actions.

The Intune generated password for the admin account is 15 characters with a mixture of lowercase and uppercase letters, numbers, and special symbols.

Because *macOS local account configuration with LAPS* is enabled only during automated device enrollment (ADE), a previously enrolled device must reenroll with Intune using a LAPS enabled ADE profile to be supported for LAPS for the administrator account.

> [!IMPORTANT]
> When a macOS device enrolls via ADE with a configured local admin account and a targeted passcode profile, it prompts for an admin password reset—even if **Change at next auth** is not enabled or if a value is set for Max Age (days). This does not affect the standard account. We're aware of the issue. As a workaround, manually rotate the admin password after the reset on the device to keep the Intune and device password state in sync.

> [!IMPORTANT]
> The local admin account does not receive a secure token, due to platform limitations. The first account that signs in after enrollment receives the secure token, which at this time will always be the local user account.

> [!TIP]
>
> The Intune implementation of macOS LAPS is similar but distinct from Intune support for Windows LAPS. For information about Windows LAPS in Intune, see [Local administrator account](../enrollment/macos-laps.md#local-administrator-account).

## Prerequisites

The following are device requirements for the macOS local account configuration with LAPS solution:

- macOS 12 and later
- Devices must be synced over to Intune from Apple Business/School Manager
- Devices must enroll with Intune through a macOS ADE enrollment profile

## Role-based access controls for macOS LAPS

The account of an admin that's trusted to view or rotate the local admin account password for a device that was onboarded to macOS LAPS, must have the following Intune role-based access control (RBAC) permissions:

Category: **Enrollment programs**:
- Set **Rotate macOS admin password** to **Yes**
- Set **View macOS admin password** to **Yes**

> [!IMPORTANT]
> The two permissions for *Enrollment programs* aren't included with any Intune built-in role or with the Microsoft Entra built-in role of Intune Administrator. Instead, use a [custom Intune role](../fundamentals/create-custom-role.md) to assign this permission to users who should have these capabilities.

For permissions and details required to manage macOS policies for automated device enrollment, see [Set up automated device enrollment (ADE) for macOS](../enrollment/device-enrollment-program-enroll-macos.md).

## Configuration account and password options

This section provides details for configuring *macOS local account configuration with LAPS*, which is accomplished during step 12 of the [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile) procedure for macOS automatic device enrollment (ADE) profiles.

When you [configure a macOS automated device enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md), the **Account Settings** tab presents options to configure both the Local administrator account and the Local user account. By default, these options are both set to *No*.

:::image type="content" source="./media/macos-laps/account-settings-initial-configuration.png" alt-text="Screen shot of the default appearance of the automated device enrollment profiles Account Setting pane.":::

When you select **Yes** for either the local or admin or user account options, you're configuring both the macOS local admin account with LAPS configuration as well as a standard user account for devices that enroll using this enrollment profile.

Unique account passwords are created using 15 characters with a mixture of lowercase and uppercase letters, numbers, and special symbols.

Whenever any part of the local account configuration, the **Await final configuration** setting is always set to **Yes** in the backend by default. This setting is set because the account configuration occurs during Setup Assistant.

### Local administrator account

:::image type="content" source="./media/macos-laps/configure-local-admin-account-options.png" alt-text="Screen capture that shows the options available for an admin account.":::

The following are examples of the available configuration options. Additional details are accessible through the *Information* icons that follow the name of some settings.

- **Admin account username** - Specify the account name or use one of the following supported variables to dynamically create the name. By default, this field uses *Admin*.
  - {{serialNumber}} - for example, **F4KN99ZUG5V2**
  - {{partialupn}} - for example, **John.Dupont**
  - {{managedDeviceName}} - for example, **F2AL10ZUG4W2_14_4/15/2025_12:45PM**
  - {{onPremisesSamAccountName}} - for example, **JDoe**

- **Admin account full name** - Specify the account name or use one of the following supported variables to dynamically create the name. By default, this field uses *Admin*.
  - {{username}} - for example, **John@contoso.com**
  - {{serialNumber}} - for example, **F4KN99ZUG5V2**
  - {{onPremisesSamAccountName}} - for example, **JDoe**
- **Hide in Users & Groups** - Make the admin account hidden in the sign-in window and in Users & Groups. By default, this set to *Not Configured*.
- **Admin account password rotation period (days)** - If configured, this setting dictates the period (1-180 days) after which the administrator account password is automatically rotated. This rotation is in addition to the automatic rotation that happens once every 180 days.  

### Local user account

:::image type="content" source="./media/macos-laps/configure-local-user-account-options.png" alt-text="Screen capture that shows the options available for a non-admin user account.":::

The following is some guidance for the available options. Additional details are accessible through the Information icons that follow the name of some settings.

- **Account type** - By default this is set to *Standard* to create a standard user account. The local user account type is set to administrator if no local admin account is configured, which is a platform limitation as an admin account is always required to set up any macOS device.

- **Prefill account info** - Set this option to *Yes* if you want to manage the account name or restrict editing.

- **Primary account name** - Specify the account name or use one of the following supported variables to dynamically create the name. Setup Assistant uses this value to prefill the Account Name field if *Prefill account info* is set to *Not configured*. By default, this field uses the *{{partialupn}}* variable.
  - {{serialNumber}} - for example, **F4KN99ZUG5V2**
  - {{partialupn}} - for example, **John.Dupont**
  - {{managedDeviceName}} - for example, **F2AL10ZUG4W2_14_4/15/2025_12:45PM**
  - {{onPremisesSamAccountName}} - for example, **JDoe**

- **Primary account full name** - Specify the full name for the account or use one of the following variables to dynamically create the name. Setup Assistant uses this value to prefill the Full Name field if *Prefill account info* is set to *Not configured*. By default, this field uses the *{{username}}* variable:
  - {{username}} - for example, **John@contoso.com**
  - {{serialNumber}} - for example, **F4KN99ZUG5V2**
  - {{onPremisesSamAccountName}} - for example, **JDoe**

- **Restrict editing** - Prevent the end user from editing the full name and account name. By default, this is set to *Not configured*.

## View account and password details

To view the local Administrator password of a device, your own account must be assigned the following [Intune RBAC permission](#role-based-access-controls-for-macos-laps):

- Category: **Enrollment programs** with **View macOS admin password** set to **Yes**

### To view the admin account password

1.    In the [Microsoft Intune admin center]( https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **macOS devices** > select a **macOS device** to open its *Overview* pane > **Passwords and keys**.

On the **Passwords and keys** pane, you can retrieve the admin password for the macOS device under the **Local administrator account password** section. Here you can also see the last time the password was rotated, manually or automatically.

To see whether an enrolled macOS device has an Intune managed admin password, if the password can be successfully retrieved in the console, that means the password for the local administrator account is managed by Intune.

:::image type="content" source="./media/macos-laps/passwords-and-keys-pane.png" alt-text="Screen capture that shows the Passwords and keys pane, and the Rotate local admin password options.":::

## Manually rotate admin account password

LAPS policy includes a schedule for automatically rotating account passwords (once every six months). In addition to a scheduled rotation, you can use the Intune [device action](../remote-actions/index.md) of **Rotate local admin password** to manually rotate a devices password at any time.

To use this device action, your account must be assigned the [Intune RBAC permission](#role-based-access- controls-for-macos-laps) of:

- Category: **Enrollment programs** with **Rotate macOS admin password** set to **Yes**

### To rotate the admin password

1. In the [Microsoft Intune admin center]( https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **macOS devices** > select a macOS device with the account you want to rotate.

2. On the devices *Overview* pane, from the list of options at the top of the pane select **Rotate local admin password**.

   :::image type="content" source="./media/macos-laps/macos-device-overview.png" alt-text="Screen capture of a devices overview pane.":::


3. To confirm when the password was last rotated for the device, from the device's *Overview* pane:
   1. Expand **Monitor** and then select **Passwords and keys**.
   2. On the **Passwords and keys** pane, you can find the last date and time that the password was rotated.

## Monitor password rotation

Password viewing and rotation both create Intune Audit events that you can view from within the Intune admin center.

In the [Microsoft Intune admin center]( https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Audit logs**.

Look for the following entries:
- **Get AdminAccountDto** - Identifies when someone viewed the admin password.
- **rotateLocalAdminPassword ManagedDevice** - Identifies when the admin password was rotated.

## Related content

- Get started with the [macOS enrollment guide](../fundamentals/deployment-guide-enrollment-macos.md).
