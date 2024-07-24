---
# required metadata

title: Import Wi-Fi settings for Windows devices in Microsoft Intune
description: Export Wi-Fi settings from a Windows device as an XML file using the network shell (netsh wlan) command. Then, import this file in Intune to create a Wi-Fi profile for devices running Windows 10/11 and Windows Holographic for Business.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
ms.reviewer: abalwan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Import Wi-Fi settings for Windows devices in Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

On Windows devices, you can export Wi-Fi settings to an XML file, and then import these settings in Intune. Using these imported settings, you can create a Wi-Fi profile, and then deploy it to your devices.

This feature applies to:

- Windows 11
- Windows 10
- Windows Holographic for Business
- Windows 8.1 and newer

This article shows you how to export Wi-Fi settings from a Windows device, and then import these settings in to Intune.

> [!NOTE]
>
> - On Windows 10/11, you can [create a Wi-Fi profile](wi-fi-settings-windows.md) directly in Intune. You don't have to import a file.
> - For Windows 8.1 devices, you must export and import Wi-Fi settings to create and deploy Wi-Fi profiles.

## Before you begin

- To configure the Intune policy, at a minimum, sign into the Intune admin center with the **Policy and Profile manager** role. For information on the built-in roles in Intune, and what they can do, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Export Wi-Fi settings from a Windows device

To export an existing Wi-Fi profile to an XML file readable by Intune, use `netsh wlan`. On a Windows computer that has the WiFi profile, use the following steps:

1. Create a local folder for the exported Wi-Fi profiles, such as **c:\WiFi**.
2. Open a command prompt as an administrator.
3. Run the `netsh wlan show profiles` command. Note the name of the profile you want to export.
4. Run the `netsh wlan export profile name="ContosoWiFi" folder=c:\Wifi` command. This command creates a Wi-Fi profile file named **Wi-Fi-ContosoWiFi.xml** in your target folder.

### Preshared keys and exporting

If you're exporting a Wi-Fi profile that includes a preshared key (PSK), you **must** add `key=clear` to the command. The key must be exported in plain text to successfully use the profile.

For example, enter:

```cmd
netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi
```

- Using a preshared key with Windows 10/11 causes a remediation error to show in Intune. When the error happens, the Wi-Fi profile is properly assigned to the device, and the profile works as expected.

- If you export a Wi-Fi profile that includes a preshared key, be sure the file is protected. The key is in plain text. It's your responsibility to protect the key.

## Import the Wi-Fi settings into Intune

When the XML file is ready, you can import it into Intune to create a Wi-Fi profile.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 8.1 and later**.

      Even though you select Windows 8.1, this feature still applies to Windows 10/11 and Windows Holographic.

    - **Profile type**: Select **Wi-Fi import**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: This setting is the profile name. You must enter the same name as the `name` attribute in the Wi-Fi profile xml. If you enter a different name, the profile fails.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended. For example, enter `Imported Wi-Fi profile for Windows Holographic devices`.

6. Select **Next**.
7. In **Configuration settings**, enter the following properties:

    - **Connection name**: Enter a name for the Wi-Fi connection. This name is shown to users when they browse available Wi-Fi networks. For example, enter `ContosoWiFi`.
    - **Profile XML**: Select the browse button, and select the XML file that contains the Wi-Fi profile settings you want to import.
    - **File contents**: Shows the XML code for the XML file you selected.

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- See the [Wi-Fi settings overview](wi-fi-settings-configure.md), including other available platforms.
