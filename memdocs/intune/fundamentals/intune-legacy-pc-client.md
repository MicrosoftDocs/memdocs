---
# required metadata

title: Legacy Intune PC software client
description: Learn about the deprecation for the Intune PC software client.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 10/15/2020
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 1f104923-12df-453c-9c20-942ef65a0945
ROBOTS: NOINDEX,NOFOLLOW

# optional metadata

#audience:

ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---

# What happened to the Intune PC software client?

> [!warning]
> Legacy PC management is no longer supported as of October 16, 2020. Upgrade devices to Windows 10 and reenroll them in Intune MDM to keep them managed by Intune. Devices managed with the PC software client will stop receiving security updates and apps, and you will no longer be able to configure them.

## Deprecation announcement

The following is information from the [original deprecation announcement](https://aka.ms/Intune_Silverlight_console) posted to the Intune Support Team blog:

> [!important]
> Microsoft Intune will retire support for the Silverlight-based Intune console on October 15, 2020. This retirement includes ending support for the Silverlight console configured PC software client (also known as the PC agent) used for Windows PC management. In addition, Intune will end the Intune Storage Add-On licensing offer which was only used for app storage in Silverlight. Move your day-to-day Intune administration from Silverlight to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
>
>**How does this affect me?**
>
>Our telemetry indicates you have PC software client managed Windows devices that will need to be MDM enrolled in order to stay managed by Intune past the above-reference date.
>
>**What do I need to do?**
>
> 1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
> 2. Recreate your existing Windows 10 policies as MDM policies. Note that many device management policies were migrated several years ago as part of the admin console migration. Check device management in Azure before you create new policies.
> 3. Review reporting in the Microsoft Intune administration console to find the devices that are managed by the Intune PC software client.
> 4. Determine the right modern enrollment method that's right for your organization. For details, see [Intune enrollment methods for Windows devices](../enrollment/windows-enrollment-methods.md).
> 5. Unenroll devices with the Intune PC software client and re-enroll the devices using Intune MDM. We strongly recommend you update to the latest version of Windows 10. As of January 14, 2020, Intune no longer supports Windows 7.
> 6. Add apps to Intune MDM. For details, see [Add apps to Microsoft Intune](../apps/apps-add.md).
>
> **Please note**: If you currently have Intune storage add-on licensing, it is not required with Intune MDM to manage your Windows 10 PC's.
>
>This change will allow you to take advantage of the enhanced capabilities available through the MDM channel for Windows management. We encourage you to migrate as soon as possible, and no later than October 15, 2020. After that date, the Silverlight-based Intune console will no longer be accessible. PCs managed with the PC software client will stop receiving security updates and apps, and will no longer be able to be configured.
>
> Contact your partner of record or [support](../../get-support.md) if you need assistance.

## Uninstall the Intune PC software client software

Using an elevated command prompt on the device to unenroll, run one of the following commands.

### Method 1

```cmd
"C:\Program Files\Microsoft\OnlineManagement\Common\ProvisioningUtil.exe" /UninstallAgents /MicrosoftIntune
```

### Method 2
The following agents are installed on every SKU of Windows:

```cmd
wmic product where name="Microsoft Endpoint Protection Management Components" call uninstall
wmic product where name="Microsoft Intune Notification Service" call uninstall
wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
wmic product where name="Microsoft Online Management Policy Agent" call uninstall
wmic product where name="Microsoft Policy Platform" call uninstall
wmic product where name="Microsoft Security Client" call uninstall
wmic product where name="Microsoft Online Management Client" call uninstall
wmic product where name="Microsoft Online Management Client Service" call uninstall
wmic product where name="Microsoft Easy Assist v2" call uninstall
wmic product where name="Microsoft Intune Monitoring Agent" call uninstall
wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
wmic product where name="Windows Firewall Configuration Provider" call uninstall
wmic product where name="Microsoft Intune Center" call uninstall
wmic product where name="Microsoft Online Management Update Manager" call uninstall
wmic product where name="Microsoft Online Management Agent Installer" call uninstall
wmic product where name="Microsoft Intune" call uninstall
wmic product where name="Windows Endpoint Protection Management Components" call uninstall
wmic product where name="Windows Intune Notification Service" call uninstall
wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
wmic product where name="Windows Online Management Policy Agent" call uninstall
wmic product where name="Windows Policy Platform" call uninstall
wmic product where name="Windows Security Client" call uninstall
wmic product where name="Windows Online Management Client" call uninstall
wmic product where name="Windows Online Management Client Service" call uninstall
wmic product where name="Windows Easy Assist v2" call uninstall
wmic product where name="Windows Intune Monitoring Agent" call uninstall
wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
wmic product where name="Windows Firewall Configuration Provider" call uninstall
wmic product where name="Windows Intune Center" call uninstall
wmic product where name="Windows Online Management Update Manager" call uninstall
wmic product where name="Windows Online Management Agent Installer" call uninstall
wmic product where name="Windows Intune" call uninstall
```

> [!TIP]
> When you unenroll the Intune PC software client, a stale server-side record for the device remains. The unenrollment process is asynchronous, and there are nine agents to uninstall, so it may take up to 30 mins to complete.

### Check the unenrollment status

Check "%ProgramFiles%\Microsoft\OnlineManagement" and ensure that only the following directories are shown on the left:

- AgentInstaller
- Logs
- Updates
- Common

### Remove the OnlineManagement folder

The unenrollment process does not remove the OnlineManagement folder. Wait 30 minutes after the uninstall, and then run this command. If you run it too soon, the uninstall could be left in an unknown state. To remove the folder, start an elevated prompt and run:

```cmd
rd /s /q %ProgramFiles%\Microsoft\OnlineManagement
```

## Resources

[Deprecation announcement on the Intune Support Blog](https://techcommunity.microsoft.com/t5/intune-customer-success/take-action-microsoft-intune-ending-support-for-the-silverlight/ba-p/916249).

## Next steps
[Intune enrollment methods for Windows devices](../enrollment/windows-enrollment-methods.md)