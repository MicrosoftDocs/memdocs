---
# required metadata

title: What happens to my data and access when my subscription ends?
description: Learn what happens to your data and access when your Windows 365 subscription ends.
keywords:
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/03/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: apineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# What happens to my data and access when my Windows 365 for business subscription ends?

If your subscription ends—either because it expires, or because you decide to upgrade or cancel it—your access to Windows 365 services and customer data go through multiple stages before the subscription is fully turned off, or *deleted*. If you're aware of this progression, you're better equipped to return your subscription to an active stage before it's too late, or, if you're leaving Windows 365, back up your data before it's ultimately deleted.

Read through this important information before you contact [Windows 365 support](/microsoft-365/admin/get-help-support).

> [!IMPORTANT]
> For some subscriptions, you can only cancel during a limited window of time after you buy or renew your subscription. If the cancellation window has passed, turn off recurring billing to cancel the subscription at the end of its term.
  
## What happens to data when a subscription expires?

When your subscription expires, it goes through the following stages: Expired > Disabled > Deleted. The Expired stage starts immediately after the subscription has reached its end date.

- **Annual subscriptions.** If you turn off recurring billing on an annual subscription, it goes through the same stages as an expired subscription. The first stage starts on the anniversary of the annual subscription, not the date that you turned off the subscription's recurring billing setting.
- **Monthly subscriptions.** If you cancel a monthly subscription, it immediately moves to the Disabled stage on the date you cancel it. In the Disabled stage, your users immediately lose access to the Windows 365 assets, and only admins have access to the data for the next 90 days.

The following table explains what you can expect when a paid Windows 365 subscription expires.

| Active | Expired <br/>(30 days\*) | Disabled <br/>(90 days\*) | Deleted |
|---|---|---|---|
| *Data accessible to all* | *Data accessible to all* | *Data accessible to admins only* | **Data deleted<br/>Azure Active Directory is removed, if not in use by other services** |
| User has normal access to Windows 365 Cloud PCs and its data. | User has normal access to Windows 365 Cloud PC and its data. Cloud PC is deprovisioned. | User can't access Windows 365 or its data. | Users can't access Windows 365 or its data |
| Admins have normal access to Windows 365 service and data | Admins can access the Windows 365 service and data. | Admins can't access the Windows 365 service. | Admins can access the admin center to buy and manage other subscriptions. |
| | Global or billing admins can reactivate the subscription. | Global or billing admins can reactivate the subscription. | |

*For most offers, in most countries and regions.
  
