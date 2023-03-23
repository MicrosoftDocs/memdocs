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
ms.date: 2/14/2023
ms.collection: 
  - M365-modern-desktop
ms.topic: article
---

# Windows Autopilot: What's new

## Device rename occurs during technician phase for pre-provisioning 

Starting in 2303 a new functional change forces the device rename to occur during the technician phase for pre-provisioning for AADJ devices. After the technician selects the provision button, we’ll immediately perform the device rename and reboot the device, then transition to the device ESP. During the user flow, the device rename is then skipped keeping resources that depend on device name (such as SCEP certs) intact. To apply this change, install the latest quality update of [KB5023773](https://support.microsoft.com/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23) or later.

## Install required apps during pre-provisioning

A new toggle is available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during pre-provisioning (white glove) technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. To help you achieve installing as many applications as possible during pre-provisioning, we've implemented an option to attempt the installation of all the required apps assigned to a device during technician phase. If there's app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if you have blocking apps selected. For more information, see [Update to Windows Autopilot pre-provisioning process for app installs](https://techcommunity.microsoft.com/t5/intune-customer-success/update-to-windows-autopilot-pre-provisioning-process-for-app/ba-p/3752516).


## New Microsoft Store apps now supported with the Enrollment Status Page

The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](../intune/enrollment/windows-enrollment-status.md).


## Win32 App Supersedence ESP improvements

Starting in January 2023, we're currently in the process of rolling out Win32 app supersedence GA, which introduces enhancements to ESP behavior around app tracking and app processing. Specifically, admins may notice a change in app counts. For more information, see [Win32 app supersedence improvements](https://techcommunity.microsoft.com/t5/intune-customer-success/upcoming-improvements-to-win32-app-supersedence/ba-p/3713026) and [Add Win32 app supersedence](/mem/intune/apps/apps-win32-supersedence).

## Support for Temporary Access Pass

Starting with 2301 Windows Autopilot, Autopilot supports the use of [Temporary Access Pass](/azure/active-directory/authentication/howto-authentication-temporary-access-pass) for Azure AD joined user driven, pre-provisioning and self-deploying mode for shared devices. A Temporary Access Pass is a time-limited passcode that can be configured for multi or single use to allow users to onboard other authentication methods. These authentication methods include passwordless methods such as Microsoft Authenticator, FIDO2 or Windows Hello for Business.

For more information on supported scenarios, see [Temporary Access Pass](windows-autopilot-scenarios.md#temporary-access-pass).

## Autopilot automatic device diagnostics collection
<!--1895390-->

Starting with Intune 2209, Intune automatically captures diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and with Windows 11. When logs are finished processing on a failed device, they're automatically captured and uploaded to Intune. Diagnostics may include user identifiable information such as user or device name. If the logs aren't available in Intune, check if the device is powered-on and has access to the internet. Diagnostics are available for 28 days before they're removed.

For more information, see [Collect diagnostics from a Windows device](../intune/remote-actions/collect-diagnostics.md).

## Updates to Autopilot device targeting infrastructure

With Intune 2208, we're updating the Autopilot infrastructure to ensure that the profiles and applications assigned are consistently ready when the devices are deployed. This change reduces the amount of data that needs to be synchronized per-Autopilot device and leverages device lifecycle change events to reduce the amount of time that it takes to recover from device resets for Azure AD and Hybrid Azure AD joined devices. No action is needed to enable this change, it's rolling out to all clients starting August 2022.

## Update Intune Connector for Active Directory for Hybrid Azure AD joined devices
<!-- 2209 -->

Starting in September 2022, the Intune Connector for Active Directory (ODJ connector) requires .NET Framework version 4.7.2 or later. If you're not already using .NET 4.7.2 or later, the Intune Connector may not work for Autopilot hybrid Azure AD deployments resulting in failures. When you install a new Intune Connector, don't use the connector installation package that was previously downloaded. Before you install a new connector, update the .NET Framework to version 4.7.2 or later. Download a new version from the **Intune Connector for Active Directory** section of the Microsoft Intune admin center. If you're not using the latest version, it may continue to work, but the auto-upgrade feature to provide updates to the Intune Connector doesn't work.

## Enroll to co-management from Windows Autopilot
<!-- 11300628 -->
<!-- 2205 -->

With the Intune 2205 release, you can configure device enrollment in Intune to enable [co-management](../configmgr/comanage/overview.md), which happens during the Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](../intune/enrollment/windows-enrollment-status.md), the device waits for Configuration Manager. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

For more information, see [How to enroll to co-management with Autopilot](../configmgr/comanage/autopilot-enrollment.md).

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

To enable the diagnostics page, go to the [ESP profile](../intune/enrollment/windows-enrollment-status.md). Make sure **Show app and profile configuration progress** is selected to **Yes**, and then select **Yes** next to **Turn on log collection and diagnostics page for end users**.

The diagnostics page is currently supported for commercial OOBE, and Autopilot user-driven mode. It's currently available on Windows 11. Windows 10 users can still collect and export diagnostic logs when this setting is enabled in Intune.

## Next steps

[What's new in Microsoft Intune](../intune/fundamentals/whats-new.md)

[What's new in Windows client](/windows/whats-new/)
