---
title: Quickstart - Enroll Intune devices
titleSuffix: Microsoft Endpoint Manager
description: In this quickstart, you enroll Intune devices into Endpoint analytics.
ms.date: 10/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: quickstart
ms.assetid: 1be507b8-c3bf-46fd-b010-e2f432659a63
author: mestew
ms.author: mstewart
manager: dougeby

# Customer intent: As a Microsoft Endpoint Manager administrator, I want to enroll Intune devices into Endpoint analytics so that I can gain insights into the user experience.
---

# Quickstart: Enroll Intune devices into Endpoint analytics

This quickstart outlines prerequisites and instructions for enrolling Intune managed devices into Endpoint analytics. If your devices are co-managed and meet the [Intune device requirements](#bkmk_prereq) below, we recommend using the instructions in this quickstart to enroll them to Endpoint analytics via Intune. Note that you do not need to move any co-management workloads to Intune to enroll eligible devices via Intune.

## <a name="bkmk_prereq"></a> Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

### Intune device requirements

- Intune enrolled or co-managed devices running Windows 10 Pro, Windows 10 Pro Education, Windows 10 Enterprise, or Windows 10 Education. Windows 10 Home isn't supported.
   - Startup performance insights are only available for devices running version 1903 or later of Windows 10 Enterprise, Education, or Pro. Windows 10 long-term servicing channel (LTSC) isn't supported.
      -  Windows 10 Pro versions 1903 and 1909 require [KB4577062](https://support.microsoft.com/help/4577062/windows-10-update-kb4577062). <!--8392089, 8389021-->
      - Windows 10 Pro versions 2004 and 20H2 require [KB4577063](https://support.microsoft.com/help/4577063/windows-10-update-kb4577063). <!--8392089, 8389021-->
- Windows 10 devices must be Azure AD joined or hybrid Azure AD joined.
   - Workplace joined or Azure AD registered devices aren't supported.
- The **Connected User Experiences and Telemetry** service on the device is running

### <a name="bkmk_endpoints"></a> Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows 10 and Windows Server **Connected User Experiences and Telemetry** component (DiagTrack) to collect the data from Intune-managed devices.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](data-collection.md#bkmk_datacollection) to the Intune data collection endpoint. |

### Licensing Prerequisites

Endpoint analytics is included in the following plans:

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) or higher
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) or higher.

### Endpoint analytics permissions

- The [Intune Service Administrator role](../intune/fundamentals/role-based-access-control.md) is required to [start gathering data](#bkmk_onboard).
   - After clicking **Start** for gathering data, other read-only roles can view the data.

[!INCLUDE [Endpoint analytics permissions information](includes/endpoint-analytics-rbac.md)]

## <a name="bkmk_onboard"></a> Onboard in the Endpoint analytics portal
Onboarding from  the Endpoint analytics portal is required for Intune managed devices. For more information about common issues, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#bkmk_enrollment_tshooter).

[!INCLUDE [Endpoint analytics overview page information](includes/onboard.md)]

## <a name="bkmk_view"></a> View the Overview page

[!INCLUDE [Endpoint analytics overview page information](includes/overview-page.md)]

## Next steps

[Enroll Configuration Manager devices](enroll-configmgr.md)
