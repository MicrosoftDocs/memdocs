---
title: What's new in Autopilot
description: News and resources about the latest updates and past versions of Windows Autopilot.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: jubaptis
ms.date: 08/24/2023
ms.collection: 
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
---

# Windows Autopilot: What's new

## Update to BitLocker Recovery Key Process for Windows Autopilot

Microsoft Intune is changing how BitLocker resets occur for reused Windows Autopilot devices in the September (2309) service release. Previously, users could access the BitLocker recovery key via BitLocker self-service when reusing devices that have been configured through Windows Autopilot. However, after the change, users will need to contact their IT admin to request a restore or to access the BitLocker recovery key. IT admins will continue to have full access to recovery keys both before and after this change.

### User impact

This change affects new primary users of the Autopilot device who are allowed self-service recovery of BitLocker keys to that device. There's no impact if the devices' primary user doesn't change across the device restore or reset.

Self-service BitLocker access can continue to work the same if the IT admin performs either:

- A remote Autopilot Reset. For more information, see [Step by step tutorial for Windows Autopilot Reset in Intune](tutorial/reset/autopilot-reset-overview.md), [Reset devices with remote Windows Autopilot Reset](tutorial/reset/remote-autopilot-reset.md), and [Windows Autopilot Reset](windows-autopilot-reset.md).
- Remove the current primary user or reassign to the new intended primary user prior to the device being reset or reimaged. For more information, see [Change a device's primary user](/mem/intune/remote-actions/find-primary-user#change-a-devices-primary-user).

If the new primary user is unable to access BitLocker self-service after changing from a previous primary user, then the IT admin should update the primary user in the device properties. The primary user on the device will then update to the new user upon the next check-in.

### What you need to do to prepare?

To ensure a smooth transition, notify your help desk of this change. Additionally, update your documentation to one of the following options:

1. Temporarily note the BitLocker recovery key prior to a restore as documented in the [BitLocker recovery guide](/windows/security/operating-system-security/data-protection/bitlocker/bitlocker-recovery-guide-plan).
1. Contact the help desk or IT Admin to unlock BitLocker self-service access.

## Win32 app configurable installation time impacts the Enrollment Status Page

Staring in Intune 2308, Win32 apps allow you to configure an installation time on a per app basis. This time is expressed in minutes. If the app takes longer to install than the set installation time, the deployment fails the app install. To avoid Enrollment Status Page (ESP) timeout failures, any changes to timeouts that you make to your Win32 apps also needs an increase in the ESP timeout to reflect those changes.

## Autopilot profile resiliency

Downloading the Windows Autopilot policy just got more resilient! A new update is being rolled out that increases the retry attempts for the Windows Autopilot policy to be applied when a network connection might not be fully initialized. The increased retry attempts help ensure that the profile is applied before the user begins the setup experience and improves the time sync. For Windows 10, install quality update [KB5028244](https://support.microsoft.com/en-us/topic/july-25-2023-kb5028244-os-build-19045-3271-preview-8cf92c9b-3a60-4c6a-8f4c-fc41fe8f4f2c) or newer. For Windows 11, install quality update [KB5028245](https://support.microsoft.com/en-us/topic/july-25-2023-kb5028245-os-build-22000-2245-preview-bbe6f09f-6cec-4777-a548-d237f5d849d2) or newer.

## One step removal of Windows Autopilot registration

Starting in 2307, Windows Autopilot is making it easier to manage devices by adding one step removal of a device in Autopilot devices in Intune. One step removal of a device means that you can now remove the Autopilot registration of a device without needing to delete the record in Intune. If the device is still active in Intune, the deletion just removes the registration, but it continues to be managed. To use this feature in Intune:

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, select **Windows enrollment**.

1. Under **Windows Autopilot Deployment Program**, select **Devices**.

1. Select the device you wish to remove and then select **Delete** in the toolbar at the top.

## Device rename occurs during technician phase for pre-provisioning 

Starting in 2303, a new functional change forces the device rename to occur during the technician phase for pre-provisioning for Azure AD join devices. After the technician selects the provision button, we'll immediately perform the device rename and reboot the device, then transition to the device ESP. During the user flow, the device rename is then skipped keeping resources that depend on device name (such as SCEP certs) intact. To apply this change, for Windows 10, install quality update [KB5023773](https://support.microsoft.com/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23) or newer. For Windows 11, install quality update [KB5023778](https://support.microsoft.com/topic/march-28-2023-kb5023778-os-build-22621-1485-preview-d490bb51-492e-410c-871f-50ad01b0f765) or newer.

## Install required apps during pre-provisioning

A new toggle is available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during pre-provisioning (white glove) technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. To help you achieve installing as many applications as possible during pre-provisioning, we've implemented an option to attempt the installation of all the required apps assigned to a device during technician phase. If there's app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if you have blocking apps selected. For more information, see [Update to Windows Autopilot pre-provisioning process for app installs](https://techcommunity.microsoft.com/t5/intune-customer-success/update-to-windows-autopilot-pre-provisioning-process-for-app/ba-p/3752516).


## New Microsoft Store apps now supported with the Enrollment Status Page

The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status).


## Win32 App Supersedence ESP improvements

Starting in January 2023, we're currently in the process of rolling out Win32 app supersedence GA, which introduces enhancements to ESP behavior around app tracking and app processing. Specifically, admins may notice a change in app counts. For more information, see [Win32 app supersedence improvements](https://techcommunity.microsoft.com/t5/intune-customer-success/upcoming-improvements-to-win32-app-supersedence/ba-p/3713026) and [Add Win32 app supersedence](/mem/intune/apps/apps-win32-supersedence).

## Support for Temporary Access Pass

Starting with 2301 Windows Autopilot, Autopilot supports the use of [Temporary Access Pass](/azure/active-directory/authentication/howto-authentication-temporary-access-pass) for Azure AD joined user driven, pre-provisioning and self-deploying mode for shared devices. A Temporary Access Pass is a time-limited passcode that can be configured for multi or single use to allow users to onboard other authentication methods. These authentication methods include passwordless methods such as Microsoft Authenticator, FIDO2 or Windows Hello for Business.

For more information on supported scenarios, see [Temporary Access Pass](windows-autopilot-scenarios.md#temporary-access-pass).

## Autopilot automatic device diagnostics collection
<!--1895390-->

Starting with Intune 2209, Intune automatically captures diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and with Windows 11. When logs are finished processing on a failed device, they're automatically captured and uploaded to Intune. Diagnostics may include user identifiable information such as user or device name. If the logs aren't available in Intune, check if the device is powered-on and has access to the internet. Diagnostics are available for 28 days before they're removed.

For more information, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

## Updates to Autopilot device targeting infrastructure

With Intune 2208, we're updating the Autopilot infrastructure to ensure that the profiles and applications assigned are consistently ready when the devices are deployed. This change reduces the amount of data that needs to be synchronized per-Autopilot device and leverages device lifecycle change events to reduce the amount of time that it takes to recover from device resets for Azure AD and Hybrid Azure AD joined devices. No action is needed to enable this change, it's rolling out to all clients starting August 2022.

## Update Intune Connector for Active Directory for Hybrid Azure AD joined devices
<!-- 2209 -->

Starting in September 2022, the Intune Connector for Active Directory (ODJ connector) requires .NET Framework version 4.7.2 or later. If you're not already using .NET 4.7.2 or later, the Intune Connector may not work for Autopilot hybrid Azure AD deployments resulting in failures. When you install a new Intune Connector, don't use the connector installation package that was previously downloaded. Before you install a new connector, update the .NET Framework to version 4.7.2 or later. Download a new version from the **Intune Connector for Active Directory** section of the Microsoft Intune admin center. If you're not using the latest version, it may continue to work, but the auto-upgrade feature to provide updates to the Intune Connector doesn't work.

## Enroll to co-management from Windows Autopilot
<!-- 11300628 -->
With the Intune 2205 release, you can configure device enrollment in Intune to enable [co-management](/mem/configmgr/comanage/overview), which happens during the Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](/mem/intune/enrollment/windows-enrollment-status), the device waits for Configuration Manager. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

For more information, see [How to enroll to co-management with Autopilot](/mem/configmgr/comanage/autopilot-enrollment).

## Improvements to the enrollment status page
<!-- 2202 -->

With the Intune 2202 release, the [enrollment status page](enrollment-status.md) has improved functionality. The application picker for selecting blocking apps has the following improvements:

- Includes a search box for easier selection of apps.
- Fixes an issue where it couldn't differentiate between store apps in online or offline mode.
- Adds a new column for **Version** to see which version of the application is selected.

:::image type="content" source="images/app-picker.png" alt-text="The enrollment status page application picker."::: 

## One-time self-deployment and pre-provisioning
<!-- 2110 -->

We made a change to the Windows Autopilot self-deployment mode and pre-provisioning mode experience, adding in a step to delete the device record as part of the device reuse process. This change impacts all Windows Autopilot deployments where the Autopilot profile is set to self-deployment or pre-provisioning mode. This change only affects a device when it's reused or reset, and it attempts to redeploy.

For more information, see [Updates to the Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-windows-autopilot-sign-in-and-deployment/ba-p/2848452)

## Update to the Windows Autopilot sign-in experience
<!-- 2110 -->

Users must enter their credentials at initial sign-in during enrollment. We no longer allow pre-population of the Azure Active Directory (Azure AD) user principal name (UPN).

For more information, see [Updates to the Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-windows-autopilot-sign-in-and-deployment/ba-p/2848452)

## MFA changes to Windows Autopilot enrollment flow
<!-- 2109 -->

To improve the baseline security for Azure Active Directory (Azure AD), we changed Azure AD behavior for multi-factor authentication (MFA) during device registration. Previously, if a user completed MFA as part of their device registration, the MFA claim was carried over to the user state after registration was complete.

Now the MFA claim isn't preserved after registration. Users are prompted to redo MFA for any apps that require MFA by policy.

For more information, see [Windows Autopilot MFA changes to enrollment flow](https://techcommunity.microsoft.com/t5/intune-customer-success/windows-autopilot-mfa-changes-to-enrollment-flow/ba-p/2774687).

## Windows Autopilot diagnostics page

When you deploy Windows 11 with Autopilot, you can enable users to view detailed troubleshooting information about the Autopilot provisioning process. A new **Windows Autopilot diagnostics** page is available, which provides a user-friendly view to troubleshoot Windows Autopilot failures.

The following example shows details for **Deployment info**, which includes **Network Connectivity**, **Autopilot Settings**, and **Enrollment Status**. You can also **Export logs** for detailed [troubleshooting](troubleshoot-oobe.md) analysis.

:::image type="content" source="images/oobe-03.png" alt-text="Windows Autopilot diagnostics page expanded to show details.":::

To enable the diagnostics page, go to the [ESP profile](/mem/intune/enrollment/windows-enrollment-status). Make sure **Show app and profile configuration progress** is selected to **Yes**, and then select **Yes** next to **Turn on log collection and diagnostics page for end users**.

The diagnostics page is currently supported for commercial OOBE, and Autopilot user-driven mode. It's currently available on Windows 11. Windows 10 users can still collect and export diagnostic logs when this setting is enabled in Intune.

## Next steps

[What's new in Microsoft Intune](/mem/intune/fundamentals/whats-new)

[What's new in Windows client](/windows/whats-new/)


