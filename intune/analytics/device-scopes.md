---
title: Device Scopes in Endpoint Analytics
description: Learn how to use device scopes in Microsoft Intune endpoint analytics with scope tags for custom device reporting and targeted insights.
ms.date: 10/09/2025
ms.topic: concept-article
---

# Device scopes in endpoint analytics

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

[!INCLUDE [advanced-analytics-overview](includes/advanced-analytics-overview.md)]

Custom device scopes use Scope tags to slice endpoint analytics reports to a subset of devices, allowing you to see scores, insights, and recommendations for a specific subset of your enrolled devices.

Custom device scopes are supported on the following endpoint analytics reports:

- [Startup performance](startup-performance.md)
- [Work from anywhere](work-from-anywhere.md)
- [Application reliability](app-reliability.md)
- [Battery health](battery-health.md)

## Permissions

Custom device scopes use Intune Scope tags, hence other permissions are required for some actions.
To create custom device scopes, a user must have the **Roles/Read** [role permission](../intune-service/fundamentals/create-custom-role.md#custom-role-permissions) and this permission is in the following built-in roles:

- Endpoint Security Manager

- Read Only Operator

- Help Desk Operator

- Intune Role Administrator

> [!NOTE]
> After custom device scopes are created, other users with access to endpoint analytics can use them.

## Create and manage custom device scopes

You can create and manage custom device scopes by using the **Manage device scopes** menu in endpoint analytics.

1. Navigate to a supported report within endpoint analytics, such as Startup performance, in the Intune admin center under **Reports** > **Endpoint analytics** > **Startup performance**.
2. Select **Device scope** menu.
3. Select **Manage device scopes** to open the flyout where you can create and modify your custom device scopes.

To create custom device scopes:

1. Open the **Manage device scopes** menu.
1. Select a Scope tag from the dropdown and select **Save**.
1. Give your new custom device scope a Name and select **OK**.

The new custom device scope appears in your list of saved device scopes. By default, custom devices scopes are in the *Off* state. To activate custom device scopes, toggle the **State** setting to *On*. Data processing starts for the selected device scope.

> [!NOTE]
> Once activated, custom device scopes can take up to 24 hours to process. During this period, custom device scopes that are still processing are not usable. Additionally, custom device scopes require 10 devices at minimum to populate supported reports. Otherwise **Insufficient Data** might show when trying to select a custom scope.

Only the user who created the custom device scopes or a Global administrator can delete the custom device scopes.

To delete custom device scopes:

1. Open the **Manage device scopes** menu.
2. Find the custom device scope you would like to delete and select the menu.
3. Select **Delete**.
4. Select **Yes** to confirm.

> [!IMPORTANT]
> If a custom device scope is associated with a Scope tag that gets deleted from your tenant, the custom device scope will no longer function. You see an error message in the **Manage device scopes** menu. Edit the impacted device scope to use a valid Scope tag or delete it to clear the error.

## Using custom device scopes

Custom device scopes can be used in any supported endpoint analytics report. To use a custom device scope:

1. Ensure that the device scope you would like to use is active.
2. Navigate to a supported report in endpoint analytics, such as **Startup performance**.
3. Select **Device scope** menu in the page.
4. From the dropdown menu, select your desired custom device scope.
5. Select **Apply**.

The page is automatically updated to show scores, data, and insights specific to the subset of devices defined by your chosen custom device scope. As you navigate through endpoint analytics, your chosen device scope remains selected on all supported reports and pages.

To return to viewing all devices, navigate to the **Device scope** menu, select **All Devices** from the dropdown menu, and select **Apply**.

## Limitations

- You can save up to 100 custom device scopes, and up to 20 can be active at a time.

- Only one Scope tag can be used to create a custom device scope. To create a custom device scope that includes devices from multiple Scope tags, you must create a new Scope tag and assign it to the full set of devices that you require.

---

## Next Steps

> [!div class="nextstepaction"]
> [Next: Learn about Enhanced Device Timeline >](enhanced-device-timeline.md)

---

For more information, go to:

- [Enhanced device timeline](enhanced-device-timeline.md)
- [Anomaly detection](anomaly-detection.md)
- [What is Intune Advanced Analytics](advanced-endpoint-analytics.md)
- [Battery health](battery-health.md)
- [Resource Performance report](resource-performance-report.md)
