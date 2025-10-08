---
title: Deploy Endpoint Privilege Management with Microsoft Intune
description: Understand the steps and phases for deploying Endpoint Privilege Management with Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 09/10/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Deploy Endpoint Privilege Management with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [intune-epm-overview](includes/intune-epm-overview.md)]

To deploy Endpoint Privilege Management (EPM), start by enabling reporting, then use reports to create rules for elevation. This article describes some common deployment scenarios and outlines the recommended deployment phases for your organization.

- [Windows elevation settings policy](epm-elevation-settings.md).
- [Windows elevation rules policy](epm-elevation-rules.md).
- [Reusable settings groups](epm-elevation-rules.md#reusable-settings-groups), which are optional configurations for your elevation rules.

## Deployment overview

EPM can help control the elevation of applications in Intune and [Local Users and Groups](endpoint-security-account-protection-policy.md) can be used to control the local administrators group and transition users from administrators to standard users.

The common deployment phases are:

:::image type="content" source="media/epm-deploy/epm-deploy-phases.png" alt-text="The five phases to deploy EPM." border="false":::

- **Phase 1: Auditing** - Enable EPM client and enable reporting collection using an [elevation settings policy](epm-elevation-settings.md).
- **Phase 2: Persona identification** - Identity groups of users with common requirements.
- **Phase 3: Build rules** - Use [EPM reports](epm-reports.md) to create [elevation rules](epm-elevation-rules.md) for different personas.
- **Phase 4: Monitoring** - Iterate and refine rules, identify new scenarios.
- **Phase 5: Review user privileges** - Identify and optionally move users from administrator to standard user using [Local Users and Groups](endpoint-security-account-protection-policy.md#manage-local-groups-on-windows-devices). Consider enabling [support approved elevation](epm-support-approved.md) so that users can request elevation for apps that aren't covered by rules.

Repeat phases 2 to 5 continuously to ensure your users have least privilege in line with [Zero Trust principles](/intune/intune-service/fundamentals/zero-trust-with-microsoft-intune).

The common deployment scenarios for EPM are:

| Scenario | Local User (Before) | Local User (After) | Example Role | Use Case |
|---|---|---|---|---|
|1|Admin|Admin|IT Support Technicians|A certain subset of users required ongoing local admin – but you want to gain security improvements by using EPM.|
|2|Admin|Standard User|Information Workers|You want to move users with local admin rights to standard users, with minimal disruption. You want to allow them to request an app to run as admin on occasion.</br></br> For step by step instructions on how to achieve this scenario with EPM, see [Using EPM to transition users from administrator to standard users](epm-transition-administrator-to-standard-user.md)|
|2|Standard User|Standard User|Developers|You want to allow specific users to 'elevate up' without granting local admin rights or using [LAPS](windows-laps-overview.md).|

---

## Next steps

> [!div class="nextstepaction"]
> [Next: Create an elevation settings policy >](epm-elevation-settings.md)
