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

<!-- start platform -->
:::row:::
:::column span="1":::
:::image type="icon" source="../../media/icons/admin-center/devices.svg" border="false"::: **Device platform and scenarios**
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

## How it works
## Enable the agent
## Explore the agent options
## Configure custom instructions
## Renew the agent
## Remove the agent



## Next steps

- [Use the Change Review Agent](/intune/agents/change-review-agent-use)