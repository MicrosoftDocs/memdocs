---
# required metadata
title: Set up forensic evidence in Windows 365
titleSuffix:
description: Learn how set up Microsoft Purview forensic evidence in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/31/2024
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

# Set up Microsoft Purview forensic evidence for Windows 365

[Microsoft Purview forensic evidence](/purview/insider-risk-management-forensic-evidence) helps you get better insights into potentially risky security-related user activities. With customizable event triggers and built-in user privacy protection controls, forensic evidence lets you customize visual activity capturing across devices. Forensic evidence helps your organization better mitigate, understand, and respond to potential data risks like unauthorized data exfiltration of sensitive data.

You set the right policies for your organization, like:

- What risky events are the highest priority for capturing forensic evidence.
- What data is most sensitive.
- Whether users are notified when forensic capturing is activated.

Forensic evidence capturing is off by default and policy creation requires dual authorization.

## Requirements

If the following requirements aren't met, you might run into Microsoft Purview client issues and the quality of forensic captures might not be reliable.

To set up Microsoft Purview forensic evidence, your environment must meet the following requirements:

### Device configuration requirements

- Gallery image type
  - Windows 11 Enterprise + Microsoft 365 Apps 23H2 or later
- Licensing options
  - Microsoft 365 E5
  - Microsoft 365 E5 (no Teams)
  - Microsoft 365 E5 Compliance
  - Microsoft 365 E5 Insider Risk Management
- Join type and network
  - [Microsoft Entra joined](/entra/identity/devices/concept-directory-join) with Microsoft hosted network and Azure network connections
  - [Microsoft Entra hybrid joined](/entra/identity/devices/concept-hybrid-join) with Azure network connection
- [Microsoft Defender Antivirus in Windows](/defender-endpoint/microsoft-defender-antivirus-windows) version 4.18.2110 or later
- Microsoft 365 Apps version 16.0.14701.0 or later
- The device must be assigned to a [primary user](/mem/intune/remote-actions/find-primary-user)
- Cloud PC size
  - For optimal performance, 8vCPU or better (for more information, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md))

### Role requirements

- Account must have at least one of these roles:
    - Microsoft Entra ID Compliance Administrator role
    - Microsoft Entra ID Global Administrator role
    - Microsoft Purview Organization Management role group
    - Microsoft Purview Compliance Administrator role group
    - Insider Risk Management role group
    - Insider Risk Management Admins role group

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

For more information about insider risk management roles, see [Enable permissions for insider risk management](/purview/insider-risk-management-configure?tabs=purview-portal#step-1-required-enable-permissions-for-insider-risk-management).

## Turn on device onboarding

1. Open the [Microsoft Purview portal](https://purview.microsoft.com). Choose **Settings** > **Device onboarding** > **Devices** > **Onboarding**.

2. Select which **Deployment method** to use to deploy the configuration package:

    - [Intune: Use Mobile Device management tools or Microsoft Intune.](#deploy-the-configuration-package-using-intune)
    - [Local script: Use a local script.](#use-a-local-script-to-deploy-configuration-package)

### Deploy the configuration package using Intune

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Microsoft Defender for Endpoint** > **Open the Microsoft Defender Security Center**.

2. Set **Microsoft Intune connection** to *On* and then **Save preferences**.

3. Return to the **Microsoft Defender for Endpoint** and set the following options:

    - **Allow Microsoft for Endpoint to enforce Endpoint Security Configurations**: *On*
    - **Connect Windows devices version 10.0.15063 and above to Microsoft Defender for Endpoint**: *On*

4. Select **Save**.

5. Select **Endpoint security** > **Endpoint detection and response** > **Create policy**.

6. Select the following options:

    - **Platform**: *Windows 10, Windows 11, and Windows Server*
    - **Profile type**: *Endpoint detection and response*

7. Select **Create**.

8. Provide a **Name** and **Description** > **Next**.

9. On the **Configuration settings** page, for **Microsoft Defender for Endpoint client configuration package type**, select *Auto from connector* > **Next**.

10. On the **Scope tags** page, select **Next**.

11. On the **Assignments** page, select the group that includes the primary user of the Cloud PC > **Next**.

12. On the **Review and create** page, when you're done, select **Create**.

After you create the policy, a user must sign in to their device before the policy is applied and the device is onboarded to Microsoft Defender for Endpoint.

### Use a local script to deploy configuration package

Follow the instructions in [Onboard Windows 10 and Windows 11 devices using a local script](/purview/device-onboarding-script). This script can be helpful when testing a subset of Cloud PCs before proceeding to onboard all your Cloud PCs.

## View onboarding devices list

1. Open the [Microsoft Purview portal](https://purview.microsoft.com) > **Settings** > **Device onboarding** > **Devices**.

2. Check the following columns:

    - **Configuration status**: Shows if the device is configured correctly.
    - **Policy sync status**: Shows if the device updated to the latest policy version. Devices must be on to update to the latest policy.

<!-- ########################## -->
## Next steps

For more information about Microsoft Purview, see [Learn about Microsoft Purview](/purview/purview).

For more information about Microsoft Purview forensic evidence capturing options, see [Capturing options](/purview/insider-risk-management-forensic-evidence#capturing-options).

For more information Microsoft Purview capacity and billing, see [Capacity and billing](/purview/insider-risk-management-forensic-evidence-manage?tabs=purview-portal#capacity-and-billing).