---
# required metadata

title: Intune add-ons for Microsoft Intune
titleSuffix: Microsoft Intune
description: When you purchase licenses for Intune add-ons for Microsoft Intune, you expand the capabilities for device management with Microsoft Endpoint Manager.  
keywords:
author: smritib17 
ms.author: smbhardwaj
manager: dougeby
ms.date: 05/03/2022
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
- tier1
- M365-identity-device-management 
- highpri
---

# Use Intune add-ons capabilities with Intune

Microsoft Endpoint Manager now offers Intune add-ons. You can find Intune add-ons in Intune under **Tenant administration** > **Intune add-ons**. The **Summary** blade shows all Intune add-ons that have been released, a short description, and the status of the add-on. You can view the status of each add-on as either **Active** or **Available for trial or purchase**. 

Licenses for the Intune add-ons can be added for an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.

> [!NOTE]
> Intune add-ons are currently not supported in Sovereign clouds.

## What add-ons capabilities are available


| Add-ons              | Intune Suite | Plan 2 | Stand-alone  |
|--|--|--|--|
| Remote Help | ![Supported](./media/certificates-configure/green-check.png) |  | ![Supported](./media/certificates-configure/green-check.png)|
| Microsoft Tunnel for Mobile Application Management  | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) |  |
| Support for specialty devices  | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | |
| Advanced features for Endpoint Analytics  | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | |
| Privilege Management | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png) | |

The following Intune add-ons are available:

### Remote Help 

Remote Help is an Intune add-on application that works with Intune and enables your information and front-line workers to get assistance when needed over a remote connection. With this connection, your support staff can remote connect to the user's device. 

During the session, they can view the device's display and if permitted by the device user, take full control. Full control enables a helper to directly make configurations or take actions on the device. 

For more information, go to [Remote Help](..\remote-actions\remote-help.md)

### Microsoft Tunnel for Mobile Application Management 

When you use the Microsoft Tunnel VPN Gateway, you can extend Tunnel support by adding Tunnel for Mobile Application Management (MAM). Tunnel MAM extends the Microsoft Tunnel VPN gateway to support devices that run Android or iOS, and that aren't enrolled with Microsoft Intune. 

With this solution, your users can use a single device that hasn't enrolled with Intune to gain secure access to the organizations on-premises apps and resources using modern authentication, Single Sign On and conditional access. 

With Tunnel for MAM, your users can use their own device (BYOD) for both work and personal use, without having to grant the organization’s IT department control over that device.

For more information, go to [Microsoft Tunnel for Mobile Application Management](..\protect\microsoft-tunnel-mam.md)

### Managing Specialty devices with Microsoft Intune

A device managed by Microsoft Intune is classified as a specialized device if it meets certain requirements. The ability to manage specialty devices in Intune will require additional licensing with Microsoft Intune add-ons. 

For more information on specialty devices, go to [Specialty devices](specialty-devices-with-intune.md) 


## What happens when you try/buy the Intune add-ons capability 

Global and Billing administrators can choose to start free trials or purchase licenses for Intune add-ons through the [Microsoft 365 admin center](https://admin.microsoft.com).  
 
Starting a free trial gives you a 90-day period to use the Intune add-on capability without any charge. Trials can be up to 250 users per tenant. At the end of the trial period, there's a 30-day grace period. After this point, you'll be unable to use the Intune add-on capability in Endpoint Manager for users within your tenant unless you've purchased the appropriate licenses. There's a one-time limit to start a trial for each tenant.  
 
Purchasing licenses lets you use the Intune add-on capability in your tenant for the duration in which the licenses are active on your tenant based on the option selected during the Billing process. 

## How to try or buy the Intune add-ons capability 

Intune add-on capabilities are disabled in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) unless you are in the free trial period or have purchased licenses. Global and Billing administrators can choose to start a free trial or purchase licenses for Intune add-ons through the [Microsoft 365 admin center](https://admin.microsoft.com). 

Administrators who aren't Global or Billing administrators can still see the status of their tenant's Intune add-ons trial or active licenses in the centralized Intune add-on page in Endpoint Manager (but can't start a free trial or purchase licenses).  

### How to start a trial through the Microsoft 365 admin center

1. Navigate to **Tenant administration** > **Intune add-ons** as a Global or Billing administrator.
2. Find the Intune add-on to start a trial. For add-ons that say **Available for trial or purchase** in their status, you don't have a free trial started or any licenses purchased for those add-ons.
3. Click **View details** to see the details. For example, this screenshot shows details for Remote Help add-on. :::image type="content" source="./media/premium-add-ons/remote-help-details.png" alt-text="Remote Help details.":::
4. Click the **To try or buy, go to Purchase services** link to navigate to the Microsoft 365 Admin Center. A new tab opens on the **Product details** page for the selected Intune add-on. For example, this screenshot shows the Product details tab for Remote help add-on. :::image type="content" source="./media/premium-add-ons/remote-help-product-details.png" alt-text="A screenshot of Remote Help add-on details."::: 
5. In the Microsoft 365 Admin Center, follow the prompts to **Start free trial** and confirm your order. :::image type="content" source="./media/premium-add-ons/confirm-order.png" alt-text="Confirm order."::: 
6. Navigate to **Tenant administration** > **Intune add-ons** and see that the Intune add-on capability you added is now **Active**.

### How to purchase Intune add-ons

Licenses for Intune add-ons can be purchased just as you would purchase Intune licenses through the following ways:
   
- web direct purchase in the Microsoft 365 Admin Center
- Microsoft Volume License Servicing Center (VLSC) 
- existing relationships with Microsoft partners/resellers
 
After you buy licenses via any source, the licenses are available in your Tenant and the status of the Intune add-ons capability will update accordingly. 

## How to assign licenses 

For information on how to assign licenses in Microsoft Endpoint Manager admin center, see [Assign Microsoft Intune licenses](licenses-assign.md)

## Monitor license use 

Each of the Intune add-ons might have their own requirements for how many licenses need to be purchased.

- [Remote Help](..\remote-actions\remote-help.md)

## Next steps

Learn about [Remote Help](..\remote-actions\remote-help.md). 
