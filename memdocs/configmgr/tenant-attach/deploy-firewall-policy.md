---
title: Tenant attach - Deploy endpoint firewall from the Microsoft Intune admin center
titleSuffix: Configuration Manager
description: Create and deploy firewall policies from the Microsoft Intune admin center and for Configuration Manager collections.
ms.date: 09/27/2021
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: apoorvseth
author: gowdhamankarthikeyan
ms.author: gokarthi
ms.localizationpriority: high
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# <a name="bkmk_atp"></a> Tenant attach: Create and deploy firewall policies from the admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*


 Create Windows Firewall policies in the Microsoft Intune admin center and deploy them to Configuration Manager collections.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Prerequisites for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]

## <a name="bkmk_firewall"></a> Assign firewall policies to a collection

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Endpoint security** > **Firewall** then **Create Policy**.
1. Create a profile with the following settings:
   - **Platform**: Windows 10 and later
      - Only Windows 10 clients can be targeted with firewall policies currently.
   - **Profile**: Microsoft Defender Firewall (ConfigMgr)
1. Select **Create** then give the profile a **Name** and a **Description**.
1. On the **Configuration settings** page, set the firewall settings for the devices. For more information about the available settings, see [Settings for firewall policy for tenant attached devices](../../intune/protect/endpoint-security-firewall-profile-settings-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)  

1. On the **Assignments** page, select the collections to include for the policy assignment then choose **Next**.
1. Review the settings on the **Review + Create** page and select **Create** when you're done.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]
## Next steps

- [Settings for firewall policy for tenant attached devices](../../intune/protect/endpoint-security-firewall-profile-settings-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)
- [Create and deploy endpoint security Antivirus policy to tenant attached devices](deploy-antivirus-policy.md)
- [Create and deploy endpoint security Attack surface reduction policy to tenant attached devices](deploy-asr-policy.md)
- [Create and deploy endpoint security Endpoint Detection and Response policy to tenant attached devices](atp-onboard.md)
