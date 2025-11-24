---
title: "Remote Device Action: Send Custom Notifications"
description: Use Intune to create and send custom notifications to users of iOS/iPadOS and Android devices.
ms.date: 10/27/2025
ms.topic: how-to
ms.reviewer: petermt
zone_pivot_groups: 22f7442d-9384-49c8-abff-aaa058b30589
---

# Remote device action: send custom notifications

Use the *send custom notifications* remote action in Intune to deliver short messages directly to users of managed devices. Notifications appear as standard push alerts from the Company Portal or Intune app, similar to messages from other mobile applications.

You can send notifications to individual devices or to users in groups. Custom notifications are useful for general communication, such as:

- Informing users of schedule changes, like building closures due to weather.
- Sending targeted messages to individual users, such as prompting a device restart to complete an update.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action is supported on the following platform:
>
> - Android Enterprise personally-owned work profile (BYOD)
> - iOS/iPadOS

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]


:::column-end:::
:::column span="3":::

::: zone pivot="android"

> To use this remote action, make sure devices meet the following requirements:
>
> - The Company Portal app or Microsoft Intune app is installed.
> - Push notification permissions for the apps are granted by the user.

::: zone-end
::: zone pivot="ios"

> To use this remote action, make sure devices meet the following requirements:
>
> - The Company Portal app is installed.
> - Push notification permissions for the app is granted by the user.

::: zone-end

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::

> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Send custom notifications**—to send notifications to devices
>   - The permission **Organization/Update**—to send notifications to groups
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

:::column-end:::
:::row-end:::

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
> Other apps might have access to the data in your custom notifications. Avoid using them for sensitive communications.

::: zone-end

### Send a custom notification to a single device

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Send Custom Notification**.
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
> Intune doesn't track sent custom notifications, and devices don't log receipt outside of the notification center. The message might appear in a temporary diagnostic log if the user requests support through the Company Portal or Intune app.

## User experience

::: zone pivot="ios"
When a custom notification is sent, users receive it as a push alert from the Company Portal on their enrolled device. The experience varies slightly depending on the app state.
:::row:::
:::column span="3":::
- Intune sends messages to the Company Portal app, which then generates the push notification. Users don't need to be signed in to the app, but the device must be enrolled by the targeted user.
- Delivery isn't guaranteed. Notifications might be delayed or not delivered at all, so they shouldn't be used for urgent communication.
- Users might still receive notifications even after being removed from a group or unenrolling a device. Similarly, users added to a group after a notification is sent might receive that previously sent message.
- Notification visibility depends on device settings. Messages might appear on the lock screen or within the app.
- If the app is open when the notification is received, it displays in-app rather than as a push notification. Users can view it by navigating to the **Notifications** tab and pulling to refresh.

:::column-end:::
:::column span="1":::
:::image type="content" source="images/ios-custom-notification.png" lightbox="images/ios-custom-notification.png" alt-text="Locked device iOS/iPadOS custom notification." border="false":::
:::column-end:::
:::row-end:::

::: zone-end

::: zone pivot="android"
When a custom notification is sent, users receive it as a push alert from the Company Portal or Intune app on their enrolled device. The experience varies slightly depending on platform and app state.
:::row:::
:::column span="3":::
- Intune sends messages to the user's Company Portal or Intune app, which then generates the push notification. Users don't need to be signed in to the app, but the device must be enrolled by the targeted user.
- Delivery isn't guaranteed. Notifications might be delayed or not delivered at all, so they shouldn't be used for urgent communication.
- Users might still receive notifications even after being removed from a group or unenrolling a device. Similarly, users added to a group after a notification is sent might receive that previously sent message.
- Notification visibility depends on device settings. Messages might appear on the lock screen or within the app.
- If the app is open when the notification is received, it displays in-app rather than as a push notification.

:::column-end:::
:::column span="1":::
:::image type="content" source="images/android-custom-notification.png" lightbox="images/android-custom-notification.png" alt-text="Locked device Android custom notification.":::

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
