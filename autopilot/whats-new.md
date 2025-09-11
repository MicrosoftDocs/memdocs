---
title: What's new in Windows Autopilot
description: News and resources about the latest updates and past versions of Windows Autopilot. # RSS subscription is based on this description so don't change. If the description needs to change, update RSS URL in the Tip in the article.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
manager: bpardi
ms.reviewer: madakeva
ms.date: 09/09/2025
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: whats-new
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot: What's new

> [!TIP]
>
> RSS can be used to notify when new features for Windows Autopilot are added to this page. For example, the following RSS link includes this article:
>
> ``` url
> https://learn.microsoft.com/api/search/rss?search=%22News+and+resources+about+the+latest+updates+and+past+versions+of+Windows+Autopilot.%22&locale=en-us&%24filter=
> ```
>
> This example includes the `&locale=en-us` variable. The `locale` variable is required, but it can be changed to another supported locale. For example, `&locale=es-es`.
>
> For more information on using RSS for notifications, see [How to use the docs](/mem/use-docs#notifications) in the Intune documentation.

## Enrollment Status Page support for installing Windows security updates during Windows OOBE

Date added: *September 3, 2025*<br>
Date updated: *September 9, 2025*

> [!IMPORTANT]
>
> As of September 9, 2025, this capability is delayed to help ensure delivery of the best possible experience. The new setting on the Enrollment Status Page (ESP) can be configured on both new and existing ESP profiles, but the automatic installation of monthly security update releases and the new user interface isn't available yet. This post will be updated with a revised timeline as soon as it's available.

The Windows out-of-box experience (OOBE) by default installs the latest available monthly security update releases to help ensure devices are secure and up to date from day one. Windows OOBE is used by Intune and by Windows Autopilot scenarios through the Intune enrollment status page (ESP) configurations. Intune refers to these monthly security update releases as quality updates.

To help manage this behavior, the Intune enrollment status page (ESP) is updated with a new setting that can be used to allow or block the automatic installation of monthly security update releases. The new setting is **Install Windows quality updates (might restart the device)**. Monthly security update releases are installed by default during the Windows out-of-box experience OOBE that's used by Intune and by Windows Autopilot

By default, this setting is set to **Yes** in all new ESP profiles that are created. Configuring this setting to **Yes** results in the most recent monthly security update releases to be installed. In all previously created ESP profiles, this setting is set to **No** until those profiles are edited and changed. When set to **No**, OOBE doesn't install the monthly security update releases. Delaying the install of monthly security update releases can give internal teams time to test the monthly security update releases before allowing them to install on new devices during provisioning.

- For more information, see [Get ready for Windows quality updates out of the box](https://techcommunity.microsoft.com/blog/windows-itpro-blog/get-ready-for-windows-quality-updates-out-of-the-box/4434498).
- For more information about configuring the setting in the Intune enrollment status page (ESP), see [Set up Enrollment Status Page](/intune/intune-service/enrollment/windows-enrollment-status).
- For information about Windows quality updates, see [Windows quality update policy](/windows/deployment/update/release-cycle#monthly-security-update-release).

## Deliver Enterprise App Catalog (EAM) apps during the Enrollment status page

Date added: *June 26, 2025*

Windows Autopilot now supports Enterprise App Catalog apps. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. With Intune's 2506 release, you can now select apps from the Enterprise App Catalog as blocking apps in the Enrollment status page (ESP) profile. This allows you to ensure those apps are delivered before the user can access the desktop.

For related information, see [Add an Enterprise App Catalog app to Microsoft Intune](/intune/intune-service/apps/apps-add-enterprise-app).

## Updated build for the low privileged account for Intune Connector for Active Directory

Date added: *April 18, 2025*

We've updated the low-privileged Intune Connector for Active Directory build. New in build **6.2504.2001.8**:

- Updated the sign in page to use WebView2, built on Microsoft Edge, instead of WebBrowser.
- **Error `MSA account <accountName> is not valid`** when signing in has been fixed.
- **Error `Cannot start service ODJConnectorSvc on computer '.'`** can now be mitigated. For more information, see [Troubleshooting FAQ](/autopilot/troubleshooting-faq#why-is-the-error--cannot-start-service-odjconnectorsvc-on-computer------occurring-when-setting-up-the-intune-connector-for-active-directory-).
- **Error `System.DirectoryServices.DirectoryServicesCOMException (0x8007202F): A constraint violation occurred.`** can now be mitigated. For more information, see [Troubleshooting FAQ](/autopilot/troubleshooting-faq#why-is-the-error--the-msa-account-couldn-t-be-granted-permission-to-create-computer-objects-in-the-following-ous--occurring-when-installing-the-intune-connector-for-active-directory-).

Download and install the latest version to get these changes.

## Low privileged account for Intune Connector for Active Directory for Hybrid join Windows Autopilot flows
<!--9544276-->
Date added: *February 27, 2025*

We've updated the Intune Connector for Active Directory to use a low privileged account to increase the security of your environment. The old connector will continue to work until deprecation in late June 2025.

For more information, see [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](windows-autopilot-hybrid.md).

## Update to enrollmentProfileName property for devices deployed via Windows Autopilot for existing devices
<!--9105086-->
Date added: *June 24, 2024*

Devices deployed via Windows Autopilot for existing devices which are also registered for Windows Autopilot would previously have an **enrollmentProfileName** property incorrectly set as **OfflineAutoPilotProfile-\<ZtdCorrelationId\>**. With a recent change, **enrollmentProfileName** has been updated to correctly display the assigned Windows Autopilot profile. This may impact customers who are using **enrollmentProfileName** for Microsoft Entra dynamic groups or Microsoft Intune assignment filters to distinguish devices deployed via Windows Autopilot for existing devices. For more information, see [Register the device for Windows Autopilot](existing-devices.md#register-the-device-for-windows-autopilot).

## Windows Autopilot support for Microsoft Teams Rooms

Date added: *June 4, 2024*

Windows Autopilot streamlines provisioning for laptops. Now Windows Autopilot adds the same support for **Microsoft Teams Rooms**! With this combination, Teams Rooms devices can now be deployed and provisioned without needing physical access to the device. Policies and apps are configured and the Teams Rooms console automatically signed in without needing to enter credentials.

For more information on supported scenarios and setup, see [Windows Autopilot and Autologin for Teams Rooms on Windows](/microsoftteams/rooms/autopilot-autologin).

## Devices are no longer re-enrolled after a motherboard change

Date added: *June 4, 2024*

When a device previously changed its motherboard and the OS remained intact, Windows Autopilot attempted to re-enroll the device to Intune. This re-enrollment no longer occurs if a motherboard swap occurs on a device due to a change in Windows Autopilot. If a motherboard is changed on a device, the new motherboard needs to be re-registered so that Windows Autopilot continues to work upon a reset.

## Windows Autopilot self-deploying mode is now generally available <!-- INADO-26780755  -->

Date added: *February 23, 2024*

Windows Autopilot self-deploying mode is now generally available and out of preview. Windows Autopilot self-deploying mode enables deployment of Windows devices with little to no user interaction. Once the device connects to network, the device provisioning process starts automatically: the device joins Microsoft Entra ID, enrolls in Intune, and syncs all device-based configurations targeted to the device. Self-deploying mode ensures that the user can't access desktop until all device-based configuration is applied. The Enrollment Status Page (ESP) is displayed during OOBE so users can track the status of the deployment. For more information, see:

- [Windows Autopilot self-deploying mode](self-deploying.md).
- [Step by step tutorial for Windows Autopilot self-deploying mode in Intune](tutorial/self-deploying/self-deploying-workflow.md).

## Windows Autopilot for pre-provisioned deployment is now generally available <!-- INADO-26780755  -->

Date added: *February 23, 2024*

Windows Autopilot for pre-provisioned deployment is now generally available and out of preview. Windows Autopilot for pre-provisioned deployment is used by organizations that want to ensure devices are business-ready before the user accesses them. With pre-provisioning, admins, partners, or OEMs can access a technician flow from the Out-of-box experience (OOBE) and kick off device setup. Next, the device is sent to the user who completes provisioning in the user phase. Pre-provisioning delivers most the configuration in advance so the end user can get to the desktop faster. For more information, see:

- [Windows Autopilot for pre-provisioned deployment](pre-provision.md).
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](tutorial/pre-provisioning/azure-ad-join-workflow.md).
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join in Intune](tutorial/pre-provisioning/hybrid-azure-ad-join-workflow.md).

## Updates to error message for manual device uploads

Date added: *October 31, 2023*

The 2310 release of Intune adds more clarity to the manual hardware hash upload in the console. If a device couldn't be imported, a notification shows the import error along with the specific lines of the CSV file that received the error. The error codes also include more details on why the device failed to upload, whether the device is assigned to another tenant, or the device already registered to the tenant.

:::image type="content" alt-text="Import Error Screenshot." source="media/windows-autopilot-whats-new/importerror1.png":::

:::image type="content" alt-text="Import error details." source="media/windows-autopilot-whats-new/importerror2.png":::

## Unblock fix pending state for self-deploying and pre-provisioning mode for disabled OEMs

Date added: *October 10, 2023*

Starting in 2310, we're making an update to the self-deployment and pre-provisioning modes for manufacturers that have not opted-in to attesting to removal of Windows Autopilot refurbished devices. Customers using these manufacturers were still subjected to the one-time device-based enrollment block in the self-deployment and pre-provisioning modes. This block means that the device could go through self-deployment or pre-provisioning mode once and then get blocked from doing it again. This behavior could cause problems if the device needed to be reset or redeployed. This change in 2310 enables a button in the Windows Autopilot devices section in Intune to manually unblock those devices. This update only works for certain OEMs and doesn't work on the **Fix pending** status. Reach out to your respective OEM to confirm whether this functionality is enabled for your device.

### How to unblock devices

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. Select the device to unblock and the select the **Unblock device** option in the toolbar at the top of the page.

## Update to BitLocker Recovery Key Process for Windows Autopilot

Date added: *August 23, 2023*

Microsoft Intune is changing how BitLocker resets occur for reused Windows Autopilot devices in the September (2309) service release. Previously, users could access the BitLocker recovery key via BitLocker self-service when reusing devices that were configured through Windows Autopilot. However, after the change, users will need to contact their IT admin to request a restore or to access the BitLocker recovery key. IT admins will continue to have full access to recovery keys both before and after this change.

### User impact

This change affects new primary users of the Windows Autopilot device who are allowed self-service recovery of BitLocker keys to that device. There's no impact if the devices' primary user doesn't change across the device restore or reset.

Self-service BitLocker access can continue to work the same if the IT admin performs either:

- A remote Windows Autopilot Reset. For more information, see [Step by step tutorial for Windows Autopilot Reset in Intune](tutorial/reset/autopilot-reset-overview.md), [Reset devices with remote Windows Autopilot Reset](tutorial/reset/remote-autopilot-reset.md), and [Windows Autopilot Reset](windows-autopilot-reset.md).
- Remove the current primary user or reassign to the new intended primary user before the device is reset or reimaged. For more information, see [Change a device's primary user](/mem/intune-service/remote-actions/find-primary-user#change-a-devices-primary-user).

If the new primary user is unable to access BitLocker self-service after changing from a previous primary user, then the IT admin should update the primary user in the device properties. The primary user on the device then updates to the new user upon the next check-in.

### What needs to be done to prepare?

To ensure a smooth transition, notify the organization's help desk of this change. Additionally, update documentation to one of the following options:

1. Temporarily note the BitLocker recovery key before restoring as documented in the [BitLocker recovery guide](/windows/security/operating-system-security/data-protection/bitlocker/bitlocker-recovery-guide-plan).

1. To unlock BitLocker self-service access, contact the help desk or IT Admin.

### Update: Temporary change

Date added: *August 23, 2023*

When devices that utilize Windows Autopilot are reused, and there's a new device owner, that new device owner must contact an administrator to acquire the BitLocker recovery key for that device. Administrative unit scoped administrators will lose access to BitLocker recovery keys after device ownership changes. These scoped administrators need to contact a non-scoped administrator for the recovery keys. This change is a temporary change for scoped administrators and will be updated once a solution is in place.

## Win32 app configurable installation time impacts the Enrollment Status Page

Starting in Intune 2308, Win32 apps allow configuration of an installation time on a per app basis. This time is expressed in minutes. If the app takes longer to install than the set installation time, the deployment fails the app install. To avoid Enrollment Status Page (ESP) timeout failures, any changes made to timeouts for Win32 apps also needs an increase in the ESP timeout to reflect those changes.

## Windows Autopilot profile resiliency

Date added: *July 26, 2023*

Downloading the Windows Autopilot policy just got more resilient! A new update is being rolled out that increases the retry attempts for applying the Windows Autopilot policy when a network connection might not be fully initialized. The increased retry attempts help ensure that the profile is applied before the user begins the setup experience and improves the time sync. Install the following quality updates for this feature:

- Windows 10: [KB5028244](https://support.microsoft.com/topic/july-25-2023-kb5028244-os-build-19045-3271-preview-8cf92c9b-3a60-4c6a-8f4c-fc41fe8f4f2c) or later.
- Windows 11: [KB5028245](https://support.microsoft.com/topic/july-25-2023-kb5028245-os-build-22000-2245-preview-bbe6f09f-6cec-4777-a548-d237f5d849d2) or later.

## One step removal of Windows Autopilot registration

Date added: *July 3, 2023*

Starting in 2307, Windows Autopilot is making it easier to manage devices by adding one step removal of a device in Windows Autopilot devices in Intune. One step removal of a device means that the Windows Autopilot registration of a device can now be removed without needing to delete the record in Intune. If the device is still active in Intune, the deletion just removes the registration, but it continues to be managed. To use this feature in Intune:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. Select the device that needs deletion and then select **Delete** in the toolbar at the top.

## Device rename occurs during technician phase for pre-provisioning

Date added: *March 28, 2023*
Date updated: *April 17, 2023*

Starting in 2303, a new functional change forces the device rename to occur during the technician phase for pre-provisioning for Microsoft Entra join devices. After the technician selects the provision button, we'll immediately perform the device rename and reboot the device, then transition to the device ESP. During the user flow, the device rename is then skipped keeping resources that depend on device name (such as System Center Endpoint Protection (SCEP) certs) intact. To apply this change, for Windows 10, install quality update [KB5023773](https://support.microsoft.com/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23) or later. For Windows 11, install quality update [KB5023778](https://support.microsoft.com/topic/march-28-2023-kb5023778-os-build-22621-1485-preview-d490bb51-492e-410c-871f-50ad01b0f765) or later.

## Install required apps during pre-provisioning

Date added: March 17, 2023*

A new toggle is available in the Enrollment Status Page (ESP) profile that allows selection to attempt to install required applications during pre-provisioning technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. To help achieve installing as many applications as possible during pre-provisioning, an option has been implemented to attempt the installation of all the required apps assigned to a device during technician phase. If there's app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, edit the Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if blocking apps are selected. For more information, see [Update to Windows Autopilot pre-provisioning process for app installs](https://techcommunity.microsoft.com/t5/intune-customer-success/update-to-windows-autopilot-pre-provisioning-process-for-app/ba-p/3752516).

## New Microsoft Store apps now supported with the Enrollment Status Page

Date added: *March 17, 2023*

The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](/mem/intune-service/enrollment/windows-enrollment-status).

## Win32 App Supersedence ESP improvements

Date added: *February 10, 2023*

Starting in January 2023, we're currently in the process of rolling out Win32 app supersedence GA, which introduces enhancements to ESP behavior around app tracking and app processing. Specifically, admins might notice a change in app counts. For more information, see [Win32 app supersedence improvements](https://techcommunity.microsoft.com/t5/intune-customer-success/upcoming-improvements-to-win32-app-supersedence/ba-p/3713026) and [Add Win32 app supersedence](/mem/intune-service/apps/apps-win32-supersedence).

## Support for Temporary Access Pass

Date added: *January 3, 2023*
Date updated: *February 15, 2023*

Starting with 2301 Windows Autopilot, Windows Autopilot supports the use of [Temporary Access Pass](/azure/active-directory/authentication/howto-authentication-temporary-access-pass) for Microsoft Entra joined user driven, pre-provisioning and self-deploying mode for shared devices. A Temporary Access Pass is a time-limited passcode that can be configured for multi or single use to allow users to onboard other authentication methods. These authentication methods include passwordless methods such as Microsoft Authenticator, FIDO2, or Windows Hello for Business.

For more information on supported scenarios, see [Temporary Access Pass](windows-autopilot-scenarios.md#temporary-access-pass).

## Windows Autopilot automatic device diagnostics collection <!--1895390-->

Date added: *September 23, 2022*

Starting with Intune 2209, Intune automatically captures diagnostics when devices experience a failure during the Windows Autopilot process on currently supported versions of Windows. When logs are finished processing on a failed device, they're automatically captured and uploaded to Intune. Diagnostics might include user identifiable information such as user or device name. If the logs aren't available in Intune, check if the device is powered-on and has access to the internet. Diagnostics are available for 28 days before they're removed.

For more information, see [Collect diagnostics from a Windows device](/mem/intune-service/remote-actions/collect-diagnostics).

## Updates to Windows Autopilot device targeting infrastructure

Date added: *August 16, 2022*

With Intune 2208, we're updating the Windows Autopilot infrastructure to ensure that the profiles and applications assigned are consistently ready when the devices are deployed. This change reduces the amount of data that needs to be synchronized per-Windows Autopilot device. Additionally, it uses device lifecycle change events to reduce the amount of time that it takes to recover from device resets for Microsoft Entra joined and Microsoft Entra hybrid joined devices. No action is needed to enable this change. It's rolling out to all clients starting August 2022.

## Update Intune Connector for Active Directory for Microsoft Entra hybrid joined devices <!-- 2209 -->

Date added: *August 3, 2022*

Starting in September 2022, the Intune Connector for Active Directory (ODJ connector) requires .NET Framework version 4.7.2 or later. If .NET 4.7.2 or later isn't used, the Intune Connector for Active Directory might not work for Windows Autopilot hybrid Microsoft Entra deployments resulting in failures. When a new Intune Connector for Active Directory is installed, don't use the connector installation package that was previously downloaded. Before installing a new connector, update the .NET Framework to version 4.7.2 or later. Download a new version from the **Intune Connector for Active Directory** section of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). If the latest version isn't used, it might continue to work, but the auto-upgrade feature to provide updates to the Intune Connector for Active Directory doesn't work.

## Enroll to co-management from Windows Autopilot <!-- 11300628 -->

Date added: *May 20, 2022*

With the Intune 2205 release, device enrollment in Intune can be configured to enable [co-management](/mem/configmgr/comanage/overview), which happens during the Windows Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

If the device is targeted with an [Windows Autopilot enrollment status page (ESP) policy](/mem/intune-service/enrollment/windows-enrollment-status), the device waits for Configuration Manager. The Configuration Manager client is installed, registers with the site, and then applies the production co-management policy. The Windows Autopilot ESP then continues.

For more information, see [How to enroll to co-management with Windows Autopilot](/mem/configmgr/comanage/autopilot-enrollment).

## Improvements to the enrollment status page <!-- 2202 -->

Date added: *May 20, 2022*

With the Intune 2202 release, the functionality of the [enrollment status page](enrollment-status.md) is improved. The application picker for selecting blocking apps has the following improvements:

- Includes a search box for easier selection of apps.
- Fixes an issue where it couldn't differentiate between store apps in online or offline mode.
- Adds a new column for **Version** to see which version of the application is selected.

:::image type="content" source="images/app-picker.png" alt-text="The enrollment status page application picker.":::

## One-time self-deployment and pre-provisioning <!-- 2110 -->

Date added: *May 20, 2022*

We made a change to the Windows Autopilot self-deployment mode and pre-provisioning mode experience, adding in a step to delete the device record as part of the device reuse process. This change impacts all Windows Autopilot deployments where the Windows Autopilot profile is set to self-deployment or pre-provisioning mode. This change only affects a device when reused or reset, and it attempts to redeploy.

For more information, see [Updates to the Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-windows-autopilot-sign-in-and-deployment/ba-p/2848452).

## Update to the Windows Autopilot sign-in experience <!-- 2110 -->

Date added: *May 20, 2022*

Users must enter their credentials at initial sign-in during enrollment. We no longer allow pre-population of the Microsoft Entra user principal name (UPN).

For more information, see [Updates to the Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-windows-autopilot-sign-in-and-deployment/ba-p/2848452).

## MFA changes to Windows Autopilot enrollment flow <!-- 2109 -->

Date added: *May 20, 2022*

To improve the baseline security for Microsoft Entra ID, we changed Microsoft Entra behavior for multifactor authentication (MFA) during device registration. Previously, if a user completed MFA as part of their device registration, the MFA claim was carried over to the user state after registration was complete.

Now the MFA claim isn't preserved after registration. Users are prompted to redo MFA for any apps that require MFA by policy.

For more information, see [Windows Autopilot MFA changes to enrollment flow](https://techcommunity.microsoft.com/t5/intune-customer-success/windows-autopilot-mfa-changes-to-enrollment-flow/ba-p/2774687).

## Windows Autopilot diagnostics page

Date added: *May 20, 2022*

When Windows 11 is deployed with Windows Autopilot, users can be enabled to view detailed troubleshooting information about the Windows Autopilot provisioning process. A new **Windows Autopilot diagnostics** page is available, which provides a user-friendly view to troubleshoot Windows Autopilot failures.

The following example shows details for **Deployment info**, which includes **Network Connectivity**, **Autopilot Settings**, and **Enrollment Status**. The **Export logs** button can also be used for detailed [troubleshooting](troubleshooting-faq.yml#troubleshooting-windows-oobe-issues-during-windows-autopilot) analysis.

:::image type="content" source="images/oobe-03.png" alt-text="Windows Autopilot diagnostics page expanded to show details.":::

To enable the diagnostics page, go to the [ESP profile](/mem/intune-service/enrollment/windows-enrollment-status). Make sure **Show app and profile configuration progress** is selected to **Yes**, and then select **Yes** next to **Turn on log collection and diagnostics page for end users**.

The diagnostics page is currently supported when signing in with a Work or School account during a Windows Autopilot user-driven deployment. It's currently available on Windows 11. Windows 10 users can still collect and export diagnostic logs when this setting is enabled in Intune.

## Related content

- [What's new in Windows Autopilot device preparation](device-preparation/whats-new.md).
- [What's new in Microsoft Intune](/mem/intune-service/fundamentals/whats-new).
- [What's new in Windows client](/windows/whats-new/).
