---
# required metadata

title: Microsoft Intune Government Service Description  
description: Intune Government Service Description is designed to serve as an overview of our offering
keywords:
author: dougeby
ms.author: dougeby
manager: johmar
ms.date: 04/06/2022
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.suite: ems


---
# Microsoft Intune for US Government GCC High and DoD service description

## How to use this service description

The Intune US Government Service Description is designed to serve as an overview of the service offering in the GCC High and DoD environments and will cover feature variations from the commercial offering.

To learn more about Intune for GCC customers, see [EMS offers for US Government and Microsoft 365 interoperability](/enterprise-mobility-security/solutions/ems-govt-service-description#ems-offers-for-us-government-and-microsoft-365-interoperability).

## Get started with Intune for US Government GCC High and DoD

The Intune GCC High and DoD offering is built on the Microsoft Azure Government Cloud and is designed to inter-operate with Microsoft 365 GCC High and DoD environments. Full details on the service and how to use it can be found in the [Intune public documentation](/mem/intune). The public documentation should be use as a starting point for deploying and operating the service and the following Service Description details and changes from functionality or features in the GCC High environment.

### Feature variations in Intune GCC High and DoD

- Intune for GCC High and DoD customers does not support legacy PC management (with the Intune agent). Management of Windows 10 is supported via the modern MDM channel.
- Intune for GCC High and DoD customers does not support on-premises Exchange Connector.
- Co-Management support is only available with Configuration Manager version 1906 or later.
- Windows Autopilot and Business Store features are not available to GCC High and DoD customers at this time, though planning is underway.
- Intune for GCC High only supports the Mobile Threat Defense (MTD) connector for Android and iOS devices with MTD vendors that **also have support** in this environment. You will see connectors enabled for those specific vendors when you log in with a GCC-H tenant.
- Microsoft Endpoint Manager Endpoint Analytics and Log Analytics features are not currently available for US Government customers.
- Diagnostics settings and Workbooks are not available to US Government cloud customers at this time.
- Intune for GCC High does not support the [TeamViewer connector](/mem/intune/remote-actions/teamviewer-support) or TeamViewer feature.
- Intune for GCC High and DoD does not support Android (AOSP) management for corporate devices.
- Intune for GCC High and DoD does not support [Feature updates](/mem/intune/protect/windows-10-feature-updates).
- Intune for GCC High and DoD does not support [Expedited updates](/mem/intune/protect/windows-10-expedite-updates).

## Next steps

To learn more about Intune and explore how to get started see, [Intune public documentation](/mem/intune/).