> [!NOTE]
>
> **What is "customer data"?** Customer data, as defined in the [Microsoft Online Service Terms](https://www.microsoft.com/en-us/licensing/product-licensing/products), refers to all data, including all text, sound, or image files that are provided to Microsoft by, or on behalf of, the customer through the customer's use of Windows 365 services. To learn more about the protection of customer data, see the [Get started with the Microsoft Service Trust Portal](/microsoft-365/compliance/get-started-with-service-trust-portal).

## What happens if I cancel a subscription?

If you cancel your subscription before its term end date, the subscription skips the Expired stage and moves directly into the Disabled stage, which is 90 days for most subscriptions, in most countries and regions. We recommend that you [back up your data](/microsoft-365/commerce/subscriptions/move-users-different-subscription) before canceling. As an admin, you can still access and back up data for your organization while it is in the Disabled stage. Any customer data that you leave behind might be deleted after 90 days and will be deleted no later than 180 days after cancellation.
  
If you're a partner who's an admin on behalf of (AOBO) a customer, and you've canceled a subscription, it can take up to 90 days for the admin center to reflect the status change.

> [!NOTE]
> If you want your subscription data to be deleted before the typical Disabled stage is over, you can [close your account](/microsoft-365/commerce/close-your-account).

Here's what to expect for you and your users if you cancel a subscription.
  
- **Admin access** Admins can still sign in and access the admin center, and buy other subscriptions as needed. As a global or billing admin, you have 90 days to [reactivate the subscription](/microsoft-365/commerce/subscriptions/reactivate-your-subscription) with all data intact.

- **User access** Users lose access to their Cloud PC which is deprovisioned right away. Data within the Cloud PC is deleted as well as [Unlicensed Product notifications](https://support.microsoft.com/office/0d23d3c0-c19c-4b2f-9845-5344fedc4380).

To learn how to cancel, see  !!!ABRAHAM is this  true for W365 Same process as for M365?!!! [Cancel your subscription](/microsoft-365/commerce/subscriptions/cancel-your-subscription).
  
> [!IMPORTANT]
> If you explicitly delete a subscription, it skips the Expired and Disabled stages and the SharePoint Online data and content, including OneDrive, is immediately deleted.

## What are my options if my subscription is about to expire?

While a subscription is active, you and your users have normal access to your data, the Windows 365 service, and users have access to their respective Cloud PCs. As the admin, you receive a series of notifications via email and in the admin center as your subscription nears its expiration date.
  
Before the subscription reaches its expiration date, you have a few options:
  
- **Enable recurring billing for the subscription.**
  - If **Recurring billing** is already turned on, you don't have to take any action. Your subscription is automatically billed, and you're charged for another year or month, depending on your current payment frequency. If for any reason you've turned **Recurring billing** off, you can always [turn Recurring billing back on](/microsoft-365/commerce/subscriptions/renew-your-subscription).
  - If you bought Windows 365 with a prepaid card, you can [turn on Recurring billing](/microsoft-365/commerce/subscriptions/renew-your-subscription) for your subscription.
  - If you're an Open Volume Licensing customer with a prepaid, one-year subscription, contact your partner to buy a new product key. You'll receive instructions via email to activate your key in the [Volume Licensing Service Center](https://go.microsoft.com/fwlink/p/?LinkID=282016). To learn how to find a new partner, or the partner you've worked with in the past, see [Find your partner or reseller](/microsoft-365/admin/manage/find-your-partner-or-reseller).
  - If you have Windows 365 Apps for business, see [Manage recurring billing for your subscription](/microsoft-365/commerce/subscriptions/renew-your-subscription).
- **Let the subscription expire.**
  - If you're paying by credit card or invoice and you don't want to continue your subscription, [turn off Recurring billing](/microsoft-365/commerce/subscriptions/renew-your-subscription). Your subscription ends on its expiration date, and you can ignore all related email notifications.
  - If you're an Open Volume Licensing customer working with a partner, you can let your subscription expire by taking no action.
  - If you're a Windows 365 Business customer, and you prepaid for your subscription and activated it with a product key, you can let your subscription expire by taking no action.
- **Cancel before the subscription expires.** For details, see [Cancel your subscription](/microsoft-365/commerce/subscriptions/cancel-your-subscription).

## What happens after my subscription expires?

If you let your subscription expire, it goes through multiple stages before it's ultimately deleted. These multiple stages give you time to reactivate if you want to continue the service, or to back up your data if you decide you no longer want the subscription.
  
Here's what you can expect when your subscription is in each stage.
  
### Stage: Expired

**What to expect:** The Expired stage lasts for 30 days for most subscriptions in most countries and regions. For Volume Licensing products, except for Microsoft Open, the Expired stage lasts 90 days.

In this stage, users have normal access to the Windows 365 service and any related applications.
  
As an admin, you still have access to the admin center. Don't worry—global or billing admins can [reactivate the subscription](/microsoft-365/commerce/subscriptions/reactivate-your-subscription) and continue using Windows 365. If you don't reactivate, [back up your data](/microsoft-365/commerce/subscriptions/move-users-different-subscription).
  
### Stage: Disabled

**What to expect:** If you don't reactivate your subscription while it is in the Expired stage, it moves into a Disabled stage. The Disabled stage lasts for 90 days for most subscriptions, in most countries and regions. For Volume Licensing products, the Disabled stage lasts 30 days.

In this stage, your access decreases significantly. Your users can't sign in or access their Windows 365 Cloud PCs. You can still sign in and get to the admin center, but can't assign licenses to users. Your customer data, including all user data, is available only to you and other admins.

As a global or billing admin, you can [reactivate the subscription](/microsoft-365/commerce/subscriptions/reactivate-your-subscription) and continue using Windows 365 with all of your customer data intact. If you choose not to reactivate, [back up your data](/microsoft-365/commerce/subscriptions/move-users-different-subscription).

### Stage: Deleted
  
**What to expect:** If you don't reactivate your subscription while it's expired or disabled, the subscription is deleted.
  
Admins and users no longer have access to the Windows 365 service. All customer data—from user data to documents and email—is permanently deleted and is unrecoverable.
  
At this point, you can't reactivate the subscription. However, as a global or billing admin, you can still access the admin center to manage other subscriptions, or to buy new subscriptions to meet your business needs.
  
> [!NOTE]
>
> - Adding a new subscription of the same type that was deleted doesn't restore the data that was associated with the deleted subscription.
> - If a Cloud Solution Provider (CSP) license is suspended, there's no 30-day Expired stage, and services are disabled immediately. Data is deleted after 90 days if the tenant isn't reactivated by adding a new license.

### What happens when my trial ends?

When your trial ends, you can't continue using Windows 365 for free. You have a few options:

- **Buy Windows 365.** When your trial expires, it moves into the Expired stage, which gives you another 30 days (for most trials, in most countries and regions) to buy a Windows 365 subscription. To learn how to convert your trial into a paid subscription, see [Buy a subscription from your free trial](/microsoft-365/commerce/try-or-buy-microsoft-365).
- **Extend your trial.** Need more time to evaluate Windows 365? In certain cases, you can [extend your trial](/microsoft-365/commerce/try-or-buy-microsoft-365).
- **Cancel the trial or let it expire.** If you decide not to buy Windows 365, you can let your trial expire or [cancel it](/microsoft-365/commerce/subscriptions/cancel-your-subscription). Back up any data that you want to keep. After the 30-day Expired stage ends, your trial account information and data are permanently deleted.

> [!NOTE]
>
> The information on this page is subject to the [Microsoft Policy Disclaimer and Change Notice](https://go.microsoft.com/fwlink/p/?LinkId=613651). Return to this site periodically to review any changes.

## Next steps

[Cancel your subscription](/microsoft-365/commerce/subscriptions/cancel-your-subscription) (article)\
[Renew Windows 365 for business](/microsoft-365/commerce/subscriptions/renew-your-subscription) (article)\
[Reactivate your subscription](/microsoft-365/commerce/subscriptions/reactivate-your-subscription) (article)
