---
# required metadata

title: Noncompliant message and actions with Microsoft Intune
description: Create a notification email to send to non-compliant devices. Add actions to apply to devices that don't meet your compliance policies. Actions can include a grace period to get compliant, block access to network resources, or retire the noncompliant device.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/12/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Configure actions for noncompliant devices in Intune

For devices that don't meet your compliance policies or rules, you can add **Actions for noncompliance**. This feature configures a time-ordered sequence of actions, such as emailing the end user, and more.

## Overview

By default, each compliance policy includes the action for noncompliance of **Mark device noncompliant** with a schedule of zero days (**0**). The result of this default is when Intune detects a device isn't compliant, Intune immediately marks the device as noncompliant. After a device is marked as noncompliance, Azure Active Directory (AD) [Conditional Access](/azure/active-directory/active-directory-conditional-access-azure-portal) can block the device.

By configuring  **Actions for noncompliance** you gain flexibility to decide what to do about noncompliant devices, and when to do it. For example, you might choose to not block the device immediately, and give the user a grace period to become compliant.

For each action you set, you can configure a schedule that determines when that action takes effect. The schedule is a number of days after the device is marked as noncompliant. You can also configure multiple instances of an action. When you set multiple instances of an action in a policy, the action runs again at that later scheduled time if the device remains non-compliant.

Not all actions are available for all platforms.

   > [!NOTE]
   > The Microsoft Endpoint Manager admin center displays the _schedule (days after noncompliance)_ in days. However it is possible to specify a more granular interval (hours), using decimal fractions such as 0.25 (6 hours), 0.5 (12 hours), 1.5 (36 hours), and so on. While other values are possible, they can only be configured using [Microsoft Graph](/graph/overview) and not via the admin center. Attempting to use other values in the admin center, such as 0.33 (8 hours) will result in an error when attempting to save the policy.

## Available actions for noncompliance

Following are the available actions for noncompliance:

- **Mark device non-compliant**: By default, this action is set for each compliance policy and has a schedule of zero (**0**) days, marking devices as noncompliant immediately.

  When you change the default schedule, you provide a grace period in which a user can remediate issues or become compliant without being marked as non-compliant.

  This action is supported on all platforms supported by Intune.

