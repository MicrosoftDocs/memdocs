---
# required metadata

title: Set up Lookout Mobile Endpoint Security with Microsoft Intune
description: How to set up Lookout Mobile Endpoint Security and Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 5b0d7644-3183-45ba-a165-0d82d70cb71e

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Set up Lookout Mobile Endpoint Security integration with Intune

With an environment that meets the [prerequisites](lookout-mobile-threat-defense-connector.md#prerequisites), you can integrate Lookout Mobile Endpoint Security with Intune. The information in this article can guide you in setting up integration and configuring important settings in Lookout for use with Intune.

> [!IMPORTANT]
> An existing Lookout Mobile Endpoint Security tenant that is not already associated with your Microsoft Entra tenant cannot be used for the integration with Microsoft Entra ID and Intune. Contact Lookout support to create a new Lookout Mobile Endpoint Security tenant. Use the new tenant to onboard your Microsoft Entra users.

<a name='collect-microsoft-entra-id-information'></a>

## Collect Microsoft Entra information

To integrated Lookout with Intune, you associate your Lookout Mobility Endpoint Security tenant with your Microsoft Entra subscription.

To enable your Lookout Mobile Endpoint Security subscription integration with Intune, you provide the following information to Lookout support (enterprisesupport@lookout.com):

- **Microsoft Entra tenant ID**

- **Microsoft Entra group Object ID** for the group with **full** Lookout Mobile Endpoint Security (MES) Console access.

  You create this user group in Microsoft Entra ID to contain the users that have *full access* to sign in to the **Lookout console**. Users must be members of this group, or the optional *restricted access* group, to sign in to the Lookout Console.

- **Microsoft Entra group Object ID** for the group with **restricted** Lookout MES Console access *(optional group)*.

  You create this optional user group in Microsoft Entra ID to contain users that shouldn't have access to several configuration and enrollment-related modules of the Lookout console. Instead, these users have read-only access to the **Security Policy** module of the Lookout console. Users must be members of this optional group, or the required *full access* group, to sign in to the Lookout Console.

### Collect information from Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com) with a Global Administrator account.

2. Go to **Microsoft Entra ID** > **Properties** and locate your **Tenant ID**. Use the *Copy* button to copy the Directory ID, and then save it in a text file.

   :::image type="content" source="./media/lookout-mtd-connector-integration/azure-ad-properties.png"alt-text="Microsoft Entra ID":::

3. Next, find the Microsoft Entra group ID for the accounts you use to grant Microsoft Entra users access to the Lookout Console. One group is for *full access*, and the second group, for *restricted access* is optional. To get the *Object ID*, for each account:

   1. Go to **Microsoft Entra ID** > **Groups** to open the *Groups - All groups* pane.

   2. Select the group you created for *full access* to open its *Overview* pane.

   3. Use the *Copy* button to copy the Object ID, and then save it in a text file.

   4. Repeat the process for the *restricted access* group if you use that group.

      :::image type="content" source="./media/lookout-mtd-connector-integration/azure-ad-group-id.png" alt-text="Microsoft Entra group Object ID":::

   After you gather this information, contact Lookout support. Lookout Support works with your primary contact to onboard your subscription and create your Lookout Enterprise account, using the information that you provide.

## Configure your Lookout subscription

The following steps are to be completed in the Lookout Enterprise admin console and enable a connection to Lookout's service for Intune enrolled devices (via device compliance) **and** unenrolled devices (via app protection policies).

After Lookout support creates your Lookout Enterprise account, Lookout support sends an email to the primary contact for your company with a link to the sign-in url: [https://aad.lookout.com/les?action=consent](https://aad.lookout.com/les?action=consent).

### Initial sign-in

The first sign-in to the Lookout MES Console displays a consent page ([https://aad.lookout.com/les?action=consent](https://aad.lookout.com/les?action=consent)). As a Microsoft Entra Global Administrator, sign-in and **Accept**. A subsequent sign-in doesn't require the user to have this level of Microsoft Entra ID privilege.

A consent page is displayed. Choose **Accept** to complete the registration.

![screenshot of the first-time sign-in page of the Lookout console](./media/lookout-mtd-connector-integration/lookout_mtp_initial_login.png)

When you accept and consent, you're redirected to the Lookout Console.

After the initial sign-in and consent is complete, users that sign in from [https://aad.lookout.com](https://aad.lookout.com) are redirected to the MES Console. If consent wasn't yet granted, all sign-in attempts result in a Bad Login Error.

### Configure the Intune Connector

The following procedure assumes you've previously created a user group in Microsoft Entra ID for testing your Lookout deployment. The best practice is to start with a small group of users to allow your Lookout and Intune admins to become familiar with the product integrations. After they're familiar, you can extend the enrollment to additional groups of users.

1. Sign in to the [Lookout MES Console](https://aad.lookout.com) and go to **System** > **Connectors**, and then select **Add Connector**. Select **Intune**.

   ![Image of the Lookout console with the Intune option on the connectors tab](./media/lookout-mtd-connector-integration/lookout_mtp_setup-intune-connector.png)

2. On the *Microsoft Intune* pane, select **Connection Settings** and specify the **Heartbeat Frequency** in minutes.

   ![Image of the connection settings tab with heartbeat frequency configured](./media/lookout-mtd-connector-integration/lookout-mtp-connection-settings.png)

3. Select **Enrollment Management**, and for **Use the following Microsoft Entra security groups to identify devices that should be enrolled in Lookout for Work**, specify the *Group name* of a Microsoft Entra group to use with Lookout, and then select **Save changes**.

   ![screenshot of the Intune connector enrollment page](./media/lookout-mtd-connector-integration/lookout-mtp-enrollment.png)

   **About the groups you use**:
   - As a best practice, start with a Microsoft Entra security group that contains only a few users to test Lookout integration.
   - The **Group name** is case-sensitive as shown in the **Properties** of the security group in the Azure portal.
   - The groups you specify for **Enrollment Management** define the set of users whose devices will enroll with Lookout. When a user is in an enrollment group, their devices in Microsoft Entra ID are enrolled and eligible for activation in Lookout MES. The first time a user opens the *Lookout for Work* application on a supported device, they're prompted to activate it.

4. Select **State Sync** and ensure both *device status* and *threat status* are set to **On**. Both are required for the Lookout Intune integration to work correctly.

5. Select **Error Management**, specify the email address that should receive the error reports, and then select **Save changes**.

   ![screenshot of the Intune connector error management page](./media/lookout-mtd-connector-integration/lookout-mtp-connector-error-notifications.png)

6. Select **Create connector** to complete configuration of the connector. Later, when you're satisfied with your results, you can extend enrollment to additional user groups.

## Configure Intune to use Lookout as a Mobile Threat Defense provider

After you configure Lookout MES, you must set up a connection to [Lookout in Intune](mtd-connector-enable.md).

## Additional settings in the Lookout MES Console

The following are additional settings you can configure in the Lookout MES Console.

### Configure Enrollment settings

In the Lookout MES Console, select **System** > **Manage Enrollment** > **Enrollment settings**.

- For **Disconnected Status**, specify the number of days before an unconnected device is marked as disconnected.

  Disconnected devices are considered as noncompliant and are blocked from accessing your company applications based on the Intune conditional access policies. You can specify values between 1 and 90 days.

  ![Lookout enrollment settings on the System module](./media/lookout-mtd-connector-integration/lookout-console-enrollment-settings.png)

### Configure Email Notifications

To receive email alerts for threats, sign in to the [Lookout MES Console](https://aad.lookout.com) with the user account that should receive notifications.

- Go to **Preferences** and then set the notifications you want to receive to **ON**, and then **Save** the changes.

- If you no longer want to receive email notifications, set the notifications to **OFF** and save your changes.

  ![screenshot of the preferences page with the user account displayed](./media/lookout-mtd-connector-integration/lookout-mtp-email-notifications.png)

## Configure threat classifications

Lookout Mobile Endpoint Security classifies mobile threats of various types. The Lookout threat classifications have default risk levels associated with them. The risk levels can be changed at any time to suit your company requirements.

For information about the threat level classifications, and how to manage the risk levels associated with them, see [Lookout Threat Reference](https://enterprise.support.lookout.com/hc/articles/360011812974).

>[!IMPORTANT]
>
> Risk levels are an important aspect of Mobile Endpoint Security because the Intune integration calculates device compliance according to these risk levels at runtime.
>
> The Intune administrator sets a rule in policy to identify a device as noncompliant if the device has an active threat with a minimum level of **High**, **Medium**, or **Low**. The threat classification policy in Lookout Mobile Endpoint Security directly drives the device compliance calculation in Intune.

## Monitor enrollment

After setup is complete, Lookout Mobile Endpoint Security starts to poll Microsoft Entra ID for devices that correspond to the specified enrollment groups. You can find information about enrolled devices by going to **Devices** in the Lookout MES Console.

- Initial status for devices is *pending*.
- The device status updates after the *Lookout for Work* app is installed, opened, and activated on the device.

For details on how to get the *Lookout for Work* app deployed to a device, see [Add Lookout for work apps with Intune](mtd-apps-ios-app-configuration-policy-add-assign.md).

## Next steps

- [Set up Lookout apps for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Set up Lookout apps for unenrolled devices](mtd-add-apps-unenrolled-devices.md)
