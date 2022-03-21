---
# required metadata

title: Tutorial - Configure Slack to use Intune for EMM and app configuration
titleSuffix: Microsoft Intune
description: In this tutorial you will configure Slack to use Intune for EMM and app configuration.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 55db37c5-0da7-4d9c-8027-525afb1c6349
Customer intent: As an Intune admin, I want to learn how to configure Slack to use Intune for EMM and app configuration..

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Tutorial: Configure Slack to use Intune for EMM and app configuration

Slack is a collaboration app that you can use with Microsoft Intune.   

In this tutorial, you will:
> [!div class="checklist"]
> - Set Intune as the Enterprise Mobility Management (EMM) provider on your Slack Enterprise Grid. You'll be able to limit access to your Grid plan's workspaces to Intune managed devices.
> - Create app configuration policies to manage the Slack for EMM app on iOS/iPadOS and the Slack app for Android personally-owned work profile devices.
> - Create Intune device compliance policies to set the conditions Android and iOS/iPadOS devices must meet to be considered compliant.

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites
You'll need a test tenant with the following subscriptions for this tutorial:
- Azure Active Directory Premium ([free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Intune subscription ([free trial](../fundamentals/free-trial-sign-up.md))

You will also need a [Slack Enterprise Grid](https://get.slack.help/hc/articles/360004150931-What-is-Slack-Enterprise-Grid-) plan.

## Configure your Slack Enterprise Grid plan
Turn on EMM for your Slack Enterprise Grid plan by following [Slack's instructions](https://get.slack.help/hc/articles/115002579426-Enable-Enterprise-Mobility-Management-for-your-org#step-2:-turn-on-emm) and [connect Azure Active Directory](/azure/active-directory/saas-apps/slack-tutorial) as your Grid plan's identity provider (IDP).

## Sign in to Intune
Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global Administrator or an Intune Service Administrator. If you have created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Set up Slack for EMM on iOS devices
Add the iOS/iPadOS app Slack for EMM to your Intune tenant and create an app configuration policy to enable your organizations' iOS/iPadOS users to access Slack with Intune as an EMM provider.

### Add the iOS/iPadOS Slack for EMM app to Intune
Add Slack for EMM as a managed iOS/iPadOS app in Intune and assign your Slack users. Apps are platform-specific, so you need to add a separate Intune app for your Slack users on Android devices.
1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**.
2. Under **App type**, choose **iOS store app** and click **Select**.
3. Click **Search the App Store**. Enter the search term "Slack for EMM" and select the app. Click **Select** in the **Search the App Store** pane.
4. In the **App information** step, configure any changes as you see fit. Select **Next** to set your app information.
5. In the **Assignments** step, click **Add group** under the **Required** section. Select one or more groups to assign the app to. When complete, click **Next** to continue. 
6. In the **Review + create** step, click **Create** once you have verified the app details. 

### Add an iOS/iPadOS app configuration policy for the Slack for EMM app
Add an app configuration policy for the iOS/iPadOS Slack for EMM app.
    > [!NOTE]
    > App configuration policies for managed devices are platform-specific, so you need to add a separate policy for your Slack users on Android devices.
1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add** > **Managed devices**.
2. For **Name**, enter "Slack app configuration policy test".
3. For **Device enrollment type**, confirm **Managed devices** is set.
4. For **Platform**, select **iOS/iPadOS**.
5. For **Targeted app**, click **Select app**. The **Associated app** pane is displayed.
6. In the search bar, enter "Slack for EMM" and select the app. Click **OK** > **Next**.
7. In the **Settings** step, set the **Configuration settings format** to **Use configuration designer**. 
8. Add `OrgDomain` as the **Configuration key**. Set the **Value type** to **String** and set the **Configuration value** to `Y`. 
    > [!NOTE]
    > The `OrgDomain` configuration key provides the ability to enter your organization’s URL domain to help users sign in. 
9. Click **Next**.
10. In the **Assignments** step, click **All Users**. Then, click **Next**.
11. In the **Review + create** step, click **Create** to create the configuration policy.

### (Optional) Create an iOS device compliance policy
Set up an Intune device compliance policy to set the conditions that a device must meet to be considered compliant. For this tutorial, we'll create a device compliance policy for iOS/iPadOS devices. Compliance policies are platform-specific, so you need to create a separate policy for your Slack users on Android devices.
1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Compliance policies** > **Policies** > **Create Policy**.
2. Select **iOS/iPadOS** as the **Platform**. Then, click **Create**.
3. In the **Basics** step, enter "iOS compliance policy test" as the **Name** and click **Next**.
4. In the **Compliance settings**, under **Device Health** and next to **Jailbroken devices**, select **Block**.
5. Under **System Security** for this tutorial, select the following settings:
    - For **Require a password to unlock mobile devices**, select **Require**.
    - For **Simple passwords**, select **Block**.
    - For **Minimum password length**, enter `4`.
    - For **Required password type**, choose **Alphanumeric**.
    - For **Maximum minutes after screen lock before password is required**, choose **Immediately**.
    - For **Password expiration (days)**, enter `41`.
    - For **Number of previous passwords to prevent reuse**, enter `5`.
6. Click **Next**, and then select **Next** again.
7. In the **Assignments** step, click **Add all users**. Then, click **Next**.
8. In the **Review + create** step, click **Create** to create the compliance policy.

## Set up Slack on Android personally-owned work profile devices
Add the Slack Managed Google Play app to your Intune tenant and create an app configuration policy to enable your organizations' Android users to access Slack with Intune as an EMM provider.

### Add the Android Slack app to Intune
Add Slack as a Managed Google Play app in Intune and assign your Slack users. Apps are platform-specific, so you need to add a separate Intune app for your Slack users on iOS/iPadOS devices.
1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**.
2. Under **App type**, choose **Managed Google Play app** and click **Select**.
3. In the **Search** box, enter the search term "Slack" and select the app. Click **Approve** in the **Manage Google Play** pane. Click **Approve** to also approve permissions of the app. After verifying the app's approval settings, click **Done**. Click **Select**.
4. On the **All apps** pane, click **Refresh** to update the app list. Then, click the newly added **Slack** app.
5. Next to **Assignments**, click **Edit**.
6. configure any changes as you see fit. Select **Next** to set your app information.
7. Click **Add group** under the **Required** section. Select one or more groups to assign the app to. When complete, click **Review + save**. 
8. In the **Review + save** step, click **Save** once you have verified the app details. 

### Add an Android app configuration policy for Slack
Add an app configuration policy for Slack. App configuration policies for managed devices are platform-specific, so you need to add a separate policy for your Slack users on iOS/iPadOS devices.
1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add** > **Managed devices**.
2. For **Name**, enter "Slack app configuration policy test".
3. For **Device enrollment type**, confirm **Managed devices** is set.
4. For **Platform**, select **Android Enterprise**.
5. For **Profile Type**, select **Personally-Owned Work Profile Only**.
6. For **Targeted app**, click **Select app**. The **Associated app** pane is displayed.
7. In the search bar, enter "Slack" and select the Manged Google Play store app. Click **OK** > **Next**.
8. In the **Settings** step, set the **Configuration settings format** to **Use configuration designer**. 
9. Add `Slack Enterprise Grid Domain URL` as the **Configuration key**.  Click **OK**.
    > [!NOTE]
    > The `Slack Enterprise Grid Domain URL` configuration key provides the ability to enter your organization’s URL domain to help users sign in. 
10. Click **Next**.
11. In the **Assignments** step, click **Add all users**. Then, click **Next**.
12. In the **Review + create** step, click **Create** to create the configuration policy.

### (Optional) Create an Android device compliance policy
Set up an Intune device compliance policy to set the conditions that a device must meet to be considered compliant. For this tutorial, we'll create a device compliance policy for Android devices. Compliance policies are platform-specific, so you need to create a separate policy for your Slack users on iOS/iPadOS devices.
1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Compliance policies** > **Policies** > **Create Policy**.
2. Select **Android Enterprise** as the **Platform** and select **Personally-owned work profile** as the **Profile type**. Then, click **Create**.
3. In the **Basics** step, enter "Android Enterprise compliance policy test" as the **Name** and click **Next**.
4. In the **Compliance settings**, under **Device Health** and next to **Rooted devices**, select **Block**.
5. Under **System Security** for this tutorial, select the following settings:
    - For **Require a password to unlock mobile devices**, select **Require**.
    - For **Required password type**, choose **At least alphanumeric**.
    - For **Minimum password length**, enter `4`. 
    - For **Number of days until password expires**, enter `41`.
    - For **Number of previous passwords to prevent reuse**, enter `5`.
    - For **Maximum minutes of inactivity before password is required**, choose **15 Minutes**.
6. Click **Next**, and then select **Next** again.
7. In the **Assignments** step, click **Add all users**. Then, click **Next**.
8. In the **Review + create** step, click **Create** to create the compliance policy.

## Launch Slack

With the policies you've just created, any iOS/iPadOS or Android personally-owned work profile devices that attempt to sign in to one of your workspaces will need to be Intune enrolled. To test this scenario, try launching Slack for EMM on an Intune enrolled iOS/iPadOS device or launching Slack on an Intune enrolled Android personally-owned work profile device. 

## Next steps

In this tutorial:
- You set Intune as the Enterprise Mobility Management (EMM) provider on your Slack Enterprise Grid. 
- You created app configuration policies to manage the Slack for EMM app on iOS/iPadOS and the Slack app for Android personally-owned work profile devices.
- You created Intune device compliance policies to set the conditions Android and iOS/iPadOS devices must meet to be considered compliant.

To learn more about app configuration policies, see [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md). To learn more about device compliance policies, see [Set rules on devices to allow access to resources in your organization using Intune](../protect/device-compliance-get-started.md).