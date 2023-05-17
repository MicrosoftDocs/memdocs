---
title: Create quiet time policies in Microsoft Intune
titleSuffix:
description: Learn how to create quiet time policies for iOS/iPadOS and Android apps.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/16/2023
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 
ms.reviewer: cdemello
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier1
- highpri
---

# Quiet time policies for iOS/iPadOS and Android apps

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The global quiet time settings allow you to create policies to schedule quiet time for your end users. These settings automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours.

## Quiet time policy types

There are three quiet time policy types available. The following table describes each policy type.

|      Policy Type     |      Description     |
|---|---|
|     Date Range    |     Select this option to automatically mute Microsoft Outlook  email and Teams notifications on iOS/iPadOS and Android platforms during the   specified range.    |
|     Days of the week    |     Select this option to automatically mute Microsoft Outlook   email and Teams notifications on iOS/iPadOS and Android platforms during   certain hours or all day on selected days of the week.    |

## Create an iOS/iPadOS and Android quiet time policy

To create a quiet time policy, use the following steps:

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Quiet Time** > **Policies**.
3. Select **Create policy**.
4. Select **Policy Type**. You can choose the **Date Range** or the **Days of the week** policy types. For more information, see, [Quiet time policy types](#quiet-time-policy-types).
5. Select **Create** to display the **Basics** page.
6. On the **Basics** page, add a **Name** and optional **Description** for the quiet time policy. The **Platform** value is prepopulated with “Android; iOS/iPadOS.”<br>Select **Next** to display the **Configuration settings** page. 
7. On the **Configuration settings** page, select how you want to apply quiet time settings. Each type of Quiet Time policy has different configuration values. For more information, see [Quiet time policy configuration settings](#quiet-time-policy-configuration-settings).<br>Select **Next** to display the **Scope tags** page.
8. The **Scope tags** page allows you to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).<br>Select **Next** to display the **Assignments** page.
9. The **Assignments** page allows you to assign the app protection policy to groups of users. You must apply the policy to a group of users to have the policy take effect.<br>Select **Next** to display the **Review + create** page.
10. The **Review + create** page allows you to review the values and settings you entered for this quiet time policy.
12. When you're ready, click **Create** to create the quiet time policy in Intune.

## Change existing quiet time policies

You can edit an existing quiet time policy and apply it to the targeted users. However, when you change existing policies, users won't see the changes for a 24-hour period.

To change the list of user groups, use the following steps:

1. In the **Quiet Time** > **Policies** pane, select the policy you want to change.
2. Next to the section titled **Assignments**, select **Edit**.
3. To add a new user group to the policy, under the **Included groups** section, choose **Add groups**. Then, find and select the user group. Choose **Select** to add the group.
4. To exclude a user group, under the **Excluded groups** section, choose **Add groups**. Then, find and select the user group.Choose **Select** to exclude the user group.
5. To delete groups that were previously added, in either the **Included groups** or **Excluded groups** section, select **Remove**.
6. Select **Review + save** to review the user groups selected for this policy.
7. After your changes to the assignments are ready, select **Save** to save the configuration and deploy the policy to the new set of users. If you select **Cancel** before you save your configuration, you'll discard all changes you have made to the **Included groups** and **Excluded groups** sections.

To change policy configuration settings, use the following steps:

1. In the **Quiet Time** > **Policies** pane, select the policy you want to change.
2. Next to the section titled **Configuration settings**, select **Edit**. Then change the settings to new values.
3. Select **Review + save** to review the updated settings for this policy.
4. Select **Save** to save your changes. If you select **Cancel** before you save your configuration, you'll discard all changes you have made to the Configuration settings pane.

## Quiet time policy configuration settings

### Date Range policy

The **Date Range** policy has a **Range Settings** configuration section. 

**Range Settings** section:

|      Policy setting     |      Description     |
|---|---|
|    Start   |     Specify **Start** date and time to mute notifications.    | 
|    End   |     Specify **End** date and time to mute notifications.    | 

:::image type="content" source="./media/apps-quiet-time-policies/apps-quiet-time-policies-01.png" alt-text="Screenshot of the Microsoft Intune quiet time - Configure Date Range policy" border="true":::

### Days of week policy

The **Days of week** policy has the **Allday**, **Certain Hours**, and **End User Overrides** configuration settings sections.

**Allday** section:

|      Policy setting     |      Description     |
|---|---|
|     Mute notifications all day    |     Set to **Require** to enable muting notifications for a full 24 hours on specific days of the week.    |
|     Days of the week    |     Set to **Configured** and then select one or more days of the week that notifications must be muted for a full 24 hours.    |

**Certain Hours** section:

|      Policy setting     |      Description     |
|---|---|
|     Mute notifications daily    |     Set to **Require** to enable muting notifications for certain hours on specific days of the week.    |
|     Start time    |     Set the start time for muting notifications for certain        hours on specific days of the week.    |
|     End time    |     Set the end time for muting notifications for certain hours on specific days of the week.    |
|     Days of the week    |     Set to **Configured** and then select one or more days of the week that notifications must be muted for certain hours.    |

**End User Overrides** section:

|      Policy setting     |      Description     |
|---|---|
|     Allow user to change settings    |     Select **Yes** to allow end users to make changes to this setting by editing their global quiet time settings. Select **No** to disallow end users from changing this setting by editing their global quiet time settings.   |

:::image type="content" source="./media/apps-quiet-time-policies/apps-quiet-time-policies-02.png" alt-text="Screenshot of the Microsoft Intune quiet time - Configure days of the week policy" border="true":::  

