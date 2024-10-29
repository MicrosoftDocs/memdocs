---
author: smritib17
ms.author: smbhardwaj
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: include
ms.date: 06/25/2020
ms.localizationpriority: medium
---
<!--Don't apply H2 in this include file since they are context driven by article. Used in enroll-configmgr.md and enroll-intune.md files -->

1. Go to `https://aka.ms/endpointanalytics`
1. Choose from the following options:
   - **All cloud-managed devices**: Creates an [Intune data collection policy](../settings.md#bkmk_profile) assigned to all Windows 10 1903 or later devices which are either Intune managed or co-managed.
   - **Selected devices**: Creates and assigns the policy to devices which you select.
   - **I'll choose later**: Doesn't deploy a policy to devices. Remediations can still be used, but any reports that rely on analytics data will be empty.
1. Click **Start**. This will automatically assign a configuration profile to collect boot performance data from all eligible devices. You can [change assigned devices](../settings.md#bkmk_profile) later. It may take up to 24 hours for startup performance data to populate from your Intune enrolled devices after they reboot.

> [!IMPORTANT]
>
> - We anonymize and aggregate the scores from all enrolled organizations to keep the **All organizations (median)** baseline up-to-date. You can [stop gathering data](../data-collection.md#bkmk_stop) at any time.
> - Client devices require a restart to fully enable all analytics. <!--7698085-->
