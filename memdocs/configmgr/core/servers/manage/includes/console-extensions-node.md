---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/02/2021
---
<!--This file will be shared. Currently it's in use by the admin-console-extensions.md file. Some headings may be context driven by the article-->

## About the Console Extensions node
<!--3555909-->
(*Introduced in version 2103*)

The **Console Extensions** node is located under **Administration** > **Overview** > **Updates and Servicing**. Actions for console extensions are grouped in the ribbon and the right-click menu. Console extensions downloaded from [Community hub](../community-hub-extensions.md) will be shown here. 

:::image type="content" source="../media/3555909-console-extensions-node.png" alt-text="The Console Extensions node in the Configuration Manager console" lightbox="../media/3555909-console-extensions-node.png":::

**Actions for All Sites** group:
- **Approve Installation**: Approves the console extension for installation across all sites. An extension must be approved before notifications are enabled.
- **Revoke Approval**:
   - Revokes the ability to install the extension from the **Console Extensions** node.
   - Notifies then uninstalls existing instances of the extension across the hierarchy at the next launch of a locally installed console.
   - Allows for reapproval of the extension at a later date.
- **Enable Notifications**: Upon next launch of the console, notifies users within the security scope that the extension can be installed.
- **Disable Notifications**: Disables the console notification messages for the extension. Users within the security scope can still install approved extensions from the **Console Extensions** node.  
- **Delete**:
   - Revokes the ability to install the extension from the **Console Extensions** node.
   - Notifies then uninstalls existing instances of the extension across the hierarchy at the next launch of a locally installed console.
   - Removes the extension from the **Console Extensions** node so it can't be reapproved later.

**Classify** group:

- **Set Security Scopes**: Set the [security scopes](../../../understand/fundamentals-of-role-based-administration.md#security-scopes) to secure the object and limit access.

**Local Extension** group:

- **Install**: Installs the selected extension for the current local console
- **Uninstall**: Uninstalls the selected extension from the current local console

> [!NOTE]
> - The WebView2 console extension is approved by default to enable using Community hub. The files are automatically downloaded from `https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download-section` with the other redistributable files.
> - When you upgrade to Configuration Manager 2107, you will be prompted to install the WebView2 console extension again. <!--10247811, 10005418-->

## Enable or disable hierarchy approved console extensions

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**.
1. Select **Hierarchy Settings** from the ribbon.
1. On the **General** tab, enable or disable the **Only allow console extensions that are approved for the hierarchy** option.
1. Select **Ok** when done to close the **Hierarchy Settings Properties**.

> [!Important]
> If this setting is `enabled`, your old style extensions that aren't approved through the **Console Extensions** node will no longer be able to be used. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](../updates.md#bkmk_Baselines). The setting remains `disabled` by default, if you upgraded from a version prior to 2103. If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

## <a name="bkmk_local_install"></a> Install and test an extension on a local console

1. Change the [security scope](../../../understand/fundamentals-of-role-based-administration.md#security-scopes) for the extension. Changing the security scope is recommended for initial testing of an extension.
   1. Go to the **Console Extensions** node under **Administration** > **Overview** > **Updates and Servicing**.
   1. Select the extension, then select **Set Security Scopes** from the ribbon.
   1. Remove the **Default** security scope and add a scope that only contains one or two admins for initial testing.
   1. Choose **OK** to save the security scope for the extension.

1. Approve the extension by selecting **Approve Installation** from the ribbon or right-click menu.
   - If the extension isn't approved, you won't be able to install it or enable in-console notifications for it.
   - If you restart your console at this point, a notification about the available extension won't occur since you haven't enabled the option yet.
1. Install the extension on the local console by choosing **Install**.
1. Once the extension is installed, verify it displays and you can use it from the local console.

## <a name="bkmk_enable-notifications"></a> Enable user notifications for extension installation

1. If needed, modify the security scopes for the extension to allow access by more admins. These admins will be targeted with the in-console notification for installing the extension.
1. Select **Enable Notifications**.
1. Launch a Configuration Manager console that doesn't have the extension installed. Ideally, use a test account that you gave access to when you modified the security scope.
1. Verify that the notification for the extension occurs and that you can install the extension.
