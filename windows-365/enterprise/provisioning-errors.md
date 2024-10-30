---
# required metadata
title: Troubleshoot provisioning errors
titleSuffix:
description: Troubleshoot provisioning errors in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/13/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Troubleshoot provisioning errors

The following errors can occur during Cloud PC provisioning.

<a name='azure-ad-service-connection-point-scp-misconfigured'></a>

## Microsoft Entra ID service connection point (SCP) misconfigured

The service connection point (SCP) is used by your Cloud PCs to discover your Microsoft Entra tenant information. You must configure your SCPs by using Microsoft Entra Connect for each forest you plan to join Cloud PCs to.

If the SCP configuration doesn't exist, or can't be discovered by using the vNet declared, provisioning will fail.

To understand more about the SCP and learn how to configure it, see the [Microsoft Entra documentation](/azure/active-directory/devices/hybrid-azuread-join-managed-domains).

**Suggested test**: Confirm with your identity team that the SCP exists for all target forests.

## Azure network connection isn’t healthy

Cloud PC provisioning is blocked if the associated ANC isn’t healthy.

The ANC refreshes every 6 hours. Provisioning will fail if the ANC refresh fails while provisioning is under way.

**Suggested test**: Make sure that the ANC is healthy and retry the provisioning.

## Disk allocation error

Windows 365 provisioned the Cloud PC but didn’t allocate the full OS storage according to what the user should have received based on their assigned Windows 365 license. As a result, the user can’t see or use the full storage that they were assigned.

**Suggested test**: Retry provisioning.

## Domain join failed

Windows 365 failed to join the Cloud PC to your on-premises Active Directory (AD) domain. Many factors can cause this failure.

- Makes sure that the AD domain, organizational unit (OU), and credentials in the associated Azure network connection (ANC) are correct.
- Make sure that the domain join user has sufficient permissions to perform the domain join.
- Make sure that the vNet and subnet can reach a domain controller correctly.

JsonADDomainExtension is the Azure function used to perform this domain join. Make sure that everything required for this domain join to be successful is in place.

**Suggested test**: Attach an Azure VM to the configured vNet and perform a domain join using the credentials provided.

<a name='hybrid-azure-ad-join-failed'></a>

## Microsoft Entra hybrid join failed

Windows 365 doesn’t perform any Microsoft Entra hybrid join function for the customer. Microsoft Entra hybrid join must be configured and healthy as a prerequisite for Cloud PC.

If provisioning fails because of Microsoft Entra hybrid join, it’s likely because of an insufficient sync period configured in your AD Sync service. Make sure that Microsoft Entra Connect is configured to sync the AD computer objects every 30 minutes, and no more than 60 minutes. This step times out if the Microsoft Entra object doesn’t appear within 90 minutes.

Another factor to consider is your on-premises AD replication time. Make sure that the domain controller being used for Windows 365 is replicated fast enough to make it into Microsoft Entra ID within this five hour timeout window.

If your organization uses Active Directory Federation Services (ADFS), this registration process is optimized and may result in Cloud PC provisioning completing faster than a Microsoft Entra Connect sync might.

**Suggested test**: Check to see that the AD object:

- Appears in the correct OU.
- Is successfully synced to Microsoft Entra ID before provisioning times out.

## Intune enrollment failed

Windows 365 performs a device-based MDM enrollment into Intune.

If Intune enrollment is failing, make sure that:

- All of the required Intune endpoints are available on the vNet of your Cloud PCs.
- There are no MDM enrollment restrictions on the tenant. Windows corporate device enrollment is allowed in custom and default policies.
- The Intune tenant is active and healthy.
- If co-managing Cloud PCs with Intune and Configuration Manager, ensure that the Cloud PC OU isn't targeted for client push installation. Instead deploy the Configuration Manager agent from Intune. For more information, see Configuration Manager [client installation methods](/mem/configmgr/core/clients/deploy/plan/client-installation-methods#microsoft-intune-mdm-installation).

**Suggested test**: Attempt an Intune enrollment using a test device or VM.

## License not found

While a provisioning is in progress, someone removed the user’s Windows 365 license

**Suggested test**: Make sure that the user has a valid license associated.

## Local administrator permissions error

Windows 365 provisioned the Cloud PC but didn’t grant the user local administrator permissions as defined by a User Settings policy. As a result, the user won’t isn't an administrator on their Cloud PC. So, they can’t make system-level changes or install apps on the system-level context.

**Suggested test**: Retry provisioning or create a new User Settings policy.

## Microsoft Teams optimization error

