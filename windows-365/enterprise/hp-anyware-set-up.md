---
# required metadata
title: Set up HP Anyware for Windows 365 Enterprise
titleSuffix:
description: Learn about using HP Anyware with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/10/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elaineyou    
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Set up HP Anyware for Windows 365 Enterprise (preview)

HP Anyware for Windows 365 is a cloud-based service that lets you deliver Windows 365 Enterprise desktops on HP Anyware’s management and PCoIP protocol. HP Anyware's infrastructure and protocol excel in low bandwidth environments and intensive workloads.

HP Anyware for Windows 365 is in [public preview](../public-preview.md) in selected regions. To submit a request to join this preview, see [https://aka.ms/HPAnywarePublicPreviewSignUp](https://aka.ms/HPAnywarePublicPreviewSignUp).

## Set up overview

To set up HP Anyware for Windows 365 Enterprise, follow these steps. The first two steps are explained here at learn.microsoft.com. The remaining steps are explained on the HP Anyware web site.

1. [Fulfill requirements](hp-anyware-requirements.md).
2. [Turn on the Windows 365 HP Anyware connector in Intune](#turn-on-the-windows-365-hp-anyware-connector-in-intune).
3. [Sign up for the Preview – HP Anyware for Windows 365](https://aka.ms/HPAnywarePublicPreviewSignUp).
4. [Connect Microsoft Entra ID to HP Anyware](https://aka.ms/HPAnywareDocConnectEntraIDtoHP).
5. [Assign HP Anyware licenses to users and provision Cloud PCs](https://aka.ms/HPAnywareDocAssignHPLic).

### Turn on the Windows 365 HP Anyware connector in Intune

To turn on the HP Anyware connector, follow these steps:

1. As a Intune Administrator, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Connectors and tokens**.

   ![Screenshot of navigating to Connectors and tokens](./media/set-up-citrix/connectors-tokens.png)

2. Select **Windows Windows partner connectors** > **Add**.
3. Under **Add connector**, select **HP Anyware (preview)** in the drop-down list.
4. Next to **Allow people to use HP Anyware to connect to their Cloud PCs**, set the toggle to **On** > **Add**.

## Public preview limitations

During the public preview, the following limitations exist:

- The initial release supports selected regions.
- Windows 365 Frontline isn't supported.
- Nested groups aren't supported.

<!-- ########################## -->
## Next steps

To complete the integration, proceed to the HP Anyare Manager. For more information about HP Anyware set up, see [https://aka.ms/HPAnywareDocConnectEntraIDtoHP](https://aka.ms/HPAnywareDocConnectEntraIDtoHP).
