---
# required metadata

title: Endpoint security firewall rule migration tool for Microsoft Intune
description: Learn about the endpoint security firewall rule migration tool for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/31/2022
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
ms.reviewer: laarrizz
---

# Endpoint security firewall rule migration tool overview

Many organizations are moving their security configuration to Microsoft Intune to make use of modern, cloud-based management. Endpoint security in Endpoint Manager offers rich management experiences of Windows Firewall configuration and granular firewall rule management.

Because it can be challenging to move large numbers of existing Group Policies for Windows Firewall rules to Endpoint security policies in Endpoint Manager, we've created the **Endpoint security firewall rule migration tool**, which is a PowerShell script.

When you run the **Endpoint security firewall rule migration tool** on a reference Windows 10/11 client that has firewall rules based on Group Policy applied, the tool can automatically create Endpoint security firewall rule policies in Endpoint Manager. After the endpoint security rules are created, administrators can target the rules to Azure AD groups to configure MDM and co-managed clients.

Download the [Endpoint security firewall rule migration tool](https://aka.ms/EndpointSecurityFWRuleMigrationTool):

<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## Tool usage

> [!TIP]
> The tool's PowerShell script looks for endpoint security policies that target **MDM**. When there are no policies that target **MDM**, the script can loop and fail to exit. To work around this condition, either add a policy that targets MDM before running the script, or edit the line 46 of the script to the following: `while(($profileNameExist) -and ($profiles.Count -gt 0))`

Run the tool on a reference machine to migrate that machines current Windows Firewall rule configuration. When run, the tool exports all enabled firewall rules that are present on the device, and automatically creates new Intune policies with the collected rules.

1. Sign in to the reference machine with local administrator privileges.

2. Download and unzip the file `Export-FirewallRules.zip`.

   The zip file contains the script file `Export-FirewallRules.ps1`.

3. Run the `Export-FirewallRules.ps1` script on the machine.

   The script downloads all the prerequisites it requires to run. When prompted, provide appropriate Intune administrator credentials. For more information about required permissions, see [Required permissions](#required-permissions).

4. Provide a policy name when prompted. The policy name must be unique for the tenant.

   When more than 150 firewall rules are found, multiple policies are created.

   Policies created by the tool are visible in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) in the **Endpoint security** > **Firewall** pane.

   > [!NOTE]
   > By default, only enabled firewall rules are migrated and only firewall rules created by GPO are migrated. The tool supports [switches](#switches) you can use to modify these defaults.  
   >
   > The time the tool takes to run depends on the number of firewall rules found.

5. After the tool runs, it outputs a count of firewall rules that it couldn't automatically migrate. For more information, see [Unsupported configuration](#unsupported-configuration).

## Switches

Use the following switches (parameters) to modify the tool's default behavior.

- `IncludeLocalRules` - Use this switch to include all locally created/default Windows firewall rules in the export. Use of this switch can result in a large count of included rules.

- `IncludedDisabledRules` - e this switch to include all enabled and disabled Windows firewall rules in the export. Use of this switch can result in a large count of included rules.

## Unsupported configuration

The following registry-based settings aren't supported because of a lack of MDM support in Windows. While these settings are uncommon, should you require these settings consider logging this need through your standard support channels.

|     GPO Field    |     Reason    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     Interface Identifier (LUID) is not manageable    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     Inbound NAT Traversal related not exposed via Group Policy or   Windows MDM    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     Loose Source Mapped not exposed via Group Policy or Windows   MDM    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     OS Versioning not exposed via Group Policy or Windows MDM    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     Local Only Mapped not exposed via Group Policy or Windows MDM    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     Redundant setting not exposed via Group Policy or Windows MDM    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     Allow profile crossing not exposed via Group Policy or Windows   MDM    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     Local User Owner SID not applicable in MDM    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     Match traffic with the trust tuple keyword not exposed via   Group Policy or Windows MDM    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     Match traffic with the trust tuple keyword not exposed via   Group Policy or Windows MDM    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     Match traffic with the trust tuple keyword not exposed via   Group Policy or Windows MDM    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     Match traffic with the trust tuple keyword not exposed via   Group Policy or Windows MDM    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     IPSec related setting not supported by Windows MDM    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     IPSec related setting not supported by Windows MDM    |

## Unsupported setting values

The following setting values aren't supported for migration:

**Ports**:

- `PlayToDiscovery` isn't supported as a local or remote port range.

**Address ranges**:

- `LocalSubnet6` isn't supported as a local or remote address range.
- `LocalSubnet4` isn't supported as a local or remote address range.
- `PlatToDevice` isn't supported as a local or remote address range.

After the tool completes, it generates a report with rules that weren't successfully migrated. You can view these rules by viewing `RulesError.csv` found in `C:\<folder>`.

## Required permissions

Users assigned the Intune roles for Endpoint Security Manager, Intune Service Admin, or Global Admin can migrate Windows Firewall rules to Endpoint security policies. Alternatively, you can assign the user a custom role where Security baselines permissions are set with **Delete**, **Read**, **Assign**, **Create**, and **Update** grants are applied. For more information, see [Grant admin permissions to Intune](../fundamentals/users-add.md#grant-admin-permissions).

## Next steps

After creating Endpoint security policies for Firewall rules, assign those policies to Azure AD groups to configure both your MDM and co-managed clients. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
