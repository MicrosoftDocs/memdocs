---
# required metadata
title: Set idle session time limits for Windows 365 Frontline Cloud PCs
titleSuffix:
description: Learn how to set idle session time limits for Windows 365 Frontline Cloud PCs
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/25/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: gkomatsu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Set idle session time limits for Windows 365 Frontline Cloud PCs

Windows 365 Frontline Cloud PCs remain active until:

- The user signs off from the Cloud PC through the start menu.
- The browser is closed (causing the Cloud PC to disconnect).
- The Cloud PC is inactive for two hours.

If a user forgets to disconnect, it might block others from their Frontline Cloud PCs if the max active session limit has been reached. To avoid this problem, you can create a configuration profile to enforce idle session time limits on all your Frontline Cloud PCs.

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration** (under **Manage devices**) > **Create** > **New policy**.
2. Under **Create a profile**, select the following options:

    - **Platform**: Windows 10 and later
    - **Profile type**: Settings catalog

3. Select **Create**.
4. On the **Basics** page, provide a name and optional description > **Next**.
5. On the **Configuration settings** page, select **Add settings**.
6. Under **Settings picker**, search for "session time limits".
7. Select the box for **Set time limit for active but idle Remote Desktop Services session**.
8. Under **Create profile**, expand **Administrative Templates** > enable **Set time limit for active but idle Remote Desktop Services sessions**.
9. For **Idle session limit: (Device)**, select a time limit that meets your company's compliance requirements. When a Frontline Cloud PC has been idle for this period of time, the Cloud PC is automatically disconnected.
10. Select **Next**.
12. On the **Scope tags** page, select the scope tags that you want > **Next**.
13. On the **Assignments** page, add the groups that you want to provide Frontline Cloud PCs > **Next**.
14. On the **Review + create** page, select **Create**.

<!-- ########################## -->
## Next steps

[Manage your Cloud PCs](device-management-overview.md).
