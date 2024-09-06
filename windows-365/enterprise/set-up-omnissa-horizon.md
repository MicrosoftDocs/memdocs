---
# required metadata
title: Set up Omnissa Horizon for Windows 365 Enterprise
titleSuffix:
description: Learn about using Omnissa Horizon with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/21/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aradinger    
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Set up Omnissa Horizon for Windows 365 Enterprise

Omnissa Horizon is a cloud-based service that lets you deliver Windows 365 Enterprise desktops to your users from any device and location. With Omnissa Horizon, you can use the power and security of Windows 365 Enterprise, while simplifying the management and deployment of your virtual desktop infrastructure (VDI).

## Set up overview

To set up Omnissa Horizon for Windows 365 Enterprise, follow these steps. The first two steps are explained here at learn.microsoft.com. The remaining steps are explained on the Omnissa web site.

1. [Fulfill requirements](requirements-omnissa-horizon.md).
2. [Turn on the Windows 365 Omnissa connector in Intune](#turn-on-the-windows-365-omnissa-connector-in-intune).
3. [Configure your Horizon Cloud Service Tenant](https://go.microsoft.com/fwlink/?linkid=2242843).
4. [Configure identity provider](https://go.microsoft.com/fwlink/?linkid=2242843).
5. [Connect Horizon Cloud Service with Windows 365](https://go.microsoft.com/fwlink/?linkid=2242843).
6. [Assign Omnissa licenses to Microsoft Entra users or groups](https://go.microsoft.com/fwlink/?linkid=2242843).

### Turn on the Windows 365 Omnissa connector in Intune

To turn on the Omnissa connector, follow these steps:

1. As an Intune administrator, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Connectors and tokens**.
![Screenshot of navigating to Connectors and tokens.](./media/set-up-citrix/connectors-tokens.png)
2. Select **Windows partner connectors** > **Add**.
3. Under **Add connector**, select **Omnissa** in the drop-down list.
4. Next to **Allow people to use Omnissa to connect to their Cloud PCs**, set the toggle to **On** > **Add**.

<!-- ########################## -->
## Next steps

To complete the integration, proceed to the Omnissa Horizon Cloud. For more information about Omnissa Horizon set up, see [Setting up Omnissa Horizon Cloud for Windows 365 integration](https://go.microsoft.com/fwlink/?linkid=2242843).
