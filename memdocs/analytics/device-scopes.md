---
title: Device scopes in Endpoint Analytics
titleSuffix: Microsoft Endpoint Manager
description: Learn about Device scopes as an advanced feature in Endpoint Analytics
ms.date: 02/22/2023
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---
# Device scopes in Endpoint Analytics

> [!NOTE]
> This capability is available as an Intune add-on. For more information, see [Intune add-ons](../intune/fundamentals/intune-add-ons.md).

Custom device scopes use Scope tags to slice Endpoint analytics reports to a subset of devices, allowing you to see scores, insights, and recommendations for a specific subset of your enrolled devices.

Custom device scopes are supported on the following Endpoint analytics reports:

- [Startup performance](startup-performance.md)

- [Work from anywhere](work-from-anywhere.md)

- [Application reliability](app-reliability.md)

## Permissions  

Custom device scopes use Intune Scope tags, hence other permissions are required for some actions. 
To create custom device scopes, a user must have the **Roles/Read** [role permission](../intune/fundamentals/create-custom-role.md#custom-role-permissions) and this permission is in the following built-in roles:

- Endpoint Security Manager

- Read Only Operator

- Help Desk Operator

- Intune Role Administrator  

> [!NOTE]
> After custom device scopes are created, they can be used by other users who have access to Endpoint analytics.

## Create and manage custom device scopes 

You can create and manage custom device scopes by using the **Manage device scopes** menu in Endpoint analytics.  

1. Navigate to a supported report within Endpoint analytics, such as Startup performance, in the Intune admin center under **Reports** > **Endpoint analytics** > **Startup performance**.
2. Select **Device scope** menu.  
3. Select **Manage device scopes** to open the flyout where you can create and modify your custom device scopes.

To create custom device scopes:

1. Open the **Manage device scopes** menu.
1. Select a Scope tag from the dropdown and select **Save**.
1. Give your new custom device scope a Name and select **OK**.

The new custom device scope appears in your list of saved device scopes. By default, custom devices scopes are in the *Off* state. To activate custom device scopes, toggle the **State** setting to *On*. Data processing starts for the selected device scope.  

> [!NOTE]
> Once activated, custom device scopes can take up to 24 hours to process. During this period, custom device scopes that are still processing will not be usable.

Only the user who created the custom device scopes or a Global administrator can delete the custom device scopes.

To delete custom device scopes:

1. Open the **Manage device scopes** menu.
2. Find the custom device scope you would like to delete and select the menu. 
3. Select **Delete**.
4. Select **Yes** to confirm.

> [!IMPORTANT]
> If a custom device scope is associated with a Scope tag that gets deleted from your tenant, the custom device scope will no longer function. You will see an error message in the **Manage device scopes** menu. Edit the impacted device scope to use a valid Scope tag or delete it to clear the error.

## Using custom device scopes

Custom device scopes can be used in any supported Endpoint analytics report. To use a custom device scope: 

1. Ensure that the device scope you would like to use is active.
2. Navigate to a supported report in Endpoint analytics, such as **Startup performance**.
3. Select **Device scope** menu in the page. 
4. From the dropdown menu, select your desired custom device scope. 
5. Select **Apply**. 

The page is automatically updated to show scores, data, and insights specific to the subset of devices defined by your chosen custom device scope. As you navigate through Endpoint analytics, your chosen device scope remains selected on all supported reports and pages.

To return to viewing all devices, navigate to the **Device scope** menu, select **All Devices** from the dropdown menu, and select **Apply**.  

## Limitations 

- You can save up to 100 custom device scopes, and up to 20 can be active at a time.  

- Only one Scope tag can be used to create a custom device scope. To create a custom device scope that includes devices from multiple Scope tags, you must create a new Scope tag and assign it to the full set of devices that you require.

## Next Steps

For more information, go to:

- [Enhanced device timeline](enhanced-device-timeline.md)
- [Anomaly detection](anomaly-detection.md)
- [What is advanced Endpoint analytics](advanced-endpoint-analytics.md)  
  