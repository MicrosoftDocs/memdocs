---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 04/06/2022
ms.localizationpriority: medium
---

<!--This file is shared by /sum/get-started/install-a-software-update-point.md and /sum/plan-design/plan-for-software-updates.md. The headers are context driven by the article and both have"bkmk_maxruntime" as an anchor. -->

You can specify the maximum amount of time a software update installation has to complete. You can specify the maximum run time for the following:<!--3734426-->

- **Maximum run time for Windows feature updates (minutes)**
  - **Feature updates** - An update that is in one of these three classifications:
    - Upgrades
    - Update rollups
    - Service packs

- **Maximum run time for Office 365 updates and non-feature updates for Windows (minutes)**
  - **Non-feature updates** - An update that isn't a feature upgrade and whose product is listed as one of the following:
    - Windows 11
    - Windows 10 (all versions)
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- **Maximum run time for all other software updates outside these categories such as third-party updates (minutes)**: The default maximum run time of these updates varies depending on when the update first synchronized into the environment and the Configuration Manager version. Use the cart below to determine the maximum runtime value for these updates: 
   
   |**2203 or later** |  **2103, 2107, or 2111**|  **2010** |
   |---|---|---|
   | The maximum run time for all other software updates is customizable. The default is 60 minutes.<!--12770887-->|  60 minutes <!--7833866-->| 10 minutes|
   > [!Important]
   > - This setting only changes the maximum runtime for new updates that are synchronized in by SUP. It doesn't change the run time on existing updates that synchronized before the run time was modified. For instance, if `Update 1` was first synchronized into a 2111 environment, then it's maximum run time is 60 minutes. You then upgrade the environment to version 2203 and set the maximum run time to 30 minutes. `Update 1` retains it's 60 minute runtime. However, when a new update, `Update 2`, synchronizes in, it is given the new 30 minute run time. 
   > - If you need to change the maximum run time of an update manually, you can [configure the software update settings](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings) for it.