- **Send email to end user**: This action sends an email notification to the user.
When you enable this action:

  - Select a *Notification message template* that this action sends. You [Create a notification message template](#create-a-notification-message-template) before you can assign one to this action. When you create the custom notification, you customize the message locale, subject, message body, and can include the company logo, company name, and additional contact information.
  - Choose to send the message to additional recipients by selecting one or more of your Azure AD Groups.

  Intune uses the email address defined in the end user's profile and not their user principal name (UPN). If there is no defined email address defined in the user's profile, then Intune does not send a notification email. When the email is sent, Intune includes details about the noncompliant device in the email notification.

  This action is supported on all platforms supported by Intune.

   > [!NOTE] 
   > In the commercial cloud, notification emails are sent from: IntuneNotificationService@microsoft.com
   > 
   > In government clouds, notification emails are sent from: microsoft-noreply@microsoft.com
   > 
   > Ensure you do not have any mailbox policies that would prevent delivery of emails from these addresses, otherwise end users may not recieve the email notification. 

- **Remotely lock the noncompliant device**: Use this action to issue a remote lock of a device. The user is then prompted for a PIN or password to unlock the device. More on the [Remote Lock](../remote-actions/device-remote-lock.md) feature.

  The following platforms support this action:
  - Android device administrator
  - Android (AOSP) (preview)  
  - Android Enterprise:
    - Fully Managed
    - Dedicated
    - Corporate-Owned Work Profile
    - Personally-Owned Work Profile
    - Android Enterprise kiosk devices
  - iOS/iPadOS
  - macOS

- **Retire the noncompliant device**: This action removes all company data off the device and removes the device from Intune management.

  The following platforms support this action:
  - Android device administrator
  - Android (AOSP) (preview)  
  - Android Enterprise:
    - Fully Managed
    - Dedicated
    - Corporate-Owned Work Profile
    - Personally-Owned Work Profile
  - iOS/iPadOS
  - macOS
  - Windows 10/11

  When this action applies to a device, that device is added to a list of devices in the admin console at **Devices** > **Compliance policies** > **Retire Noncompliant Devices**. The device isn't retired until an admin takes explicit action to retire the device.
  
  > [!NOTE]
  > Only devices to which the **Retire the noncompliant device** action has been triggered appear in the **Retire Selected Devices** view. To see a list of all devices that are not compliant, see the **Noncompliant devices** report mentioned in [Monitor device compliance policy](../protect/compliance-policy-monitor.md#view-compliance-reports).

  To retire one or more devices from the list, select devices to retire and then select **Retire Selected Devices**. When you choose an action that retires devices, you're then presented with a dialog box to confirm the action. It's only after confirming the intent to retire the devices that they are cleared of company data and removed from Intune management. 

  Other options include *Retire All Devices*, *Clear All Devices Retire State*, and *Clear Selected Devices Retire State*. Clearing the retire state for a device removes the device from the list of devices that can be retired until the action to *Retire the noncompliant device* is applied to that device again.

  Learn more about [retiring devices](../remote-actions/devices-wipe.md#retire).

- **Send push notification to end user**: Configure this action to send a push notification about non-compliance to a device through the Company Portal app or Intune App on the device.

  The following platforms support this action:
  - Android device administrator
  - Android Enterprise:
    - Fully Managed
    - Dedicated
    - Corporate-Owned Work Profile
    - Personally-Owned Work Profile
  - iOS/iPadOS

  The push notification is sent the first time a device checks in with Intune and is found to be non-compliant to the compliance policy. When a user selects the notification, the Company Portal app or Intune app opens and displays information about why they're non-compliant. The user can then take action to resolve the issue. The message details about non-compliance are generated by Intune and can't be customized.

  > [!IMPORTANT]
  > Intune, the Company Portal app, and the Microsoft Intune app, can't guarantee delivery of a push notification. Notifications might show up after several hours of delay, if at all. This includes when users have turned off push notifications.
  >
  > Do not rely on this notification method for urgent messages.

  Each instance of the action sends a notification a single time. To send the same notification again from a policy, configure additional instances of the action in that policy, each with a different schedule.
  
  For example, you might schedule the first action for zero days and then add a second instance of the action set to three days. This delay before the second notification gives the user a few days to resolve the issue, and avoid the second notification.

  To avoid spamming users with too many duplicate messages, review and streamline which compliance policies include a push notification for non-compliance, and review the schedules to avoid repeat notifications for the same too often.

  Consider:
  - For a single policy that includes multiple instances of a push notification set for the same day, only a single notification is sent for that day.

  - When multiple compliance policies include the same compliance conditions, and include the push notification action with the same schedule, Intune sends multiple notifications to the same device on the same day.

> [!NOTE]
> The following actions for noncompliance are not supported for devices that are managed by a [device compliance management partner](../protect/device-compliance-partners.md):  
> - Send push notification to end user
> - Remotely lock the noncompliant device
> - Retire the noncompliant device
> - Send push notification to end user

## Before you begin

You can [add actions for noncompliance](#add-actions-for-noncompliance) when you configure device compliance policy, or later by editing the policy. You can add additional actions to each policy to meet your needs. Keep in mind that each compliance policy automatically includes the default action for noncompliance that marks devices as noncompliant,  with a schedule set to zero days.

To use device compliance policies to block devices from corporate resources, Azure AD Conditional Access must be set up. See [Conditional Access in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal) or [common ways to use Conditional Access with Intune](conditional-access-intune-common-ways-use.md) for guidance.

To create a device compliance policy, see the following platform-specific guidance:

- [Android](compliance-policy-create-android.md)
- [Android (AOSP)](compliance-policy-create-android-aosp.md) (preview)  
- [Android work profiles](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## Create a notification message template

To send email to your users, create a notification message template and associate that to your compliance policy as an action for noncompliance. Then, when a device is noncompliant, the details you enter in the template is shown in the email sent to your users.

A *notification message template* can include multiple messages that are each specified for a different locale. One local must be specified as the default.

When you specify multiple messages and locales, non-compliant end users receive the appropriate localized message based on their O365 preferred language. Intune sends the default message to users that haven’t set a preferred language or when the template doesn’t include a specific message for their locale.

### To create the template

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Device compliance** > **Notifications** > **Create notification**.
3. On the **Basics** page, configure the following settings:

   - **Name** - Give the template a friendly name to help you identify it.
   - **Email header – Include company logo** (default = *Enable*) - The logo you upload as part of the Company Portal branding is used for email templates. For more information about Company Portal branding, see [Company identity branding customization](../apps/company-portal-app.md#customizing-the-user-experience).
   - **Email footer – Include company name** (default = *Enable*)
   - **Email footer – Include contact information** (default = *Enable*)
   - **Company Portal Website Link** (default = *Disable*) - When set to *Enable*, the email includes a link to the Company Portal website.

   > [!div class="mx-imgBorder"]
   > ![Example of the basics page for a notification message in Intune](./media/actions-for-noncompliance/actions-for-noncompliance-1.png)

   Select **Next** to continue.

4. On the **Notification message templates** page, configure one or more messages. For each message, specify the following details:

   - **Locale**
   - **Subject**
   - **Message body text**

   > [!NOTE] 
   > The maximum number of characters for the Subject is 78, and the maximum number of characters for the message body text is 2000.

   Before continuing, you must select the checkbox for *Is Default* for one of the messages. Only one message can be set as default. To delete a message, select the ellipsis (...) and then **Delete**. 

   > [!div class="mx-imgBorder"]
   > ![Example of the Notification message temmplate page in Intune](./media/actions-for-noncompliance/actions-for-noncompliance-2.png)

   Select **Next** to continue.

5. Under **Review + create**, review your configurations to ensure the notification message template is ready to use. Select **Create** to complete creation of the notification.

### View and edit notifications

Notifications that have been created are available in the *Compliance policies* > *Notifications* page. From the page you can select a notification to view its configuration and:

- Select **Send preview email** to send a preview of the notification email to the account you've used to sign in to Intune.

  To successfully send the preview email, your account must have permissions equal to those of the following Azure AD groups or Intune roles: *Azure AD Global Administrator*, Intune *Administrator* (Intune Azure AD Intune Service Administrator), or  Intune *Policy and Profile Manager*.
- Select **Edit** for *Basics* or *Scope tags* to make a change.

## Add actions for noncompliance

When you create a device compliance policy, Intune automatically creates an action for noncompliance. If a device isn't meeting your compliance policy, this action marks the device as not compliant. You can customize how long the device is marked as not compliant. This action can't be removed.

You can add optional actions when you create a compliance policy, or update an existing policy.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance policies** > **Policies**, select one of your policies, and then select **Properties**.

   Don't have a policy yet? Create an [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md), or other platform policy.

   > [!NOTE]
   > Devices managed by third-party device compliance partners that are targeted with device groups cannot receive compliance actions at this time.

3. Select **Actions for noncompliance** > **Add**.

4. Select your **Action**:

   - **Send email to end users**: When the device is noncompliant, choose to email the user. Also:
     - Choose the **Message template** you previously created
     - Enter any **Additional recipients** by selecting groups

   - **Remotely lock the noncompliant device**: When the device is noncompliant, lock the device. This action forces the user to enter a PIN or passcode to unlock the device.

   - **Retire the noncompliant device**: When the device is noncompliant, remove all company data off the device and remove the device from Intune management.

   - **Send push notification to end user**: Configure this action to send a push notification about non-compliance to a device through the Company Portal app or Intune App on the device.

5. Configure a **Schedule**: Enter the number of days (0 to 365) after noncompliance to trigger the action on users' devices. After this grace period, you can enforce a [conditional access](conditional-access-intune-common-ways-use.md) policy. If you enter **0** (zero) number of days, then conditional access takes effect **immediately**. For example, if a device is noncompliant, use conditional access to block access to email, SharePoint, and other organization resources immediately.

   When you create a compliance policy, the **Mark device noncompliant** action is automatically created, and automatically set to **0** days (immediately). With this action, when the device checks-in with Intune and evaluates the policy, if it is not compliant to that policy Intune immediately marks that device as noncompliant. If the client checks-in at a later time after remediating the issues that lead to noncompliance, its status will update to its new compliance status. If you use Conditional Access, those policies also apply as soon as a device is marked as noncompliant. To set a grace period to allow for a condition of noncompliance to be remediated before the device is marked as noncompliant, change the **Schedule** on the **Mark device noncompliant** action.

   In your compliance policy, for example, you also want to notify the user. You can add the **Send email to end user** action. On this **Send email** action, you set the **Schedule** to two days. If the device or end user is still evaluated as non-compliant on day two, then your email is sent on day two. If you want to email the user again on day five of noncompliance, then add another action, and set the **Schedule** to five days.

   For more information on compliance, and the built-in actions, see the [compliance overview](device-compliance-get-started.md).

6. When finished, select **Add** > **OK** to save your changes.

## Next steps

[Monitor your policies](compliance-policy-monitor.md).
