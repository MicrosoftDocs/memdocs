---
# required metadata

title: Tutorial - Use Microsoft Intune to protect Exchange Online email from unmanaged iOS devices 
titleSuffix: Microsoft Intune
description: Learn how to use Microsoft Intune app protection policies and Conditional Access to prevent unmanaged iOS devices from accessing Exchange Online.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/18/2024
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata
 
#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-device-compliance
---

# Tutorial: Protect Exchange Online email on unmanaged iOS devices with Microsoft Intune

This tutorial demonstrates how to use Microsoft Intune app protection policies with Microsoft Entra Conditional Access to block access to Exchange Online by users who are using an unmanaged iOS device or an app other than the Outlook mobile app to access Microsoft 365 email. The results of these policies apply when the iOS devices aren't enrolled in a device management solution like Intune.

In this tutorial, you'll learn how to:

> [!div class="checklist"]
>
> * Create an Intune app protection policy for the Outlook app. You'll limit what the user can do with app data by preventing *Save As* and restricting *cut*, *copy*, and *paste* actions.
> * Create Microsoft Entra Conditional Access policies that allows only the Outlook app to access company email in Exchange Online. You'll also require multi-factor authentication (MFA) for Modern authentication clients, like Outlook for iOS and Android.

## Prerequisites

For this tutorial, we recommend using nonproduction trial subscriptions.

Trial subscriptions help you avoid affecting a production environment with wrong configurations during this tutorial. Trials also allow us to use only the account you created when creating the trial subscription to configure and manage Intune, as it has permissions to complete each task for this tutorial. Use of this account eliminates the need to make and manage administrative accounts as part of the tutorial.

This tutorial requires a test tenant with the following subscriptions:

- Microsoft Intune Plan 1 subscription ([sign up for a free trial account](../fundamentals/free-trial-sign-up.md))
- Microsoft Entra ID P1 ([free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Microsoft 365 Apps for business subscription that includes Exchange ([free trial](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## Sign in to Intune

For this tutorial, when you sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in with the account that was created when you signed up for the Intune trial subscription. Continue to use this account to sign in to the admin center throughout this tutorial.

## Create the app protection policy

In this tutorial, we set up an Intune [app protection policy](../apps/app-protection-policy.md) for iOS for the Outlook app to put protections in place at the app level. We'll require a PIN to open the app in a work context. We'll also limit data sharing between apps and prevent company data from being saved to a personal location.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **Protection** > **Create policy**, and then select **iOS/iPadOS**.

3. On the **Basics** page, configure the following settings:

   - **Name**: Enter **Outlook app policy test**.
   - **Description**: Enter **Outlook app policy test**.

   The **Platform** value was set in the previous step by selecting *iOS/iPadOS*.

   Select **Next** to continue.

4. On the **Apps** page, you choose the apps that this policy manages. For this tutorial we'll add only Microsoft Outlook:

   1. Ensure *Target policy to* is set to **Selected apps**.
   1. Choose **+ Select public apps** to open the *Select apps to target* pane. Then, from the list of Apps, select **Microsoft Outlook** to add it to the *Selected Apps* list. You can search for an app by Bundle ID or by name. Choose **Select** to save the app selection.

      :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/create-app-protection-policy.png" alt-text="Locate and add Microsoft Outlook as a public app for this policy.":::

      The *Select apps to target* pane closes and Microsoft Outlook now appears under *Public apps* on the Apps page.

      :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/add-outlook-to-app-protection-policy.png" alt-text="Select Outlook to add it to the Public apps list for this policy.":::

   Select **Next** to continue.

5. On the **Data protection** page, you configure the settings that determine how users can interact with data while using the apps that are protected by this app protection policy.​ Configure the following options:

   For the *Data Transfer* category, configure the following settings and leave all other settings at their default values:

   - **Send org data to other apps** - From the drop-down list, select **None**.
   - **Receive data from other apps** - From the drop-down list, select **None**.
   - **Restrict cut, copy and paste between other apps**- From the drop-down list, select **Blocked**.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png" alt-text="Select the Outlook app protection policy data relocation settings.":::

   Select **Next** to continue.

6. The **Access requirements** page provides settings to allow you to configure PIN and credential requirements that users must meet before they can access the protected apps in a work context. Configure the following settings, leaving all other settings at their default values:

   - For **PIN for access**, select **Require**.
   - For **Work or school account credentials for access**, select **Require**.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png" alt-text="Select the Outlook app protection policy access actions.":::

   Select **Next** to continue.

7. On the **Conditional launch** page, you configure the sign-in security requirements for this app protection policy. For this tutorial, you don't need to configure these settings.

   Select **Next** to continue.

8. The **Assignments** page is where you assign the app protection policy to groups of users. For this tutorial, we don't assign this policy to a group.

   Select **Next** to continue.

9. On the **Next: Review + create** page, review the values and settings you entered for this app protection policy. Select **Create** to create the app protection policy in Intune.

The app protection policy for Outlook is created. Next, you'll set up Conditional Access to require devices to use the Outlook app.

## Create Conditional Access policies

Next, use the Microsoft Intune admin center to create two Conditional Access policies to cover all device platforms. You integrate [Conditional Access with Intune](../protect/conditional-access-exchange-create.md) to help control the devices and apps that can connect to your organizations email and resources.

- The first policy requires that Modern Authentication clients use the approved Outlook app and multifactor authentication (MFA). Modern Authentication clients include Outlook for iOS and Outlook for Android.

- The second policy requires that Exchange ActiveSync clients use the approved Outlook app. (Currently, Exchange Active Sync doesn't support conditions other than device platform). You can configure Conditional Access policies in the Microsoft Entra admin center or use the Microsoft Intune admin center, which presents the Conditional Access UI from Microsoft Entra. Because we're already in the admin center, we can create the policy here.

When you configure Conditional Access policies in the Microsoft Intune admin center, you're really configuring those policies in the Conditional Access blades from the Azure portal. Therefore, the user interface is a bit different than the interface you use for other policies for Intune.

### Create a multi-factor authentication policy for Modern Authentication clients

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** >**Conditional Access** > **Create new policy**.

3. For **Name**, enter **Test policy for modern auth clients**.

4. Under **Assignments**, for *Users*, select **0 users and groups selected**. On the **Include** tab, select **All users**. The value for *Users* updates to *All users*.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/conditional-access-users.png" alt-text="Begin configuration of the Conditional Access policy.":::

5. Under **Assignments**, for *Target resources*, select **No target resources selected**. Ensure that *Select what this policy applies to* is set to **Cloud apps**. Because we want to protect Microsoft 365 Exchange Online email, select it by following these steps:

   1. On the **Include** tab, choose **Select apps**.
   2. For *Select*, click **None** to open the Cloud apps *Select* pane.
   3. From the list of applications, select the checkbox for **Office 365 Exchange Online**, and then choose **Select**.
   4. Select **Done** to return to the New policy pane.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png" alt-text="Select the Office 365 Exchange Online app.":::

6. Under **Assignments**, for *Conditions*, select **0 conditions selected**, and then for *Device platforms* select *Not configured* to open the Device platforms pane:

   1. Set the *Configure* toggle to **Yes**.
   2. On the **Include** tab, choose **Select device platforms**, and then select the checkboxes for **Android** and for **iOS**.
   3. Select **Done** to save the Device platforms configuration.

7. Remain on the *Conditions* pane, and select *Not configured* for *Client apps* to open the Client apps pane:

   1. Set the *Configure* toggle to **Yes**.
   2. Select the checkboxes for **Mobile apps and desktop clients**.
   3. Clear the other check boxes.
   4. Select **Done** to return to the New policy pane.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png" alt-text="Select Mobile apps and clients as conditions.":::

8. Under **Access controls**, for *Grant*, select **0 conditions selected**, and then:

   1. On the *Grant* pane, select **Grant access**.
   2. Select **Require multi-factor authentication**.
   3. Select **Require approved client app**.
   4. Set *For multiple controls* to **Require all the selected controls**. This setting ensures that both requirements you selected are enforced when a device tries to access email.
   5. Choose **Select** to save the Grant configuration.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png" alt-text="To configure Grant, select access controls.":::

9. Under **Enable policy**, select **On**, and then select **Create**.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png" alt-text="To enable policy, set the Enable policy slider to On.":::

The Conditional Access policy for Modern Authentication clients is created. Now you can create a policy for Exchange Active Sync clients.

### Create a policy for Exchange Active Sync clients

The process to configure this policy is similar to the previous Conditional Access policy:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Conditional Access** > **Create new policy**.

3. For **Name**, enter **Test policy for EAS clients**.

4. Under **Assignments**, for *Users*, select **0 users and groups**. On the *Include* tab, select **All users**.

5. Under **Assignments**, for *Target resources*, select *No target resources selected*. Ensure that *Select what this policy applies to* is set to **Cloud apps**, and then configure Microsoft 365 Exchange Online email with these steps:

   1. On the *Include* tab, choose **Select apps**.
   2. For *Select*, choose *None*.
   3. From the Cloud apps list, select the checkbox for **Office 365 Exchange Online**, and then choose **Select**.
  
6. Under **Assignments** open *Conditions* > *Device platforms*, and then:

   1. Set the *Configure* toggle to **Yes**.
   2. On the **Include** tab, select **Any device**, and then select **Done**.

7. Remain on the *Conditions* pan, expand **Client apps**, and then:

   1. Set the *Configure* toggle to **Yes**.
   2. Select **Mobile apps and desktop clients**.
   3. Select **Exchange ActiveSync clients**.
   4. Clear all other check boxes.
   5. Select **Done**.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png" alt-text="Configure client apps for the Conditions category.":::

8. Under **Access controls**, expand **Grant** and then:

   1. On the **Grant** pane, select **Grant access**.
   2. Select **Require approved client app**. Clear all other check boxes, but leave the configuration *For multiple controls* set to *Require all the selected controls*.
   3. Choose **Select**.

   :::image type="content" source="./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png" alt-text="configure Require approved client app for the Grant category.":::

9. Under **Enable policy**, select **On**, and then select **Create**.

Your app protection policies and Conditional Access are now in place and ready to test.

## Try it out

With the policies that you created in this tutorial, devices must enroll in Intune and use the Outlook mobile app before the device can be used to access Microsoft 365 email. To test this scenario on an iOS device, try signing in to Exchange Online using credentials for a user in your test tenant.

1. To test on an iPhone, go to **Settings** > **Passwords & Accounts** > **Add Account** > **Exchange**.

2. Enter the email address for a user in your test tenant, and then press **Next**.
3. Press **Sign In**.

4. Enter the test user's password, and press **Sign in**.

5. The message **More information is required** appears, which means you're being prompted to set up MFA. Go ahead and set up another verification method.

6. Next you'll see a message that says you're trying to open this resource with an app that isn't approved by your IT department. The message means you're being blocked from using the native mail app. Cancel the sign-in.

7. Open the Outlook app and select **Settings** > **Add Account** > **Add Email Account**.

8. Enter the email address for a user in your test tenant, and then press **Next**.

9. Press **Sign in with Office 365**. You'll be prompted for another authentication and registration. Once you've signed in, you can test actions such as cut, copy, paste, and *Save As*.

## Clean up resources

When the test policies are no longer needed, you can remove them.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance**.

3. In the **Policy name** list, select the context menu (**...**) for your test policy, and then select **Delete**. Select **OK** to confirm.

4. Go to **Endpoint security** > **Conditional Access** > Policies.

5. In the **Policy Name** list, select the context menu (**...**) for each of your test policies, and then select **Delete**. Select **Yes** to confirm.

## Next steps

In this tutorial, you created app protection policies to limit what the user can do with the Outlook app, and you created Conditional Access policies to require the Outlook app and require MFA for Modern Authentication clients. To learn more about using Intune with Conditional Access to protect other apps and services, see [Learn about Conditional Access and Intune](conditional-access.md).
