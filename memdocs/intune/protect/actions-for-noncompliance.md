---
# required metadata

title: Noncompliant message and actions with Microsoft Intune - Azure | Microsoft Docs
description: Create a notification email to send to non-compliant devices. Add actions after a device is  marked as non-compliant, such as add a grace period to get compliant, or create a schedule to block access until the device is compliant. Do this using Microsoft Intune in Azure.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Automate email and add actions for noncompliant devices in Intune

For devices that don't meet your compliance policies or rules, you can add **Actions for noncompliance**. This feature configures a time-ordered sequence of actions, such as emailing the end user, and more.

## Overview

By default, when Intune detects a device that isn't compliant, Intune immediately marks the device as noncompliant. Azure Active Directory (AD) [Conditional Access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) then blocks the device. When a device isn't compliant, **action for noncompliance** also gives you flexibility to decide what to do. For example, don't block the device immediately, and give the user a grace period to be compliant.

There are several types of actions:

- **Send email to end user**: Customize an email notification before sending it to the end user. You can customize the recipients, subject, and message body, including company logo, and contact information.

    Additionally, Intune includes details about the noncompliant device in the email notification.

- **Remotely lock the noncompliant device**: For devices that are noncompliant, you can issue a remote lock. The user is then prompted for a PIN or password to unlock the device. More on the [Remote Lock](../remote-actions/device-remote-lock.md) feature.

- **Mark device non-compliant**: Create a schedule (in number of days) after the device is marked not compliant. You can configure the action to take effect immediately, or give the user a grace period to be compliant.

- **Retire the noncompliant device**: This action removes all company data off the device and removes the device from Intune management. To prevent accidental wipe of a device, this action supports a minimum schedule of 30 days. The following platforms support this action:
  - Android
  - iOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 and later

  Learn more about [retiring devices](../remote-actions/devices-wipe.md#retire).
  
  This article shows you how to:

- Create a message notification template
- Create an action for noncompliance, such as send an email or remotely lock a device


## Before you begin

- To set up actions for non-compliance, you need at least one device compliance policy. To create a device compliance policy, see the following platforms:

  - [Android](compliance-policy-create-android.md)
  - [Android work profiles](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows](compliance-policy-create-windows.md)

- When using device compliance policies to block devices from corporate resources, Azure AD Conditional Access must be set up. See [Conditional Access in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) or [common ways to use Conditional Access with Intune](conditional-access-intune-common-ways-use.md) for guidance.

## Create a notification message template

To send email to your users, create a notification message template. When a device is noncompliant, the details you enter in the template is shown in the email sent to your users.

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Compliance policies** > **Notifications** > **Create notification**.
3. Under *Basics*, specify the following information:

   - **Name**
   - **Subject**
   - **Message**

4. Also under *Basics*, configure the following options for the notification, which all default to *Enabled*:

   - **Email header – Include company logo**
   - **Email footer – Include company name**
   - **Email footer – Include contact information**

   The logo you upload as part of the Company Portal branding is used for email templates. For more information about Company Portal branding, see [Company identity branding customization](../apps/company-portal-app.md#company-identity-branding-customization).

   ![Example of a compliant notification message in Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Select **Next** to continue.

5. Under **Review + create**, review your configurations to ensure the notification message template is ready to use. Select **Create** to complete creation of the notification.

> [!NOTE]
> You can also select an existing notification template you previously created, and **Edit** its information to update the template.

## Add actions for noncompliance

When you create a device compliance policy, Intune automatically creates an action for noncompliance. If a device isn't meeting your compliance policy, this action marks the device as not compliant. You can customize how long the device is marked as not compliant. This action can't be removed.

In addition to the default action to mark devices as not compliant, you can add optional actions when you create a compliance policy, or update an existing policy.

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance policies** > **Policies**, select one of your policies, and then select **Properties**.

   Don't have a policy yet? Create an [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md), or other platform policy.

   > [!NOTE]
   > JAMF devices and devices targeted with device groups cannot receive compliance actions at this time.

3. Select **Actions for noncompliance** > **Add**.

4. Select your **Action**:

   - **Send email to end users**: When the device is noncompliant, choose to email the user. Also:
     - Choose the **Message template** you previously created
     - Enter any **Additional recipients** by selecting groups

   - **Remotely lock the noncompliant device**: When the device is noncompliant, lock the device. This action forces the user to enter a PIN or passcode to unlock the device.

   - **Retire the noncompliant device**: When the device is noncompliant, remove all company data off the device and remove the device from Intune management. To prevent accidental wipe of a device, this action supports a minimum schedule of **30** days.

5. Configure a **Schedule**: Enter the number of days (0 to 365) after noncompliance to trigger the action on users' devices. (*Retire the noncompliant device* supports a minimum of 30 days.) After this grace period, you can enforce a [conditional access](conditional-access-intune-common-ways-use.md) policy. If you enter **0** (zero) number of days, then conditional access takes effect **immediately**. For example, if a device is noncompliant, use conditional access to block access to email, SharePoint, and other organization resources immediately.

   When you create a compliance policy, the **Mark device noncompliant** action is automatically created, and automatically set to **0** days (immediately). With this action, when the device checks-in, the device is evaluated as non-compliant immediately. If also using conditional access, then conditional access kicks in immediately. If you want to allow a grace period, then change the **Schedule** on the **Mark device noncompliant** action.

  In your compliance policy, for example, you also want to notify the user. You can add the **Send email to end user** action. On this **Send email** action, you set the **Schedule** to two days. If the device or end user is still evaluated as non-compliant on day two, then your email is sent on day two. If you want to email the user again on day five of noncompliance, then add another action, and set the **Schedule** to five days.

   For more information on compliance, and the built-in actions, see the [compliance overview](device-compliance-get-started.md).

6. When finished, select **Add** > **OK** to save your changes.

## Next steps

[Monitor your policies](compliance-policy-monitor.md).
