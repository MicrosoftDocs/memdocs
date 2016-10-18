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
You can now filter on the content size for software updates in automatic deployment rules. For example, you can set the **Content Size** filter to **< 2048** to only download software updates that are smaller than 2MB. Using this filter prevents large software updates from automatically downloading to better support simplified Windows down-level servicing when network bandwidth is limited. For details, see [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### Configure the Content Size field
To configure the **Content Size** field, go to the **Software Updates** page in the Create Automatic Deployment Rule Wizare when you create an ADR or go to the **Software Updates** tab in the properties for an existing ADR.

![Content size field](media/contentsizefield.png)

## Feature 2





## See Also
[Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md)
