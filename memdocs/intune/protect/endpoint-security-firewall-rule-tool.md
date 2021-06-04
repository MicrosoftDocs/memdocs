---
# required metadata

title: Endpoint security firewall rule migration tool for Microsoft Intune - Azure | Microsoft Docs
description: Understand how to use the endpoint security firewall rule migration tool for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
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
ms.collection: M365-identity-device-management
ms.reviewer: aanavath
---

# Endpoint security firewall rule migration tool overview

Many organizations are looking to move their security configuration to Microsoft Endpoint Manager to make use of modern, cloud-based management.

Endpoint security in Endpoint Manager offers rich management experiences of Windows Firewall configuration and granular firewall rule management.

In many organizations, they already have Group Policies in place to manage their Windows Firewall rules. Moving to modern management can be tricky as manually creating hundreds of firewall rules can be tiresome.

To help customers move their firewall rule configuration to Endpoint security policies in Endpoint Manager, the **Endpoint security firewall rule migration tool** has been developed.

Customers can run the **Endpoint security firewall rule migration tool** on a reference/pre-configured Windows 10 client, and automatically create Endpoint security firewall rule policies in Endpoint Manager. Once created, administrators can target these rules to Azure AD groups to configure MDM and co-managed clients.

Download the [Endpoint security firewall rule migration tool](https://aka.ms/EndpointSecurityFWRuleMigrationTool):<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## Tool usage

The tool is run on a reference machine and migrates the current Windows Firewall rule configuration. Running the tool will export all enabled firewall rules present on the device, and automatically create new Intune policies with the collected rules.

1. Log on to the reference machine with local administrator privileges.
2. Download and unzip the file `Export-FirewallRules.zip`. <br>
   The zip file contains the script file `Export-FirewallRules.ps1`. 
3. Run the `Export-FirewallRules.ps1` script on the machine. <br>
   The script will download all the prerequisites required to run. When prompted, provide appropriate Intune administrator credentials. For more information about required permissions, see [Required permissions](#required-permissions).
4. Provide a policy name when prompted. <br>
   This policy will be visible in the [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) in the **Endpoint security** > **Firewall** pane. 

    > [!IMPORTANT]
    > The policy name must be unique for the tenant.

    If more than 150 firewall rules are found, multiple policies will be created.

    > [!NOTE]
    > Only enabled firewall rules will be migrated by default and only firewall rules created by GPO will be migrated by default. Switches are provided to modify these default values. For more information, see [Switches](#switches).
    >
    > Depending on the count of firewall rules found, the tool may take some time to run.

5. Once complete, the tool will output a count of firewall rules that could not be automatically migrated. For more information, see [Unsupported configuration](#unsupported-configuration).

## Switches

You can use the following switches (parameters) to modify the tool's default functionality.

- `IncludeLocalRules` - Using this switch will include all locally created/default Windows firewall rules in the export. Note that enabling this switch may result in many included rules. 
- `IncludedDisabledRules` - Using this switch will include all enabled and disabled Windows firewall rules in the export. Note that enabling this switch may result in many included rules.

## Unsupported configuration

The following registry-based settings are not supported due to lack of MDM support in Windows. These settings are uncommon, however should you require these settings please log this need via your standard support channels.

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
The following setting values are not supported for migration:

**Ports**
- `PlayToDiscovery` is not supported as a local or remote port range.

**Address ranges**
- `LocalSubnet6` is not supported as a local or remote address range. 
- `LocalSubnet4` is not supported as a local or remote address range.
- `PlatToDevice` is not supported as a local or remote address range.

Once the tool has been run, a report will be generated with rules that were not successfully migrated. You can view any of these rules by viewing `RulesError.csv` found in `C:\<folder needed>`. 

## Required permissions
Endpoint Security Manager, Intune Service Admin or Global Admin users can migrate Windows Firewall rules to Endpoint security policies. Alternatively, a custom role may be used where Security baselines permissions are set with **Delete**, **Read**, **Assign**, **Create**, and **Update** grants are applied. For more information, see [Grant admin permissions to Intune](../fundamentals/users-add.md#grant-admin-permissions).

## Next steps

- Assign the rules to Azure AD groups to configure MDM and co-managed clients. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
