---
title: Configure Apple account service access
description: Use Apple access management settings to control how Apple accounts are used on organization‑owned devices managed by Microsoft Intune.  
ms.date: 03/16/2026  
ms.topic: how-to
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
- highpri
---

# Configure service access for Apple accounts

You can use Apple access management settings in Apple Business or Apple School Manager to control how Apple accounts are used on organization-owned devices. These settings define which devices users can sign in to with Apple accounts and which Apple apps and services are available.   

## Prerequisites  

To configure service access for Apple accounts, ensure your environment meets the following prerequisites:  

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)] 

:::column-end:::
:::column span="3":::  
> Configurations apply to the following platforms:
>
> - iOS/iPadOS  
> - macOS  
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::  
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]  
:::column-end:::
:::column span="3":::

> You must have sufficient permissions in Apple Business or Apple School Manager to manage Apple account service access. For current role requirements, see [Customize user access to apps and services using Apple Business](https://support.apple.com/guide/apple-business-manager/customize-user-access-to-apps-and-services-axm53xk34bq/web)(opens Apple support site).  

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::  
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]  

:::column-end:::  
:::column span="3":::  
> Devices must meet the following requirements:  
>
> - Owned by the organization in Apple Business.  
> - Enrolled in Microsoft Intune through automated device enrollment (ADE).  
> - Run a supported operating system version:
>   - iOS/iPadOS 17 or later  
>   - macOS 14 or later 
:::column-end:::
:::row-end:::

> [!IMPORTANT] 
> These settings apply to all Apple accounts regardless of whether a sign in is actively happening. If the setting is changed and the device doesn't meet the requirement, the account is automatically signed out.  

## Configure service access   

Service access settings are configured in Apple Business or Apple School Manager. Microsoft Intune doesn’t configure these settings directly. Instead, Intune issues a management token that Apple uses during device activation to confirm the device’s Intune assignment.  

### Available settings  

In Apple Business or Apple School Manager, you can configure settings that control:

- Which devices users can sign in to with Apple accounts, such as:
  - Any device
  - Managed devices only
  - Supervised devices only
- Whether users can sign in to organization-owned devices using:
  - Managed Apple accounts only
  - Any Apple account
- Which Apple apps and services are available to users, such as:
   - iCloud services 
   - Collaboration and communication services  

> [!NOTE]
> For devices enrolled through automated device enrollment (ADE), the **Managed devices only** and **Supervised devices only** options behave the same. ADE devices are both managed and supervised by default.  

These controls apply to organization-owned devices and are defined by Apple as part of their access management model. For detailed instructions and descriptions of available settings, see [Service access with Managed Apple Accounts](https://support.apple.com/guide/apple-business-manager/service-access-with-managed-apple-accounts-axm171b3ee95/web)(opens Apple support site).    

### How service access enforcement works   

Service access for Apple accounts is defined and enforced across Apple and Microsoft Intune as follows:  

1. An administrator configures service access settings for Managed Apple Accounts in Apple Business or Apple School Manager. These settings define which devices users can sign in to and which Apple apps and services are available.  
1. Devices are enrolled in Microsoft Intune through automated device enrollment.  
1. When a user signs in with a managed Apple account on an enrolled device, Apple validates whether the device meets the configured service access requirements.  
1. Microsoft Intune enforces the service access requirements on enrolled devices during device check-in and Apple account sign-in.
1. If a device no longer meets the configured requirements, Apple automatically signs the user out of affected Apple services.  

These controls help ensure that managed Apple accounts are used only on devices that meet your organization’s access requirements.  

### What it doesn’t do  

Configuring service access for Apple accounts doesn’t change how devices enroll in Microsoft Intune. Specifically, this configuration- 

- Doesn’t configure enrollment settings in the Intune admin center. Service access is configured in Apple Business or Apple School Manager, not in Intune.

- Doesn’t replace device enrollment. Devices must still be enrolled in Intune using an Apple-supported enrollment method that results in a managed (or supervised) device.  

- Doesn't determine whether a device is marked as corporate or personal in Intune. Device ownership is determined by the enrollment method and corporate identifiers.  

- Doesn’t provide per-service configuration controls in Intune. Apple defines which apps and services (such as iCloud features, FaceTime, or Messages) are available to managed Apple accounts.  
