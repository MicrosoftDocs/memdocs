---
title: Settings list for the Local AI Agent Baseline - OpenClaw security baseline in Intune
description: View the settings in the Microsoft Intune security baseline for Local AI Agent Baseline - OpenClaw. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
ms.date: 05/29/2026
ms.topic: reference
ai-usage: ai-assisted
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Local AI Agent Baseline - OpenClaw security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Local AI Agent Baseline - OpenClaw security baseline for Microsoft Intune.

This baseline limits the use of unauthorized local AI agents such as OpenClaw by configuring device settings that disrupt commonly used execution paths. Included firewall rules restrict outbound network communication from common local agent runtime environments like Node.js.

> [!IMPORTANT]
> These settings might not fully block all agent execution paths. This baseline includes controls that restrict runtime environments (for example, Windows Subsystem for Linux and Node.js) which can be leveraged by local agents. This baseline might also block other processes in addition to OpenClaw. Review and test each setting before deployment, and disable settings that have an unacceptable impact on legitimate workloads.

> [!TIP]
> To identify devices that have local AI agents installed before deploying this baseline, use the [properties catalog](../../device-configuration/collect-device-properties.md) to collect **Local AI Agent** inventory data.

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration settings.

This article displays:

- A list of each setting with its configuration as found in the default instance of that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation or other related content from the relevant product group that provides context and possibly additional details for a settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that were created before the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the current version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:
- [Use security baselines](./overview.md)
- [Change the baseline version for a profile](./configure-baselines.md#update-a-baseline-profile-to-the-latest-version)
- [Manage security baselines](./configure-baselines.md)

## Local AI Agent Baseline - OpenClaw (Preview), Version 1

### Windows Subsystem For Linux

- **Allow WSL1**\
  Baseline default: *Enabled*\
  [Learn more](/windows/wsl/compare-versions)

- **Allow the Windows Subsystem For Linux**\
  Baseline default: *Enabled*\
  [Learn more](/windows/wsl/about)

### Firewall

- **Firewall Rule Name**\
  Baseline default: *Configured*\
  [Learn more](/windows/client-management/mdm/firewall-csp)

  This baseline includes two preconfigured firewall rules. Both rules block outbound TCP connections from Node.js executables to disrupt common execution paths used by OpenClaw.

  #### Rule: block nodejs in LOCALAPPDATA folder

  | Property | Default value |
  |---|---|
  | Enabled | *Enabled* |
  | Name | block nodejs in LOCALAPPDATA folder |
  | Interface Types | *All* |
  | File Path | `%LOCALAPPDATA%\Programs\node\node.exe` |
  | Network Types | *FW_PROFILE_TYPE_ALL* |
  | Direction | *The rule applies to outbound traffic* |
  | Action | *Block* |
  | Protocol | *Configured* - 6 (TCP) |

  #### Rule: block nodejs in ProgramFiles folder

  | Property | Default value |
  |---|---|
  | Enabled | *Enabled* |
  | Name | block nodejs in ProgramFiles folder |
  | Interface Types | *All* |
  | File Path | `%ProgramFiles%\nodejs\node.exe` |
  | Network Types | *FW_PROFILE_TYPE_ALL* |
  | Direction | *The rule applies to outbound traffic* |
  | Action | *Block* |
  | Protocol | *Configured* - 6 (TCP) |

  For details about firewall rule properties, see [Firewall CSP - FirewallRules](/windows/client-management/mdm/firewall-csp#mdmstorefirewallrules).
