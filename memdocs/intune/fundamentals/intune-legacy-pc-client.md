---
# required metadata

title: Legacy Intune PC client
description: Considerations when using Intune on Azure to manage your organization's Windows devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/16/2020
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 1f104923-12df-453c-9c20-942ef65a0945

# optional metadata

#audience:

ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# What happened to the Intune PC client?

> [!warning]
> Legacy PC management is no longer supported as of October 16, 2020. Upgrade devices to Windows 10 and reenroll them in Intune MDM to keep them managed by Intune. Devices managed with the PC software client will stop receiving security updates and apps, and you will no longer be able to configure them.

## Use Intune MDM for all Windows 10 devices

You must enroll new Windows 10 devices in Intune MDM instead of using the PC software client. For existing PC software client devices, you’ll want to remove the PC software client and enroll the device in Intune MDM instead.

### General steps to use Intune MDM instead of the Intune PC client

1. Open the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com).
2. Recreate your existing Windows 10 policies as MDM policies. Note that many device management policies were migrated several years ago as part of the admin console migration. Check device management in Azure before you create new policies.
3. Review reporting in the Microsoft Intune administration console to find the devices that are managed by the PC software client.
4. Determine the right modern enrollment method that's right for your organization. For details, see [Intune enrollment methods for Windows devices](../enrollment/windows-enrollment-methods.md).
5. Unenroll devices with the Intune PC client and re-enroll the devices using Intune MDM. We strongly recommend you update to the latest version of Windows 10. As of January 14, 2020, Intune no longer supports Windows 7.
6. Add apps to Intune MDM. For details, see [Add apps to Microsoft Intune](../apps/apps-add.md).

   > [!note] If you currently have Intune storage add-on licensing, it is not required with Intune MDM to manage your Windows 10 PC's.

## Uninstall the Intune PC client software

There are two ways to unenroll the legacy Intune PC client software:

- From the Microsoft Intune administration console (recommended method)
- From a command prompt on the device

### Unenroll by using the Microsoft Intune administration console

To unenroll the software client by using the [Microsoft Intune administration console](https://admin.manage.microsoft.com/), go to **Groups** > **All Computers** > **Devices**. Right-click the device, and select **Retire/Wipe**.

### Unenroll by using a command prompt on the device

Using an elevated command prompt, run one of the following commands.

**Method 1**:

```cmd
"C:\Program Files\Microsoft\OnlineManagement\Common\ProvisioningUtil.exe" /UninstallAgents /MicrosoftIntune
```

**Method 2** 
> [!note] All of the following agents are installed on every SKU of Windows

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
> Client unenrollment leaves a stale server-side record for the affected client. The unenrollment process is asynchronous, and there are nine agents to uninstall, so it may take up to 30 mins to complete.

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

## Next steps
[Intune enrollment methods for Windows devices](../enrollment/windows-enrollment-methods.md)
