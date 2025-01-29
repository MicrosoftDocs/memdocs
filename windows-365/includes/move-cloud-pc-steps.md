---
title: include file
description: include file
author: ErikjeMS  
ms.service: windows-365
ms.topic: include
ms.date: 12/06/2024
ms.author: erikje
ms.custom: include file
---

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Provisioning**) > **Provisioning policies** > select a policy.
2. Under **General**, select **Edit**.
3. Under **Join type details**, make changes depending on the original type:
  
    - For **Hybrid Microsoft Entra Join**, change the ANC\*.
    - For **Microsoft Entra Join**:

      - You can change **Network** type from ANC to Microsoft hosted network, or vice versa.
      - If a **Microsoft hosted network** is used, change the **Geography** and/or **Region**.
      - If an **Azure network connection** is used, change the ANC\*.

4. Select **Next** > **Update**.
5. When ready to move the existing Cloud PCs, select **Apply this configuration**.
