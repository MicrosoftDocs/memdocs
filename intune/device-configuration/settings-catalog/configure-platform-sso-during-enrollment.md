---
title: Add Platform SSO Policy to ADE Profile on macOS devices
description: Add a settings catalog platform single single sign-on (PSSO) policy to an Automated Device Enrollment (ADE) profile and configure it to run during Setup Assistant with modern authentication on macOS devices.
ms.date: 04/27/2026
ms.topic: how-to
appliesto:
- ✅ macOS
ms.reviewer: iye, arnab
ms.collection:
- M365-identity-device-management
---

# Configure Platform Single Sign-On (PSSO) during Automated Device Enrollment for macOS devices

On macOS devices, you can configure [Platform Single Sign-On (PSSO)](configure-platform-sso-macos.md) during Automated Device Enrollment (ADE) so users can sign in with their Microsoft Entra account and immediately access Microsoft Entra ID resources. Platform SSO minimizes the number of times users need to enter their organizational credentials.

When you add the Platform SSO policy to the Setup Assistant await final configuration phase of ADE enrollment, the policy runs during device registration. When users arrive at the desktop, they have a seamless sign-in experience and can access resources protected by Conditional Access right away.

This feature:

- Enables Microsoft Entra device registration during macOS Setup Assistant.
- Establishes device identity early in the provisioning process.
- Allows Platform SSO credentials to be set up during initial device configuration.
- Minimizes delays accessing resources protected by Conditional Access.

This article lists and describes the settings you need to configure to enable Platform SSO during ADE with Setup Assistant. It also lists the steps to add a Platform SSO policy to an Automated Device Enrollment profile and configure it to run during Setup Assistant. To learn more about Platform SSO, see [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md).

This feature applies to:

- macOS

## Before you begin

- During enrollment, users are prompted to enter their Microsoft Entra organizational credentials at least twice. The first sign-in starts the regular enrollment process. The second sign-in authenticates the identity in Company Portal, which gets the SSO extension.
- This feature requires three different policies - settings catalog policy, line-of-business app policy, and enrollment profile. All the policies and settings listed in this article are required and work together. If any of the steps are misconfigured or skipped, the enrollment fails. In this situation, [wipe](../device-management/actions/wipe.md) the device, follow the steps, and re-enroll the device.
- Assign all the policies to the same **Assigned (static)** device groups that use this feature. You can create new groups for this feature and add the devices to those groups. If you assign these policies to different groups, Platform SSO during enrollment fails.

  Remember, the groups must be:

  - Device groups, not user groups. This feature doesn't work with user groups.
  - Assigned (static) groups, not dynamic groups. This feature doesn't work with dynamic groups.

- Platform SSO has its own set of requirements and configurations. Make sure to review the requirements before you start configuring this feature. For more information, see [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]
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

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create the settings catalog policy (**Devices > Manage devices > Configuration**):

    - If you already use Platform SSO on existing devices, update your existing Platform SSO settings catalog policy. You can apply only one Platform SSO policy to a device.
    - If you're configuring Platform SSO for the first time, follow the steps in [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md).

      When you create the policy, Microsoft recommends using the **Secure Enclave** authentication method.

2. In your settings catalog policy, add and configure the following setting:

    | Name | Configuration value | Description |
    |---|---|---|
    | **Authentication > Extensible single sign-on > Platform SSO > Enable Registration During Setup** | **Enabled** | When enabled, the system enables the Platform SSO registration process during Setup Assistant. |
    | **Authentication > Extensible single sign-on > Platform SSO > Enable Create First User During Setup** | **Enabled** | If you're using the **Password** authentication method, enable this setting. When enabled, the system enables the password synchronization experience during Setup Assistant. <br/><br/> If you're not using the **Password** authentication method, don't add or configure this setting. |

3. Assign the policy to the groups you created.

When you create the Platform SSO settings catalog policy, you add and configure more settings than what's listed in this article. This article only lists the settings that are required to enable Platform SSO during ADE with Setup Assistant. So, add this setting to your existing Platform SSO policy. Or, if you're creating a new Platform SSO policy, add this setting along with the other Platform SSO settings that are required to configure Platform SSO.

## Step 2 - Install Company Portal as a line-of-business app

The Company Portal for macOS deploys and installs the Microsoft Enterprise SSO plug-in. This plug-in enables Platform SSO. Make sure you add the latest Company Portal. If you have an older version of the Company Portal installed, then Platform SSO fails.

1. Download Company Portal for macOS PKG app from [https://go.microsoft.com/fwlink/?linkid=853070](https://go.microsoft.com/fwlink/?linkid=853070).

2. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), add the Company Portal as a line-of-business (LOB) app (**Apps > All Apps > Create**):

    - [Add macOS Line-of-Business (LOB) Apps to Microsoft Intune](../../app-management/deployment/add-lob-macos.md)

3. Make it a required app and assign it to the same groups as the Platform SSO policy you created or updated in [Step 1](#step-1---create-or-update-the-settings-catalog-policy-that-configures-platform-sso).

When Intune detects the Company Portal as a deployed policy, it sends the Company Portal with priority in the enrollment process.

## Step 3 - Set up enrollment profile and configure await final configuration

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create the Automated Device Enrollment profile (**Devices > Device onboarding > Enrollment > Apple** tab):

    - [Set up automated device enrollment (ADE)](../../device-enrollment/apple/setup-automated-macos.md)

2. In **Management Settings**, configure the following settings:

    | Name | Configuration value |
    |---|---|
    | **User affinity** |**Enroll with User Affinity** |
    | **Authentication** | **Setup Assistant with modern authentication** |
    | **Await final configuration** | **Yes** |
    | **Locked enrollment** | **Yes** |

3. Assign the profile to the same groups as the Platform SSO policy you created or updated in [Step 1](#step-1---create-or-update-the-settings-catalog-policy-that-configures-platform-sso).

When devices enroll using this ADE profile, the Platform SSO policy and LOB app policy will automatically apply during Setup Assistant. When enrollment completes and users arrive at the desktop, they have a more integrated sign-in experience on the device and can access Microsoft Entra ID-joined resources.

## Related articles

- [Platform SSO configuration guide for macOS devices using Microsoft Intune](configure-platform-sso-macos.md)
- [Add macOS Line-of-Business (LOB) Apps to Microsoft Intune](../app-management/deployment/add-lob-macos.md)
- [Set up automated device enrollment (ADE)](/device-enrollment/apple/setup-automated-macos.md)