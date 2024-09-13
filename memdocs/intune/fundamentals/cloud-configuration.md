---
# required metadata

title: Use Windows cloud configuration in a guided scenario
description: Use a guided scenario to configure Windows 10/11 client devices in a cloud configuration in Microsoft Intune. Cloud config focuses on a simplified device experience for internet browsing and using Microsoft 365 apps, including Microsoft Teams.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/19/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rashok
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
- intune-scenario
---

# Guided scenario - Windows 10/11 in cloud configuration

Windows 10/11 in cloud configuration is a Microsoft-recommended device configuration. You can turn any Windows 10/11 Professional, Enterprise, and Education device into a cloud-optimized device.

Cloud configuration is ideal for:

- Frontline workers (FLW)
- Remote workers
- Users with focused workflow needs, like productivity and browsing

Cloud config makes these devices easy to use, and secures these devices with Microsoft-recommended security features.

There are two ways to deploy cloud config:

- **Option 1 - Automatic** (this article): Use the guided scenario described in this article to automatically create all the groups and policies with their configured values.
- **Option 2 - Manual**: Use a step-by-step setup guide to deploy cloud config yourself, including manually creating all the policies. For information on this option, go to [Windows client cloud config setup guide](cloud-configuration-setup-guide.md).

With Windows 10/11 in cloud configuration:

- You can configure new devices, or reuse existing hardware.
- End users get an easy-to-use, and familiar Windows experience.
- Administrators get a uniform device configuration across devices, which makes management and troubleshooting easier.
- You can customize the names of your resources, so they're easy to see and monitor.

