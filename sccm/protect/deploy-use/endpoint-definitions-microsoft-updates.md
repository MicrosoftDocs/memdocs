---
title: "Endpoint Protection malware definitions from network share"
description: "Learn how to enable the download of Endpoint Protection malware definitions from Microsoft Updates for Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: 21
author: NathBarnms.author: nathbarnmanager: angrobe

---

# Enable Endpoint Protection malware definitions to download from Microsoft Updates for Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

 When you select to download definition updates from Microsoft Update, clients will check the Microsoft Update site at the interval defined in the **Definition updates** section of the antimalware policy dialog box.

 This method can be useful when the client does not have connectivity to the Configuration Manager site or when you want users to be able to initiate definition updates.

> [!IMPORTANT]
>  Clients must have access to Microsoft Update on the Internet to be able to use this method to download definition updates.

## Using the Microsoft Malware Protection Center to Download Definitions
 You can configure clients to download definition updates from the Microsoft Malware Protection Center. This option is used by Endpoint Protection clients to download definition updates if they have not been able to download updates from another source. This update method can be useful if there is a problem with your Configuration Manager infrastructure that prevents the delivery of updates.

> [!IMPORTANT]
>  Clients must have access to Microsoft Update on the Internet to be able use this method to download definition updates.


> [!div class="button"]
[Next step >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Back >](endpoint-configure-alerts.md)
