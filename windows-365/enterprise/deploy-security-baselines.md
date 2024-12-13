---
# required metadata
title: Deploy security baselines for Windows 365
titleSuffix:
description: Learn how to deploy security baselines for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/09/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ryclark
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Deploy security baselines

Windows 365 Security Baselines version 24H1 are a set of policy templates built on security best practices and experience from real world implementations. You can use security baselines to get security recommendations that can help lower risks. The Windows 365 baselines enable security configurations for Windows 11, Windows 10, Microsoft Edge, and Microsoft Defender for Endpoint. They include versioning features and help customers choose when to update user policies to the latest release.

The settings in the Windows 365 Cloud PC security baseline version 24H1 apply to Windows devices managed through Intune. When available, the setting name links to the source Configuration Service Provider (CSP), and then displays that settings default configuration in the baseline.

> [!TIP]
> Like any configuration change, it is always a good idea to test the security baseline on a pilot group of Cloud PCs. For information on how to build a rollout plan in Microsoft Intune, see the [Microsoft Intune planning guide](/mem/intune/fundamentals/intune-planning-guide#task-5-create-a-rollout-plan). For information on Microsoft Defender for Endpoint features can be tested, see [Test how Microsoft Defender for Endpoint features work in audit mode](/microsoft-365/security/defender-endpoint/audit-windows-defender).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) select **Endpoint Security** > **Security Baselines**.
![Screenshot of view security baselines](./media/deploy-security-baselines/view-security-baselines.png)
2. Select **Windows 365 Security Baseline Version 24H1**.
3. On the **Create a profile** pane, select **Create profile** > **Create**.
4. On the **Basics** page, provide a **Name** > **Next**.
5. On the **Configuration settings** tab, view the groups of settings that are available in the baseline you selected. You can expand a group to view the settings in that group, and the default values for those settings in the baseline. To find specific settings:
    - Select a group to expand and review the available settings.
    - To display only those groups that contain your search criteria, use the Search bar and specify keywords that filter the view.

    Each setting in a baseline has a default configuration for that baseline version. Reconfigure the default settings to meet your business needs. Different baselines might contain the same setting, and use different default values for the setting, depending on the intent of the baseline.
5. Select **Next**.
6. On the **Scopes** page, optionally select scope tags > **Next**.
7. On the **Assignments** tab, select a device group with the Cloud PCs to include and then assign the baseline to one or more groups with your Cloud PCs. Use **Add groups** under **Excluded groups** to fine-tune the assignment. Select **Next**.
8. When you're ready to deploy the baseline, advance to the **Review + create** tab and review the details for the baseline. Select **Create** to save and deploy the profile.

As soon as you create the profile, it's pushed to the assigned group and is applied immediately.

<!-- ########################## -->
## Next steps

For more information, see [Use security baselines to configure Windows devices in Intune](/mem/intune/protect/security-baselines).

For a detailed list of the 24H1 settings, see [Settings list for the Windows 365 Cloud PC security baseline in Intune](/mem/intune/protect/security-baseline-settings-windows-365?pivots=win365-24h1).

[Set Conditional Access policies](set-conditional-access-policies.md).
