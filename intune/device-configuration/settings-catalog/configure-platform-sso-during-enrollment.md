---
title: Add Platform SSO policy to ADE Profile on macOS devices
description: Add a settings catalog platform single sign-on (PSSO) policy to an Automated Device Enrollment (ADE) profile and configure it to run during Setup Assistant with modern authentication on macOS devices.
ms.date: 05/11/2026
ms.topic: how-to
appliesto:
- ✅ macOS
ms.reviewer: iye, arnab
ms.collection:
- M365-identity-device-management
---

# Configure Platform Single Sign-On (PSSO) during Automated Device Enrollment for macOS devices

On macOS devices, you can configure [Platform Single Sign-On (PSSO)](configure-platform-sso-macos.md) during Automated Device Enrollment (ADE). With Platform SSO, users sign in with their Microsoft Entra account and can get immediate access to Microsoft Entra ID resources. Platform SSO also minimizes the number of times users need to enter their organizational credentials.

When you add the Platform SSO policy and enable the Setup Assistant await final configuration in an ADE enrollment profile, the Platform SSO policy runs during device registration. When users arrive at the desktop, they're already signed into Microsoft Entra resources and can start using productivity apps, like Teams, immediately.

This feature:

- Enables Microsoft Entra device registration during macOS Setup Assistant.
- Establishes device identity early in the provisioning process.
- Allows Platform SSO credentials to be set up during initial device configuration.
- Minimizes delays accessing resources, including resources protected by Conditional Access.

This article lists and describes the settings you need to configure to enable Platform SSO during ADE with Setup Assistant. It also lists the other required steps to use this feature, including adding the Company Portal as a line-of-business app, and configuring the enrollment profile.

To learn more about Platform SSO, see [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md).

This feature applies to:

- macOS

## Before you begin

- During enrollment, users are prompted to enter their Microsoft Entra organizational credentials at least twice. The first sign-in starts the regular enrollment process. The second sign-in authenticates the identity in Company Portal, which gets the SSO extension.
- This feature requires three different policies - settings catalog policy, line-of-business app policy, and enrollment profile. All the policies and settings listed in this article are required and work together. If any of the steps are misconfigured or skipped, the enrollment fails. In this situation, [wipe](../../device-management/actions/wipe.md) the device, follow the steps, and re-enroll the device.
- Assign all the policies to the same **Assigned (static)** user groups that will use this feature. You can use [assignment filters](../../fundamentals/filters/overview.md) on the static user groups.

  You can create new groups for this feature and add the users to those groups. If you assign these policies to different groups, Platform SSO during enrollment fails.  

  Remember, the groups must be:

  - User groups, not device groups. This feature doesn't work with device groups.
  - Assigned (static) groups, not dynamic groups. This feature doesn't work with dynamic groups.

- Platform SSO has its own set of requirements and configurations. Make sure to review the requirements before you start configuring this feature. For more information, see [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platform:
>
> - macOS 26 and newer
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [enrollment-methods](../../includes/requirements/enrollment-methods.md)]
:::column-end:::
:::column span="3":::
> - Devices enrolled using Apple Business Manager or Apple School Manager
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To configure this policy, use an account with at least one of the following roles:
>
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

## Step 1 - Create or update the Platform SSO settings catalog policy

This policy enables the Platform SSO registration process during Setup Assistant in the ADE enrollment flow.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create the settings catalog policy (**Devices > Manage devices > Configuration**):

    - If you already use Platform SSO on existing devices, update your existing Platform SSO settings catalog policy. You can apply only one Platform SSO policy to a device.
    - If you're configuring Platform SSO for the first time, follow the steps in [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md).

      When you create the policy, Microsoft recommends using the **Secure Enclave** authentication method.

2. In your settings catalog policy, add and configure the following setting:

    | Name | Configuration value | Description |
    |---|---|---|
    | **Authentication > Extensible single sign-on > Platform SSO > Enable Registration During Setup** | Enabled | When enabled, the system enables the Platform SSO registration process during Setup Assistant. |

    **If you're using the **Password** authentication method**, also add and configure the following setting. If you're not using the **Password** authentication method, don't add or configure the following setting.

    | Name | Configuration value | Description |
    |---|---|---|
    | **Authentication > Extensible single sign-on > Platform SSO > Enable Create First User During Setup** | Enabled | When enabled, the system enables the password synchronization experience during Setup Assistant. <br/><br/> Remember, only configure this setting if you're using the **Password** authentication method. If you're not using the **Password** authentication method, don't add or configure this setting. |

3. Assign the policy to the static groups you created. 

When you create the Platform SSO settings catalog policy, you add and configure more settings than what's listed in this article. This article only lists the settings that are required to enable Platform SSO during ADE with Setup Assistant. So, add this setting to your existing Platform SSO policy. Or, if you're creating a new Platform SSO policy, add this setting along with the other Platform SSO settings that are required to configure Platform SSO.

## Step 2 - Install Company Portal as a line-of-business app

The Company Portal for macOS deploys and installs the Microsoft Enterprise SSO plug-in. This plug-in enables Platform SSO. Make sure you add the latest Company Portal version. If you install an older version of the Company Portal, Platform SSO fails.

