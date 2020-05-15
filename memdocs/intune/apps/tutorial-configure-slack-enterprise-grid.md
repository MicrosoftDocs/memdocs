---
# required metadata

title: Tutorial - Configure Slack to use Intune for EMM and app configuration
titleSuffix: Microsoft Intune
description: In this tutorial you will configure Slack to use Intune for EMM and app configuration.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 55db37c5-0da7-4d9c-8027-525afb1c6349
Customer intent: As an Intune admin, I want to learn how to configure Slack to use Intune for EMM and app configuration..

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
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
> - Create app configuration policies to manage the Slack for EMM app on iOS/iPadOS and the Slack app for Android work profile devices.
> - Create Intune device compliance policies to set the conditions Android and iOS/iPadOS devices must meet to be considered compliant.

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites
You'll need a test tenant with the following subscriptions for this tutorial:
- Azure Active Directory Premium ([free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Intune subscription ([free trial](../fundamentals/free-trial-sign-up.md))

You will also need a [Slack Enterprise Grid](https://get.slack.help/hc/articles/360004150931-What-is-Slack-Enterprise-Grid-) plan.

## Configure your Slack Enterprise Grid plan
Turn on EMM for your Slack Enterprise Grid plan by following [Slack's instructions](https://get.slack.help/hc/articles/115002579426-Enable-Enterprise-Mobility-Management-for-your-org#step-2:-turn-on-emm) and [connect Azure Active Directory](https://docs.microsoft.com/azure/active-directory/saas-apps/slack-tutorial) as your Grid plan's identity provider (IDP).

## Sign in to Intune
Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global Administrator or an Intune Service Administrator. If you have created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Set up Slack for EMM on iOS devices
Add the iOS/iPadOS app Slack for EMM to your Intune tenant and create an app configuration policy to enable your organizations' iOS/iPadOS users to access Slack with Intune as an EMM provider.

### Add Slack for EMM to Intune
Add Slack for EMM as a managed iOS/iPadOS app in Intune and assign your Slack users. Apps are platform-specific, so you need to add a separate Intune app for your Slack users on Android devices.
1. In the admin center, select **Apps** > **All apps** > **Add**.
2. Under **App type**, select the **iOS** store app.
3. Select **Search the App Store**. Enter the search term "Slack for EMM" and select the app. Click **Select** in the **Search the App Store** pane.
4. Select **App information** and configure any changes as you see fit. Select **OK** to set your app information.
5. Click **Add**.
6. Select **Assignments**.
7. Click **Add group**. Depending on who you chose to be affected when you turned on EMM for Slack, under **Assignment type** you may wish to select:
    - **Available for enrolled devices** if you chose "All members (including guests)" OR
    - **Available with or without enrollment** if you chose "All members (excluding guests)" or "Optional".
8. Select **Included Groups** and under **Make this app available to all users** select **Yes**.
9. Click **OK**, and then click **OK** again to add the group.
10. Click **Save**.

### Add an app configuration policy for Slack for EMM
Add an app configuration policy for the Slack for EMM iOS/iPadOS. App configuration policies for managed devices are platform-specific, so you need to add a separate policy for your Slack users on Android devices.
1. In the admin center, select **Apps** > **App configuration policies** > **Add** > **Managed devices**.
2. In Name, enter 'Slack app configuration policy test'.
3. Under Device enrollment type, confirm **Managed devices** is set.
4. Under Platform, select **iOS**.
5. Select **Associated app**.
6. In the search bar, enter "Slack for EMM" and select the app.
7. Click **OK**, and then select **Configuration settings**. 
8. Select **OK**, and then select **Add**.
9. In the search bar, enter "Slack app configuration policy test" and select the policy you just added.
10. From Manage, select **Assignments**.
11. Under Assign to, select **All Users + All Devices**.
12. Click **Save**.

### (Optional) Create an iOS device compliance policy
Set up an Intune device compliance policy to set the conditions that a device must meet to be considered compliant. For this tutorial, we'll create a device compliance policy for iOS/iPadOS devices. Compliance policies are platform-specific, so you need to create a separate policy for your Slack users on Android devices.
1. In the admin center, select **Device compliance** > **Policies** > **Create Policy**.
2. In Name, enter "iOS compliance policy test".
3. In Description, enter "iOS compliance policy test".
4. Under Platform, select **iOS**.
5. Select **Device Health**. Next to Jailbroken devices, select **Block**, and then select **OK**.
6. Select **System Security** and enter Password settings. For this tutorial, select the following recommended settings:
    - For Require a password to unlock mobile devices, select **Require**.
    - For Simple passwords, select **Block**.
    - For Minimum password length, enter 4.
    - For Required password type, choose **Alphanumeric**.
    - For Maximum minutes after screen lock before password is required, choose **Immediately**.
    - For Password expiration (days), enter 41.
    - For Number of previous passwords to prevent reuse, enter 5.
7. Click **OK**, and then select **OK** again.
8. Click **Create**.

## Set up Slack on Android work profile devices
Add the Slack Managed Google Play app to your Intune tenant and create an app configuration policy to enable your organizations' Android users to access Slack with Intune as an EMM provider.

### Add Slack to Intune
Add Slack as a Managed Google play app in Intune and assign your Slack users. Apps are platform-specific, so you need to add a separate Intune app for your Slack users on iOS/iPadOS devices.
1. In Intune, select **Apps** > **All apps** > **Add**.
2. Under App type, select **Store app – Managed Google Play**.
3. Select **Managed Google Play - Approve**. Enter the search term "Slack for EMM" and select the app.
4. Select **Approve**.
5. In the search bar, enter "Slack" and select the app you just added.
6. From Manage, select **Assignments**.
7. Select **Add group**. Depending on who you chose to be affected when you turned on EMM for Slack, under **Assignment type** you may wish to select:
    - **Available for enrolled devices** if you chose "All members (including guests)" OR
    - **Available with or without enrollment** if you chose "All members (excluding guests)" or "Optional".
8. Select Included Groups and under Make this app available to all users select **Yes**.
9. Click **OK**, and then click **OK** again.
10. Click **Save**.

### Add an app configuration policy for Slack
Add an app configuration policy for Slack. App configuration policies for managed devices are platform-specific, so you need to add a separate policy for your Slack users on iOS/iPadOS devices.
1. In Intune, select **Apps** > **App configuration policies** > **Add**.
2. In Name, enter Slack app configuration policy test.
3. Under Device enrollment type, select **Managed devices**.
4. Under Platform, select **Android**.
5. Select **Associated app**.
6. In the search bar, enter "Slack" and select the app.
7. Select **OK**, and then select **Configuration settings**.
    - For information on configuration keys and their values, consult the documentation on the "Technical" tab of [Slack's AppConfig web page](https://www.appconfig.org/company/slack/).
8. Click **OK**, and then select **Add**.
9. In the search bar, enter "Slack app configuration policy test" and select the policy you just added.
10. From Manage, select **Assignments**.
11. Under Assign to, select **All Users + All Devices**.
12. Click **Save**.

### (Optional) Create an Android device compliance policy
Set up an Intune device compliance policy to set the conditions that a device must meet to be considered compliant. For this tutorial, we'll create a device compliance policy for Android devices. Compliance policies are platform-specific, so you need to create a separate policy for your Slack users on iOS/iPadOS devices.
1. In Intune, select **Device compliance** > **Policies** > **Create Policy**.
2. In Name, enter "Android compliance policy test".
3. In Description, enter "Android compliance policy test".
4. Under Platform, select **Android Enterprise**.
5. Under Profile type, select **Work profile**.
6. Select **Device Health**. Next to Rooted devices, select **Block**, and then select **OK**.
7. Select **System Security** and enter **Password settings**. For this tutorial, select the following recommended settings:
    - For Require a password to unlock mobile devices, select **Require**.
    - For Required password type, select **At least alphanumeric**.
    - For Minimum password length, enter 4.
    - For Maximum minutes after screen lock before password is required, choose **15 Minutes**.
    - For Password expiration (days), enter 41.
    - For Number of previous passwords to prevent reuse, enter 5.
8. Click **OK**, and then click **OK** again.
9. Click **Create**.

## Launch Slack

With the policies you've just created, any iOS/iPadOS or Android work profile devices that attempt to sign in to one of your workspaces will need to be Intune enrolled. To test this scenario, try launching Slack for EMM on an Intune enrolled iOS/iPadOS device or launching Slack on an Intune enrolled Android work profile device. 

## Next steps

In this tutorial:
- You set Intune as the Enterprise Mobility Management (EMM) provider on your Slack Enterprise Grid. 
- You created app configuration policies to manage the Slack for EMM app on iOS/iPadOS and the Slack app for Android work profile devices.
- You created Intune device compliance policies to set the conditions Android and iOS/iPadOS devices must meet to be considered compliant.

To learn more about app configuration policies, see [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md). To learn more about device compliance policies, see [Set rules on devices to allow access to resources in your organization using Intune](../protect/device-compliance-get-started.md).
