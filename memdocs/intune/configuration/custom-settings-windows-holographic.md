---
# required metadata

title: Custom settings - Windows Holographic for Business devices - Microsoft Intune | Microsoft Docs
description: Add or create a custom profile to use the OMA-URI settings for devices running Windows Holographic for Business in Microsoft Intune, including Microsoft HoloLens. You can set AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates, and ApplicationLaunchRestrictions policy configuration service provider (CSP) settings.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/16/2024
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
---

# Use custom settings for Windows Holographic for Business devices in Intune

Using Microsoft Intune, you can add or create custom settings for your Windows Holographic for Business devices using **custom profiles**. Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

This article applies to:

- Windows Holographic for Business
- Windows 10/11

Windows Holographic for Business custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure different features. These settings are typically used by mobile device manufacturers to control features on the device.

Windows Holographic for Business makes many configuration service providers (CSPs) settings available. For a CSP overview, go to [Introduction to configuration service providers (CSPs) for IT pros](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers). For specific CSPs supported by Windows Holographic, go to [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens).

If you're looking for a specific setting, remember that the [Windows Holographic for Business device restriction profile](device-restrictions-windows-holographic.md) includes many built-in settings. So, you might not need to enter custom values.

This article shows you how to create a custom profile for Windows Holographic for Business devices. It also includes a list of the recommended OMA-URI settings.

## Before you begin

- [Create a Windows custom profile](custom-settings-configure.md#create-the-profile).

## Custom OMA-URI Settings

**Add**: Enter the following settings:

- **Name**: Enter a unique name for the OMA-URI setting so you can identify the setting in the settings list.
- **Description**: Enter a description that gives an overview of the setting, and any other important details.
- **OMA-URI** (case sensitive): Enter the OMA-URI you want to use as a setting.
- **Data type**: Select the data type you want for this OMA-URI setting. Your options:

  - String
  - String (XML file)
  - Date and time
  - Integer
  - Floating point
  - Boolean
  - Base64 (file)

- **Value**: Enter the data value you want to associate with the OMA-URI you entered. The value depends on the data type you selected. For example, if you select **Date and time**, select the value from a date picker.

After you add and **Save** your settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (`.csv`) file.

## Recommended custom settings

The following settings are useful for devices running Windows Holographic for Business:

### [AllowFastReconnect](/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect` | Integer<br/>0 - not allowed<br/>1 - allowed (default)|

### [AllowUpdateService](/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Policy/Config/Update/AllowUpdateService` |Integer<br/>0 – Update service is not allowed <br/>1  – Update service is allowed (default).|

### [AllowVPN](/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Policy/Config/Settings/AllowVPN` |Integer<br/>0 - not allowed<br/>1 - allowed (default)|

### [RequireUpdateApproval](/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval` |This setting is available in RS5 (build 17763) and earlier. Starting with 19H1 (build 18362), use [Windows Update for Business](../protect/windows-update-for-business-configure.md).<br/><br/>Integer<br/>0 – Not configured. The device installs all applicable updates.<br/>1 – The device only installs updates that are both applicable and on the Approved Updates list. Set this policy to 1 if IT wants to control the deployment of updates on devices, like when testing is required prior to deployment.|

### [ScheduledInstallTime](/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime` |Integer 0-23, where 0=12AM and 23=11PM<br/>Default value is 3.|

### [UpdateServiceURL](/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl` |This setting is available in RS5 (build 17763) and earlier. Starting with 19H1 (build 18362), use [Windows Update for Business](../protect/windows-update-for-business-configure.md).<br/><br/>String<br/>URL - the device checks for updates from the WSUS server at the specified URL.<br/>Not configured - The device checks for updates from Microsoft Update.|

### [ApprovedUpdates](/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> | `./Vendor/MSFT/Update/ApprovedUpdates/*GUID*` <br/><br/>**Important**<br/>You must read and accept the update EULAs on behalf of your end users. If you don't read and accept the EULA, it's a breach of legal or contractual obligations.|Node for update approvals and EULA acceptance on behalf of the end user.<br/><br/>For more information, go to [Update CSP](/windows/client-management/mdm/update-csp).|

### [ApplicationLaunchRestrictions](/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> | `./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy` <br/><br/>**Important**<br/>The AppLocker CSP article uses escaped XML examples. To configure the settings with Intune custom profiles, you must use plain XML.|String<br/>For more information, go to [AppLocker CSP](/windows/client-management/mdm/applocker-csp).|

### [DeletionPolicy](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> | `./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy` |Integer<br/>0 - delete immediately when the device returns to a state with no currently active users<br/>1 - delete at storage capacity threshold (default)<br/>2 - delete at both storage capacity threshold and profile inactivity threshold|

### [EnableProfileManager](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> | `./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager` |Boolean<br/>True - enable<br/>False - disable (default)|

### [ProfileInactivityThreshold](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> | `./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold` |Integer<br/>Default value is 30.|

### [StorageCapacityStartDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> | `./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion` |Integer<br/>Default value is 25.|

### [StorageCapacityStopDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> | `./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion` |Integer<br/>Default value is 50.|

## Find the policies you can configure

There's a complete list of all configuration service providers (CSPs) that Windows Holographic supports at [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens). Not all settings are compatible with all Windows Holographic versions. The table in [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens) lists the supported versions for each CSP.

Also, Intune doesn't support all of the settings listed in [CSPs supported in Windows Holographic](/windows/client-management/mdm/configuration-service-provider-reference#hololens). To find out if Intune supports the setting you want, open the article for that setting. Each setting page shows its supported operation. To work with Intune, the setting must support the **Add** or **Replace** operations.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- Create a [custom profile on Windows devices](custom-settings-windows-10.md).

- Learn more about [custom profiles](custom-settings-configure.md) in Intune.