Windows 365 provisioned the Cloud PC. However, it didn’t configure the Cloud PC to use Microsoft Teams in the mode optimized for running on a remote VM. This optimization doesn't install Microsoft Teams and all components. It only sets the configuration that takes effect if you do install Microsoft Teams on the Cloud PC. If this optimization isn't set and Microsoft Teams is installed on this device, Microsoft Teams doesn't run in the optimized mode for remote connections.

**Suggested test**: Retry provisioning.

## Not enough IP addresses available

When providing a subnet to the ANC, make sure that there are more than sufficient IP addresses.

Every Cloud PC provisioning process uses one of the IP addresses provided in the range.

If a provisioning fails, it's retried a total of three times. Each time, a new vNic and IP address is allocated. These IP addresses will be released in a matter of hours, but this allocation can cause issues if the address space is too narrow.

**Suggested test**: Check the vNet for available IP addresses, and make sure that there are more than enough IPs available for the retry process to succeed.

## Provisioning policy not found

While a provisioning is in progress, someone deleted the provisioning policy.

**Suggested test**: Make sure that the provisioning policy is available and assigned to the correct user group.

## Request disallowed by policy

Windows 365 uses the customer provided vNet to perform a vNic ingestion from the Cloud PC into the customer’s vNet. Sometimes an enterprise implements an Azure Policy to restrict certain Azure objects being created. Make sure that there are no Azure policies that may restrict Windows 365 from creating Azure objects on your behalf.

**Suggested test**: View **Policy** in the Azure portal and look for any policy events that would stop the Windows 365 service from provisioning the Cloud PC.

## Start Menu power icons error

Windows 365 provisioned the Cloud PC but didn’t hide the shutdown and restart icons in the Start Menu. As a result, the user sees the shutdown and restart icons in the Start Menu. If the user ends their Cloud PC connection by selecting the shutdown icon, they may need to restart the Cloud PC from the Cloud PC portal before connecting again.

**Suggested test**: Retry provisioning or create a device configuration policy to [hide the shut down button](/windows/client-management/mdm/policy-csp-start#start-hideshutdown) and to [hide the restart button](/windows/client-management/mdm/policy-csp-start#start-hiderestart).

## Supported Azure regions for Cloud PCs not listed in provisioning user interface

If a specific region isn't listed in the Cloud PC provisioning user interface (UI), but is listed in the [Windows 365 requirements documentation](requirements.md), Windows 365 might expand in a new region. If your networking infrastructure is in such a region, select **New support request** to open a support ticket for evaluation.

## Time zone redirection error

Windows 365 provisioned the Cloud PC but didn’t configure time zone redirection. As a result, the user doesn't see their local time reflected when connected to their Cloud PC. Instead, they see the standard UTC time.

**Suggested test**: Retry provisioning or create a Group Policy Object with the Allow time zone redirection group policy configured. To learn more about the policy, download the [Group Policy Settings Reference Spreadsheet](https://www.microsoft.com/download/101451).

## User not found

While a provisioning is in progress, someone deleted the associated user.

**Suggested test**: Make sure that the assigned user account is valid.

## Windows reset error

Windows 365 provisioned the Cloud PC but didn’t disable the built-in Windows reset option. As a result, the user can manually trigger the built-in Windows reset option under Settings. The Cloud PC will never successfully complete the reset, which makes the Cloud PC unusable.

**Suggested test**: Retry provisioning.

## Blocking High Risk Ports: One or more high risk ports couldn’t be disabled

Windows 365 provisioned the Cloud PC but was unable to block all high-risk ports based on Microsoft security standards. Windows 365 disables high risk ports used for the management of resources or unsecure/unencrypted data transmission and shouldn't be exposed to the internet by default.

If you are seeing this error, some factors to consider are:

- Sometimes an enterprise will implement an Intune group policy that enables one of these ports by default.  
- Make sure that there are no Intune policies that may override Windows 365's default of disabling these high-risk ports.

**Suggested test**: Try any of these solutions:

- Retry provisioning.
- If the device is Intune-enrolled, you can apply Intune policy to disable the ports.
- The user can also disable the ports manually by adding a local firewall rule onto their device. For a list of high risk ports that are recommended for blocking, please see [Security admin rules in Azure Virtual Network Manager](/azure/virtual-network-manager/concept-security-admins#protect-high-risk-ports).

## Other provisioning failures

If you encounter other provisioning errors not covered above, make sure all the required endpoints are allowed on the VNet used for your ANC and any gateway device.

<!-- ########################## -->
## Next steps
[Troubleshooting](troubleshooting.md).
