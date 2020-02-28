---
# required metadata

title: Microsoft Intune policy to allow/block apps for Samsung Knox
titleSuffix:
description: Create a custom profile to allow and block apps for Samsung Knox Standard devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection: M365-identity-device-management
---
# Use custom policies in Microsoft Intune to allow and block apps for Samsung Knox Standard devices 

Use the procedure in this article to create a Microsoft Intune custom policy that creates one of the following:

- A list of apps that are blocked from running on the device. Apps in this list are blocked from being run, even if they were already installed when the policy was applied.
- A list of apps that users of the device are allowed to install from the Google Play store. Only the apps you list can be installed. No other apps can be installed from the store.

These settings can only be used by devices that run Samsung Knox Standard.

## Create an allowed or blocked app list

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following settings:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Windows phone custom profile**.
    - **Description**: Enter a description that gives an overview of the setting, and any other important details.
    - **Platform**: Select **Android**.
    - **Profile type**: Select **Custom**.

4. In **Custom OMA-URI Settings**, select **Add**. Enter the following settings:

    For a list of apps that are blocked from running on the device:

    - **Name**: Enter **PreventStartPackages**.
    - **Description**: Enter a description that gives an overview of the setting, and any other relevant information to help you locate the profile. For example, enter **List of apps that are blocked from running**.
    - **OMA-URI** (case sensitive): Enter **./Vendor/MSFT/PolicyManager/My/ApplicationManagement/PreventStartPackages**.
    - **Data type**: Select **String**.
    - **Value**: Enter a list of the app package names you want to allow. You can use `;`, `:`, or `|` as a delimiter. For example, enter `package1;package2;`.

   For a list of apps that users are allowed to install from the Google Play store while excluding all other apps:

    - **Name**: Enter **AllowInstallPackages**.
    - **Description**:Enter a description that gives an overview of the setting, and any other relevant information to help you locate the profile. For example, enter **List of apps that users can install from Google Play**.
    - **OMA-URI** (case sensitive): Enter **./Vendor/MSFT/PolicyManager/My/ApplicationManagement/AllowInstallPackages**.
    - **Data type**: Select **String**.
    - **Value**: Enter a list of the app package names you want to allow. You can use `;`, `:`, or `|` as a delimiter. For example, enter `package1;package2;`.

5. Select **OK** to save your changes.
6. When finished, select **OK** > **Create** to create the Intune profile. When complete, your profile is shown in the **Devices - Configuration profiles** list.

>[!TIP]
> You can find the package ID of an app by browsing to the app on the Google Play store. The package ID is contained in the URL of the app's page. For example, the package ID of the Microsoft Word app is **com.microsoft.office.word**.

The next time each targeted device checks in, the app settings are applied.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](../device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
