---
title: "Capabilities in Technical Preview 1610 for System Center Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1610."
ms.custom: na
ms.date: 10/21/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brendunsms.author: brendunsmanager: angrobe
---
# Capabilities in Technical Preview 1610 for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*


This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1610. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    

**Known Issues in this Technical Preview:**  
*add known issues here*



**The following are new features you can try out with this version.**  

## Filter by content size in automatic deployment rules
You can now filter on the content size for software updates in automatic deployment rules. For example, you can set the **Content Size (KB)** filter to **< 2048** to only download software updates that are smaller than 2MB. Using this filter prevents large software updates from automatically downloading to better support simplified Windows down-level servicing when network bandwidth is limited. For details, see [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### To configure the Content Size field
To configure the **Content Size (KB)** field, go to the **Software Updates** page in the Create Automatic Deployment Rule Wizare when you create an ADR or go to the **Software Updates** tab in the properties for an existing ADR.

![Content size field](media/contentsizefield.png)

## Improved functionality for required software dialogs
When a required software deployment is received by users, they now have the ability to choose from a list of values for the new option **Snooze and remind me:**. This gives users some additional control over the notification schedule for required software. The notification settings for upcoming deployment deadlines, which you configure on the Computer Agent page in Client Agent settings, continue to provide the minimum notification schedule for required software.
![Computer Agent page in Client Agent settings](media/computeragentsettings.png)

When a user receives required software, from the **Snooze and remind me:** setting, they can select from the following drop-down list of values:
- Later: specifies that notifications are scheduled based on the notification settings configured in Client Agent settings.
- Fixed time: specifies that the notification will be scheduled to display again after the selected time. For example, if a user selects 30 minutes, the notification will display again in 30 minutes.

The maximum snooze time is always based on the notification settings configured in the Client Agent settings. For example, if the **Deployment deadline less than 1 hour, remind users every (minutes)** setting on the Computer Agent page is configured for 10 minutes, the notification would display again in 10 minutes even if the user set the **Snooze and remind me:** setting to 30 minutes.

For a high-risk deployment, such as a task sequence that deploys an operating system, a dialog box such as the following displays on the user's computer:

![Required Software dialog](media/requiredsoftwaredialog.png)

For more information:
- [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [How to configure client settings](../clients/deploy/configure-client-settings.md)





## See Also
[Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md)
