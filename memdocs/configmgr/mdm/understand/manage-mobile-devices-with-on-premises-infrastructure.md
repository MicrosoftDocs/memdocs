---
title: On-premises MDM
titleSuffix: Configuration Manager
description: Learn about on-premises mobile device management (MDM) in Configuration Manager
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# On-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in November 2021, this feature of Configuration Manager is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901 -->

Configuration Manager on-premises mobile device management (MDM) is a device management solution that relies on the built-in management capabilities of Windows. This feature is based on the Open Mobile Alliance (OMA) Device Management (DM) standard. It uses your organization's Configuration Manager infrastructure to manage and maintain the devices. Your organization requires Microsoft Intune licenses to use this feature, but it doesn't require any cloud connection. Configuration Manager stores all data about your devices in your on-premises site database.

On-premises MDM differs from Microsoft Intune, which also relies on built-in OMA DM capabilities. All of the management functions in Intune are delivered through cloud services. On-premises MDM also differs from the client-based management solution traditionally offered by Configuration Manager. It relies on similar infrastructure, but doesn't use separately installed client software on the devices it manages.  

## Comparison

The following sections list the advantages and disadvantages of on-premises MDM as compared to traditional client-based management:  

### Advantages

- **Simplified infrastructure**: Fewer site system roles are required.

- **Easier to maintain**: Because management functionality is built in to the device OS, new versions of the Configuration Manager client aren't required when new management features are introduced to the site.

- **On-premises**: - All management and data are kept on-premises.

### Disadvantages

**Less client management functionality**: No orchestration, software metering, third-party integration, task sequencing, or Software Center support.

- **Limited device support**: on-premises MDM doesn't support as many OS versions as the Configuration Manager client. For more information, see [Supported OS versions for clients and devices](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## Next step

Learn about what to consider when setting up the Configuration Manager infrastructure and planning for device enrollment in on-premises MDM.

> [!div class="nextstepaction"]
> [Plan for on-premises MDM](../plan-design/plan-on-premises-mdm.md)  
