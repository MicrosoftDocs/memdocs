---
# required metadata

title: Custom settings - Windows Holographic for Business devices - Microsoft Intune
description: Add or create a custom profile to use the OMA-URI settings for devices running Windows Holographic for Business in Microsoft Intune, including Microsoft Hololens. You can set AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates, and ApplicationLaunchRestrictions policy configuration service provider (CSP) settings.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.article: article
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---
# Use custom settings for Windows Holographic for Business devices in Intune

Using Microsoft Intune, you can add or create custom settings for your Windows Holographic for Business devices using "custom profiles". Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

Windows Holographic for Business custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure different features. These settings are typically used by mobile device manufacturers to control features on the device.

Windows Holographic for Business makes many configuration service providers (CSPs) settings available. For a CSP overview, see [Introduction to configuration service providers (CSPs) for IT pros](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers). For specific CSPs supported by Windows Holographic, see [CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens).

If you're looking for a specific setting, remember that the [Windows Holographic for Business device restriction profile](device-restrictions-windows-holographic.md) includes many built-in settings. So, you may not need to enter custom values.

This article shows you how to create a custom profile for Windows Holographic for Business devices. It also includes a list of the recommended OMA-URI settings.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following settings:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Hololens custom profile**.
    - **Description**: Enter a description that gives an overview of the setting, and any other important details.
    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Custom**.

4. In **Custom OMA-URI Settings**, select **Add**. Enter the following settings:

    - **Name**: Enter a unique name for the OMA-URI setting to help you identify it in the list of settings.
    - **Description**: Enter a description that gives an overview of the setting, and any other important details.
    - **OMA-URI** (case sensitive): Enter the OMA-URI you want to use as a setting.
    - **Data type**: Select the data type you'll use for this OMA-URI setting. Your options:

        - String
        - String (XML file)
        - Date and time
        - Integer
        - Floating point
        - Boolean
        - Base64 (file)

    - **Value**: Enter the data value you want to associate with the OMA-URI you entered. The value depends on the data type you selected. For example, if you select **Date and time**, select the value from a date picker.

    After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (.csv) file.

5. Select **OK** to save your changes. Continue to add more settings as needed.
6. When finished, select **OK** > **Create** to create the Intune profile. When complete, your profile is shown in the **Devices - Configuration profiles** list.

## Recommended custom settings

The following settings are useful for devices running Windows Holographic for Business:

### [AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Integer<br/>0 - not allowed<br/>1 - allowed (default)|

### [AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Integer<br/>0 – Update service is not allowed <br/>1  – Update service is allowed (default).|

### [AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Integer<br/>0 - not allowed<br/>1 - allowed (default)|

### [RequireUpdatesApproval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Integer<br/>0 – Not configured. The device installs all applicable updates.<br/>1 – The device only installs updates that are both applicable and on the Approved Updates list. Set this policy to 1 if IT wants to control the deployment of updates on devices, such as when testing is required prior to deployment.|

### [ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Integer 0-23, where 0=12AM and 23=11PM<br/>Default value is 3.|

### [UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|String<br/>URL - the device checks for updates from the WSUS server at the specified URL.<br/>Not configured - The device checks for updates from Microsoft Update.|

### [ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Important**<br/>You must read and accept the update EULAs on behalf of your end users. Failure to do so is a breach of legal or contractual obligations.|Node for update approvals and EULA acceptance on behalf of the end user.<br/><br/>For more information, see [Update CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp).|

### [ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**Important**<br/>The AppLocker CSP article uses escaped XML examples. To configure the settings with Intune custom profiles, you must use plain XML.|String<br/>For more information, see [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).|

### [DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Integer<br/>0 - delete immediately when the device returns to a state with no currently active users<br/>1 - delete at storage capacity threshold (default)<br/>2 - delete at both storage capacity threshold and profile inactivity threshold|

### [EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Boolean<br/>True - enable<br/>False - disable (default)|

### [ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Integer<br/>Default value is 30.|


### [StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Integer<br/>Default value is 25.|

### [StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Data type|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Integer<br/>Default value is 50.|

## Find the policies you can configure

You can find a complete list of all configuration service providers (CSPs) that Windows Holographic supports in [CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). Not all settings are compatible with all Windows Holographic versions. The table in [CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) lists the supported versions for each CSP.

Additionally, Intune doesn't support all of the settings listed in [CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). To find out if Intune supports the setting you want, open the article for that setting. Each setting page shows its supported operation. To work with Intune, the setting must support the **Add** or **Replace** operations.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](../device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Create a [custom profile on Windows 10 devices](../custom-settings-windows-10.md).
