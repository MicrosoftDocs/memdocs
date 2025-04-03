---
title: Tenant attach - Create and deploy Attack surface reduction policies from the admin center
titleSuffix: Configuration Manager
description: Create and deploy Attack surface reduction policies from the Microsoft Intune admin center and for Configuration Manager collections.
ms.date: 05/31/2022
ms.topic: install-set-up-deploy
ms.subservice: core-infra
ms.service: configuration-manager
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: apoorvseth
author: gowdhamankarthikeyan
ms.author: gokarthi
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# <a name="bkmk_atp"></a> Tenant attach: Create and deploy Attack surface reduction policies from the admin center
<!--7323386-->
*Applies to: Configuration Manager (current branch)*


 Create Attack surface reduction policies in the Microsoft Intune admin center and deploy them to Configuration Manager collections.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]

## <a name="bkmk_asr"></a> Assign Attack surface reduction policy to a collection

1. In a browser, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Endpoint security** > **Attack surface reduction** then **Create Policy**.
1. Create a profile with the following settings:

   - **Platform**: Windows 10 and later (ConfigMgr)
   - **Profile**: Choose one of the following profiles:
     - Attack Surface Reduction Rules (ConfigMgr)
     - Exploit Protection (ConfigMgr)
     - Web Protection (ConfigMgr)

> [!NOTE]
>The Microsoft Edge installer, Attack Surface Reduction rules engine for tenant attach, and [CMPivot](../core/servers/manage/cmpivot.md) are currently signed with the **Microsoft Code Signing PCA 2011** certificate. If you set PowerShell execution policy to **AllSigned**, then you need to make sure that devices trust this signing certificate. You can export the certificate from a computer where you've installed the Configuration Manager console. View the certificate on `"C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\CMPivot.exe"`, and then export the code signing certificate from the certification path. Then import it to the _machine_'s **Trusted Publishers** store on managed devices. You can use the process in the following blog, but make sure to export the _code signing certificate_ from the certification path: [Adding a Certificate to Trusted Publishers using Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/adding-a-certificate-to-trusted-publishers-using-intune/ba-p/1974488)

1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about available settings for both profiles, see [Attack surface reduction policy settings for tenant attached devices](../../intune-service/protect/endpoint-security-asr-profile-settings.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json#attack-surface-reduction-configmgr).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]

## Next steps

- [Attack surface reduction policy settings for tenant attached devices](../../intune-service/protect/endpoint-security-asr-profile-settings.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json#attack-surface-reduction-configmgr).
- [Create and deploy endpoint security Antivirus policy to tenant attached devices](deploy-antivirus-policy.md)
- [Create and deploy endpoint security Endpoint Detection and Response policy to tenant attached devices](atp-onboard.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)