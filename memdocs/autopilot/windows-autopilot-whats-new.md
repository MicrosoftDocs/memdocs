---
title: What's new in Autopilot
description: News and resources about the latest updates and past versions of Windows Autopilot.
ms.prod: w10
ms.technology: windows
ms.localizationpriority: medium
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: jubaptis
ms.date: 08/02/2022
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: article
---

# Windows Autopilot: What's new

## Update Intune Connector for Active Directory for Hybrid Azure AD joined devices
<!-- 2209 -->

Starting in September 2022, the Intune Connector for Active Directory (ODJ connector) will require .NET Framework version 4.7.2 or later. If you're not already using .NET 4.7.2 or later, the Intune Connector may not work for Autopilot hybrid Azure AD deployments and will result in failures. When you install a new Intune Connector, don't use the connector installation package that was previously downloaded. You shoud update the .NET framework to version 4.7.2 or later before installing a new connector. Download a new version from the **Intune Connector for Active Directory** section of the Microsoft Endpoint Manager admin center. If you're not using the latest version, it may continue to work, but the auto-upgrade feature to provide updates to the Intune Connector won't work.

## Enroll to co-management from Windows Autopilot
<!-- 11300628 -->
<!-- 2205 -->

With the Intune 2205 release, you can configure device enrollment in Intune to enable [co-management](../configmgr/comanage/overview.md), which happens during the Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](../intune/enrollment/windows-enrollment-status.md), the device will wait for Configuration Manager. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

For more information, see [How to enroll to co-management with Autopilot](../configmgr/comanage/autopilot-enrollment.md).

## Improvements to the enrollment status page
<!-- 2202 -->

With the Intune 2202 release, the [enrollment status page](enrollment-status.md) has improved functionality. The application picker for selecting blocking apps has the following improvements:

- Includes a search box for easier selection of apps.
- Fixes an issue where it couldn't differentiate between store apps in online or offline mode.
- Adds a new column for **Version** to see which version of the application is selected.

:::image type="content" source="images/app-picker.png" alt-text="The enrollment status page application picker.":::

## Autopilot agility rolling out

Autopilot agility is a new feature that allows updates and bug fixes to the OOBE experience. These updates occur before device enrollment, and after the Azure Active Directory (Azure AD) sign in page. It may result in another reboot and authentication prompt to the user. This feature is rolling out to Windows 10 1909 and 2004/20H2 with August cumulative update and isn't yet available for Windows 11.

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

To enable the diagnostics page, go to the [ESP profile](../intune/enrollment/windows-enrollment-status.md). Select **Yes** to **Turn on log collection and diagnostics page for end users**.

The diagnostics page is currently supported for commercial OOBE, and Autopilot user-driven mode. It's currently available on Windows 11. Windows 10 users can still collect and export diagnostic logs when this setting is enabled in Intune.

## Next steps

[What's new in Microsoft Intune](../intune/fundamentals/whats-new.md)

[What's new in Windows client](/windows/whats-new/)
