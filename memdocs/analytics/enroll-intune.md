---
title: Quickstart - Enroll Intune devices
titleSuffix: Microsoft Endpoint Manager
description: In this quickstart, you enroll Intune devices into Endpoint analytics.
ms.date: 06/25/2020
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

This quickstart outlines prerequisites and instructions for enrolling Intune devices into Endpoint analytics.

## <a name="bkmk_prereq"></a> Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

### Intune device requirements

- Intune enrolled devices running Windows 10
- The **Connected User Experiences and Telemetry** service on the device is running

### Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows 10 and Windows Server **Connected User Experiences and Telemetry** component (DiagTrack) to collect the data from Intune-managed devices.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](privacy.md#bkmk_datacollection) to the Intune data collection endpoint. |

### Licensing Prerequisites

Endpoint analytics is included in the following plans:

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) or higher
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) or higher.

### Endpoint analytics permissions

- The [Intune Service Administrator role](../intune/fundamentals/role-based-access-control.md) is required to [start gathering data](#bkmk_onboard).
   - By clicking **Start**, you agree to and acknowledge that your customer data may be stored outside the location you selected when you provisioned your Microsoft Intune tenant.
   - After clicking **Start** for gathering data, other read-only roles can view the data.

- The following permissions are used for Endpoint analytics:
   - **Read** under the **Device configurations** category.
   - **Read** under the **Organization** category. <!--temporary for pp-->
   - Permissions appropriate to the user's role under the **Endpoint Analytics** category.

A read-only user would only need the **Read** permission under both the **Device configurations** and **Endpoint Analytics** categories. An Intune administrator would typically need all permissions.

## <a name="bkmk_onboard"></a> Onboard in the Endpoint analytics portal
Onboarding from  the Endpoint analytics portal is required for Intune managed devices.

1. Go to `https://aka.ms/endpointanalytics`
1. Click **Start**. This will automatically assign a configuration profile to collect boot performance data from all eligible devices. You can [change assigned devices](settings.md#bkmk_profile) later. It may take up to 24 hours for startup performance data to populate from your Intune enrolled devices after they reboot.

> [!Important]  
> We anonymize and aggregate the scores from all enrolled organizations to keep the **All organizations (median)** baseline up-to-date. You can [stop gathering data](privacy.md#bkmk_stop) at any time.

   - For more information about common issues, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#bkmk_enrollment_tshooter).

## <a name="bkmk_view"></a> View the Overview page

[!INCLUDE [Endpoint analytics overview page information](includes/overview-page.md)]

## Next steps

[Enroll Configuration Manager devices](enroll-configmgr.md)