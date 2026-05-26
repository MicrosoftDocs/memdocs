---
title: Set up an iOS/iPadOS ADE token in Intune
description: Create, renew, and delete Apple enrollment program tokens in Microsoft Intune for automated device enrollment on iOS/iPadOS.
ms.date: 04/15/2026
ms.topic: how-to
ms.reviewer: annovich
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Set up automated device enrollment token for Apple mobile  

An *enrollment program token* (sometimes called an automated device enrollment token) is a required component of Apple automated device enrollment (ADE). It creates the trust relationship between Microsoft Intune and Apple Business or Apple School Manager, and allows Intune to:

- Sync device information from your Apple enrollment program account.
- Upload enrollment policies to Apple.
- Assign devices to enrollment policies.

This article describes how to create, renew, and delete enrollment program tokens.

> [!NOTE]
> The steps in this article are the same whether you're using Apple Business or Apple School Manager. For brevity, this article refers to *Apple Business* only, except where clarification is necessary.  

This article applies to:  
- iOS/iPadOS
- tvOS
- visionOS  

## Create an enrollment program token

You need access to both the Microsoft Intune admin center and Apple Business to complete these steps. Keep both open in your browser throughout the process.  

## Scope tags  

For tvOS and visionOS devices, ADE enrollment policies inherit the scope tag assigned to the enrollment program token at the time the policy is created. Changes made later to the token’s scope tag aren’t reflected in existing tvOS or visionOS enrollment policies. To ensure correct RBAC visibility, assign the intended scope tag to your enrollment program token before creating enrollment policies for tvOS or visionOS devices.  

### Step 1: Download the Intune public key certificate

The public key certificate is needed to request a trust-relationship certificate from Apple Business.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
1. Select the **Apple mobile** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select **Add**.
1. Select **I agree** to give permission to Microsoft to send user and device information to Apple.
1. Select **Download the Intune public key certificate required to create the token**. This step downloads and saves the encryption key (.pem) file locally.

   > [!IMPORTANT]
   > Keep this browser tab open. If you close the tab, the certificate you downloaded is invalidated and you'll need to start over. The **Create** button on the **Review + create** tab won't be available if you close the tab.

### Step 2: Add an MDM server in Apple Business and download the server token

Add Intune as a mobile device management (MDM) server in Apple Business, and then download the server token.

1. In the admin center, select the link that corresponds with the Apple portal you use:
   - **Create a token via Apple Business**
   - **Create a token via Apple School Manager**

   The selected portal opens in a new browser tab. Switch to the new tab, but keep the Intune tab open.

1. Sign in to the Apple portal with your company Apple ID.

   > [!IMPORTANT]
   > Use your organization's Apple ID, not a personal one. You and your organization will need this Apple ID to renew and manage the token going forward.

1. Go to your account profile > **Preferences** > **MDM server assignments**.
1. Select the option to add an MDM server.
1. Enter a name for the MDM server. The name is for your reference in Apple Business and doesn't need to match the actual Microsoft Intune server name or URL.
1. Upload the public key (.pem) file you downloaded in Step 1, and then save your changes.
1. Download the server token (.p7m file).

### Step 3: Assign devices to the MDM server

After you create the MDM server in Apple Business, assign devices to it. You can do this now or come back later.

1. In Apple Business, go to **Devices**.
1. Select the devices you want to assign. You can sort by serial number and select multiple devices at once.
1. Select **Edit device management**, and then choose the MDM server you created.

For more information and steps, see [Assign, reassign, or unassign devices in Apple Business](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web).

### Step 4: Save the Apple ID

1. Return to the Intune admin center tab.
1. In the **Apple ID** field, enter the Apple ID used to download the server token.

   This ID is the Apple ID you'll need to renew the token each year. Make sure future Intune admins know which Apple ID was used, in case you leave your organization and need to transition token management.

   :::image type="content" source="./media/setup-automated-ios/image03.png" alt-text="Screenshot highlighting the Apple ID field in the Add enrollment program token pane.":::

### Step 5: Upload the server token and finish

1. In the **Apple token** field, browse to the server token (.p7m file) you downloaded from Apple Business.
1. Select **Open**, and then select **Create**.

Intune automatically connects with Apple Business to sync device information from your enrollment program account.

## Renew an enrollment program token  

Renew your enrollment program token yearly. The Intune admin center shows the token expiration date. Also renew the token in these situations:

- The Apple ID password changes for the user who set up the token in Apple Business.
- The user who set up the token in Apple Business leaves the organization.

> [!NOTE]
> Changing the Apple ID used to create the token doesn't affect currently enrolled devices until they re-enroll. This is unlike the Apple MDM Push Notification Service (APNS) certificate, which requires all devices to re-enroll if changed. 

For renewal steps, see [Manage ADE tokens and devices](manage-devices-tokens-apple.md).  
