---
# required metadata

title: Quickstart - Send notifications to noncompliant devices
titleSuffix: Microsoft Intune
description: In this quickstart, you use Microsoft Intune to send email notifications to noncompliant devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: a1b89f2d-7937-46bb-926b-b05f6fa9c749

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Quickstart: Send notifications to noncompliant devices

In this quickstart, you'll use Microsoft Intune to send an email notification to the members of your workforce that have noncompliant devices.

By default, when Intune detects a device that isn't compliant, Intune immediately marks the device as noncompliant. Azure Active Directory (Azure AD) [Conditional Access](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) then blocks the device. When a device isn't compliant, Intune allows you to add actions for noncompliance, which gives you flexibility to decide what to do. For example, you can give users a grace period to be compliant before blocking noncompliant devices.

One action to take when a device doesn't meet compliance is to send email to the devices user. You can also customize an email notification before sending it. Specifically, you can customize the recipients, subject, and message body, including company logo, and contact information. Intune also includes details about the noncompliant device in the email notification.

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

When using device compliance policies to block devices from corporate resources, Azure AD Conditional Access must be set up. If you've completed the [Create a device compliance policy](quickstart-set-password-length-android.md) quickstart, you're using Azure Active Directory. For more information about Azure AD, see [Conditional Access in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) and [common ways to use Conditional Access with Intune](../protect/conditional-access-intune-common-ways-use.md).

## Sign in to Intune

Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a [Global administrator](../fundamentals/users-add.md#types-of-administrators) or an Intune [Service administrator](../fundamentals/users-add.md#types-of-administrators). If you've created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Create a notification message template

To send email to your users, create a notification message template. When a device is noncompliant, the details you enter in the template is shown in the email sent to your users.

1. In Intune, select **Devices** > **Compliance policies** > **Notifications** > **Create notification**.
2. Enter the following information:

   - **Name**: *Contoso Admin*
   - **Subject**: *Device compliance*
   - **Message**: *Your device is currently not meeting our organization's compliance requirements.*
   - **Email header – Include company logo**: Set to **Enabled** to show your organization's logo.
   - **Email footer – Include company name**: Set to **Enabled** to show your organization's name.
   - **Email footer – Include contact information**: Set to **Enabled** to show your organization's contact information.

   ![Example of a compliant notification message in Intune](./media/quickstart-send-notification/quickstart-send-notification-01.png)

3. Select **Next** and review your notification. Select **Create** and the notification message template is ready to use.

   > [!NOTE]
   > You can also edit a Notification template that was previously created.

For details about setting your company name, company contact information, and company logo, see the following articles:

- [Company information and privacy statement](../apps/company-portal-app.md#configuration)
- [Support information](../apps/company-portal-app.md#support-information)
- [Customizing the user experience](../apps/company-portal-app.md#customizing-the-user-experience).

## Add a noncompliance policy

When you create a device compliance policy, Intune automatically creates an action for noncompliance. Intune then marks devices as noncompliant when they fail to meet your compliance policy. You can customize how long the device is marked as noncompliant. You can also add another action when you create a compliance policy, or update an existing compliance policy.

The following steps will create a compliance policy for Windows 10 devices.

1. In Intune, select **Devices** > **Compliance Policies** > **Create Policy**.

2. Enter the following information:

   - **Name**: *Windows 10 compliance*
   - **Description**: *Windows 10 compliance policy*
   - **Platform**: Windows 10 and later

3. Select **Settings** > **System Security** to display the device security-related settings.

4. Configure the following options:

   - Set **Require a password to unlock mobile devices** to **Require**. This setting specifies whether to require users to enter a password before access is granted to information on their mobile devices.

   - Set **Minimum password length** to **6**. This setting specifies the minimum number of digits or characters in the password.

   ![System Security settings for a new compliance policy](./media/quickstart-send-notification/system-security-settings-01.png)

5. Select **OK** > **OK** > **Create** to create your compliance policy.

6. Select **Properties** > **Action for noncompliance** > **Add**.

7. In the **Action** drop-down box, confirm **Send email to end users** is selected.

8. Select **Message template**,  the template you created earlier in this article, and then **Select** to select the message template.

9. Select **ADD** > **OK** > **Save** to save your changes.

## Assign the policy

You can assign the compliance policy to a specific group of users or to all users. When Intune recognizes that a device is noncompliant, the user is notified that they must update their device to meet the compliance policy. Use the following steps to assign the policy.

1. In Intune go to **Devices** > **Compliance Policies** and select the **Windows 10 compliance** policy that you created earlier.

2. Select **Assignments**.

3. In the **Assign to** drop-down box, select **All Users**. This will select all users. Any user that has a **Windows 10 and later** device that doesn't meet this compliance policy will be notified.

    > [!NOTE]
    > You can include and exclude groups when assign compliancy policies.

4. Click **Save**.

When you've successfully created and saved the policy, it will appear in the list of **Compliance policies - Policies**. Notice in the list that **Assigned** is set to **Yes**.

## Next steps

In this quickstart, you used Intune to create and assign a compliance policy for your workforce's Windows 10 devices to require a password of at least six characters in length. For more information about creating compliance policies for Windows devices, see [Add a device compliance policy for Windows devices in Intune](compliance-policy-create-windows.md).

To follow this series of Intune quickstarts, continue to the next quickstart.

> [!div class="nextstepaction"]
> [Quickstart: Add and assign a client app](../apps/quickstart-add-assign-app.md)