> [!TIP]
> For a more comprehensive guide on Windows 10/11 in cloud configuration, go to [Windows 10/11 in cloud configuration](https://aka.ms/cloud-config).

## What this guided scenario does

Using Microsoft Intune, you can use a guided scenario to deploy a cloud configuration. The guided scenario automatically creates all the resources you need, including:

- Creates a new Microsoft Entra security group, or uses an existing Microsoft Entra security group.
- Deploys the Microsoft Edge and Microsoft Teams apps. For information on deploying these apps individually, go to:
  - [Add Microsoft Edge for Windows 10/11](../apps/apps-windows-edge.md)
  - [Add Microsoft 365 apps to Windows 10/11 devices](../apps/apps-add-office365.md)

- Creates a Windows 10/11 security baseline policy with recommended security settings that are already configured.

  For information about security baselines, and what they do, go to [Use security baselines to configure Windows client devices](../protect/security-baselines.md).

- Creates a Windows Autopilot enrollment profile that automatically enrolls devices in Microsoft Intune.

  For information on creating your own Windows Autopilot profile, go to [Configure Autopilot profiles](/autopilot/profiles).

- Turns on and configures the Windows Autopilot enrollment status page (ESP). This page shows users the enrollment progress.

  For information about the ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

- Creates an administrative template that configures OneDrive with the Known Folder Move settings. With these settings, user files and data are automatically saved in OneDrive.

  For information on this setting, go to [Redirect and move Windows known folders](/onedrive/redirect-known-folders).

- Creates an administrative template that configures some SmartScreen settings in the Microsoft Edge app. For information on creating your own profile, go to [Configure Microsoft Edge policy settings](../configuration/administrative-templates-configure-edge.md).

- Creates a compliance policy that monitors compliance and health. Users are allowed to use noncompliant devices, and access resources. If your organization blocks access to noncompliant devices, then create another compliance policy that blocks access, and assign it to the same group.

  For information on the compliance settings you can configure on your own, go to [Windows client settings to mark devices as compliant or not compliant](../protect/compliance-policy-create-windows.md).

- Deploys a Windows PowerShell script that removes built-in apps, and simplifies the Start menu.

  For information about PowerShell scripts in Intune, go to [Use PowerShell scripts on Windows client devices](../apps/intune-management-extension.md).

- Creates a Windows client update ring policy. This policy automatically updates the devices, including product updates, drivers, and Windows updates.

  For information about update rings, and creating your policy, go to [Update rings for Windows client devices](../protect/windows-10-update-rings.md).

> [!TIP]
> This guided scenario creates all these resources for you, automatically. If you want create your own individual resources, and not use the guided scenario, you can. For the steps, go to the [cloud config overview and setup guide](https://aka.ms/CloudConfigGuide).

## Prerequisites

- Confirm your licenses. At a minimum, the account creating the guided scenario must have the following licenses:

  - Microsoft Entra ID P1
  - Microsoft Intune
  - Microsoft Teams
  - OneDrive
  - Windows 10 Pro
  - Windows 11 Pro

  All of these services are included with the Microsoft 365 E3 license. For more security options and features, use the Microsoft 365 E5 license. To help decide which license is right for your organization, go to [Transform your enterprise with Microsoft 365](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans).

- [Set the MDM authority to Intune](mdm-authority-set.md). The mobile device management (MDM) authority setting determines how you manage your devices. As an IT admin, you must set an MDM authority before users can enroll devices for management.

- Enable automatic enrollment for Windows client devices. For information, go to:

  - [Quickstart: Set up automatic enrollment for Windows client devices](../enrollment/quickstart-setup-auto-enrollment.md)
  - [Enable Windows 10/11 automatic enrollment](../enrollment/windows-enroll.md#enable-windows-automatic-enrollment)

- Sign in as the Intune Service Administrator Microsoft Entra role, also known as the Intune Administrator. For information on the roles that affect Intune, go to:

  - [Intune Administrator - Microsoft Entra built-in role](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
  - [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)

## Step 1 - Introduction

Open the guided scenario:

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Troubleshooting + support** > **Guided scenarios** > **Deploy Windows 10 and later in cloud configuration** > **Start**.
3. In **Introduction**, select **Next**.

## Step 2 - Basics

Choose how your devices are named when they enroll, and choose the prefix of all the resources created.

- **Autopilot device name template**: The cloud configuration guided scenario enrolls your devices in Windows Autopilot. When they enroll, you can optionally name your devices using a unique pattern that applies to all devices. Your options:

  - **Apply device name template**: **No** doesn't create a template or pattern when naming your devices. The device will have the OEM name, such as `DESKTOP-`, followed by some random characters. Select **Yes** to create a unique pattern to name your devices. For example, enter `Contoso-%RAND:7%` to name all your devices **Contoso-** followed by seven random characters.

    The names:

    - Must be 15 characters or less.
    - Can include letters (a-z, A-Z), numbers (0-9), and hyphens.
    - Can't be only numbers, and can't include a blank space.
    - Can use the `%SERIAL%` macro to add a hardware-specific serial number.
    - Can use the `%RAND:x%` macro to add a random string of characters, where `x` equals the number of characters to add.

- **Resource name prefix**: When you deploy the guided scenario, several resources are automatically created. To distinguish the items used in this deployment, add a prefix:

  - **Enter a resource prefix name**: Enter some text that will be at the beginning of the items created. For example, enter `Windows cloud config`. All resources created are named something like **Windows cloud config Autopilot profile**, or **Windows cloud config compliance policy**.

- **Resources to be created**: Select the default file format for the resources created by this guided scenario. Your options:

  - **Office Open Document**: Creates the resources in Office Open Document format (ODF).
  - **Office Open XML**: Creates the resources in Office Open XML format, which is typically the recommended format.

  Your settings look similar to the following image:

  :::image type="content" source="./media/cloud-configuration/guided-scenario-basics.png" alt-text="Screenshot that shows how to configure the device name template and resource name prefix in a Windows 10/11 cloud configuration guided scenario in Microsoft Intune." lightbox="./media/cloud-configuration/guided-scenario-basics.png":::

- Select **Next**.

## Step 3 - Apps

Select the apps you want to deploy to devices. Microsoft recommends you deploy the smallest number of apps as possible. The idea is to keep your cloud config devices simple, and easy to manage.​

- **Cloud config defaults**: This guided scenario automatically includes the Microsoft Edge and Microsoft Teams apps. They can't be removed when creating the guided scenario. You can delete or uninstall these apps after the guided scenario finishes.

  To remove the Microsoft Edge app, go to [Uninstall the app](../apps/apps-windows-edge.md#uninstall-the-app).

- **Select additional M365 apps (optional)**: From the list, add other Microsoft 365 apps that you want on the devices. Remember, keep the list small, and only include apps your users need. The idea is to keep the devices simple.

  > [!TIP]
  > To add apps not listed, or add line-of-business apps, complete this guided scenario. Then, in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps**, and create a policy. Deploy the app policy to the same group that you deployed this cloud config guided scenario. For information on adding apps, go to [Add apps to Microsoft Intune](../apps/apps-add.md).

- Select **Next**.

## Step 4 - Assignments

Select the groups that should receive this guided scenario, and all the resources it creates.

- **Create new group**: Creates a new group, and deploys the guided scenario policies to this group. As devices are added to this group, they receive this guided scenario.
  - **Group name**: Enter the group name. For example, enter `Cloud configured devices`.

- **Choose an existing group**: Select an existing group. You guided scenario policies are deployed to this group.

- Select **Next**.

## Step 5 - Review + deploy

A summary of the settings and the values you configured are shown. You can go back to the other tabs, and change any values you added.

Look at the following properties:

- **Configurations to be made**: Expand this option to see all the resources that will be created, including the policies.
- **Deploy**: Select this option to save your changes, and deploy the guided scenario. The groups you added will receive the policies in this guided scenario.

  As the resources are being created in the Intune admin center, the status is shown, similar to the following image:

  :::image type="content" source="./media/cloud-configuration/guided-scenario-deployment-status.png" alt-text="Screenshot that shows how to review the Windows 10/11 in cloud configuration guided scenario deployment status in Microsoft Intune.":::

If there's an error, then the guided scenario isn't deployed, and all changes are reverted. The [Cloud configuration overview and setup guide](https://aka.ms/CloudConfigGuide) is also a good resource.

When it deploys successfully, you can use the monitoring and reporting features in the Intune admin center:

- [Intune reports](reports.md)
- [Monitor device profiles](../configuration/device-profile-monitor.md)
- [Monitor security baselines and profiles](../protect/security-baselines-monitor.md)

## What you need to know

- You can complete the guided scenario before there are any devices in the group. When devices are added to the group, and have internet access, then they automatically start receiving the policies in this guided scenario.

  You can also:

  - Add preregistered Windows Autopilot devices to the group. Add them to the group before you enroll or apply any policies.
  - Add existing Windows client devices that are already enrolled. Microsoft recommends removing other apps and profiles targeted to these devices. After adding them to the group, reset the devices so they start fresh with just cloud config applied.

  For information on the policy refresh times, go to [Common questions and answers with device policies in Microsoft Intune](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

- Microsoft recommends only assigning cloud config settings and apps. After this guided scenario deploys, then you can add any other required resources, such as certificates, VPN profiles, line-of-business apps, and more. Be sure to deploy these policies to the same group as this guided scenario. Remember, keep the list small, and only include resources your users need.
- Because of a OneDrive sync issue with shared devices, Microsoft doesn't recommend using Windows 10/11 in cloud configuration with shared devices. Shared devices typically have multiple users that sign in and sign out.
- After the guided scenario is deployed, you can go to a policy, and see the settings and their configured values. You can change any of these settings to another value, if you like.
- To remove the guided scenario settings from devices, go to each policy created by the cloud config guided scenario. Configure the settings to **Not Configured**. Deploy each policy again to the same group as this guided scenario.

  The next time the device checks in, the setting is no longer locked. Then, another policy or possibly the end can change the setting. It's possible the setting might have the same value set by the guided scenario.

  Now, you can delete the individual items created by this guided scenario, including apps, policies, the Windows PowerShell script, and the group.

## Related content

- [Guided scenarios overview](guided-scenarios-overview.md)
- [Windows client cloud config step by step setup guide](cloud-configuration-setup-guide.md)
