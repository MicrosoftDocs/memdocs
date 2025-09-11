---
title: "Intune Remote Actions: Send Custom Notifications"
description: Use Intune to create and send custom notifications to users of iOS/iPadOS and Android devices.
ms.date: 08/27/2025
ms.topic: how-to

ms.reviewer: petermt
ms.custom: intune-azure

ms.collection:
- tier2
- M365-identity-device-management

zone_pivot_groups: 22f7442d-9384-49c8-abff-aaa058b30589
---

# Send custom notifications in Intune


Use the **Send custom notifications** remote action in Intune to deliver short messages directly to users of managed devices. Notifications appear as standard push alerts from the Company Portal or Intune app, similar to messages from other mobile applications.

You can send notifications to individual devices or to users in groups. Custom notifications are useful for general communication, such as:

- Informing users of schedule changes, like building closures due to weather.
- Sending targeted messages to individual users, such as prompting a device restart to complete an update.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platform:
>
> - Android Enterprise personally-owned work profile (BYOD)
> - iOS/iPadOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, you must use an account that has at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Send custom notifications**—to send notifications to devices
>   - The permission **Organization/Update**—to send notifications to groups
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

### :::image type="icon" source="../media/icons/headers/config.svg" border="false"::: Device configuration

> [!div class="checklist"]
> For users to receive notifications, the following requirements must be met:
>
> - Devices must be enrolled in Intune.
> - The Company Portal app or the Microsoft Intune app must be installed.
> - Users must have granted permission for the apps to send push notifications.

## How to send custom notifications from the Intune admin center

You can send custom notifications in Intune to individual devices or to users in groups. Keep the following limitations and behaviors in mind:

- When targeting groups, notifications are sent to the users in the group—not the devices. Each supported device enrolled by the user receives the message.
- You can target up to 25 groups per notification. Nested groups don't count toward this limit.
- You can send up to 25 group-targeted notifications per hour. This limit applies at the tenant level.
- When sending to individual devices, you can send up to 10 notifications per hour to the same device.
- Intune doesn't store previously sent notification text. To resend a message, you must recreate it.
- Intune doesn't track sent custom notifications, and devices don't log receipt outside of the device's notification center. The notification might appear in a temporary diagnostic log if the user requests support through the Company Portal or Intune app.

::: zone pivot="android"

> [!CAUTION]
> Other apps may have access to the data in your custom notifications. Avoid using them for sensitive communications.

::: zone-end

### Send a custom notification to a single device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, locate the row of remote action icons. Select **Send Custom Notification**.
1. On the **Send Custom Notification** pane, specify the following message details:
   - **Title**: Specify a title for this notification. Titles are limited to 50 characters.
   - **Body**: Specify the message. Messages are limited to 500 characters.
1. Select **Send** to send the custom notification to the device. Unlike notifications you send to groups, you don't configure an assignment or review the message before sending it.

Intune processes the message immediately. The only confirmation is a notification in the admin center showing the message content.

### Send a custom notification to a group

Group notifications target users, not devices. Each supported device enrolled by the user receives the message. Devices that are member of the group are ignored.

1. In the [Microsoft Intune admin center][INT-AC], select **Tenant administration** > **Custom notifications**.
1. On the **Basics** tab, specify the following, and then select **Next** to continue.
   - **Title**: Specify a title for this notification. Titles are limited to 50 characters.
   - **Body**: Specify the message. Messages are limited to 500 characters.
1. On the **Assignments** tab, select the groups to which you'd like to send this custom notification, and then select **Next** to continue.
1. On the **Review + Create** tab, review the information and when ready to send the notification, select **Create**.

Intune processes the message immediately. A confirmation appears in the admin center once the notification is sent.

> [!NOTE]
> Intune doesn't track sent custom notifications, and devices don't log receipt outside of the notification center. The message might appear in a temporary diagnostic log if the user requests support through the Company Portal or Intune app.2. Select the device from the list.

## User experience

When a custom notification is sent, users receive it as a push alert from the Company Portal or Intune app on their enrolled device. The experience varies slightly depending on platform and app state.

- Intune sends messages to the user's Company Portal or Intune app, which then generates the push notification. Users don't need to be signed in to the app, but the device must be enrolled by the targeted user.
- Delivery isn't guaranteed. Notifications might be delayed or not delivered at all, so they shouldn't be used for urgent communication.
- Users might still receive notifications even after being removed from a group or unenrolling a device. Similarly, users added to a group after a notification is sent might receive that previously sent message.
- Notification visibility depends on device settings. Messages might appear on the lock screen or within the app.

::: zone pivot="ios"

:::row:::
:::column span="2":::
If the app is open when the notification is received, it displays in-app rather than as a push notification. Users can view it by navigating to the **Notifications** tab and pulling to refresh.

If the device is locked, the notification resembles the following screenshot:
:::column-end:::
:::column span="2":::
:::image type="content" source="images/ios-custom-notification.png" alt-text="Locked device iOS/iPadOS custom notification." border="false":::
:::column-end:::
:::row-end:::

::: zone-end

::: zone pivot="android"

:::row:::
:::column span="2":::
If the app is open when the notification is received, it displays in-app rather than as a push notification. Users can view it by navigating to the **Notifications** tab and pulling to refresh.

If the device is locked, the notification resembles the following screenshot:
:::column-end:::
:::column span="2":::
:::image type="content" source="images/android-custom-notification.png" alt-text="Locked device Android custom notification.":::

:::column-end:::
:::row-end:::

::: zone-end

## Reference links

- Microsoft Graph API: [sendCustomNotificationToCompanyPortal action][GRAPH-1]

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator

[GRAPH-1]: /graph/api/intune-devices-manageddevice-sendcustomnotificationtocompanyportal
