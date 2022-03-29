---
# required metadata

title: Create and deploy app protection policies 
titleSuffix: Microsoft Intune
description: This topic describes how to create and assign Microsoft Intune app protection policies (APP).
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
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# How to create and assign app protection policies

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Learn how to create and assign Microsoft Intune app protection policies (APP) for users of your organization. This topic also describes how to make changes to existing policies.

## Before you begin

App protection policies can apply to apps running on devices that may or may not be managed by Intune. For a more detailed description of how app protection policies work and the scenarios that are supported by Intune app protection policies, see [App protection policies overview](app-protection-policy.md).

The choices available in app protection policies (APP) enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

If you're looking for a list of apps that have integrated the Intune SDK, see [Microsoft Intune protected apps](apps-supported-intune-apps.md).

For information about adding your organization's line-of-business (LOB) apps to Microsoft Intune to prepare for app protection policies, see [Add apps to Microsoft Intune](apps-add.md).

## App protection policies for iOS/iPadOS and Android apps

When you create an app protection policy for iOS/iPadOS and Android apps, you follow a modern Intune process flow that results in a new app protection policy. For information about creating app protection policies for Windows apps, see [Create and deploy Windows Information Protection (WIP) policy with Intune](../apps/windows-information-protection-policy-create.md).

### Create an iOS/iPadOS or Android app protection policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **App protection policies**. This selection opens the **App protection policies** details, where you create new policies and edit existing policies.
3. Select **Create policy** and select either **iOS/iPadOS** or **Android**. The **Create policy** pane is displayed.
4. On the **Basics** page, add the following values:

    | Value | Description |
    |--------------|------------------------------------------------|
    | Name | The name of this app protection policy. |
    | Description | [Optional] The description of this app protection policy. |


    The **Platform** value is set based on your above choice.

    ![Screenshot of the Basics page of the Create policy pane](./media/app-protection-policies/app-protection-add-policies-01.png)

5. Click **Next** to display the **Apps** page.<br>
    The **Apps** page allows you to choose how you want to apply this policy to apps on different devices. You must add at least one app.<p>

    | Value/Option | Description |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Target to apps on all devices types | Use this option to target your policy to apps on devices of any management state. Choose **No** to target apps on specific devices types. For information, see [Target app protection policies based on device management state](#target-app-protection-policies-based-on-device-management-state). |
    |     Device types | Use this option to specify whether this policy applies to MDM managed devices or unmanaged devices. For iOS/iPadOS APP policies, select from **Unmanaged** and **Managed** devices. For Android APP policies, select from **Unmanaged**, **Android device administrator**, and **Android Enterprise**.  |
    | Target policy to | In the **Target policy to** dropdown box, choose to target your app protection policy to **All Apps**, **Microsoft Apps**, or **Core Microsoft Apps**.<p>-**All Apps** includes all Microsoft and partner apps that have integrated the Intune SDK.</br>-**Microsoft Apps** includes all Microsoft apps that have integrated the Intune SDK.</br>-**Core Microsoft Apps** includes the following apps: Edge, Excel, Office, OneDrive, OneNote, Outlook, PowerPoint, SharePoint, Teams, To Do, and Word.<p>Next, you can select **View a list of the apps that will be targeted** to view a list of the apps that will be affected by this policy.|
    | Public apps | If you do not want to select one of the pre-defined app groups, you can choose to target individual apps by selecting **Selected apps** in the **Target policy to** dropdown box. Click **Select public apps** to select public apps to target. |
    | Custom apps | If you do not want to select one of the pre-defined app groups, you can choose to target individual apps by selecting **Selected apps** in the **Target policy to** dropdown box. Click **Select custom apps** to select custom apps to target based on a Bundle ID. |

    The app(s) you have selected will appear in the public and custom apps list.

    > [!NOTE]
    > **Public apps** are supported are apps from Microsoft and partners that are commonly used with Microsoft Intune. These Intune protected apps are enabled with a rich set of support for mobile application protection policies. For more information, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md). Custom apps are LOB apps that have been integrated with the Intune SDK or wrapped by the Intune App Wrapping Tool. For more information see [Microsoft Intune App SDK Overview](../developer/app-sdk.md) and [Prepare line-of-business apps for app protection policies](../developer/apps-prepare-mobile-application-management.md).

