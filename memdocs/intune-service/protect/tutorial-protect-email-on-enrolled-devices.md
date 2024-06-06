---
# required metadata

title: Tutorial - Protect Exchange Online email on managed devices
titleSuffix: Microsoft Intune
description: Learn to secure Exchange Online with iOS Intune compliance policies and Microsoft Entra Conditional Access to require managed devices and the Outlook app.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/16/2023
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
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Tutorial: Protect Exchange Online email on managed devices with Microsoft Intune

This tutorial demonstrates how to use Microsoft device compliance policies with Microsoft Entra conditional access policy, to allow iOS devices access to Exchange  only when they're managed by Intune and use an approved email app.

In this tutorial, you'll learn how to:

> [!div class="checklist"]
> * Create an Intune iOS device compliance policy to set the conditions that a device must meet to be considered compliant.
> * Create a Microsoft Entra Conditional Access policy that requires iOS devices to enroll in Intune, comply with Intune policies, and use the approved Outlook mobile app to access Exchange Online email.


## Prerequisites

You need a test tenant with the following subscriptions for this tutorial:

- Microsoft Intune Plan 1 subscription ([sign up for a free trial account](../fundamentals/free-trial-sign-up.md))
- Microsoft Entra ID P1 ([free trial](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Microsoft 365 Apps for business subscription that includes Exchange ([free trial](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## Sign in to Intune

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a [Global administrator](../fundamentals/users-add.md#types-of-administrators) or an Intune [Service administrator](../fundamentals/users-add.md#types-of-administrators). If you have an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Create an email device profile

This tutorial requires you to create an iOS/iPadOS device Email profile. TO do so, follow the guidance in [Step 11 – Create a device profile](../configuration/quickstart-email-profile.md) from the *Try Intune tasks* area of the Intune documentation. The email profile is used to require iOS/iPad devices to use work email.

When you create the email profile, assign the profile to the same group of devices that you use later for the *device compliance* policy and *Conditional Access* policies that you create in subsequent steps of this tutorial.

After you create the email profile, return here to continue.

## Create the iOS device compliance policy

Set up an Intune device compliance policy to set the conditions that a device must meet to be considered compliant. For this tutorial, we create a device compliance policy for iOS devices. Compliance policies are platform-specific, so you need a separate compliance policy for each device platform you want to evaluate.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance**.  
3. On the **Policies** tab, choose **Create policy**. 
4. On the *Create a policy* page, for *Platform* select **iOS/iPadOS**. Select **Create** to continue.  

5. On the **Basics** tab, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile. For this example,  enter **iOS compliance policy test**.
   - **Description**: Optional - Enter **iOS compliance policy test**.

   Select **Next** to continue.

6. On the **Compliance settings** tab:

   1. Expand *Email*, and then set **Unable to set up email on the device** to **Require**.
   1. Expand *Device Health*, and set **Jailbroken** devices to **Block**.
   1. Expand *System Security*, and configure the following settings:

      - **Require a password to unlock mobile devices** to **Require**
      - **Simple passwords** to **Block**
      - **Minimum password length** to **4**

      > [!TIP]
      >
      > Default values that are grayed out and italicized are only recommendations. You must replace values that are recommendations to configure a setting.

      - **Required password type** to **Alphanumeric**
      - **Maximum minutes after screen lock before password is required** to **Immediately**
      - **Password expiration (days)** to **41**
      - **Number of previous passwords to prevent reuse** to **5**

   To continue, select **Next**.

   :::image type="content" source="./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-system-security.png" alt-text="Configureation of the iOS compliance policy.":::

7. Select **Next** to skip **Actions for noncompliance**.

8. On the **Assignments** tab, for *Included groups*, select **Add all devices**, or select a group that contains only those devices that should receive this policy. Be sure to use the same assignment as you used for the [email device profile](#create-an-email-device-profile).

   Select **Next** to continue.

9. On the **Review + create** tab, review your settings. When you select **Create**, your changes are saved, and the profile is assigned.

## Create the Conditional Access policy

Next, use the Microsoft Intune admin center to create a Conditional Access policy. You integrate [Conditional Access with Intune](../protect/conditional-access-exchange-create.md) to help control the devices and apps that can connect to your organizations email and resources.

The Conditional Access policy will:

- Require devices that run any platform to enroll in Intune and to comply with your Intune compliance policy before those devices can be used to access Exchange Online.
- Require devices use the Outlook app for email access.

Conditional Access policies are configurable in either the Microsoft Entra admin center or the Microsoft Intune admin center. Since we're already in the admin center, we can create the policy here.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Conditional Access** > **Create new policy**.

3. For **Name**, enter **Test policy for Microsoft 365 email**.

4. Under **Assignments**, for *Users*, select **0 users and groups selected**. On the **Include** tab, select **All users**. The value for *Users* updates to *All users*.

5. Also under **Assignments**, select **Target resources**. For *Select what this policy applies to* drop-down, select **Cloud apps**.

   Next, because we want to protect *Microsoft 365 Exchange Online* email, select that app by following these steps:

   1. On the **Include** tab, choose **Select apps**.
   2. For the **Select** category, select **None** to open the *Select* pane with its applications list.
   3. From the applications list, select the checkbox for **Office 365 Exchange Online**, and then choose **Select**.

   :::image type="content" source="./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-apps.png" alt-text="Select Office 365 Exchange Online.":::

6. Also under **Assignments**, select **Conditions** > **Device platforms** to open the *Device platforms* pane.
   1. Set **Configure** to **Yes**.
   2. On the **Include** tab, select **Any device**, and then select **Done**.

   :::image type="content" source="./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-device-platforms.png" alt-text="Configure the device platforms":::

7. Once again, under **Assignments**, select **Conditions** > **Client apps**.

   1. Set **Configure** to **Yes**.

   2. For this tutorial, select **Mobile apps and desktop clients**, part of *Modern authentication clients* (which refers to apps like Outlook for iOS and Outlook for Android). Clear all other check boxes.

   3. Select **Done**, and then select **Done** again.

   :::image type="content" source="./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-client-apps.png" alt-text="Select apps and clients.":::
 
8. Under **Access controls**, select **Grant**.

   1. On the **Grant** pane, select **Grant access**.

   2. Select **Require device to be marked as compliant**.

   3. Select **Require approved client app**.

   4. Under **For multiple controls**, select **Require all the selected controls**. This setting ensures that both requirements you selected are enforced when a device tries to access email.

   5. Choose **Select**.

   :::image type="content" source="./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-grant-access.png" alt-text="Select controls":::

9. Under **Enable policy**, select **On**.

   :::image type="content" source="./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-enable-policy.png" alt-text="Enable policy.":::

10. Select **Create** to save your changes. The profile is assigned.

## Try it out

With the policies you've created, any iOS device that attempts to sign in to Microsoft 365 email must enroll in Intune and use the Outlook mobile app for iOS/iPadOS. To test this scenario on an iOS device, try signing in to Exchange Online using credentials for a user in your test tenant. You're prompted to enroll the device and install the Outlook mobile app.

1. To test on an iPhone, go to **Settings** > **Passwords & Accounts** > **Add Account** > **Exchange**.

2. Enter the email address for a user in your test tenant, and then press **Next**.

3. Press **Sign In**.

4. Enter the test user's password, and press **Sign in**.

5. A message appears that says your device must be managed to access the resource, along with an option to enroll.

## Clean up resources

When the test policies are no longer needed, you can remove them.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global Administrator or an Intune Service Administrator.

2. Select **Devices** > **Compliance**.

3. In the **Policy name** list, select the context menu (**...**) for your test policy, and then select **Delete**. Select **OK** to confirm.

4. Select **Endpoint security** > **Conditional access** > **policies**. 

5. In the **Policy name** list, select the context menu (**...**) for your test policy, and then select **Delete**. Select **Yes** to confirm.

## Next steps

In this tutorial, you created policies that require iOS devices to enroll in Intune and use the Outlook app to access Exchange Online email. To learn about using Intune with Conditional Access to protect other apps and services, including Exchange ActiveSync clients for Microsoft 365 Exchange Online, see [Set up Conditional Access](conditional-access.md).
