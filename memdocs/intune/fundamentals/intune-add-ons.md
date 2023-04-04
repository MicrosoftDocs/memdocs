---
# required metadata

title: Use Intune Suite add-on capabilities
titleSuffix: Microsoft Intune
description: Microsoft Intune Suite unifies a series of mission-critical advanced endpoint management and security capabilities. The capabilities of the suite are integrated with Microsoft 365 and Microsoft Security across endpoint platforms for both cloud and on-premises co-managed devices.  
keywords:
author: smritib17 
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/18/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- M365-identity-device-management
- highpri
- tier1
---

# Use Intune Suite add-on capabilities

Microsoft Intune Suite provides mission-critical advanced endpoint management and security capabilities into Microsoft Intune. You can find add-ons to Intune in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Tenant administration** > **Intune add-ons**. The **Summary** blade shows all available Intune add-ons, a short description, and the status of the add-on. Each add-on shows a status of either **Active** or **Available for trial or purchase**.

Licenses for the Intune add-ons can be added for an additional cost to the licensing options that include Microsoft Intune or Microsoft Configuration Manager. For more information, see [Licenses available for Microsoft Intune](licenses.md).

> [!NOTE]
> Intune add-ons are currently not supported in Sovereign clouds.

## Available add-ons

Some capabilities are available to buy as a standalone add-on. Other capabilities are only available with Intune Plan 2 or the Intune Suite.

- **Standalone add-ons**: Some add-on capabilities, such as Remote Help, are available as a Standalone add-on.
- **Microsoft Intune Plan 2**: Offers advanced endpoint management capabilities, including management and configuration of specialty devices and Microsoft Tunnel for Mobile Application Management.
- **Microsoft Intune Suite**: Unifies a series of mission-critical advanced endpoint management and security capabilities. The capabilities of the suite are integrated with Microsoft 365 and Microsoft Security across endpoint platforms for both cloud and on-premises co-managed devices. The Intune Suite includes Remote Help (standalone) and all capabilities that come with Intune Plan 2.

The following table provides a list of add-on capabilities and associated Intune Plans. For information about Microsoft Intune Plans and pricing, see [Intune Plans and pricing](https://aka.ms/IntuneSuitePricing).

|Capability|Standalone add-on|Intune Plan 2|Intune Suite|
|:---|:---:|:---:|:---:|
|Advanced endpoint analytics| | |✔️|
|Endpoint Privilege Management |✔️| |✔️|
|Microsoft Tunnel for Mobile Application Management| |✔️|✔️|
|Remote help|✔️| |✔️|
|Specialized devices management| |✔️|✔️|

<!-- original sequence >
|Remote help|✔️| |✔️|
|Microsoft Tunnel for Mobile Application Management| |✔️|✔️|
|Specialized devices management| |✔️|✔️|
|Advanced endpoint analytics| | |✔️|
-->

### Advanced endpoint analytics

Microsoft Intune advanced Endpoint analytics is set of analytics-driven capabilities that help IT admins understand, anticipate, and improve the end-user experience.

For more information, see [Advanced endpoint analytics](../../analytics/advanced-endpoint-analytics.md).

### Endpoint Privilege Management

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

For more information, see [Endpoint Privilege Management](../protect/epm-overview.md).

### Microsoft Tunnel for Mobile Application Management

When you use the Microsoft Tunnel VPN Gateway, you can extend Tunnel support by adding Tunnel for Mobile Application Management (MAM). Tunnel MAM extends the Microsoft Tunnel VPN gateway to support devices that run Android or iOS, and that aren't enrolled with Microsoft Intune.

For more information, see [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md).

### Remote Help

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. For more information, see [Remote Help](../fundamentals/remote-help.md).

### Managing Specialty devices with Microsoft Intune

Specialized devices management is a set of device management, configuration, and protection capabilities for special, purpose-built devices such as AR/VR headsets, large smart-screen devices, and conference room meeting devices.

For more information, see [Managing specialized devices with Microsoft Intune](specialty-devices-with-intune.md).

## Try or buy Intune add-ons

Global and Billing administrators can choose to start free trials or purchase licenses for Intune add-ons through the [Microsoft 365 admin center](https://admin.microsoft.com). Administrators who aren't Global or Billing administrators can still see the status of their tenant's Intune add-ons trial or active licenses in the centralized Intune add-on page in the Intune admin center. However, they can't start a free trial or purchase licenses.

Starting a free trial gives you a 90-day period to use the Intune add-on capability without any charge. Trials can be up to 250 users per tenant. At the end of the trial period, there's a 30-day grace period. After this point, you'll be unable to use the Intune add-on capability in Microsoft Intune for users within your tenant unless you've purchased the appropriate licenses. There's a one-time limit to start a trial for each tenant.  

Purchasing licenses lets you use the Intune add-on capability in your tenant for the duration in which the licenses are active on your tenant based on the option selected during the Billing process.

Intune add-on capabilities are disabled in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) unless you are in the free trial period or have purchased licenses.

### How to start a trial through the Microsoft 365 admin center

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global or Billing administrator.
1. Navigate to **Tenant administration** > **Intune add-ons**.
1. Find the Intune add-on to start a trial. For add-ons that say **Available for trial or purchase** in their status, you don't have a free trial started or any licenses purchased for those add-ons.
1. Click **View details** to see the details.
1. Click the **To try or buy, go to Purchase services** link to navigate to the Microsoft 365 admin center. A new tab opens on the **Product details** page for the selected Intune add-on.
1. In the Microsoft 365 Admin Center, follow the prompts to **Start free trial** and confirm your order.
1. Navigate to **Tenant administration** > **Intune add-ons** and see that the Intune add-on capability you added is now **Active**.

### How to purchase Intune add-ons

Licenses for Intune add-ons can be purchased just as you would purchase Intune Plan 1 licenses through the following ways:

- Web direct purchase in the Microsoft 365 Admin Center
- Microsoft Volume License Servicing Center (VLSC)
- Existing relationships with Microsoft partners/resellers

After you buy licenses via any source, the licenses are available in your tenant and the status of the Intune add-ons capability will update accordingly.

## How to assign licenses

For information on how to assign licenses in the Microsoft Intune admin center, see [Assign Microsoft Intune licenses](licenses-assign.md).

## Monitor license use

Each of the Intune add-ons have their own requirements for how many licenses need to be purchased.

## Next steps

Learn more about:

- [Advanced endpoint analytics](../../analytics/overview.md)
- [Endpoint Privilege Management](../protect/epm-overview.md).
- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [Remote Help](..\fundamentals\remote-help.md)
- [Managing specialized devices with Microsoft Intune](specialty-devices-with-intune.md)