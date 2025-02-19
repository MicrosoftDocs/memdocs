---
# required metadata

title: Enable use of Windows diagnostic data by Intune
titleSuffix: Microsoft Intune
description: Enable Windows diagnostic data in processor configuration for your tenant to enable its use by Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 11/26/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: b204a956-18ec-11e8-accf-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: zadvor
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- privacy
- sub-data-privacy
---

# Enable use of Windows diagnostic data by Intune

Before you can use some Intune features, you must enable *Windows diagnostic data in processor configuration* for your tenant. This enables you as the [controller of Windows diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enable-windows-diagnostic-data-processor-configuration) collected from your devices to then allow its use by Intune when it's required by features that are dependent on that data.

In addition, several of the features that require Windows diagnostic data also require you to have Windows E3 (or equivalent) licenses, and you must attest to having these licenses to enable use of those features.

Both configuration of the Windows diagnostic data in processor configuration and the license attestation are configured on the **Windows data** page of the Microsoft Intune admin center.

## Manage Windows data configurations

To manage Windows data configurations for your tenant, open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Connectors and tokens** > **Windows data**.

On the *Windows data* page, you can configure your tenant to support Windows diagnostic data in processor configuration, and to attest ownership of the required Windows E3 or equivalent licenses. It’s possible that some features require only one of the available configurations to be enabled, while other features could require both.

### Windows data

Use the *Windows data* category to enable use of Intune features in your tenant that require diagnostic data in processor configuration.

The following features require you to enable this support:

- [Windows feature update device readiness report](../protect/windows-update-compatibility-reports.md#use-the-windows-feature-update-device-readiness-report) 
- [Windows feature update compatibility risks report](../protect/windows-update-compatibility-reports.md#use-the-windows-feature-update-compatibility-risks-report)
- [Windows driver updates report](../protect/windows-driver-updates-overview.md)
- Windows feature update report
- Windows expedited Update Report
- Driver update policies with alerts / Windows driver update failures
- Expedited quality update policies with alerts /  Windows expedited update failures
- Feature update policies with alerts / Feature update failures

To enable support, set **Enable features that require Windows diagnostic data in processor configuration** to **On**. By default, it's *Off*.

- While there are other methods to enable this support for a tenant, this toggle only reflects your configuration choice for Intune features.
- Changing this toggle from *On* to *Off* disables use of Intune features that require this configuration but might not turn off processor configuration configured by other methods.

To learn more about this configuration, see [Enable Windows diagnostic data processor configuration](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enable-windows-diagnostic-data-processor-configuration) in the Windows privacy documentation.

### Windows license verification

Use the *Windows license verification* category to enable use of Intune features in your tenant that require Windows E3 or equivalent licenses.

The following features require you to attest to having Windows E3 or equivalent licenses:

- [Windows update app and driver compatibility reports](../protect/windows-update-compatibility-reports.md)

Supported licenses include the following options:

- Windows 10 or later Enterprise E3 or E5; or Microsoft 365 F3, E3, or E5.
- Windows 10 or later Education A3 or A5; or Microsoft 365 A3 or A5.
- Windows Virtual Desktop Access E3 or E5.

To confirm you own the required licenses for these features, set **I confirm that my tenant owns one of these license** to **On**. By default, it's *Off*.

- Other features can require these same licenses, but only the features listed in this section currently require this toggle to be set to *On*.
- Features that require this attestation aren't available for use when this toggle is set to *Off*.

## Next steps

To learn more about Windows diagnostic data collection, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization) in the Windows privacy documentation.

