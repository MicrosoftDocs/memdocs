---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/01/2021
ms.localizationpriority: medium
---
<!--This file is shared. Currently it's in use by the admin-console-extensions.md file and the import-admin-console-extensions.md file. Some headings may be context driven by the article-->

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
