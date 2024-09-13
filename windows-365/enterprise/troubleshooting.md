---
# required metadata
title: Troubleshooting Windows 365
titleSuffix:
description: Troubleshooting issues with Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/20/2024
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: docoombs
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier1
---

# Troubleshooting

This article provides suggestions for troubleshooting Windows 365 issues.

## Contact help/support

For instructions on how to get help and open a support ticket, see  [How to get support in Microsoft Intune](/mem/get-support). Support is included as part of your Windows 365 subscription.

Since Cloud PCs work like most physical devices, you can use existing troubleshooting documentation to troubleshoot issues with [Windows client](/troubleshoot/windows-client/welcome-windows-client), [Microsoft 365 services](/microsoft-365/), and [Microsoft Intune admin center](/mem/get-support).

## Audio and video redirection not working

For connections using the Remote Desktop client for Windows to access Cloud PCs, the first time a user signs in to their Cloud PC, Microsoft Teams will be installed.

After the installation, the optimizations to redirect audio and video to your local Windows endpoint don’t work. The user must close Teams and sign out from or restart the Cloud PC to activate the Optimized status.

## Conditional access

Make sure that you apply conditional access policies to both the dedicated Windows 365 cloud app and the Azure Virtual Desktop cloud app. You can apply these policies in the conditional access UI of Microsoft Intune admin center or Microsoft Entra ID.

Any conditional access policy that you apply will affect:

- Access to the end-user web portal
- The connection to the Cloud PC from the Remote Desktop apps.

For more information about service dependencies in Microsoft Entra Conditional Access, see [Conditional Access service dependencies](/azure/active-directory/conditional-access/service-dependencies).

Applying a more restrictive policy to Azure Virtual Desktop than the Windows 365 cloud app will result in Microsoft Entra ID honoring the more restrictive policy. This policy will affect end user connectivity to their Cloud PCs after accessing the Windows 365 end user portal.

For more information on how a given policy may affect your environment, see [Troubleshoot using the What If tool in Conditional Access](/azure/active-directory/conditional-access/what-if-tool).

## Help users in your organization

You can use the Intune Troubleshooting page to view enrollment issues, remediation steps, and user details. For more information, see [Use the troubleshooting portal to help users at your company](/mem/intune/fundamentals/help-desk-operators).

[App Assure](https://www.microsoft.com/fasttrack/microsoft-365/app-assure) is a service for Microsoft’s enterprise customers who encounter application compatibility issues. App Assure will help remediate issues with your ISV, line-of-business and Microsoft-developed apps at no extra cost. If you encounter any app compatibility issues, follow the instructions above to submit a case and include a short description of the issue.

## Language pack installation failed

You can try either of these possible solutions:

- If the language pack installation failed, try reprovisioning the Cloud PC to install the language pack again.
- Check to see if there's an Attack Surface Reduction rule set on Intune. If the **Block process creations originating from PSExec and WMI commands** is set to Block, it will block language pack installation. You can remove the rule and retry provisioning, or provisioning with default language set to en-us. Then, let the user change the language by using the Windows Settings App in the Cloud PC.

## Networking

The [Azure network connection checks](health-checks.md) help to make sure that network connectivity is working. Always retry the Azure network connection if you suspect networking issues might be causing issues. Using the Azure network connection checks helps make sure that repeated and consistent checks are used as the first troubleshooting step.

Keep in mind that the Azure network connection checks are validating the infrastructure configuration of your environment. They don't run checks to validate any extra configuration or applications deployed to Cloud PCs after provisioning by Microsoft Intune or third party agents. These agents or configurations can introduce other issues that the Azure network connection can't test for ahead of provisioning.

For example, if you deploy a VPN client to all devices in Microsoft Intune, make sure that this client doesn’t:

- Break connectivity to Azure Virtual Desktop [endpoints required](requirements-network.md) by Windows 365.
- Exclude your Cloud PCs for having the VPN client deployed to them.

Finally, consider temporarily deploying a test Azure virtual machine to the Azure network subnet that you’re trying to provision or connect to your Cloud PCs. This test machine will let you run all the network tests that you require from that network. You can use the PowerShell Test-NetConnection command to test connectivity on specific ports to specific network endpoints/URLs:

```Test-NetConnection <hostname> -Port 443```

## Azure network connections

For suggested remediations on, see [Troubleshoot Azure network connections](troubleshoot-azure-network-connection.md).

## Provisioning issues

For suggested remediations on, see [Troubleshoot provisioning errors](provisioning-errors.md).

## Troubleshooting by end users

The end user can troubleshoot some issues that might be preventing them from connecting to their Cloud PC. For more information, see [End-user actions](../end-user-access-cloud-pc.md#user-actions).

## Video playback improvements

You can improve video playback performance on your Cloud PCs by using multimedia redirection (MMR).

For Cloud PCs, MMR is supported on the following platforms: Windows, macOS, ChromeOS, Linux.

For more information, see [Multimedia redirection for Azure Virtual Desktop](/azure/virtual-desktop/multimedia-redirection) and [Troubleshoot multimedia redirection for Azure Virtual Desktop](/azure/virtual-desktop/troubleshoot-multimedia-redirection).

## Your organization hasn’t assigned you a Cloud PC

When accessing windows365.microsoft.com, the user receives a message "Your organization hasn't assigned you a Cloud PC".

**Possible cause**: To have access to a Cloud PC, a user must be assigned a license and a provisioning policy must be created.

**Troubleshooting steps**: Make sure that:

1. The user has been assigned a Windows 365 license. For more information, see [Assign licenses](assign-licenses.md) and [Windows 365 plans and pricing](https://www.microsoft.com/windows-365/enterprise?rtc=1).
2. You’ve created a provisioning policy that includes the user. For more information, see [Create provisioning policies]( /windows-365/enterprise/create-provisioning-policy).

## Performance decreases with nested virtualization

Some users may experience a decline in their 4vCPU Cloud PC performance when using nested virtualization.

**Troubleshooting steps:**

- [Reprovision](reprovision-cloud-pc.md) the Cloud PC, or
- Uninstall Hyper-V on the Cloud PC.  

## Windows 365 Frontline user message: Your Cloud PC should be available soon

If you've reached the maximum number of active user sessions in your tenant, any more users who try to start a user session will see a  message in the end user portal that says: "Your Cloud PC should be available soon".

**Troubleshooting steps**: Use the [utilization report](report-cloud-pc-utilization.md) to estimate the right amount of license for your organization.

<!-- ########################## -->
## Next steps

[Troubleshoot Azure network connections](troubleshoot-azure-network-connection.md).
