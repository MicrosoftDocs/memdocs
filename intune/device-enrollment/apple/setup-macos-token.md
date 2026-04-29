---
title: Set up a macOS ADE token in Intune
description: Create, renew, and delete Apple enrollment program tokens for macOS automated device enrollment in Microsoft Intune.
ms.date: 04/15/2026
ms.topic: how-to
ms.reviewer: beflamm
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Set up a macOS ADE token

*Applies to macOS*

An *enrollment program token* (sometimes called an automated device enrollment token) is a required component of Apple automated device enrollment (ADE) for macOS. It creates the trust relationship between Microsoft Intune and Apple Business or Apple School Manager, and allows Intune to:

- Sync device information from your Apple enrollment program account.
- Upload enrollment policies to Apple.
- Assign devices to enrollment policies.

This article describes how to create, renew, and delete enrollment program tokens for macOS.

> [!NOTE]
> The steps in this article are the same whether you're using Apple Business or Apple School Manager. For brevity, this article refers to *Apple Business* only, except where clarification is necessary.

## Create an enrollment program token

### Step 1: Download the Intune public key certificate

The public key certificate is needed to request a trust-relationship certificate from Apple Business.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
1. Select the **Apple** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select **Add**.
1. Select **I agree** to grant permission to Microsoft to send user and device information to Apple.
1. Select **Download your public key** and save the key as a PEM file locally. The key is used to get the MDM server token in the next step.

   > [!IMPORTANT]
   > Keep this browser tab open. If you close the tab, the certificate you downloaded is invalidated and you'll need to start over.

### Step 2: Add an MDM server in Apple Business and download the server token

Add Intune as a mobile device management (MDM) server in Apple Business, and then download the server token.

1. In the admin center, select the link that corresponds with the Apple portal you use:
   - **Create a token via Apple Business**
   - **Create a token via Apple School Manager**

   The selected portal opens in a new browser tab. Switch to the new tab, but keep the Intune tab open.

1. Sign in to the Apple portal with your company Apple ID.

   > [!IMPORTANT]
   > Use your organization's Apple ID, not a personal one. You and your organization will need this Apple ID to renew and manage the token going forward.

1. Go to your account profile > **Preferences**.
1. Go to your MDM server assignments.
1. Select the option to add an MDM server.
1. Name the MDM server. The name is for identification purposes in Apple Business and doesn't have to match the actual Microsoft Intune server name or URL.
1. Upload your public key (.pem) file, and then save your changes.
1. Download the server token (.p7m file).

### Step 3: Assign devices to the MDM server

After you create the MDM server in Apple Business, assign devices to it. You can do this now or come back later.

We recommend assigning devices now since you're already in Apple Business. You can use available features like *filters* and *bulk assignment* to simplify selection. For more information and steps, see [Assign, reassign, or unassign devices in Apple Business](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web).

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

1. Sign in to [Apple Business](http://business.apple.com) with an account that has an Administrator or Device Enrollment Manager role.
1. Select **Settings**. Under **MDM Servers**, select the MDM server associated with the token file you want to renew.
1. Select **Download Token**.

   > [!NOTE]
   > Don't select **Download Server Token** unless you intend to renew the token. Doing so invalidates the token currently in use by Intune. If you already downloaded the token, complete the remaining steps to finish the renewal.

1. After downloading the token, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Go to **Devices** > **Enrollment**.
1. Select the **Apple** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select the token you want to renew.
1. Select **Renew token**. Enter the **Apple ID** used to create the original token.
1. Upload the newly downloaded token.
1. Select **Next**. Assign scope tags if needed.
1. Select **Create** to save your changes.

## Delete an enrollment program token

> [!WARNING]
> Deleting devices from a token (required before you can delete the token) removes those devices from Intune management. If the devices are still in use, users will lose access to corporate resources and apps managed by Intune. Wipe and re-enroll devices with a new token if you want to continue managing them.

You can delete an enrollment program token from Intune as long as:

- No devices are assigned to the token.
- No devices are assigned to the default profile.
- There are no enrollment policies under that token.

To delete an enrollment program token:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
1. Select the **Apple** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select the token, and then select **Devices**.
1. Delete all devices assigned to the token.
1. Return to **Enrollment program tokens**. Select the token, and then select **Profiles**.
1. Delete all enrollment policies listed, including any default profile.
1. Return to **Enrollment program tokens**. Select the token, and then select **Delete**.

## Next steps

- [Set up an enrollment policy for macOS](setup-automated-macos.md)
- [Manage macOS ADE devices and tokens](manage-devices-tokens-macos.md)
