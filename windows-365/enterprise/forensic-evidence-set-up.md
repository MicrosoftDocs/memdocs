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
ms.subservice:
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



## Requirements

To set up Microsoft Purview forensic evidence, your environment must meet the following requirements:

- Gallery image type
    - Windows 11 Enterprise + Microsoft 365 Apps 23H2
- Licensing
  - Microsoft 365 E5, or
  - Windows 365 Enterprise 2 vCPU, 4 GB, 64 GB
 - Join type and network
  - Microsoft Entra join for Azure network connection
  - Microsoft Entra hybrid join for Microsoft hosted network
- Animalware client version 4.18.2110 or later
- Microsoft 365 Apps version 16.0.14701.0 or later
- The device must be assigned to a primary user
- Account must have at least one of these roles
    - Global admin
    - Security admin
    - Compliance admin

## Turn on device onboarding

1. Open the [Microsoft Purview compliance portal](https://compliance.microsoft.com). Choose **Settings** > **Device onboarding** > **Devices** > **Onboarding**.

2. Select which **Deployment method** to use to deploy the configuration package:

  - Intune: Use Mobile Device management tools or Microsoft Intune.
  - Local script: Use a local script

### Deploy the configuration package using Intune

To deploy the configuration package, first set up the service-to-service connection between Intune and Microsoft Defender for Endpoint.

1. Sign in to the Intune admin center Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Microsoft Defender for Endpoint** > **Open the Microsoft Defender Security Center**.

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

To view a list of onboarded devices, go to the newly created device configuration profile's page. To view this list, you need an Intune role that provides read permissions for the **Microsoft Defender Advanced Threat Protection**.

### Use local script to deploy configuration package

Follow the instructions in  [Onboard Windows 10 and Windows 11 devices using a local script](/purview/device-onboarding-script).

## View configuration status

1. Open the [Microsoft Purview compliance portal](https://compliance.microsoft.com) > **Settings** > **Device onboarding** > **Devices**.

2. Check the following columns:

  - **Configuration status**: Shows if the device is configured correctly.
  - **Policy sync status**: Shows if the device updated to the latest policy version. Devices must be on to update to the latest policy.

<!-- ########################## -->
## Next steps

For more information about Microsoft Purview, see [Learn about Microsoft Purview](/purview/purview).
