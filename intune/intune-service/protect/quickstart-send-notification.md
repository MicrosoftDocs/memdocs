---
title: Send Email Notifications to Noncompliant Devices
description: Learn how to create notification templates and send email alerts to users with noncompliant devices in Microsoft Intune. Configure actions for noncompliance.
author: nicholasswhite
ms.author: nwhite
ms.date: 01/15/2026
ms.topic: how-to
ms.reviewer: tycast
ms.collection:
- M365-identity-device-management
- sub-device-compliance
---

# Step 7 - Send notifications to noncompliant devices using Microsoft Intune

Learn how to send email notifications to noncompliant devices using Microsoft Intune. This article walks you through creating notification templates and configuring actions that alert users when their devices fail to meet compliance requirements.

In this article, you use Microsoft Intune to send an email notification to the members of your workforce that have noncompliant devices.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

When Intune detects a device that isn't compliant, Intune immediately marks the device as noncompliant. When a device isn't compliant, Intune allows you to add actions for noncompliance, which gives you flexibility to decide what to do. For example, you can give users a grace period to be compliant before blocking noncompliant devices using [Microsoft Entra Conditional Access](conditional-access.md).

When a device isn't compliant, a common action is to email the device user. You can customize the email notification. Specifically, you can customize the recipients, subject, and message body, including company logo, and contact information. Intune also includes details about the noncompliant device in the email notification.

> [!NOTE]
> Admins need to set the target language for the notification template in the Intune admin center. When the message is sent, its language is determined by the user's preferred language in Microsoft Entra ID.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> - A Microsoft Intune subscription. [Sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with the following role:
> - Built-in **[Policy and Profile manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager)** Microsoft Intune role
:::column-end:::
:::row-end:::

## Create a notification message template

To send email to your users, create a notification message template. When a device is noncompliant, the details you enter in the template are shown in the email sent to your users.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **Compliance**.
2. Select the **Notifications** tab and then select **Create notification**.
3. Enter the following information for the **Basics** step:
   - **Name**: *Contoso Admin*
   - **Email header – Include company logo**: Set to **Enabled** to show your organization's logo.
   - **Email footer – Include company name**: Set to **Enabled** to show your organization's name.
   - **Email footer – Include contact information**: Set to **Enabled** to show your organization's contact information.
   - **Company Portal Website Link**: Set to **Disabled**.
4. Select **Next**.
5. Enter the following information for the **Notification message templates** step:
   - **Subject**: *Device compliance*
   - **Message**: *Your device is currently not meeting our organization's compliance requirements.*
6. Select **Next** and review your notification.
7. Select **Create**. The notification message template is ready to use.

   > [!NOTE]
   > You can also edit a Notification template that you previously created.

For details about setting your company name, company contact information, and company logo, see the following articles:

- [Company information and privacy statement](../apps/company-portal-app.md#configuration)
- [Support information](../apps/company-portal-app.md#support-information)
- [Customizing the user experience](../apps/company-portal-app.md#customizing-the-user-experience).

## Add a noncompliance policy

When you create a device compliance policy, Intune automatically creates an action for noncompliance. Intune marks devices as noncompliant when they fail to meet your compliance policy. You can customize how long the device is marked as noncompliant. You can also add another action when you create a compliance policy, or update an existing compliance policy.

The following steps create a compliance policy for Windows devices:

1. In the Intune admin center, go to **Devices** > **Compliance**.
2. On the **Policies** tab, choose **Create policy**.
3. Under **Platform**, select **Windows 10 and later**.
4. Select **Create**.
5. Enter the following information in the **Basics** step followed by **Next**:

   - **Name**: *Windows compliance*
   - **Description**: *Windows compliance policy*

6. Select **System Security** to display the device security-related settings.
7. Configure the following options:

   - Set **Require a password to unlock mobile devices** to **Require**. This setting specifies whether to require users to enter a password before access is granted to information on their mobile devices.
   - Set **Minimum password length** to **6**. This setting specifies the minimum number of digits or characters in the password.
8. Select **Next** for each of the remaining steps until you reach the **Review + create** step. Select **Create** to create your compliance policy.

## Add an action for noncompliance

After you create a noncompliance policy, set an action for when a device is out of compliance.

The following steps show how to create an action for noncompliance for Windows devices:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance**.
2. Select your Windows compliance policy from the list.
3. Select **Properties**.
4. Next to the **Action for noncompliance** section, choose **Edit**.
5. In the **Action** drop-down box, select **Send email to end users**.
6. In the **Schedule (days after noncompliance)** drop-down box, select **0**.
7. Under **Message template**,  select **None selected** to display the **Notification message templates** pane.
8. Select the template you created earlier in this topic, and then choose **Select** to select the message template.
9. Select **Review + save** > **Save** to save your compliance policy.

## Assign the policy

You can assign the compliance policy to a specific group of users or to all users. When Intune recognizes that a device is noncompliant, it notifies the user that they must update their device to meet the compliance policy. Use the following steps to assign the policy.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Compliance** and select the **Windows compliance** policy that you created earlier.
2. Select **Properties**.
3. Next to **Assignments**, select **Edit**.
4. In the **Assign to** drop-down box, select **All Users**. Any user that has a **Windows 10 and later** device that doesn't meet this compliance policy is notified.

    > [!NOTE]
    > You can include and exclude groups when assigning compliancy policies.

5. Select **Review + save** > **Save**.

When you successfully create and save the policy, it appears in the list of **Compliance policies - Policies**. Notice in the list that **Assigned** is set to **Yes**.

## Next steps

In this article, you used Intune to create and assign a compliance policy for your workforce's Windows devices to require a password of at least six characters in length. For more information about creating compliance policies for Windows devices, see [Add a device compliance policy for Windows devices in Intune](compliance-policy-create-windows.md).

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 8 - Add and assign a client app](../apps/quickstart-add-assign-app.md)
