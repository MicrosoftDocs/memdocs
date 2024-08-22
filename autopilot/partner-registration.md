---
title: Reseller, distributor, or partner registration of Windows Autopilot devices
description: How partners add devices to Windows Autopilot.
ms.service: windows-client
ms.subservice: itpro-autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - tier2
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Reseller, distributor, or partner registration

Customers can purchase devices from resellers, distributors, or other partners. As long as these resellers, distributors, and partners are part of the [Cloud Solution Partners (CSP) program](https://partner.microsoft.com/cloud-solution-provider), they too can register devices for the customer.

As with OEMs, CSP partners must be granted permission to register devices for an organization. This process is described in the [CSP authorization](registration-auth.md#csp-authorization) section of the Windows Autopilot customer consent article. In summary:

- The CSP partner requests a relationship with the organization. That organization's Global Administrator approves the request.
- After the approval, CSP partners add devices using [Partner Center](https://partner.microsoft.com/pcv/dashboard/overview), either directly through the web site or via available APIs that can automate the same tasks.

For Surface devices, Microsoft Support can help with device registration. For more information, see [Surface Registration Support for Windows Autopilot](/surface/surface-autopilot-registration-support).

Windows Autopilot doesn't require delegated administrator permissions when establishing the relationship between the CSP partner and the organization. As part of the Global Administrator's approval process, they can choose to uncheck the **Include delegated administration permissions** checkbox.

<!-- MAXADO-9048730 -->

> [!IMPORTANT]
>
> Microsoft recommends using roles with the fewest permissions. Using lower permissioned accounts helps improve security for an organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when an existing role can't be used.

> [!TIP]
>
> While resellers, distributors, or partners could boot each new Windows device to obtain the hardware hash for purposes of providing them to customers or direct registration by the partner, this method isn't recommended. Instead, these partners should register devices using the PKID information obtained from the device packaging, such as the barcode, or obtained electronically from the OEM or upstream partner/distributor.

> [!NOTE]
>
> Partner Center doesn't have access to profiles created in Intune or Microsoft Store for Business. It only has access to the Autopilot profiles created through Partner Center.

## Related content

- [Registration overview](registration-overview.md).
