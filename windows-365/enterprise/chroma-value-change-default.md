---
# required metadata
title: Configure the default chroma value for Windows 365 Cloud PCs
titleSuffix:
description: Learn how to configure the default chroma value for Windows 365 Cloud PCs
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/10/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jordanm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Change the default chroma value for Windows 365 Cloud PCs

The chroma value determines the color space used for encoding. By default, the chroma value is set to 4:2:0 for Windows 365 Cloud PCs. This value provides a good balance between image quality and network bandwidth. You can increase the default chroma value to 4:4:4 to improve image quality. You don't need to use GPU acceleration to change the default chroma value.

## Requirements

- Microsoft Entra ID account that is assigned the [Policy and Profile manager](/mem/intune-service/fundamentals/role-based-access-control-reference#policy-and-profile-manager) built-in RBAC role.
- A group containing the devices you want to configure.

## Increase the default chroma value to 4:4:4

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. [Create or edit a configuration profile](/mem/intune-service/configuration/administrative-templates-windows) for **Windows 10 and later** devices, with the **Settings catalog** profile type.

3. In the settings picker, browse to **Administrative templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Remote Session Environment**.

4. Check the box for the following settings, then close the settings picker:

   - **Prioritize H.264/AVC 444 Graphics mode for Remote Desktop connections**

   - **Configure image quality for RemoteFX Adaptive Graphics**

5. Expand the **Administrative templates** category, then set each setting as follows:

   - Set toggle the switch for **Prioritize H.264/AVC 444 Graphics mode for Remote Desktop connections** to **Enabled**.

   - Set toggle the switch for **Configure image quality for RemoteFX Adaptive Graphics** to **Enabled**, then for **Image quality: (Device)**, select **High**.

6. Select **Next**.

7. *Optional*: On the **Scope tags** tab, select a scope tag to filter the profile. For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](/mem/intune-service/fundamentals/scope-tags).

8. On the **Assignments** tab, select the group containing the computers providing a remote session you want to configure, then select **Next**.

9. On the **Review + create** tab, review the settings, then select **Create**.

10. Once the policy applies to the computers providing a remote session, restart them for the settings to take effect.

<!-- ########################## -->
## Next steps

[Manage your Windows 365 Cloud PCs](device-management-overview.md)
