---
title: Manage Apple mobile devices and tokens in Intune
description: Sync devices, distribute devices, and re-enroll devices for Apple automated device enrollment on iOS/iPadOS in Microsoft Intune.
ms.date: 04/15/2026
ms.topic: how-to
ms.reviewer: annovich
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
---

# Manage Apple mobile devices and tokens for automated device enrollment    

Use this article to sync Apple mobile devices with Apple Business, manage your enrollment tokens, and distribute devices to users.

> [!NOTE]
> The steps in this article are the same whether you're using Apple Business or Apple School Manager. For brevity, this article refers to *Apple Business* only, except where clarification is necessary.  

This article applies to:  
- iOS/iPadOS
- tvOS
- visionOS  

## Prerequisites

Before completing the tasks in this article:

- [Set up an Apple mobile automated device enrollment (ADE) token](setup-apple-token.md)  
- Create an enrollment profile and assign it to devices:
    - [Create enrollment profile for iOS/iPadOS](setup-automated-ios.md)
    - [Create enrollment profile for tvOS](setup-automated-tvos.md)
    - [Create enrollment profile for visionOS](setup-automated-visionos.md)

## Sync managed devices

Syncing refreshes existing device status and imports new devices assigned to the Apple MDM server. After creating a token, sync Intune with Apple to see your managed devices in the Microsoft Intune admin center.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.
1. Select the **Apple mobile** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select a token from the list.
1. Select **Devices** > **Sync**.

## Sync restrictions  

To comply with Apple's terms for acceptable enrollment program traffic, Microsoft Intune imposes the following restrictions:  

- A *full sync* can run no more than once every seven days. During a full sync, Intune fetches the complete, updated list of serial numbers assigned to the connected Apple MDM server.  

  > [!IMPORTANT]
  > If you delete a device from Intune but it remains assigned to the ADE token in Apple Business, the device reappears in Intune on the next full sync. If you don't want the device to reappear, unassign it from the Apple MDM server in Apple Business first.

- If a device is released from Apple Business, it can take up to 45 days for it to be automatically deleted from the **Devices** page in Intune. You can manually delete released devices one by one if needed. Released devices are reported as *removed* from Apple Business in Intune until they're automatically deleted within 30–45 days.  

- A delta sync runs automatically every 12 hours. You can also trigger a sync manually by selecting **Sync**, no more than once every 15 minutes. All sync requests have 15 minutes to finish. The **Sync** button becomes inactive until the sync completes.

- Apple Business and Apple School Manager sync approximately 3,000 devices to Intune per minute. If you have more than 200,000 devices per token, we recommend waiting for all devices to finish syncing before manually triggering another sync (total devices ÷ 3,000 devices per minute = estimated wait time).  

## Renew your token

1. Go to [Apple Business](http://business.apple.com) and sign in with an account that has an Administrator or Device Enrollment Manager role.
1. Select **Settings**. Under **MDM Servers**, select the MDM server associated with the token file you want to renew.
1. Select **Download Token**.

   > [!NOTE]
   > Don't select **Download Token** unless you intend to renew the token. Doing so invalidates the token currently in use by Intune. If you already downloaded the token, complete the remaining steps to finish the renewal.

1. After downloading the token, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Go to **Devices** > **Enrollment**.
1. Select the **Apple mobile** tab.
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
1. Select the **Apple mobile** tab.
1. Under **Bulk Enrollment Methods**, select **Enrollment program tokens**.
1. Select the token, and then select **Devices**.
1. Delete all devices assigned to the token.
1. Return to **Enrollment program tokens**. Select the token, and then select **Profiles**.
1. Delete all enrollment profiles listed, including any default profile.
1. Return to **Enrollment program tokens**. Select the token, and then select **Delete**.

## Limits  
If you exceed 200,000 devices per token, you might experience sync problems. Split devices across multiple ADE tokens instead.  

| Resource | Maximum |
|----------|---------|
| Enrollment profiles per token | 1,000 |
| ADE devices per profile | 200,000 |
| ADE tokens per Intune account | 2,000 |
| ADE devices per token | 200,000 |  

## Distribute devices

Users on devices enrolled with user affinity must have an Intune license assigned. Devices enrolled without user affinity need an Intune device license, unless an Intune-licensed user is associated with the device. For more information, see [Microsoft Intune licensing](../../fundamentals/licensing/index.md) and the [Intune planning guide](../../intune-service/fundamentals/intune-planning-guide.md).  

A device that is already activated needs to be wiped before it can enroll with automated device enrollment. After you wipe it but before activating it again, you can apply the enrollment profile. For more information, see [Set up an existing iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207516) (opens Apple support site).   

If you're enrolling with ADE and user affinity, the following error can happen during setup:  

`The SCEP server returned an invalid response.`

You can resolve this error by trying to download the management profile again within 15 minutes. After 15 minutes, you have to factory reset the device to resolve the error. This error occurs because of a 15-minute time limit on SCEP certificates, enforced for security.  

## End user experience

For information about the end user experience, see:
- [ADE end user tasks](guide-ios-ipados.md#ade-end-user-tasks)
- [Enroll your iOS/iPadOS device](../../user-help/enrollment/enroll-automated-ios.md)  