6. Click **Next** to display the **Data protection** page.<br>
    This page provides settings for data loss prevention (DLP) controls, including cut, copy, paste, and save-as restrictions. These settings determine how users interact with data in the apps that this app protection policy applies.​

    **Data protection settings**:<br>
    - **iOS/iPadOS data protection** - For information, see [iOS/iPadOS app protection policy settings - Data protection](app-protection-policy-settings-ios.md#data-protection).
    - **Android data protection** - For information, see [Android app protection policy settings - Data protection](app-protection-policy-settings-android.md#data-protection).

7. Click **Next** to display the **Access requirements** page.<br>
    This page provides settings to allow you to configure the PIN and credential requirements that users must meet to access apps in a work context.

    **Access requirements settings**:<br>
    - **iOS/iPadOS access requirements** - For information, see [iOS/iPadOS app protection policy settings - Access requirements](app-protection-policy-settings-ios.md#access-requirements).
    - **Android access requirements** - For information, see [Android app protection policy settings - Access requirements](app-protection-policy-settings-android.md#access-requirements).

8. Click **Next** to display the **Conditional launch** page.<br>
    This page provides settings to set the sign-in security requirements for your app protection policy. Select a **Setting** and enter the **Value** that users must meet to sign in to your company app. Then select the **Action** you want to take if users do not meet your requirements. In some cases, multiple actions can be configured for a single setting.

    **Conditional launch settings**:<br>
    - **iOS/iPadOS conditional launch** - For information, see [iOS/iPadOS app protection policy settings - Conditional launch](app-protection-policy-settings-ios.md#conditional-launch).
    - **Android conditional launch** - For information, see [Android app protection policy settings - Conditional launch](app-protection-policy-settings-android.md#conditional-launch).

9. Click **Next** to display the **Assignments** page.<br>
   The **Assignments** page allows you to assign the app protection policy to groups of users. You must apply the policy to a group of users to have the policy take effect.

10. Click **Next: Review + create** to review the values and settings you entered for this app protection policy.

11. When you are done, click **Create** to create the app protection policy in Intune.

    > [!TIP]
    > These policy settings are enforced only when using apps in the work context. When end users use the app to do a personal task, they aren't affected by these policies. Note that when you create a new file it is considered a personal file.

    > [!IMPORTANT]
    > It can take time for app protection policies to apply to existing devices. End users will see a notification on the device when the app protection policy is applied. Apply your app protection policies to devices before applying condidtional access rules.

End users can download the apps from the App store or Google Play. For more information, see:
* [What to expect when your Android app is managed by app protection policies](../fundamentals/end-user-mam-apps-android.md)
* [What to expect when your iOS/iPadOS app is managed by app protection policies](../fundamentals/end-user-mam-apps-ios.md)

## Change existing policies
You can edit an existing policy and apply it to the targeted users. However, when you change existing policies, users who are already signed in to the apps won't see the changes for an eight-hour period.

To see the effect of the changes immediately, the end user must sign out of the app, and then sign back in.

### To change the list of apps associated with the policy

1. In the **App protection policies** pane, select the policy you want to change.

2. In the *Intune App Protection* pane, select **Properties**.

3. Next to the section titled *Apps*, select **Edit**.

4. The **Apps** page allows you to choose how you want to apply this policy to apps on different devices. You must add at least one app.<p>
    
    | Value/Option | Description |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Target to apps on all devices types | Use this option to target your policy to apps on devices of any management state. Choose **No**  to target apps on specific devices types. Additional app configuration may be required for this setting. For more information, see [Target app protection policies based on device management state](#target-app-protection-policies-based-on-device-management-state). |
    |     Device types | Use this option to specify whether this policy applies to MDM managed devices or unmanaged devices. For iOS/iPadOS APP policies, select from **Unmanaged** and **Managed** devices. For Android APP policies, select from **Unmanaged**, **Android device administrator**, and **Android Enterprise**.  |
    | Public apps | In the **Target policy to** dropdown box, choose to target your app protection policy to **All public apps**, **Microsoft Apps**, or **Core Microsoft Apps**. Next, you can select **View a list of the apps that will be targeted** to view a list of the apps that will be affected by this policy.<p>If needed, you can choose to target individual apps by clicking **Select public apps**.  |
    | Custom apps | Click **Select custom apps** to select custom apps to target based on a Bundle ID. |

    The app(s) you have selected will appear in the public and custom apps list.

5. Click **Review + create** to review the apps selected for this policy.

6. When you are done, click **Save** to update the app protection policy.
 
#### To change the list of user groups

1. In the **App protection policies** pane, select the policy you want to change.

2. In the *Intune App Protection* pane, select **Properties**.

3. Next to the section titled *Assignments*, select **Edit**.

4. To add a new user group to the policy, on the *Include* tab choose **Select groups to include**, and select the user group. Choose **Select** to add the group. 

5. To exclude a user group, on the *Exclude* tab choose **Select groups to exclude**, and select the user group. Choose **Select** to remove the user group.  

6. To delete groups that were added previously, on either the *Include* or *Exclude* tabs, select the ellipsis (...) and select **Delete**.

7. Click **Review + create** to review the user groups selected for this policy.

8. After your changes to the assignments are ready, select **Save** to save the configuration and deploy the policy to the new set of users. If you select **Cancel** before you save your configuration, you will discard all changes you've made to the *Include* and *Exclude* tabs.

### To change policy settings

1. In the **App protection policies** pane, select the policy you want to change.

2. In the *Intune App Protection* pane, select **Properties**.

3. Next to the section corresponding to the settings you want to change, select **Edit**. Then change the settings to new values.

7. Click **Review + create** to review the updated settings for this policy.

4. Select the **Save** to save your changes. Repeat the process to select a settings area and modify and then save your changes, until all your changes are complete. You can then close the *Intune App Protection - Properties* pane. 

## Target app protection policies based on device management state
In many organizations, it's common to allow end users to use both Intune Mobile Device Management (MDM) managed devices, such as corporate owned devices, and un-managed devices protected with only Intune app protection policies. Unmanaged devices are often known as Bring Your Own Devices (BYOD).

Because Intune app protection policies target a user's identity, the protection settings for a user can apply to both enrolled (MDM managed) and non-enrolled devices (no MDM). Therefore, you can target an Intune app protection policy to either Intune enrolled or unenrolled iOS/iPadOS and Android devices. You can have one protection policy for unmanaged devices in which strict data loss prevention (DLP) controls are in place, and a separate protection policy for MDM managed devices, where the DLP controls may be a little more relaxed. For more information how this works on personal Android Enterprise devices, see [App protection policies and work profiles](android-deployment-scenarios-app-protection-work-profiles.md).

To create these policies, browse to **Apps** > **App protection policies** in the Intune console, and then select **Create policy**. You can also edit an existing app protection policy. To have the app protection policy apply to both managed and un-managed devices, navigate to the **Apps** page and confirm that **Target to apps on all device types** is set to **Yes**, the default value. If you want to granularly assign based on management state, set **Target to apps on all device types**  to **No**. 

### Device types

- **Unmanaged**: For iOS/iPadOS devices, unmanaged devices are any devices where either Intune MDM management or a 3rd party MDM/EMM solution does not pass the `IntuneMAMUPN` key. For Android devices, unmanaged devices are devices where Intune MDM management has not been detected. This includes devices managed by third-party MDM vendors.
- **Intune managed devices**: Managed devices are managed by Intune MDM.
- **Android device administrator**: Intune-managed devices using the Android Device Administration API.
- **Android Enterprise**: Intune-managed devices using Android Enterprise Work Profiles or Android Enterprise Full Device Management.

On Android, Android devices will prompt to install the Intune Company Portal app regardless of which Device type is chosen. For example, if you select 'Android Enterprise' then users with unmanaged Android devices will still be prompted.

For iOS/iPadOS, for the 'Device type' selection to be enforced to Intune managed devices, additional app configuration settings are required. These configurations will communicate to the APP service that a particular app is managed - and that APP settings will not apply:

- **IntuneMAMUPN** must be configured for all MDM managed applications. For more information, see [How to manage data transfer between iOS/iPadOS apps in Microsoft Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).
- **IntuneMAMDeviceID** must be configured for all third-party and line-of-business MDM managed applications. The **IntuneMAMDeviceID** should be configured to the device ID token. For example, `key=IntuneMAMDeviceID, value={{deviceID}}`. For more information, see [Add app configuration policies for managed iOS/iPadOS devices](app-configuration-policies-use-ios.md).
- If only the **IntuneMAMDeviceID** is configured, the Intune APP will consider the device as unmanaged.

> [!NOTE]
> For specific iOS/iPadOS support information about app protection policies based on device management state, see [MAM protection policies targeted based on management state](../fundamentals/whats-new-archive.md#mam-protection-policies-targeted-based-on-management-state).

## Policy settings
To see a full list of the policy settings for iOS/iPadOS and Android, select one of the following links:

- [iOS/iPadOS policies](app-protection-policy-settings-ios.md)
- [Android policies](app-protection-policy-settings-android.md)

## Next steps
[Monitor compliance and user status](app-protection-policies-monitor.md)

## See also
* [What to expect when your Android app is managed by app protection policies](../fundamentals/end-user-mam-apps-android.md)
* [What to expect when your iOS/iPadOS app is managed by app protection policies](../fundamentals/end-user-mam-apps-ios.md)
