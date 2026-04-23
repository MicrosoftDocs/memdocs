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

# Set up an iOS/iPadOS ADE token

*Applies to iOS/iPadOS*

An *enrollment program token* (sometimes called an automated device enrollment token) is a required component of Apple automated device enrollment (ADE). It creates the trust relationship between Microsoft Intune and Apple Business Manager or Apple School Manager, and allows Intune to:

- Sync device information from your Apple enrollment program account.
- Upload enrollment profiles to Apple.
- Assign devices to enrollment profiles.

This article describes how to create, renew, and delete enrollment program tokens.

> [!NOTE]
> The steps in this article are the same whether you're using Apple Business Manager or Apple School Manager. For brevity, this article refers to *Apple Business Manager* only, except where clarification is necessary.

## Create an enrollment program token

You need access to both the Microsoft Intune admin center and Apple Business Manager to complete these steps. Keep both open in your browser throughout the process.

### Step 1: Download the Intune public key certificate

The public key certificate is needed to request a trust-relationship certificate from Apple Business Manager.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
1. Select the **Apple** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select **Add**.
1. Select **I agree** to give permission to Microsoft to send user and device information to Apple.
1. Select **Download the Intune public key certificate required to create the token**. This step downloads and saves the encryption key (.pem) file locally.

   > [!IMPORTANT]
   > Keep this browser tab open. If you close the tab, the certificate you downloaded is invalidated and you'll need to start over. The **Create** button on the **Review + create** tab won't be available if you close the tab.

### Step 2: Add an MDM server in Apple Business Manager and download the server token

Add Intune as a mobile device management (MDM) server in Apple Business Manager, and then download the server token.

1. In the admin center, select the link that corresponds with the Apple portal you use:
   - **Create a token via Apple Business Manager**
   - **Create a token via Apple School Manager**

   The selected portal opens in a new browser tab. Switch to the new tab, but keep the Intune tab open.

1. Sign in to the Apple portal with your company Apple ID.

   > [!IMPORTANT]
   > Use your organization's Apple ID, not a personal one. You and your organization will need this Apple ID to renew and manage the token going forward.

1. Go to your account profile > **Preferences** > **MDM server assignments**.
1. Select the option to add an MDM server.
1. Enter a name for the MDM server. The name is for your reference in Apple Business Manager and doesn't need to match the actual Microsoft Intune server name or URL.
1. Upload the public key (.pem) file you downloaded in Step 1, and then save your changes.
1. Download the server token (.p7m file).

### Step 3: Assign devices to the MDM server

After you create the MDM server in Apple Business Manager, assign devices to it. You can do this now or come back later.

1. In Apple Business Manager, go to **Devices**.
1. Select the devices you want to assign. You can sort by serial number and select multiple devices at once.
1. Select **Edit device management**, and then choose the MDM server you created.

For more information and steps, see [Assign, reassign, or unassign devices in Apple Business Manager](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web).

### Step 4: Save the Apple ID

1. Return to the Intune admin center tab.
1. In the **Apple ID** field, enter the Apple ID used to download the server token.

   This ID is the Apple ID you'll need to renew the token each year. Make sure future Intune admins know which Apple ID was used, in case you leave your organization and need to transition token management.

   :::image type="content" source="./media/setup-automated-ios/image03.png" alt-text="Screenshot highlighting the Apple ID field in the Add enrollment program token pane.":::

### Step 5: Upload the server token and finish

1. In the **Apple token** field, browse to the server token (.p7m file) you downloaded from Apple Business Manager.
1. Select **Open**, and then select **Create**.

Intune automatically connects with Apple Business Manager to sync device information from your enrollment program account.

## Renew an enrollment program token  

Renew your enrollment program token yearly. The Intune admin center shows the token expiration date. Also renew the token in these situations:

- The Apple ID password changes for the user who set up the token in Apple Business Manager.
- The user who set up the token in Apple Business Manager leaves the organization.

> [!NOTE]
> Changing the Apple ID used to create the token doesn't affect currently enrolled devices until they re-enroll. This is unlike the Apple MDM Push Notification Service (APNS) certificate, which requires all devices to re-enroll if changed.

### Renew your token

1. Go to [Apple Business Manager](http://business.apple.com) and sign in with an account that has an Administrator or Device Enrollment Manager role.
1. Select **Settings**. Under **MDM Servers**, select the MDM server associated with the token file you want to renew.
1. Select **Download Token**.

   > [!NOTE]
   > Don't select **Download Token** unless you intend to renew the token. Doing so invalidates the token currently in use by Intune. If you already downloaded the token, complete the remaining steps to finish the renewal.

1. After downloading the token, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Go to **Devices** > **Enrollment**.
1. Select the **Apple** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select the token you want to renew.
1. Select **Renew token**. Enter the **Apple ID** used to create the original token.

   :::image type="content" source="./media/setup-automated-ios/renewtoken.png" alt-text="Screenshot showing the Renew token page." lightbox="./media/setup-automated-ios/renewtoken.png":::

1. Upload the newly downloaded token.
1. Select **Next**. Assign scope tags if needed.
1. Select **Renew token** and wait for confirmation that the renewal is complete.

   :::image type="content" source="./media/setup-automated-ios/confirmation.png" alt-text="Screenshot showing the token renewal confirmation message.":::

## Delete an enrollment program token

> [!WARNING]
> Deleting devices from a token (required before you can delete the token) removes those devices from Intune management. If the devices are still in use, users will lose access to corporate resources and apps managed by Intune. Wipe and re-enroll devices with a new token if you want to continue managing them.

You can delete an enrollment program token from Intune as long as:

- No devices are assigned to the token.
- No devices are assigned to the default profile.
- There are no enrollment profiles under that token.

To delete an enrollment program token:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
1. Select the **Apple** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select the token, and then select **Devices**.
1. Delete all devices assigned to the token.
1. Return to **Enrollment program tokens**. Select the token, and then select **Profiles**.
1. Delete all enrollment profiles listed, including any default profile.
1. Return to **Enrollment program tokens**. Select the token, and then select **Delete**.

## Next steps

- [Set up an enrollment profile for iOS/iPadOS](setup-automated-ios.md)
- [Manage iOS/iPadOS ADE devices and tokens](manage-devices-tokens-apple.md)