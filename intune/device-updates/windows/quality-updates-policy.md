---
title: Windows quality updates policy
description: Use Hotpatch updates to receive security updates without restarting your device
ms.date: 04/17/2025
ms.reviewer: Mounika
ms.topic: how-to
---

# Windows quality updates policy

## Before you begin

> [!div class="checklist"]
> - Ensure your environment meets the requirements in [Windows quality updates overview](quality-updates.md#prerequisites).
> - To avoid conflicts or configurations that can block the installation of expedited updates, configure devices as follows. You can use *update rings policies* to manage these settings.
>
>    | Update ring setting       | Recommended value        |
>    |---------------------------|-------------------------------------|
>    | Enable pre-release builds | This setting should be set to **Not configured**. Preview builds, including the Beta and Dev channels, are not >supported with expedited updates. |
>    | Automatic update behavior | **Reset to default**  <br><br> Other values might cause a poor user experience and  slow the process to expedite >updates. |
>    | Change notification update level | Use any value other than **Turn off all notifications, including restart warnings** |
>    
>    For more information about these settings, see [Policy CSP Update](/windows/client-management/mdm/policy-csp-update).
>
> - The following list of Group Policy settings can interfere with Expedited policy. On devices where these settings were managed by Group Policy, restore them to their device defaults (Not configured):
>    - **CorpWuURL** - Specify intranet Microsoft update service location.
>    - **AutoUpdateCfg** - Configure Automatic Updates.
>    - **DeferFeatureUpdates** - Select when Preview Builds and Feature Updates are received.
>    - **Disable Dual Scan** - Don't allow update deferral policies to cause scans against Windows Update.
