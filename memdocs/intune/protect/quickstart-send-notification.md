---
# required metadata

title: Send notifications to noncompliant devices
titleSuffix: Microsoft Intune
description: In this topic, you use Microsoft Intune to send email notifications to noncompliant devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/07/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.assetid: a1b89f2d-7937-46bb-926b-b05f6fa9c749

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-device-compliance
---

# Step 7: Send notifications to noncompliant devices

In this topic, you'll use Microsoft Intune to send an email notification to the members of your workforce that have noncompliant devices.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

> [!NOTE]
> The remote action to send an email notification is not supported on devices that are managed by a [device compliance partner](../protect/device-compliance-partners.md).
> 
> For localization, admin must configure the target language from Intune admin center when creating the notification message template. The notification message language sent to the user will be based on the preferred language configured for the user in Microsoft Entra ID. 

By default, when Intune detects a device that isn't compliant, Intune immediately marks the device as noncompliant. Microsoft Entra [Conditional Access](/azure/active-directory/active-directory-conditional-access-azure-portal) then blocks the device. When a device isn't compliant, Intune allows you to add actions for noncompliance, which gives you flexibility to decide what to do. For example, you can give users a grace period to be compliant before blocking noncompliant devices.

One action to take when a device doesn't meet compliance is to send email to the devices user. You can also customize an email notification before sending it. Specifically, you can customize the recipients, subject, and message body, including company logo, and contact information. Intune also includes details about the noncompliant device in the email notification.

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

When using device compliance policies to block devices from corporate resources, Microsoft Entra Conditional Access must be set up. If you've completed the [Create a device compliance policy](quickstart-set-password-length-android.md) evaluation step, you're using Microsoft Entra ID. For more information about Microsoft Entra ID, see [Conditional Access in Microsoft Entra ID](/azure/active-directory/active-directory-conditional-access-azure-portal) and [common ways to use Conditional Access with Intune](../protect/conditional-access-intune-common-ways-use.md).


## Sign in to Intune

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as an [Intune administrator](../fundamentals/users-add.md#types-of-administrators). If you've created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Create a notification message template

To send email to your users, create a notification message template. When a device is noncompliant, the details you enter in the template is shown in the email sent to your users.  

1. In the Intune admin center, go to **Devices** > **Compliance**.  
2. Select the **Notifications** tab and then choose **Create notification**.  
3. Enter the following information for the **Basics** step:
   - **Name**: *Contoso Admin*
   - **Email header – Include company logo**: Set to **Enabled** to show your organization's logo.
   - **Email footer – Include company name**: Set to **Enabled** to show your organization's name.
   - **Email footer – Include contact information**: Set to **Enabled** to show your organization's contact information.
   - **Company Portal Website Link**: Set to **Disabled**.
4. Click **Next**.
5. Enter the following information for the **Notification message templates** step:
   - **Subject**: *Device compliance*
   - **Message**: *Your device is currently not meeting our organization's compliance requirements.*
6. Click **Next** and review your notification. 
7. Click **Create**. The notification message template is ready to use.

   > [!NOTE]
   > You can also edit a Notification template that was previously created.

For details about setting your company name, company contact information, and company logo, see the following articles:

- [Company information and privacy statement](../apps/company-portal-app.md#configuration)
- [Support information](../apps/company-portal-app.md#support-information)
- [Customizing the user experience](../apps/company-portal-app.md#customizing-the-user-experience).

## Add a noncompliance policy

When you create a device compliance policy, Intune automatically creates an action for noncompliance. Intune then marks devices as noncompliant when they fail to meet your compliance policy. You can customize how long the device is marked as noncompliant. You can also add another action when you create a compliance policy, or update an existing compliance policy.

The following steps will create a compliance policy for Windows 10 devices:

1. In the Intune admin center, go to **Devices** > **Compliance**. 
2. On the **Policies** tab, choose **Create policy**.  
3. Under **Platform**, click **Windows 10 and later**.  
4. Click **Create**.  
5. Enter the following information in the **Basics** step followed by **Next**:

   - **Name**: *Windows 10 compliance*
   - **Description**: *Windows 10 compliance policy*

6. Select **System Security** to display the device security-related settings.
7. Configure the following options:

   - Set **Require a password to unlock mobile devices** to **Require**. This setting specifies whether to require users to enter a password before access is granted to information on their mobile devices.
   - Set **Minimum password length** to **6**. This setting specifies the minimum number of digits or characters in the password.
8. Select **Next** for each of the remaining steps until you reach the **Review + create** step. Click **Create** to create your compliance policy.

## Add an action for noncompliance

After you have created a noncompliance policy, you can set an action to take place with the device is out of compliance.

The following steps will create an action for noncompliance for Windows 10 devices:

1. In the Intune admin center, select **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance**.  
2. Select your Windows 10 compliance policy from the list.
3. Select **Properties**.  
4. Next to the **Action for noncompliance** section, choose **Edit**.
5. In the **Action** drop-down box, select **Send email to end users**.
6. In the **Schedule (days after noncompliance)** drop-down box, select **0**.
7. Under **Message template**,  click **None selected** to display the **Notification message templates** pane.
8. Click the template you created earlier in this topic, and then click **Select** to select the message template.
9. Click **Review + save** > **Save** to save your compliance policy.

## Assign the policy

You can assign the compliance policy to a specific group of users or to all users. When Intune recognizes that a device is noncompliant, the user is notified that they must update their device to meet the compliance policy. Use the following steps to assign the policy.

1. In the admin center, go to **Devices** > **Compliance** and select the **Windows 10 compliance** policy that you created earlier.  
2. Select **Properties**. 
3. Next to **Assignments**, click **Edit**.
4. In the **Assign to** drop-down box, select **All Users**. This will select all users. Any user that has a **Windows 10 and later** device that doesn't meet this compliance policy will be notified.

    > [!NOTE]
    > You can include and exclude groups when assign compliancy policies.

4. Click **Review + save** > **Save**.

When you've successfully created and saved the policy, it will appear in the list of **Compliance policies - Policies**. Notice in the list that **Assigned** is set to **Yes**.

## Next steps

In this topic, you used Intune to create and assign a compliance policy for your workforce's Windows 10 devices to require a password of at least six characters in length. For more information about creating compliance policies for Windows devices, see [Add a device compliance policy for Windows devices in Intune](compliance-policy-create-windows.md).

To continue to evaluate Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 8: Add and assign a client app](../apps/quickstart-add-assign-app.md)
