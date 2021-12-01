---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/01/2021
ms.localizationpriority: medium
---
<!--This file is shared. Currently it's in use by the admin-console-extensions.md file and the import-admin-console-extensions.md file. Some headings may be context driven by the article-->
## <a name="bkmk_allow-unsigned"></a> Allow unsigned console extensions for the hierarchy
<!--9761129-->
(*Applies to Configuration Manager version 2107 or later*)

Starting in Configuration Manager version 2107, you can choose to allow unsigned hierarchy approved console extensions. It's a best practice to always used signed extensions to minimize security risks and to confirm the authenticity of a console extension. However, in some cases you may need to allow unsigned console extensions due to an unsigned internally developed extension, or for testing your own custom extension in a lab. To allow [import](../import-admin-console-extensions.md#how-to-import-console-extensions) and install of unsigned hierarchy approved console extensions, you'll enable a hierarchy setting.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**.
1. Select **Hierarchy Settings** from the ribbon.
1. On the **General** tab, enable the **Hierarchy approved console extensions can be unsigned** option.
1. Select **Ok** when done to close the **Hierarchy Settings Properties**.

> [!NOTE]
> Currently, when an unsigned extension isn't [enabled for user notification](#bkmk_enable-notifications), in the **Console Extensions** node, the **Required** column remains blank instead of populating a value of **No**. <!--10349053, 10401804  -->
