---
title: Monitor Microsoft Defender for Endpoint with Microsoft Intune
description: Learn how to monitor device compliance and onboarding status for Microsoft Defender for Endpoint with Microsoft Intune in the admin center.
ms.date: 04/28/2026
ms.topic: how-to
ms.reviewer: aanavath
ms.custom: msecd-doc-authoring-1012
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Monitor device status for Microsoft Defender for Endpoint with Microsoft Intune

When you integrate Microsoft Intune and Microsoft Defender for Endpoint, you can monitor device compliance and onboarding status in the Microsoft Intune admin center to verify that devices are protected.

## Monitor device compliance

Monitor the state of devices that have the Microsoft Defender for Endpoint compliance policy.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance**. On the **Monitor** tab, select **Noncompliant devices**.

3. Find your Microsoft Defender for Endpoint policy in the list, and see which devices are compliant or noncompliant.

For more information about reports, see [Intune reports](../../device-management/reports/overview.md).

## View onboarding status

To view the onboarding status of your Intune-managed devices:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Overview**.

   The default *Summary* tab includes a **Windows devices onboarded onto Microsoft Defender for Endpoint** visualization report that displays the count of devices reporting status from the Defender for Endpoint sensor.

## Next step

- [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](./overview.md)
