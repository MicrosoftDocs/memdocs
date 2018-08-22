---
title: Actions for noncompliance
titleSuffix: Configuration Manager
description: Learn how to setup actions for noncompliance with Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Set up actions for non-compliance

The **Actions for non-compliance** allow you to configure a time-ordered sequence of actions that are applied to devices that fall out of compliance. For example, send e-mails to the end user of non-compliant devices and mark those devices non-compliant.



## Before you begin

> [!IMPORTANT]  
> To set up actions for non-compliance, first create at least one device compliance policy.  

These are the supported actions for non-compliance:

- Send e-mail to end user
- Mark devices non-compliant

### Send e-mail to end user

Choose from pre-created default email templates or create a fully customized email notification. Configuration Manager provides customization of the subject, message body, including company logo, contact information and additional recipients.

### Mark devices non-compliant

Determine a schedule in number of days which the device should be blocked from accessing corporate resources. This action can be immediate, but you can also give the user a grace period to be compliant with the device compliance policies.

### Supported platforms

Supported by [all platforms managed through Intune](https://docs.microsoft.com/intune/supported-devices-browsers).



## To add an email template

Configuration Manager provides e-mail templates, but you can also create your own. The e-mail template is used later in the process of creating actions for non-compliance to communicate with users.

1. In the Configuration Manager console, choose **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then choose **Compliance notification templates**.  

3. On the **Home** tab, in the **Create Compliance Notification Template**.  

4. Enter the following information:  

	a. **Name**: E-mail template name  

    > [!Note]  
    > The **From** field is auto-populated with a no-reply email address from Microsoft.<!--SCCMDocs issue 652-->  

	c. **Subject**: A subject that explains the e-mail notification being sent  

	d. **Message body**: More details on the e-mail notification  

	> [!TIP]  
	> You can also include **E-mail header** with your company logo, and **E-mail footer**, which can include your organization's name and contact information. Also edit this information in the properties of you Intune subscription.  

5. Click **OK** to save the new e-mail template.  

6. On the **Add Action** page, select your new e-mail template from the list.  

7. Once you select your e-mail template, click **OK**.  



## To create actions for non-compliance

1. In the Configuration Manager console, choose **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, expand **Compliance Settings**, and then choose **Compliance Policies**.  

3. On the **Home** tab, in the **Create** group, choose **Create Compliance Policy**.  

4. Select the **Supported Platforms** you want, then click **Next** twice. You can skip the **Rules** page.  

5. On the **Noncompliance Actions** page, to define what happens when a device becomes non compliant, click **New**.  

6. You can choose two options: **Send e-mail to end user** or **Mark device non-compliant**.  

7. If you select **Send e-mail to end user**, enter the following details:  

	a. **Grace period (in days):** Enter a number of days from 0 to 365  

	b. **Additional recipients (via e-mail)**  

	c. **Select the message template:** Choose a default e-mail template or custom template that you created.  
	
	> [!TIP]   
	> You can also add a new e-mail template when adding the **Send e-mail to end user** action by clicking **New** from the **Add Action** page.  

8. If you select **Mark device non-compliant**, enter the following details:  

	a. **Grace period (in days):** Enter a number of days from 0 to 365  

9. Complete the wizard.  