1. Download the Company Portal for macOS PKG app from [https://go.microsoft.com/fwlink/?linkid=853070](https://go.microsoft.com/fwlink/?linkid=853070).

    > [!IMPORTANT]
    > Company Portal 5.2604.0 and newer is required.

2. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal as a line-of-business (LOB) app (**Apps > All Apps > Create**):

    - [Add macOS Line-of-Business (LOB) Apps to Microsoft Intune](../../app-management/deployment/add-lob-macos.md)

3. Make it a required app and assign it to the same groups as the Platform SSO policy you created or updated in [Step 1](#step-1---create-or-update-the-platform-sso-settings-catalog-policy).

When Intune detects the Company Portal as a deployed policy, it sends the Company Portal with priority in the enrollment process.

## Step 3 - Set up enrollment profile and configure await final configuration

This policy configures the enrollment profile to run during Setup Assistant with modern authentication and configures the await final configuration. These settings are required for Platform SSO to run correctly during enrollment.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create the Automated Device Enrollment profile (**Devices** > **Device onboarding** > **Enrollment** > **Apple** tab):

    - [Set up automated device enrollment (ADE)](../../device-enrollment/apple/setup-automated-macos.md)

2. In **Management Settings**, configure the following settings:

    | Name | Configuration value |
    |---|---|
    | **User affinity** | Enroll with User Affinity |
    | **Authentication** | Setup Assistant with modern authentication |
    | **Await final configuration** | Yes |
    | **Locked enrollment** | Yes |

3. Assign the profile to the same groups as the Platform SSO policy you created or updated in [Step 1](#step-1---create-or-update-the-platform-sso-settings-catalog-policy).

When devices enroll using this ADE profile, the Platform SSO policy and LOB app policy will automatically apply during Setup Assistant. When enrollment completes and users arrive at the desktop, they have a more integrated sign-in experience on the device and can access Microsoft Entra ID resources.

## Possible issues and resolutions

If there are issues completing the Setup Assistant with Platform SSO (PSSO), make sure all three policies and their settings are configured and assigned correctly. If troubleshooting is still needed after verifying the policies, the following steps can help.

### Unable to sign in message during Setup Assistant

**Issue**: During Setup Assistant, you might see the following error message:

```error
Unable to sign-in  
There was an issue with the extension while registering your account for single sign-on. Try again in a few moments or contact your administrator.
```

The Company Portal includes the SSO extension used by Platform SSO. If the settings catalog policy and/or the Company Portal policy arrive late, Setup Assistant might show this message.

It's possible the Platform SSO settings catalog policy is delivered, and the Company Portal is still downloading or installing. Enrollment actions occur in separate steps rather than as a single transaction.

**Resolution**: Select the **Try again** button on the error message until the Company Portal finishes downloading and installing. When it completes, the SSO extension is available and the error message no longer appears.

### Remove Platform SSO and reenroll if steps are misconfigured

All the steps in this article are required - the settings catalog policy, Company Portal as a LOB app, and using Setup assistant with Modern Authentication and await final configuration enabled in the ADE profile. If any of these steps are misconfigured or missing, then the configuration fails. 

In this situation, remove the existing Platform SSO (PSSO) configuration and re-enroll the devices by using the following steps. Complete all of the following steps. For more information, see [Steps to Opt out of Platform SSO on macOS](/entra/identity/devices/troubleshoot-mac-sso-extension-plugin#steps-to-opt-out-of-platform-sso-on-macos).

1. Unassign the Platform SSO policy that has the **Enable Registration During Setup** setting enabled. [Sync](../../device-management/actions/sync.md) the device to ensure the policy is removed.
2. Update the Platform SSO policy and set the **Enable Registration During Setup** setting to disabled. [Sync](../../device-management/actions/sync.md) the device to ensure the setting is removed.

    If you use the **Password** authentication method in the Platform SSO policy, set the **Enable Create First User During Setup** to disabled. [Sync](../../device-management/actions/sync.md) the device.

3. [Wipe](../../device-management/actions/wipe.md) the device. Wiping is required as it restarts the enrollment process and applies the updated enrollment profiles.

When complete, follow the steps in this article and make sure all your policies are correctly configured. Ensure you update the Platform SSO policy to set the **Enable Registration During Setup** setting to enabled.

> [!TIP]
> Platform SSO and its components, including the Microsoft Enterprise SSO Extension plugin, are features of Microsoft Entra. Intune manages the deployment and configuration of these features on enrolled devices. If you need more troubleshooting help, see:
>
> - [Troubleshooting the Microsoft Enterprise SSO Extension plugin on Apple devices](/entra/identity/devices/troubleshoot-mac-sso-extension-plugin)
> - [macOS Platform single sign-on known issues and troubleshooting](/entra/identity/devices/troubleshoot-macos-platform-single-sign-on-extension)

## Related articles

- [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md)
- [Add macOS Line-of-Business (LOB) Apps to Microsoft Intune](../../app-management/deployment/add-lob-macos.md)
- [Set up automated device enrollment (ADE)](../../device-enrollment/apple/setup-automated-macos.md)
