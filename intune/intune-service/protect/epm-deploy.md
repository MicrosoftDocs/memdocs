---
title: Deploy Endpoint Privilege Management with Microsoft Intune
description: Understand the steps and phases for deploying Endpoint Privlege Management with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/22/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Configure policies for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

The information in this article can help you to configure the following policies and reusable settings for EPM:

- Windows elevation settings policy.
- Windows elevation rules policy.
- Reusable settings groups, which are optional configurations for your elevation rules.

Applies to:

- Windows 10
- Windows 11

## Common deployment scenarios

The table below lists the common deployment scenarios for EPM. We can choose to focus on all scenarios, or mainly scenario 2 (scenario 1 is very quickly/easy).

| Scenario | Local User (Before) | Local User (After) | Example Role | Use Case |
|---|---|---|---|---|
|1|Admin|Admin|IT Support Technicians|A certain subset of users required ongoing local admin – but you want to gain security improvements by using EPM.|
|2|Admin|Standard User|Information Workers|You want to move users with local admin rights to standard users, without big disruptions. You want to allow them to request an app to run as admin on occasion.</br></br> For step by step instructions on how to achieve thsi scenario with EPM, see [Using EPM to transition users from administrator to standard users](epm-scenario-admin-to-standard-user.md)|
|2|Standard User|Standard User|Developers|You want to allow specific users to 'elevate up' without granting local admin rights or using LAPS.|

EPM can help control the elevation of applications in Intune and [Local Users and Groups](endpoint-security-account-protection-policy.md) can be used to control the local administrators group and transition users from administrators to standard users.

Regardless of deployment scenario, we should start by enabling the EPM client for reporting.

Microsoft anticipates customers adopting EPM will go through the folloing phases:

- **Phase 1: Auditing** - Enable EPM client and enable reporting collection.
- **Phase 2: Persona identification** - Identity groups of users with common requirements.
- **Phase 3: Build rules** - Use reporting data to create rules for different personas.
- **Phase 4: Monitoring** - Iterate and refine rules, identify new scenarios.
- **Phase 5: Review user privileges** - Identify and optionally move users from administrator to standard user. Consider enabling 'Support Approved' so that users can request elevation for apps that aren't covered by rules.

Repeat phases 2 to 5 continuously to ensure your users have least privelge in line with Zero Trust principles.

## Next steps

> [!div class="nextstepaction"]
> [Next: Create an elevation settings policy >](epm-elevation-settings.md)
