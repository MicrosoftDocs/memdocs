---
# required metadata

title: Add custom settings to Linux devices in Microsoft Intune
titleSuffix:
description: Add Bash scripts to create a custom Linux profile in Microsoft Intune. Use the script to create, use, and control custom settings and features on Linux devices. This custom profile can then be assigned or distributed to Linux devices in your organization to create a baseline or standard.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/15/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use custom Bash scripts to configure Linux devices in Microsoft Intune

> [!IMPORTANT]
> Custom configuration profiles shouldn't be used for sensitive information, such as WiFi connections or authenticating apps, sites, and more.

Using Microsoft Intune, you can add or create custom configuration settings for your Linux devices using custom Bash scripts. They're designed to add device settings and features that aren't built in to Intune.

In Intune, you import an existing Bash script, and then assign the script policy to your Linux users and devices. Once assigned, the settings are distributed. They also create a baseline or standard for Linux in your organization.

This article lists the steps to add an existing script and has a GitHub repo with some sample scripts.

## Prerequisites

- **Linux Ubuntu Desktop**, **RedHat Enterprise Linux 8**, or **RedHat Enterprise Linux 9**: For a list of the supported versions, go to [Supported operating systems and browsers in Intune](../fundamentals/supported-devices-browsers.md).
- **Linux devices are enrolled in Intune**. For more information on Linux enrollment, go to [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-linux.md).  

## Import the script

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Scripts and remediations** > **Platform scripts** tab > **Add** > **Linux**:

    :::image type="content" source="./media/custom-settings-linux/add-linux-script.png" alt-text="Screenshot that shows how to select devices, scripts, add, and select Linux from the drop-down list to add a custom Bash script in Microsoft Intune.":::

3. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

4. Select **Next**.

5. In **Configuration settings**, configure the following settings:

    - **Execution context**: Select the context the script is executed in. Your options:
      - **User** (default): When a user signs in to the device, the script runs. If a user never signs into the device, or there isn't any user affinity, then the script doesn't run.
      - **Root**: The script always runs (with or without users logged in) at the device level. (**Note**: The user will have to give consent for the first time the script is executing, afterward it will continue to execute in its schedule) 

    - **Execution frequency**: Select how frequently the script is executed. The default is **Every 15 minutes**.

    - **Execution retries**: If the script fails, enter how many times Intune should retry running the script. The default is **No retries**.

    - **Execution Script**: Select the file picker to upload an existing Bash script. Only add `.sh` files.  

      Microsoft has some sample Bash scripts at [https://github.com/microsoft/shell-intune-samples/tree/master/Linux](https://github.com/microsoft/shell-intune-samples/tree/master/Linux).

    - **Bash Script**: After you add an existing Bash script, the script text is shown. You can edit this script.

6. Select **Next**.
7. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

8. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

9. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Next steps

You can also run shell scripts on [macOS](../apps/macos-shell-scripts.md) and [Windows](../apps/intune-management-extension.md).
