---
# required metadata

title: Premium add-ons for Microsoft Intune
titleSuffix: Microsoft Intune
description: When you purchase licenses for Premium add-ons for Microsoft Intune, you expand the capabilities for device management with Microsoft Endpoint Manager.  
keywords:
author: smbhardwaj 
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/05/2022
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
---

# Use Premium add-ons capabilities with Intune

Microsoft Endpoint Manager now offers Premium add-ons. You can find premium add-ons in Intune under **Tenant administration** > **Premium add-ons**. The **Summary** blade shows all premium add-ons that have been released, a short description, and the status of the add-on. You can view the status of each add-on as either **Active** or **Available for trial or purchase**. 

Licenses for the Premium add-ons can be added for an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.

Global and Billing administrators can use the **Premium add-ons** page from the [Microsoft 365 admin center](https://admin.microsoft.com) to start a free trial or purchase licenses for each Premium add-on. 
## What add-ons capabilities are available 

The following Premium add-ons are available: 

- [Remote help](..\remote-actions\remote-help.md)

## What happens when you try/buy the Premium add-ons capability 

Global and Billing administrators can choose to start free trials or purchase licenses for Premium add-ons through the [Microsoft 365 admin center](https://admin.microsoft.com).  
 
Starting a free trial gives you a 90-day period to use the Premium add-on capability without any charge. Trials can be up to 250 users per tenant. At the end of the trial period, there's a 30-day grace period. After this point, you'll be unable to use the Premium add-on capability in Endpoint Manager for users within your tenant unless you've purchased the appropriate licenses. There's a one-time limit to start a trial for each tenant.  
 
Purchasing licenses lets you use the Premium add-on capability in your tenant for the duration in which the licenses are active on your tenant based on the option selected during the Billing process. 

## How to try or buy the premium add-ons capability 

Premium add-on capabilities are disabled in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) unless you are in the free trial period or have purchased licenses. Global and Billing administrators can choose to start a free trial or purchase licenses for Premium add-ons through the [Microsoft 365 admin center](https://admin.microsoft.com). 

Administrators who aren't Global or Billing administrators can still see the status of their tenant's Premium add-ons trial or active licenses in the centralized Premium add-on page in Endpoint Manager (but can't start a free trial or purchase licenses).  

### How to start a trial through the Microsoft 365 admin center 

1. Navigate to **Tenant administration** > **Premium add-ons** as a Global or Billing administrator.
2. Find the Premium add-on to start a trial. For add-ons that say **Available for trial or purchase** in their status, you don't have a free trial started or any licenses purchased for those add-ons.
3. Click **View details** and see the details. :::image type="content" source="./media/premium-add-ons/remote-help-details.png" alt-text="Remote help details.":::
4. Click the **To try or buy, go to Purchase services** link to navigate to the Microsoft 365 Admin Center. A new tab opens on the **Product details** page for the relevant Premium add-on. *Screenshot will be added here.* 
5. In the Microsoft 365 Admin Center, follow the prompts to **Start free trial** and confirm your order. *Screenshot will be added here.* 
6. Navigate to **Tenant administration** > **Premium add-ons** and see that the Premium add-on capability you added is now **Active**.

### How to purchase premium add-ons

Licenses for Premium add-ons can be purchased just as you would purchase Intune licenses,  through a web direct purchase in the Microsoft 365 Admin Center, Microsoft Volume License Servicing Center (VLSC) or through your existing relationships with Microsoft partners/resellers. 
After you buy licenses via any source, the licenses are available in your Tenant and the status of the Premium add-ons capability will update accordingly. 

## How to assign licenses 

For information on how to assign licenses in Microsoft Endpoint Manager admin center, see [Assign Microsoft Intune licenses](licenses-assign.md)

## Monitor license use 

Each of the Premium add-ons might have their own requirements for how many licenses need to be purchased.

- [Remote help](..\remote-actions\remote-help.md)

## Next steps

Learn about [Remote help](..\remote-actions\remote-help.md). 
