---
title: Change Review Agent Overview
description: Learn about the Change Review Agent in Microsoft Intune, its prerequisites, and how it works.
ms.date: 11/17/2025
ms.topic: overview
author: brenduns
ms.author: brenduns
ms.reviewer: 
---

# Change Review Agent overview

## How it works

## Prerequisites

<!-- start cloud -->
:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]
:::column-end:::

:::column span="3":::
> The agent is supported on the public cloud ony. It isn't supported on government clouds.
:::column-end:::
:::row-end:::
<!-- end cloud -->

<!-- start license -->
:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> To use Security Copilot agents in Microsoft Intune, your organization must meet specific licensing requirements.
>
> Required licenses:
> - [Microsoft Intune Plan 1 subscription](../intune-service/fundamentals/licenses.md)
> - [Microsoft Security Copilot](/copilot/security/get-started-security-copilot) with sufficient security compute units (SCUs)
:::column-end:::
:::row-end:::
<!-- end license -->

<!-- stat plugin -->
:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/plugins.md)]
:::column-end:::
:::column span="3":::
> Plugins enable Security Copilot agents to connect with Microsoft services and perform specialized actions.
>
> The Change Review Agent requires the following plugins:
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
>
> Optional plugins:
> - [!INCLUDE [plugin-entra](includes/plugin-entra.md)] 
> - [!INCLUDE [plugin-defender](includes/plugin-defender.md)] 
> - Pending clarification 'Microsoft Threat Intelligence`
>
> [Learn more about plugins](https://go.microsoft.com/fwlink/?linkid=2316474).
:::column-end:::
:::row-end:::
<!-- end plugin -->

<!-- start platform ../../media/icons/admin-center/devices.svg  -->
:::row:::
:::column span="1":::
:::image type="icon" source="../media/icons/admin-center/devices.svg" border="false"::: **Platform requirements and scenarios**
:::column-end:::
:::column span="3":::
> The agent supports evaluation and recommendations for the following platforms and scenarios:
> - Windows
> - PowerShell scripts in Intune
:::column-end:::
:::row-end:::
<!-- end platform -->

<!-- start rbac -->
:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> Role requirements vary based on whether you're configuring the agent or using it, and on the specific actions performed.
>
> ---
>
> To **enable and configure** the Change Review Agent, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
>
> :::image type="icon" source="../media/icons/admin-center/defender.svg" border="false"::: Defender roles - Defender role-based access control (RBAC) roles depend on your Defender XDR implementation:
> - [Unified RBAC](/defender-xdr/manage-rbac): Assign the Microsoft Entra ID Security Reader to the agent's identity account. This role provides read-only access to Defender Vulnerability Management data and automatically enforces device group scoping.
> - [Granular RBAC](/defender-endpoint/rbac): Assign a custom RBAC role with permissions equivalent to the Unified RBAC Security Reader role. For example: 
>   - **View data** – **Defender Vulnerability Management** - This permission maps to the Unified RBAC permission *Security posture / Posture management / Vulnerability management (read)*.
>   - **Entra/Identity risky user (read)** - This permission maps to the Unified RBAC permission *Security posture / Identity risk / Risky users (read)*.
>
>    For details about mapping permissions to the Unified RBAC Security Reader role, see [Microsoft Entra Global roles access](/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access) in the *Map Microsoft Defender XDR Unified role-based access control (RBAC)* article in the Defender documentation.
>
>    Ensure the agent’s identity is scoped in Microsoft Defender to include all relevant device groups. The agent can't access or report on devices outside its assigned scope.
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot owner](/copilot/security/authentication#security-copilot-roles) 
>
> ---
>
> To **use** the agent and perform offboarding actions, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles:
> - [Read Only Operator](/intune/intune-service/fundamentals/role-based-access-control#built-in-roles) or [custom role](/intune/intune-service/fundamentals/role-based-access-control#custom-roles) with equivalent permissions.
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Entra roles:
> - [Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)
> 
> :::image type="icon" source="../media/icons/admin-center/defender.svg" border="false"::: Defender roles
> - Use of the agent requires the same access as agent setup.
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot contributor](/copilot/security/authentication#security-copilot-roles)

:::column-end:::
:::row-end:::
<!-- end rbac -->





<!-- start  -->
<!-- end   -->
<!-- start  -->
<!-- end   -->
<!-- start  -->
<!-- end   -->
<!-- start  -->
<!-- end   -->
<!-- start  -->
<!-- end   -->

## Configuration

## Enable the agent
## Explore the agent options
## Configure custom instructions
## Renew the agent
## Remove the agent



## Next steps

- [Use the Change Review Agent](/intune/agents/change-review-agent-use)