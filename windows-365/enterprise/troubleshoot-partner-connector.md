---
# required metadata
title: Troubleshoot partner connectors for Windows 365
titleSuffix:
description: Troubleshoot partner connectors for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/01/2024
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aradinger
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Troubleshoot partner connectors for Windows 365

When you turn on a partner connector (Citrix HDX Plus, Omnissa, or HP Anyware) for a user, the partner agent is automatically installed on that user's Cloud PCs. The agent enables the corresponding third party protocol. If this installation runs into a problem, you get an error message in the All Cloud PC list. The description of the error includes advice on how to troubleshoot the error.

If the partner agent installation fails, the user can still connect to their Cloud PC by using Remote Desktop.

While troubleshooting errors, make sure that the following steps were successful:

- The users license state is synchronized from the partner service to Microsoft Intune, including the users Microsoft Entra user ID.
  - The prerequisites have been met.
  - The partner connector is enabled and healthy in Microsoft Intune.
  - The correct permissions have been set for the partner third-party apps in Microsoft Entra ID.
  - The Microsoft Entra user is added and discoverable  in the Parter Cloud console.
- The partner agent is downloaded on the Cloud PC.
  - The Cloud PC can access partner download URL.
  - No security policy is blocking PowerShell or any app/agent installation as System.
- The partner Agent is installed.
  - Check **Apps & Features** to see if the partner Agent is installed on the Cloud PC.
  - Check Windows event viewer (eventvwr.msc) logs to make sure that the agent installation is executed.
  - Check installation logs for any failures:
    - Citrix: %TEMPsystemdrive%\Windows\Temp\Citrix\XenDesktop Installer.
    - Omnissa:
      - For installation issues: C:\Windows\Temp\Omnissa_Horizon_Agents_Installer_**.log
      - Run this script for collecting the logs for post installation issues: C:\Program Files\Omnissa\Horizon Agents\Horizon Agent\DCT\support.bat
    - HP Anyware:
      - C:\Teradici\provisioning.log 
      - Or on the client side, select **Generate support bundle**. 
- The Cloud PC is registered into the partner cloud tenant.
  - Check the Cloud PC registration status in the partner configuration console.
  - If the Cloud PC is unregistered, check the Application sign-in Windows event viewer (eventvwr.msc) for partner service errors and warnings.

After you find the root cause, remove the assigned license from the partner console and then add the license back in. This removal should trigger a reinstallation of the partner agent.

If no other solution works, you can [reprovision](reprovision-cloud-pc.md) the Cloud PC to reattempt the enablement. Reprovisioning deletes the Cloud PC and create a brand new one. All data on the original Cloud PC will be lost. Therefore, reprovisioning should be the last resort to resolve the issue.

## Troubleshoot connection issues

If you’re having connectivity issues with your partner-provisioned Cloud PC, you may want to test the default RDP-based connectivity. This process is a handy troubleshooting technique to determine if the issue is with the Cloud PC or the partner connectivity.

### Turn on the RDP protocol

When the partner protocol is turned on, the Windows 365 remoting protocol remains enabled but inactive. This inactivity means that users trying to connect with the Windows 365 supported Remote Desktop clients (including the HTML5 browser) are blocked by default. Users can only connect by using the partner protocol. Users trying to connect with non-partner clients get a generic error message.

You can turn on the RDP protocol so users can sign in with RDP to test the Cloud PC connectivity. You can do either of the following to turn on the RDP protocol:

- [Make a user a local admin](assign-users-as-local-admin.md) on the Cloud PC.
- [Add the user to the Direct Access Users group on the Cloud PC](/windows/client-management/mdm/policy-csp-localusersandgroups?WT.mc_id=Portal-fx).

After taking either of these steps,  you might have to reboot the Cloud PC for the group membership updates to take effect. Afterwards, the user can connect by using either RDP or the partner protocol.

You can now test the connectivity by using RDP, and raise a support case with the relevant support team if problems persist.

<!-- ########################## -->
## Next steps

[Learn about Citrix HDX Plus for Windows 365](set-up-citrix.md).
[Learn about HP Anyware for Windows 365](hp-anyware-set-up.md).
[Learn about Omnissa Horizon for Windows 365](set-up-omnissa-horizon.md).
