---
# required metadata

title: Allow or block apps for Samsung Knox Standard devices
titleSuffix:
description: Create a custom profile to allow and block apps for Samsung Knox Standard Android device administrator devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/16/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection:
- tier2
- M365-identity-device-management
---

# Use custom policies in Microsoft Intune to allow and block apps for Samsung Knox Standard devices 

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

Use the steps in this article to create a Microsoft Intune custom policy that creates one of the following lists:

- A list of apps that are blocked from running on the device. Apps in this list are blocked from being run, even if they were already installed when the policy was applied.
- A list of apps that users of the device are allowed to install from the Google Play store. Only the apps you list can be installed. No other apps can be installed from the store.

This feature applies to:

- Android device administrator (DA)

These settings are only used on devices that run Samsung Knox Standard.

## Prerequisites

- [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]

## Create an allowed or blocked app list

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Android device administrator**.
    - **Profile type**: Select **Custom**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Android Samsung Knox - blocks apps**.
    - **Description**: Enter a description that gives an overview of the setting, and any other important details. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Add**. Enter the following custom OMA-URI settings:

    For a list of apps that are blocked from running on the device:

    - **Name**: Enter **PreventStartPackages**.
    - **Description**: Enter a description that gives an overview of the setting, and any other relevant information to help you locate the profile. For example, enter **List of apps that are blocked from running**.
    - **OMA-URI** (case sensitive): Enter `./Vendor/MSFT/PolicyManager/My/ApplicationManagement/PreventStartPackages`.
    - **Data type**: Select **String**.
    - **Value**: Enter a list of the app package names you want to block. You can use `;`, `:`, or `|` as a delimiter. For example, enter `package1;package2;`.

    For a list of apps that users are allowed to install from the Google Play store while excluding all other apps:

    - **Name**: Enter **AllowInstallPackages**.
    - **Description**: Enter a description that gives an overview of the setting, and any other relevant information to help you locate the profile. For example, enter **List of apps that users can install from Google Play**.
    - **OMA-URI** (case sensitive): Enter `./Vendor/MSFT/PolicyManager/My/ApplicationManagement/AllowInstallPackages`.
    - **Data type**: Select **String**.
    - **Value**: Enter a list of the app package names you want to allow. You can use `;`, `:`, or `|` as a delimiter. For example, enter `package1;package2;`.

8. **Save** your changes > **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or device groups that will receive your profile. For more information on assigning profiles, go to [assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

> [!TIP]
> You can find the package ID of an app by browsing to the app on the Google Play store. The package ID is contained in the URL of the app's page. For example, the package ID of the Microsoft Word app is `com.microsoft.office.word`.

The next time each targeted device checks in, the app settings are applied.

## Resources

The profile is created, but might not be doing anything yet. Be sure to [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
