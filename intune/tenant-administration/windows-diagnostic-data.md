---
title: Enable Windows diagnostic data and license verification
description: Learn how to enable Intune tenant settings to use Windows diagnostic data and verify Windows licenses required for dependent features.
author: paolomatarazzo
ms.author: paoloma
ms.date: 02/24/2026
ms.topic: how-to
ms.reviewer: zadvor
ms.collection:
- M365-identity-device-management
- privacy
- sub-data-privacy
---

# Enable Windows diagnostic data and license verification


Some Microsoft Intune features depend on access to Windows diagnostic data and verification of eligible Windows licenses. These requirements are configured at the tenant level.

This article explains how to enable Windows diagnostic data for use by Intune and how to attest to Windows license eligibility so dependent features can function correctly.

## Enable Windows data

To allow Intune to access Windows diagnostic data collected from enrolled devices:

1. In the [Microsoft Intune admin center][INT-AC], select **Tenant administration** > **Connectors and tokens** > **Windows data**.
1. Toggle **Enable features that require Windows diagnostic data in processor configuration** to **On**. The default is *Off*.

> [!NOTE]
> There are multiple ways to enable Windows diagnostic data for a tenant. This toggle reflects only your configuration choice for **Intune features**.
>
> Turning this setting **Off** disables Intune features that rely on this configuration, but it might not disable processor configuration that was enabled by other methods.

Features that require Windows diagnostic data include:

- [Compatibility reports for Windows updates](../device-updates/windows/compatibility-reports.md)
- [Reports for expedite policies](../device-updates/windows/expedite-policy.md#monitoring-and-reporting)
- Driver update policies with alerts for Windows driver update failures
- Expedited quality update policies with alerts for Windows expedited update failures
- Feature update policies with alerts for feature update failures

To learn more about this configuration, see [Enable Windows diagnostic data processor configuration](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enable-windows-diagnostic-data-processor-configuration) in the Windows privacy documentation.

## Enable Windows license verification

To enable Intune features that require Windows license verification, you must attest that your tenant has the required Windows licenses. This attestation is required because some Intune features depend on the presence of eligible Windows licenses in the tenant, and this setting allows you to confirm that requirement is met.

> [!NOTE]
> This attestation doesn't validate individual device activation or assign licenses. It confirms that your tenant is entitled to use Intune features that require eligible Windows licenses.

Supported licenses include:

- Windows Enterprise E3 or E5, or Microsoft 365 F3, E3, or E5
- Windows Education A3 or A5, or Microsoft 365 A3 or A5
- Windows Virtual Desktop Access E3 or E5

To attest ownership of the required Windows licenses:

1. In the [Microsoft Intune admin center][INT-AC], select **Tenant administration** > **Connectors and tokens** > **Windows data**.
1. Toggle **I confirm that my tenant owns one of these licenses** to **On**. By default, it's *Off*.

Features theat require license verification include:

- [Compatibility reports for Windows updates](../device-updates/windows/compatibility-reports.md)
- [Remediations](../intune-service/fundamentals/remediations.md)

## Next steps

To understand how Windows diagnostic data is collected and managed, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization) in the Windows privacy documentation.

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431