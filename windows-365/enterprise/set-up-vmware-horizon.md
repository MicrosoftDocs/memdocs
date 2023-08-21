---
# required metadata
title: Set up VMware Horizon for Windows 365 Enterprise
titleSuffix:
description: Learn about using VMware Horizon with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/21/2023
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
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

# Set up VMware Horizon for Windows 365 Enterprise

VMware Horizon is a cloud-based service that lets you deliver Windows 365 Enterprise desktops to your users from any device and location. With VMware Horizon, you can use the power and security of Windows 365 Enterprise, while simplifying the management and deployment of your virtual desktop infrastructure (VDI).

VMware Horizon for Windows 365 Enterprise is in limited [public preview](..\public-preview.md). To submit a request to join this preview, see [Tech Preview – VMware Horizon extending Microsoft Windows 365](https://www.vmware.com/learn/1733900_REG.html).

## Set up overview

To set up VMware Horizon for Windows 365 Enterprise, follow these steps. The first two steps are explained here at learn.microsoft.com. The remaining steps are explained on the VMware web site.

1. [Fulfill requirements](requirements-vmware-horizon.md).
2. [Turn on the Windows 365 VMware connector in Intune](#turn-on-the-windows-365-vmware-connector-in-intune).
3. [Sign up for the Tech Preview – VMware Horizon extending Microsoft Windows 365](https://www.vmware.com/learn/1733900_REG.html).
4. [Configure your Horizon Cloud Service Tenant](https://go.microsoft.com/fwlink/?linkid=2242843).
5. [Configure identity provider](https://go.microsoft.com/fwlink/?linkid=2242843).
6. [Connect Horizon Cloud Service with Windows 365](https://go.microsoft.com/fwlink/?linkid=2242843).
7. [Assign VMware licenses to Azure Active Directory users or groups](https://go.microsoft.com/fwlink/?linkid=2242843).

### Turn on the Windows 365 VMware connector in Intune

To turn on the VMware connector, follow these steps:

1. As a Global administrator, sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Connectors and tokens**.
![Screenshot of navigating to Connectors and tokens.](./media/set-up-citrix/connectors-tokens.png)
2. Select **Windows partner connectors** > **Add**.
3. Under **Add connector**, select **VMware (preview)** in the drop-down list.
4. Next to **Allow people to use VMware to connect to their Cloud PCs**, set the toggle to **On** > **Add**.

## Public preview limitations

During the [public preview](..\public-preview.md), the following limitations exist:

- Only the Horizon Cloud Service web access client and native Windows client is available.
- Only one Cloud PC per user is supported.
- Microsoft Frontline licenses aren't supported.
- VMware UAG as a Service has reduced capabilities from its standalone customer managed counterpart.
  - Users with interrupted sessions must manually reconnect.
  - Only TCP streaming protocol is supported.

<!-- ########################## -->
## Next steps

Proceed to the VMware Horizon Cloud to complete the integration. For more information about VMware Horizon set up, see [Setting up VMware Horizon Cloud for Windows 365 integration](https://go.microsoft.com/fwlink/?linkid=2242843).
