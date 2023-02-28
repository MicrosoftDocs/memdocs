---
# required metadata

title: Microsoft Intune Government Service Description  
description: Intune Government Service Description is designed to serve as an overview of the Microsoft Intune offering for GCC High and DoD environments.
keywords:
author: dougeby
ms.author: dougeby
manager: johmar
ms.date: 01/26/2023
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.suite: ems

# optional metadata
ms.reviewer: pfetty
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Microsoft Intune for US Government GCC High and DoD service description

The Intune U.S. government service description is as an overview of the service offering in the GCC High and DoD environments. It lists the feature differences compared to the commercial offering of Microsoft Intune.

To learn more about Intune for GCC customers, go to [EMS offers for US Government and Microsoft 365 interoperability](/enterprise-mobility-security/solutions/ems-govt-service-description#ems-offers-for-us-government-and-microsoft-365-interoperability).

## Get started with Intune for US Government GCC High and DoD

The Intune GCC High and DoD offering are built on the Microsoft Azure Government Cloud. It's designed to interoperate with Microsoft 365 GCC High and DoD environments. 

For more information about Intune, and what you can do, go to [Microsoft Intune securely manages identities, manages apps, and manages devices](what-is-intune.md). Use this documentation as your starting point for deploying and using Microsoft Intune.

Intune has two service instances:

- **Commercial service**: The commercial service is available to anyone with an Intune license and is used by most Intune customers.
- **Government cloud**: This service is also known as **GCC High** or **DoD**. This instance is a datacenter that's physically separate from the commercial instances. The datacenter is locked down and is only used by government customers who purchase the appropriate license.

  These government instances are also known as **IL4** and **IL5**, where **IL** refers to Information Level.

:::image type="content" source="./media/intune-govt-service-description/migration-public-government-cloud.png" alt-text="Screenshot that shows the Microsoft government cloud, including GCC High and DoD services, is physically separate from the public cloud and commercial cloud instances.":::

### What you need to know

- There isn't a built-in way to migrate from the commercial service to the government cloud, and vice versa. To migrate, devices need to unenroll from the current tenant, and then re-enroll to the new tenant.

  This approach is similar to unenrolling from another MDM service and enrolling in Intune. For more information, go to [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md#currently-use-a-third-party-mdm-provider).

- In the government cloud, the Intune service instance is shared with GCC High and DoD tenants. This architecture is slightly different than other services, such as Microsoft 365 and Azure.

- For Intune, there isn't a "GCC" instance. Other services offer a "GCC" instance. GCC instances are commonly used by state and local government customers that require extra accreditation for the cloud services they use.

## Feature differences in Intune GCC High and DoD

- Intune for GCC High and DoD does not support the on-premises Exchange Connector.
- Intune for GCC High and DoD customers doesn't support the Chrome OS Connector.
- Windows Autopilot is not available to GCC High and DoD customers. Planning is underway.
- Microsoft Store for Business is not available to GCC High and DoD customers.
- Intune for GCC High only supports the Mobile Threat Defense (MTD) connectors for Android and iOS devices with MTD vendors that **also have support** in this government environment. When you sign in to a GCC-H tenant, you'll see the connectors enabled for those specific vendors.
- Microsoft Endpoint Manager Endpoint Analytics and Log Analytics are not currently available for U.S. Government customers.
- Intune for GCC High does not support the [TeamViewer connector](../remote-actions/teamviewer-support.md) or TeamViewer feature.
- Intune for GCC High and DoD does not support Android (AOSP) management for corporate devices.
- Intune for GCC High and DoD does not support [Feature updates](../protect/windows-10-feature-updates.md).
- Intune for GCC High and DoD does not support [Expedited updates](../protect/windows-10-expedite-updates.md).
- [Android based Teams devices](/microsoftteams/rooms/teams-devices-feature-comparison#feature-comparison-between-windows-and-android) are not fully supported in GCC High and DoD clouds. Planning is underway. 
  - Android based Teams devices may still function correctly in GCC High and DoD clouds. If a functionality issue is discovered, support is best effort.
  - Windows based Teams devices are fully supported in GCC High and DoD clouds. 
- Intune for GCC High and DoD doesn't support management of [Linux](../user-help/enroll-device-linux.md) devices.

## Next steps

To learn more about Intune and how to get started, go to the [Microsoft Intune planning guide](intune-planning-guide.md).
