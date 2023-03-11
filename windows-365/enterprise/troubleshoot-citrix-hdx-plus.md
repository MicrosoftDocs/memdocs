---
# required metadata
title: Troubleshoot Citrix HDX Plus for Windows 365
titleSuffix:
description: Troubleshoot Citrix HDX Plus for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/12/2022
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
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

# Troubleshoot Citrix HDX Plus for Windows 365

When you turn on Citrix HDX Plus for a user, the Citrix Virtual Delivery Agent is automatically installed on that user's Cloud PCs. The agent enables the HDX protocol. If this installation runs into a problem, you'll receive an error message in the All Cloud PC list. The description of the error includes advice on how to troubleshoot the error.

If the Citrix HDX Plus agent installation fails, the user can still connect to their Cloud PC by using Remote Desktop.

While troubleshooting errors, make sure that the following steps have all been successful:

- The users license state is synchronized from Citrix to Microsoft Endpoint Manager, including the users Azure Active Directory (Azure AD) user ID.
  - The prerequisites have been met.
  - The Citrix connector is enabled and healthy in Microsoft Endpoint Manager.
  - The correct permissions have been set for the Citrix third-party apps in Azure AD. For more information on required permissions, see [Requirements for using Citrix HDX Plus for Windows 365 Enterprise](requirements-citrix.md).
  - The Azure AD user is added and discoverable  in the Citrix console.
- The Citrix agent is downloaded on the Cloud PC.
  - The Cloud PC can access Citrix download URL.
  - No security policy is blocking PowerShell or any app/agent installation as System.
- The Citrix Virtual Delivery Agent is installed.
  - Check **Apps & Features** to see if the Citrix Virtual Apps and Desktops Virtual Delivery Agent is installed on the Cloud PC.
  - Check Windows event viewer (eventvwr.msc) logs to make sure that the agent installation is executed.
  - Check Citrix installation logs for any failures:  %TEMPsystemdrive%\Windows\Temp\Citrix\XenDesktop Installer.
- The Cloud PC is registered into the Citrix cloud tenant.
  - Check the Cloud PC registration status in the Citrix configuration console.
  - If the Cloud PC is unregistered, check the Application sign-in Windows event viewer (eventvwr.msc) for Citrix Desktop Service errors and warnings.

After you find the root cause, remove the assigned license from the Citrix console and re-add the license. This should trigger a reinstallation of the Citrix Virtual Delivery Agent.

If no other solution works, you can [reprovision](reprovision-cloud-pc.md) the Cloud PC to reattempt the Citrix HDX plus enablement. Reprovisioning will delete the Cloud PC and create a brand new one. All data on the original Cloud PC will be lost. Therefore, reprovisioning should be the last resort to resolve the issue.

## Troubleshoot connection issues

If you’re having connectivity issues with your Citrix HDX Plus Cloud PC, you may want to test the default RDP-based connectivity. This process is a handy troubleshooting technique to determine if the issue is with the Cloud PC or the HDX connectivity.

### Turn on the RDP protocol

When the Citrix HDX Plus protocol is turned on, the Windows 365 remoting protocol remains enabled but inactive. This inactivity means that users trying to connect with the Windows 365 supported Remote Desktop clients (including the HTML5 browser) are blocked by default. Users can only connect by using HDX. Users trying to connect with non-HDX clients will get a generic error message.

You can turn on the RDP protocol so users can sign in with RDP to test the Cloud PC connectivity. You can do either of the following to turn on the RDP protocol:

- [Make a user a local admin](assign-users-as-local-admin.md) on the Cloud PC.
- [Add the user to the Direct Access Users group on the Cloud PC](/windows/client-management/mdm/policy-csp-localusersandgroups?WT.mc_id=Portal-fx).

After taking either of these steps,  you might have to reboot the Cloud PC for the group membership updates to take effect. Afterwards, the user will be able to connect by using either RDP or Citrix HDX.

You can now test the connectivity by using RDP, and raise a support case with the relevant support team if problems persist.

<!-- ########################## -->
## Next steps

[Learn about Citrix HDX Plus for Windows 365](set-up-citrix.md).
