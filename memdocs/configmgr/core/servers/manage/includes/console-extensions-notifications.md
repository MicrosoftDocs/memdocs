---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 04/08/2022
ms.localizationpriority: medium
---
<!--This file is shared by the admin-console-extensions.md, admin-console-notifications.md, and community-hub-extension.md files. Some headings may be context driven by the article. -->

Users are notified when console extensions are approved for installation. These notifications occur for users in the following scenarios:

- The Configuration Manager console requires a built-in extension, such as WebView2, to be installed or updated.
- Console extensions are approved and notifications are enabled from **Administration** > **Overview** > **Updates and Servicing** > **Console Extensions**. 
   - When notifications are enabled, users within the [security scope](../../../understand/fundamentals-of-role-based-administration.md#security-scopes) for the extension receive the following prompts:

1. In the upper-right corner of the console, select the bell icon to display Configuration Manager console notifications.

   :::image type="content" source="../media/3555909-notification.png" alt-text="Notifications in the Configuration Manager console":::

1. The notification will say **New custom console extensions are available**.

   :::image type="content" source="../media/3555909-extension-notification.png" alt-text="New custom console extensions are available notification":::

1. Select the link **Install custom console extensions** to launch the install.
1. When the install completes, select **Close** to restart the console and enable the new extension.

    :::image type="content" source="../media/3555909-extension-installed.png" alt-text="Console extension completed install":::

> [!Note]
> When you upgrade to Configuration Manager 2107, you will be prompted to install the WebView2 console extension again. For more information about the WebView2 installation, see the [WebView2 installation](../community-hub.md#bkmk_webview2) section if the Community hub article. <!--10247811, 10005418-->
