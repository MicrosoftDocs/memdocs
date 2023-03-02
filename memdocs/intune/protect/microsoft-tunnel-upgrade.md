---
title: Upgrade the Microsoft Tunnel Gateway server software
description: Understand how Microsoft Tunnel Gateway upgrades to new versions of the tunnel software for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Upgrade Microsoft Tunnel for Microsoft Intune

Microsoft Tunnel, a VPN gateway solution for Microsoft Intune, periodically receives [software upgrades](#microsoft-tunnel-update-history), which must install on the tunnel servers to keep them in support. To stay in support, servers must run the most recent release, or at most be one version behind. The information in this article explains the upgrade process, upgrade controls, and status reports you use to understand the software version of tunnel servers, when upgrades are available, and how to control when upgrades happen.

Intune handles the upgrade of servers assigned to each tunnel site for you. When upgrades for  site begin, all servers in the site will upgrade one at a time, which is referred to as an upgrade cycle. While a server is upgrading, the Microsoft Tunnel on the server isn't available for use. Upgrading a single server at a time helps minimize disruptions to users when the site includes multiple servers.  

During an upgrade cycle:

- Intune begins by upgrading one server in the site. The upgrade can start as soon as 10 minutes after the release becomes available.
- If a server was off, upgrade begins after the server turns on.
- After a successful upgrade of one server at a site, Intune waits a short time before it starts the upgrade of the next server.

## Use upgrade controls

To help control when Intune begins the upgrade cycle, configure the following settings at each site. You can configure the settings when [creating a new site](../protect/microsoft-tunnel-configure.md#create-a-site), or by editing the properties of an existing site:

- **Automatically upgrade servers at this site**
- **Limit server upgrades to maintenance window**

### Automatically upgrade servers at this site

This setting determines if an upgrade cycle for the site can begin automatically, or if an admin must explicitly approve the upgrade before the cycle can begin.

- **Yes** *(default)* – When set to *Yes*, the site automatically upgrade servers as soon as possible after a new tunnel version becomes available. Upgrades begin without admin intervention.

  If you set a maintenance window for the site, the upgrade cycle begins between the windows start and end time. When no maintenance window is set, the upgrade cycle starts as soon as possible.

- **No** – When set to *No*, Intune won’t upgrade servers until an admin explicitly chooses to begin the upgrade cycle.

  After upgrade is approved for a site with a maintenance window, the upgrade cycle begins between the windows start and end time. If there's no maintenance window, the upgrade cycle starts as soon as possible.

  > [!IMPORTANT]  
  > When you configure site for manual upgrades, periodically review the [Health check](#view-tunnel-server-status) tab to understand when newer versions of Microsoft Tunnel are available to install. The report also identifies when the current tunnel version at the site is out of support.

### Limit server upgrades to maintenance window

Use this setting to define a maintenance window for the site.

When configured for site, the server upgrade cycle can begin only during the configured period. However, once begun, the cycle continues to update servers one-by-one until all servers assigned to the site complete the upgrade.

- **No** *(default)* – No maintenance window is set. Sites configured to upgrade automatically will do so as soon as possible. Sites configured to require explicit action to start the upgrade will do so as soon as possible *after* the upgrade is approved.

- **Yes** – Set a maintenance window. The window limits when a server upgrade cycle can begin at the site. The maintenance window doesn’t define when individual servers assigned to the site might start to upgrade.

  Sites configured to upgrade automatically will start the upgrade cycle only during the configured period. Sites configured to require the admin to approve the upgrade before beginning, will do during the next maintenance window *after* the upgrade is approved.

  When set to *Yes*, configure the following options:

  - **Time zone** – The time zone you select determines when the maintenance window starts and ends on all servers in the site. The time zone of individual servers isn't used.
  - **Start time** – Specify the earliest time that the upgrade cycle can start, based on the time zone you selected.
  - **End time** - Specify the latest time that upgrade cycle can start, based on the time zone you selected. Upgrade cycles that start before this time will continue to run and can complete after this time.

## View tunnel server status

You can view information about the status of Microsoft Tunnel servers, including the version of Microsoft Tunnel on a server.

For sites that don't support automatic upgrade, you can also view when upgrades to a new version are available.

Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**.  Select a server and then open the **Health check** tab to view the following information about it:

- **Server version** - The status of the Tunnel Gateway Server software, in the context of the most recent version available.

  - **Healthy** - Up to date with the most recent software version. 
  - **Warning** - One version behind.
  - **Unhealthy** - Two or more versions behind, and out of support.

When a server doesn’t run the most recent software version, plan to install an available upgrade to keep the Microsoft Tunnel in support.

## Approve upgrades

Sites that have the setting *Automatically upgrade servers at this site* set to *No* won't automatically upgrade servers. Instead, an admin must approve upgrades for servers at that site before the upgrade cycle starts.

To understand when an upgrade is available for servers, use the [Health check](#view-tunnel-server-status) tab to review server status.
### To approve an upgrade

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > **Sites**.

2. Select the site with an **Upgrade type** of **Manual**.

3. On the site’s properties, select **Upgrade servers**.

After you choose to upgrade servers, Intune starts the process to do so, which cannot be canceled. The time that upgrades begin at the site depends on the configuration of maintenance windows for the site.

<!-- ## Manage upgrades

Upgrade installation depends on how a site is configured.

### Sites that support automatic upgrade

When a site [supports automatic upgrades](#automatically-upgrade-servers-at-this-site) of servers, no administrative action is necessary. When the upgrade starts depends on the configuration of a maintenance window for the site:

- **Without a maintenance window**: Upgrade start as soon as possible after a new version of Microsoft Tunnel becomes available.

- **With a maintenance window**: Upgrades start during the next maintenance window after a new version of Microsoft Tunnel becomes available.

### Sites that don't support automatic upgrade

When a site [doesn’t support automatic upgrade](#automatically-upgrade-servers-at-this-site), new versions of Microsoft Tunnel must be explicitly approved for the site before servers will upgrade.

Use the [Health check](#view-tunnel-server-status) tab to understand when newer versions of Microsoft Tunnel are available to install. The report also identifies when the current tunnel version at the site is out of support.

#### To approve installation of an upgrade

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway** > **Sites**.

2. Select the site with an **Upgrade type** of **Manual**.

3. On the site’s properties, select **Upgrade servers**.

After you choose to upgrade servers, Intune starts the process to do so, which cannot be canceled. The time that upgrades begin at the site depends on the configuration of maintenance windows for the site.
-->
## Microsoft Tunnel update history

Updates for the Microsoft Tunnel release periodically. When a new version is available, read about the changes here.

After an update releases, it rolls out to tenants over the following days. This rollout time means new updates might not be available for your tunnel servers for a few days.

The Microsoft Tunnel version for a server isn’t available in the Intune UI at this time. Instead, run the following command on the Linux server that hosts the tunnel to identify the hash values of  *agentImageDigest* and *serverImageDiegest*: `cat /etc/mstunnel/images_configured`

### March 1, 2023

Image hash values:

- **agentImageDigest**:  sha256:c4478f5e54dc1536523113885095b6eda37da1b2a31461347cd85ea8a7d487b5

- **serverImageDigest**: sha256:cf706bc6a5ea8a743bab84ed8be9901733738881e2e84d0f9083654e9c5cd317

Changes in this release:
- Minor bug fixes
- Updated Microsoft Tunnel Server Gateway EULA


### February 2, 2023

Image hash values:

- **agentImageDigest**:  sha256:9140d4e7f397d0a7c6c203b0c74a4f11b66affee3d36837298a50821b5dca9a4

- **serverImageDigest**: sha256:709219327f6aff5f81f6b6dc9f644334ccefd6af2f75ed4461ae06885bff9551

Changes in this release:
- Minor bug fixes


### November 16, 2022

Image hash values:

- **agentImageDigest**:  sha256:517a2267b5b4fbbd58ab46be22202158e55562bfb8f79eb7ef4fc35a0fc3cc8d

- **serverImageDigest**: sha256:3a367955746522fe89fc8f0fb6edc259aefe0e681db652281b1ff264fdcce6dc

Changes in this release:
- Minor bug fixes
- Security improvements
- Journalctl logging fix in mst-cli



### September 23, 2022

Image hash values:

- **agentImageDigest**:  sha256:df03d4ad8469511a4b649dcbbad5dbaa5c7f10cdc9640b7801190623090a67ae

- **serverImageDigest**: sha256:0f66f2b5463e283c1621fc4250f69fac97ebda77bef8f570ed181b78000d762c

Changes in this release:
- Minor bug fixes
- Security improvements
- Mst-readiness script enhancements
- Add Azure storage endpoint 


### August 22, 2022

Image hash values:

- **agentImageDigest**:  sha256:186ff8d5c9a70085adc01778251f577988fef9b456801dc30e846f1a2bc3784c

- **serverImageDigest**: sha256:ec5bd023b5582e58b6b9eb6aa41a9b064003f5b2b228508115bf6d42be9564a3

Changes in this release:
- Security improvements
- Mst-readiness script enhancements


### July 27, 2022

Image hash values:

- **agentImageDigest**:  sha256:94e08d27c4f18706b2e3d92594d8a173446638a641240ae86a18a583be257cae

- **serverImageDigest**: sha256:683ff13cfc16824741e961f04b94bce766777a5dcc80f019af234b4c9948fd66

Changes in this release:
- Minor bug fixes
- Set process limit to 6000 in the server container 


### June 30, 2022

Image hash values:

- **agentImageDigest**:  sha256:b42b8e158cebb91b6a69f2bdcedffde18a5f3f12cc502509c8aa9fea80f4daaa

- **serverImageDigest**: sha256:aa45b73bf143f1e440329853362cb4f300d9cc865d758534a94b983c8286ca4d

Changes in this release:
- Minor bug fixes
- Advanced setting improvements in Microsoft Tunnel configurations 
- Logging improvements


### April 27, 2022

Image hash values:

- **agentImageDigest**:  sha256:588c0c59fb9e0032640e78b06cfe12c7be0b28b1d8ca01ad87fb315da4088446

- **serverImageDigest**: sha256:81d42ec83b5157068b81d6243d46601b8c003e99513426ffb90d9cbac31bd271

Changes in this release:
- Minor bug fixes
- Security bug fixes
- Agent changes for forced cert renewal 
- ADAL depcrecation, enables MSAL authentication during Agent enrollment 

### April 4, 2022

Image hash values:

- **agentImageDigest**:  sha256:14a5f496bf9d36ba1577e8e6059f5d06b7c03abe319eaba91a4ac88eeafc4825

- **serverImageDigest**: sha256:f21481a2a299cb2beed7faadf4faba50fdcf1bb591d193ee78d1e0505bcaa192

Changes in this release:
- Minor bug fixes
- Access log enhancements

### February 16, 2022

Image hash values:

- **agentImageDigest**: sha256:3298794bfda519886591cd8676a3074adb05911fa63278cc1436dd7a0b223166

- **serverImageDigest**: sha256:4021370532c3659e304bbc594fde7d788bd660a53542e427048931a0d660bfaa

Changes in this release:
- Minor bug fixes

### January 31, 2022

Image hash values:

- **agentImageDigest**: sha256:7371a4bd6979f71260093b7ab51ad414c28f3894284f7a7ae950362917a4654b

- **serverImageDigest**: sha256:c8e2be399ca813b0d70c71e56c3b15946a341458c5e1e0ccd07bfd7574e47827

Changes in this release:

- Minor bug fixes
- A new version of the *mst-readiness* tool is available for download. We recommend using the updated script, which now checks the Linux server build for the presence of the *ip_tables* module. While most Linux distributions load this module be default, some versions, like RHEL 8.5 and RHEL 8.6, do not.

  For more information including where to download the tool, see [Run the readiness tool](../protect/Microsoft-tunnel-prerequisites.md#run-the-readiness-tool).  



### October 25, 2021

Image hash values:

- **agentImageDigest**: sha256:fa4a1e5bd701adc447aa41f11daf83c615b7b16b7994b5d86c383955fd6cdad7

- **serverImageDigest**: sha256:aefcb35c5410b87eb8a46da3e98199aa60e74cdc12eb5b86a0a36420cd64005d

Changes in this release:

- Added ability to get a client network trace
- Added ability to enabled resource access tracking
- Added support for Podman when using [some versions](../protect/microsoft-tunnel-prerequisites.md#linux-server) of Red Hat Enterprise Linux
- Minor bug fixes

### September 7, 2021

Image hash values:

- **agentImageDigest**: sha256:21ea5938137c1339a2425c16009ba7de0fd0179a61399f8fe840814f51f45ded

- **serverImageDigest**: sha256:f7b89b8358b90e24a2d7a478944cccfdca960b8b0267f31849b35d933f5a9a7b

Changes in this release:

- Added ability to add host entries to the server container
- Security patches applied
- Minor bug fixes


### June 14, 2021

Image hash values:

- **agentImageDigest**: sha256:7e6be11bcd9fef42d015665f2335c2a09f729c71e886f3722d9c7b18a782a98b

- **serverImageDigest**: sha256:08992453eac8908f1cad3cbbdac75e41b363c457a95cd2924d5bbc3951fe2e6d

Changes in this release:

- Minor bug fixes
- Image updates with security updates for all dependencies

### March 29, 2021

Image hash values:

- **agentImageDigest**: sha256:7ff81ebec9d129558cf07ba1d044d4051dbfaf9eb75cc91500a11f4ef0cb447e

- **serverImageDigest**: sha256:56dc303c67735bad243b2dc8644cc3d1e5318aa963be05a9a685ec6bcbb41c4e

Changes in this release:

- Minor bug fixes and enhancements

### January 19, 2021

Image hash values:

- **agentImageDigest**: sha256:227557e71b197c5c26baeed7633e5f89b476bbb8eb23fc82dec260890d5145f1

- **serverImageDigest**: sha256:70026dc3585db871f419d25066e655902af732286b0537512d53e1f0897cc423

Changes in this release:

- Support for Red Hat Enterprise Linux 8.
- Extraneous logging suppressed.

### October 29, 2020

Image hash values:

- **agentImageDigest**: sha256:ba48de2c746a68286d15985f807702c60004131368a4a6a50ceab0f04653031a

- **serverImageDigest**: sha256:a60d778664f7f3ba28d363ec783014d9fc2eda6cc5f6057a1eab8635928e7b07

Changes in this release:

- Fixes for logging. [View the Microsoft Tunnel system logs](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs).
- Additional bug fixes.

### October 12, 2020

Image hash values:

- **agentImageDigest**: sha256:d168e416591d94d6a02b64e5dde8709e2d5a44261d67036caafcb55b12912ca5

- **serverImageDigest**: sha256:8b50257a94b9825915cb6a77ed49cfb3e5c6f68da9ae0272cdf8e49cff3d342e

Changes in this release:

- Microsoft Tunnel now [logs](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs) operational and monitoring details to Linux server logs in the *syslog* format.
- Various bug fixes.

### September 23, 2020

The initial public preview release of Microsoft Tunnel.

<!-- Archive of past releases
-->

## Next steps

[Reference for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md)
