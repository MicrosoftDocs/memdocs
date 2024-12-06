---
title: Get started with Windows 365 Business and Cloud PCs
description: Learn about getting started with Windows 365 Business.
f1.keywords:
- NOCSH
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 03/27/2024
audience: Admin
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-business
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
- essentials-get-started
---

# Get started with Windows 365 Business and Cloud PCs

This article is for people who plan to buy and set up Windows 365 Business for their organization.
  
[Windows 365 Business](https://www.microsoft.com/windows-365/business) is a version of Windows 365 that is made specifically for use in smaller companies (up to 300 seats). It gives organizations an easy, streamlined way of providing Cloud PCs to their users.  With Windows 365 Cloud PCs, you can stream your apps, data, content, settings, and storage from the Microsoft cloud.

> [!NOTE]  
> Before starting, make sure that your [Microsoft Entra device settings](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) for **Users may join devices to Azure AD** are set to **All**.

   ![Screenshot of Users may join devices to Microsoft Entra settings.](./media/get-started-windows-365-business/azure-device-settings.png)

## Prerequisites

There are no licensing prerequisites to set up Windows 365 Business.

For the best onboarding experience, refer to the [setup troubleshooting guide](troubleshoot-windows-365-business.md). This article can help make sure you optimize your environment preferences for Windows 365 Business. For example, the guide can help you if you're using multi-factor authentication, Conditional Access policies, or Intune in your environment.

## Buy subscriptions

There are two different ways in which you can buy Windows 365 Business subscriptions for your users:

- The [Windows 365 products site](https://www.microsoft.com/windows-365/business/compare-plans-pricing)
- Microsoft 365 admin center

After you buy a subscription, you can use the Microsoft 365 admin center to assign licenses to users in your organization.

### Buy subscriptions through the Windows 365 products site

If you don't already have a Microsoft 365 subscription, you can buy your Windows 365 Business subscriptions on the [Windows 365 products site](https://www.microsoft.com/windows-365/business/compare-plans-pricing). Use the following steps to buy a Windows 365 Business subscription through the Windows 365 products page.

1. On the [Windows 365 Business](https://www.microsoft.com/windows-365/business) page, select **See plans and pricing**.
2. On the next page, select the subscription you want to purchase, and then select **Buy now**.
3. Follow the steps to set up your account.
4. After confirming, if you're ready to assign licenses to users, select **Get started** to go to your [Windows 365 home page](https://windows365.microsoft.com).
5. On the Windows 365 home page, in the **Quick actions** section, select **Manage your organization**. This link takes you to the Microsoft 365 admin center where you can assign licenses to users.

> [!NOTE]
> Self-service purchase isn’t available in India or for government or education customers.

To learn more about self-service purchase, see the [Self-service purchase FAQ](/microsoft-365/commerce/subscriptions/self-service-purchase-faq).

### Buy a subscription through the Microsoft admin center

You can use the Microsoft 365 admin center to buy a Windows 365 Business subscription for your organization if you:

- Have a Microsoft 365 tenant.
- Are a Global or Billing admin.

If you meet both these requirements, follow these steps:

1. In the Microsoft admin center, go to the **Billing > Purchase services** page.
2. On the **Purchase services** page, search for **Windows 365 Business**. When you find it, select **Details**.
3. On the **Windows 365 Business** page, in the **Processor/Ram/Storage Options** section, use the **Select a subscription** menu to select a subscription for your users based on their CPU, RAM, and storage needs. See [Windows 365 Business sizing options](windows-365-business-sizing.md) for guidance on selecting the subscription that best fits your users' needs.
4. On the **Checkout** page, enter the number of subscriptions you want to buy, as well and your payment information. Then select **Place Order**.
5. The **You're all set!** page appears confirming your purchase.

## Assign licenses to users

Whether you purchased your subscriptions through the Windows 365 products site, or through the Microsoft 365 admin center, you can assign licenses to users through either:

- The **Billing** page in the Microsoft 365 admin center. For more information, see [assign licenses to users](/microsoft-365/admin/manage/assign-licenses-to-users).
- [windows365.microsoft.com](https://windows365.microsoft.com). For more information, see [Assign or unassign a license](assign-unassign-license.md).

As soon as you assign a license to a user, Windows 365 will create a Cloud PC for that user. This process can take up to 30 minutes.

You can assign different Windows 365 Business license types to a user, based on the users business need. See [Windows 365 Business sizing options](windows-365-business-sizing.md)  for guidance on which license type might be suitable for your users.

## How to get help

If you need to get help while setting up Windows 365 Business in the Microsoft 365 admin center, see [Get help or support](/microsoft-365/business-video/get-help-support).

## Next steps

[Get users started on their Cloud PCs](../end-user-access-cloud-pc.md)

[Manage your Cloud PCs](device-management.md)

[Windows 365 Business](https://www.microsoft.com/windows-365/business)

[Windows 365 Business sizing options](windows-365-business-sizing.md)

[Windows 365 Business plan comparison](https://www.microsoft.com/windows-365/business/compare-plans-pricing)

[Remote Desktop client app comparison](/windows-server/remote/remote-desktop-services/clients/remote-desktop-app-compare)

[Set up Microsoft Teams in your small business](/microsoftteams/deploy-small-business)
