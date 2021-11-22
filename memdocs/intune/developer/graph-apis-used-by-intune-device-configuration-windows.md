---
# required metadata

title: Graph APIs to configure devices in Microsoft Intune
titleSuffix:
description: See a list of all the Graph API entities with the matching Windows CSP and offset URI on Windows 10 devices and newer used when configuring devices in Microsoft Intune. See the matching API and CSP for shared PCs, endpoint protection, Microsoft Defender for Endpoint, identity protection, Windows 10 Teams, kiosk, and Windows Update for Business.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- M365-identity-device-management
- Windows
---

# Graph APIs and matching Windows 10 CSPs used in Intune

Microsoft Intune uses the [Graph API entities](/graph/api/resources/intune-graph-overview) (opens another Docs site) to configure devices (**Intune** > **Device configuration**) running Windows 10 and later. The Graph API uses configuration service providers (CSPs) to read, set, change, and/or delete configuration settings on devices.

This list applies to:

- Windows 10 and later

This article lists the Graph entities and their matching Windows 10 CSPs and offset URIs.

This information is useful for a variety of scenarios. For example, see what's used by Intune, see settings to include in custom OMA-URI configurations, and so on. 

## Windows 10 CSPs

For more information on Windows 10 configuration service providers, see the [configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (opens another Docs site).

## Graph API properties to CSP mapping

The following list shows the majority of Graph API entities used by Microsoft Intune for Windows 10 device configuration. It also shows the corresponding Windows 10 CSP and offset URI.

To see the Windows 10 versions the following APIs apply, use the Windows 10 [configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (opens another Docs site).

### EditionUpgradeConfiguration.License 
**CSP**: ./Device/Vendor/MSFT/WindowsLicensing  
**Offset URI**: /UpgradeEditionWithLicense

### EditionUpgradeConfiguration.LicenseType 
**CSP**: ./Device/Vendor/MSFT/WindowsLicensing  
**Offset URI**: /LicenseKeyType

### EditionUpgradeConfiguration.ProductKey 
**CSP**: ./Device/Vendor/MSFT/WindowsLicensing  
**Offset URI**: /UpgradeEditionWithProductKey

### EditionUpgradeConfiguration.WindowsSMode 
**CSP**: ./Device/Vendor/MSFT/WindowsLicensing  
**Offset URI**: /SMode/SwitchingPolicy

### SharedPCConfiguration.AccountManagerPolicy 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /DeletionPolicy, /DiskLevelCaching, /InactiveThreshold, /DiskLevelDeletion

### SharedPCConfiguration.AccountManagerPolicy (Windows Holographic for Business edition targeted devices) 
**CSP**: ./Vendor/MSFT/AccountManagement  
**Offset URI**: /DeletionPolicy, /StorageCapacityStartDeletion, /StorageCapacityStopDeletion, /ProfileInactivityThreshold

### SharedPCConfiguration.AllowedAccounts 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /AccountModel

### SharedPCConfiguration.AllowLocalStorage 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /RestrictLocalStorage

### SharedPCConfiguration.DisableAccountManager 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /EnableAccountManager

### SharedPCConfiguration.DisableEduPolicies 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /SetEduPolicies

### SharedPCConfiguration.DisablePowerPolicies 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /SetPowerPolicies

### SharedPCConfiguration.DisableSignInOnResume 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /SignInOnResume

### SharedPCConfiguration.Enabled 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /EnableSharedPCMode

### SharedPCConfiguration.IdleTimeBeforeSleepInSeconds 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /InactiveThreshold

### SharedPCConfiguration.KioskAppDisplayName 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /KioskModeUserTileDisplayText

### SharedPCConfiguration.KioskAppUserModelId 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /KioskModeAUMID

### SharedPCConfiguration.LocalStorage 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /RestrictLocalStorage

### SharedPCConfiguration.MaintenanceStartTime 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /MaintenanceStartTime

### SharedPCConfiguration.SetAccountManager
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /EnableAccountManager

### SharedPCConfiguration.SetEduPolicies 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /SetEduPolicies

### SharedPCConfiguration.SetPowerPolicies 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /SetPowerPolicies

### SharedPCConfiguration.SignInOnResume 
**CSP**: ./Vendor/MSFT/SharedPC  
**Offset URI**: /SignInOnResume

### Windows10endpointconfiguration.smartScreenBlockOverrideForFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/SmartScreen/PreventOverrideForFilesInShell

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowFileSaveOnHost 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/SaveFilesToHost

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPersistence 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/AllowPersistence

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToLocalPrinters 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/PrintingSettings

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToNetworkPrinters 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/PrintingSettings

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToPDF 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/PrintingSettings

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowPrintToXPS 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/PrintingSettings

### Windows10EndpointProtectionConfiguration.ApplicationGuardAllowVirtualGPU 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/AllowVirtualGPU

### Windows10EndpointProtectionConfiguration.ApplicationGuardBlockClipboardSharing 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/ClipboardSettings

### Windows10EndpointProtectionConfiguration.ApplicationGuardBlockFileTransfer 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/ClipboardFileType

### Windows10EndpointProtectionConfiguration.ApplicationGuardBlockNonEnterpriseContent 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/BlockNonEnterpriseContent

### Windows10EndpointProtectionConfiguration.ApplicationGuardEnabled 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Settings/AllowWindowsDefenderApplicationGuard

### Windows10EndpointProtectionConfiguration.ApplicationGuardForceAuditing 
**CSP**: ./Device/Vendor/MSFT/WindowsDefenderApplicationGuard  
**Offset URI**: /Audit/AuditApplicationGuard

### Windows10EndpointProtectionConfiguration.BitLockerAllowStandardUserEncryption 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /AllowStandardUserEncryption

### Windows10EndpointProtectionConfiguration.BitLockerDisableWarningForOtherDiskEncryption 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /AllowWarningForOtherDiskEncryption

### Windows10EndpointProtectionConfiguration.BitLockerEnableStorageCardEncryptionOnMobile 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /RequireStorageCardEncryption

### Windows10EndpointProtectionConfiguration.BitLockerEncryptDevice 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /RequireDeviceEncryption

### Windows10EndpointProtectionConfiguration.BitLockerFixedDrivePolicy 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /EncryptionMethodByDriveType, /FixedDrivesRequireEncryption, /FixedDrivesRecoveryOptions

### Windows10EndpointProtectionConfiguration.BitLockerRemovableDrivePolicy 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /EncryptionMethodByDriveType, /RemovableDrivesRequireEncryption

### Windows10EndpointProtectionConfiguration.BitLockerSystemDrivePolicy 
**CSP**: ./Device/Vendor/MSFT/BitLocker  
**Offset URI**: /EncryptionMethodByDriveType, /SystemDrivesRequireStartupAuthentication, /SystemDrivesMinimumPINLength, /SystemDrivesRecoveryMessage, /SystemDrivesRecoveryOptions

### windows10endpointprotectionconfiguration.clientConnectionEncryptionLevel 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteDesktopServices/ClientConnectionEncryptionLevel

### windows10endpointprotectionconfiguration.configureSMBV1ClientDriver 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/ConfigureSMBV1ClientDriver

### Windows10EndpointProtectionConfiguration.ConnectivityDownloadingOfPrintDriversOverHttp 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/DisableDownloadingOfPrintDriversOverHTTP

### Windows10EndpointProtectionConfiguration.ConnectivityHardenedUncPaths 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/HardenedUNCPaths

### Windows10EndpointProtectionConfiguration.ConnectivityInternetDownloadForWebPublishingAndOnlineOrderingWizards 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/DisableInternetDownloadForWebPublishingAndOnlineOrderingWizards

### Windows10EndpointProtectionConfiguration.ConnectivityPrintingOverHttp 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/DiablePrintingOverHTTP

### Windows10EndpointProtectionConfiguration.CredentialsUIEnumerateAdministrators 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/CredentialsUI/EnumerateAdministrators

### Windows10EndpointProtectionConfiguration.DefenderAdditionalGuardedFolders 
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/Defender/ControlledFolderAccessProtectedFolders

### Windows10EndpointProtectionConfiguration.DefenderAdvancedRansomewareProtectionType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderAttackSurfaceReductionExcludedPaths 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionOnlyExclusions

### Windows10EndpointProtectionConfiguration.DefenderEmailContentExecution 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowEmailScanning

### Windows10EndpointProtectionConfiguration.DefenderEmailContentExecutionType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderExploitProtectionXml 
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/ExploitGuard/ExploitProtectionSettings

### Windows10EndpointProtectionConfiguration.DefenderExploitProtectionXmlFileName 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/ExploitGuard/ExploitProtectionSettings

### Windows10EndpointProtectionConfiguration.DefenderGuardedFoldersAllowedAppPaths 
**CSP**: ./Device/Vendor/MSFT/Policy 
**Offset URI**: /Config/Defender/ControlledFolderAccessAllowedApplications

### Windows10EndpointProtectionConfiguration.DefenderGuardMyFoldersType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/EnableControlledFolderAccess

### Windows10EndpointProtectionConfiguration.DefenderNetworkProtectionType 
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/Defender/EnableNetworkProtection

### Windows10EndpointProtectionConfiguration.DefenderOfficeAppsExecutableContentCreationOrLaunch 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderOfficeAppsExecutableContentCreationOrLaunchType
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderOfficeAppsLaunchChildProcess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderOfficeAppsLaunchChildProcessType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderOfficeAppsOtherProcessInjection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderOfficeAppsOtherProcessInjectionType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType 

### Windows10EndpointProtectionConfiguration.DefenderOfficeMacroCodeAllowWin32Imports 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderOfficeMacroCodeAllowWin32ImportsType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderPreventCredentialStealingType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderProcessCreation 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderProcessCreationType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderProtectAgainstPotentiallyUnwantedApplications 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/TurnOnWindowsDefenderProtectionAgainstPotentiallyUnwantedApplications

### Windows10EndpointProtectionConfiguration.DefenderScriptDownloadedPayloadExecution 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderScriptDownloadedPayloadExecutionType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderScriptObfuscatedMacroCode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderScriptObfuscatedMacroCodeType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterBlockExploitProtectionOverride 
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableAccountUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableAccountProtectionUI

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableAppBrowserUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableAppBrowserUI

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableFamilyUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableFamilyUI

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableHealthUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableHealthUI

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableNetworkUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableNetworkUI

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableSecureBootUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/HideSecureBoot

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableTroubleshootingUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/HideTPMTroubleshooting

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterDisableVirusUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/DisableVirusUI

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterHelpEmail 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/Email

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterHelpPhone 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/Phone

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterHelpURL 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/URL

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterITContactDisplay 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /WindowsDefenderSecurityCenter/EnableCustomizedToasts, /WindowsDefenderSecurityCenter/EnableInAppCustomization

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterNotificationsFromApp 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/HideWindowsSecurityNotificationAreaControl

### Windows10EndpointProtectionConfiguration.DefenderSecurityCenterOrganizationDisplayName 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsDefenderSecurityCenter/CompanyName

### Windows10EndpointProtectionConfiguration.DefenderUntrustedExecutable 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderUntrustedExecutableType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderUntrustedUSBProcess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules

### Windows10EndpointProtectionConfiguration.DefenderUntrustedUSBProcessType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AttackSurfaceReductionRules (CSP/Configuration requires Graph properties: windows10endpointprotection/Configuration.defenderOfficeAppsOtherProcessInjectionType, windows10endpointprotection/Configuration.defenderOfficeAppsExecutableContentCreationOrLaunchType, windows10endpointprotection/Configuration.defenderOfficeAppsLaunchChildProcessType, windows10endpointprotection/Configuration.defenderOfficeMacroCodeAllowWin32ImportsType, windows10endpointprotection/Configuration.defenderScriptObfuscatedMacroCodeType, windows10endpointprotection/Configuration.defenderScriptDownloadedPayloadExecutionType, windows10endpointprotection/Configuration.defenderEmailContentExecutionType, windows10endpointprotection/Configuration.defenderPreventCredentialStealingType, windows10endpointprotection/Configuration.defenderUntrustedUSBProcessType

### Windows10EndpointProtectionConfiguration.DeviceGuardEnableSecureBootWithDMA 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceGuard/RequirePlatformSecurityFeatures

### Windows10EndpointProtectionConfiguration.DeviceGuardEnableVirtualizationBasedSecurity 
**CSP**: ./Device/Vendor/MSFT/Policy 
**Offset URI**: /Config/DeviceGuard/EnableVirtualizationBasedSecurity

### Windows10EndpointProtectionConfiguration.DeviceGuardLaunchSystemGuard 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceGuard/ConfigureSystemGuardLaunch

### Windows10EndpointProtectionConfiguration.DeviceGuardLocalSystemAuthorityCredentialGuardSettings 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceGuard/LsaCfgFlags

### Windows10EndpointProtectionConfiguration.DmaGuardDeviceEnumerationPolicy 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DmaGuard/DeviceEnumerationPolicy

### Windows10EndpointProtectionConfiguration.EventLogServiceApplicationLogMaximumFileSizeInKb 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/EventLogService/SpecifyMaximumFileSizeApplicationLog

### Windows10EndpointProtectionConfiguration.EventLogServiceSecurityLogMaximumFileSizeInKb 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/EventLogService/SpecifyMaximumFileSizeSecurityLog

### Windows10EndpointProtectionConfiguration.EventLogServiceSystemLogMaximumFileSizeInKb 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/EventLogService/SpecifyMaximumFileSizeSystemLog

### Windows10EndpointProtectionConfiguration.ExplorerDataExecutionPrevention 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/FileExplorer/TurnOffDataExecutionPreventionForExplorer

### Windows10EndpointProtectionConfiguration.ExplorerHeapTerminationOnCorruption 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/FileExplorer/TurnOffHeapTerminationOnCorruption

### Windows10EndpointProtectionConfiguration.FirewallBlockStatefulFTP 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/DisableStatefulFtp

### Windows10EndpointProtectionConfiguration.FirewallCertificateRevocationListCheckMethod 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/CRLcheck

### Windows10EndpointProtectionConfiguration.FirewallIdleTimeoutForSecurityAssociationInSeconds 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/SaIdleTime

### Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowDHCP 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowICMP 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowNeighborDiscovery 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### Windows10EndpointProtectionConfiguration.FirewallIPSecExemptionsAllowRouterDiscovery 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/IPsecExempt

### Windows10EndpointProtectionConfiguration.FirewallMergeKeyingModuleSettings 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/OpportunisticallyMatchAuthSetPerKM

### Windows10EndpointProtectionConfiguration.FirewallPacketQueueingMethod 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/EnablePacketQueue

### Windows10EndpointProtectionConfiguration.FirewallPreSharedKeyEncodingMethod 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/Global/PresharedKeyEncoding

### Windows10EndpointProtectionConfiguration.FirewallProfileDomain 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /EnableFirewall, /DisableStealthMode, /Shielded, /DisableUnicastResponsesToMulticastBroadcast, /DisableInboundNotifications, /AuthAppsAllowUserPrefMerge, /GlobalPortsAllowUserPrefMerge, /AllowLocalPolicyMerge, /DefaultOutboundAction, /DefaultInboundAction, /DisableStealthModeIpsecSecuredPacketExemption, /AllowLocalIpsecPolicyMerge

### windows10endpointprotectionconfiguration.firewallProfileDomain.inboundConnectionsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/DefaultInboundAction

### windows10endpointprotectionconfiguration.firewallProfileDomain.inboundNotificationsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/DisableInboundNotifications

### windows10endpointprotectionconfiguration.firewallProfileDomain.inboundNotificationsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/EnableFirewall

### windows10endpointprotectionconfiguration.firewallProfileDomain.outboundConnectionsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/DomainProfile/DefaultOutboundAction

### Windows10EndpointProtectionConfiguration.FirewallProfilePrivate 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /EnableFirewall, /DisableStealthMode, /Shielded, /DisableUnicastResponsesToMulticastBroadcast, /DisableInboundNotifications, /AuthAppsAllowUserPrefMerge, /GlobalPortsAllowUserPrefMerge, /AllowLocalPolicyMerge, /DefaultOutboundAction, /DefaultInboundAction, /DisableStealthModeIpsecSecuredPacketExemption, /AllowLocalIpsecPolicyMerge

### windows10endpointprotectionconfiguration.firewallProfilePrivate.firewallEnabled 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/EnableFirewall

### windows10endpointprotectionconfiguration.firewallProfilePrivate.inboundConnectionsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/DefaultInboundAction

### windows10endpointprotectionconfiguration.firewallProfilePrivate.inboundNotificationsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/DisableInboundNotifications

### windows10endpointprotectionconfiguration.firewallProfilePrivate.outboundConnectionsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PrivateProfile/DefaultOutboundAction

### Windows10EndpointProtectionConfiguration.FirewallProfilePublic 
**CSP**: ./Vendor/MSFT/Firewall  
**Offset URI**: /EnableFirewall, /DisableStealthMode, /Shielded, /DisableUnicastResponsesToMulticastBroadcast, /DisableInboundNotifications, /AuthAppsAllowUserPrefMerge, /GlobalPortsAllowUserPrefMerge, /AllowLocalPolicyMerge, /DefaultOutboundAction, /DefaultInboundAction, /DisableStealthModeIpsecSecuredPacketExemption, /AllowLocalIpsecPolicyMerge

### windows10endpointprotectionconfiguration.firewallProfilePublic.connectionSecurityRulesFromGroupPolicyMerged 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/AllowLocalIpsecPolicyMerge

### windows10endpointprotectionconfiguration.firewallProfilePublic.firewallEnabled 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/EnableFirewall

### windows10endpointprotectionconfiguration.firewallProfilePublic.inboundConnectionsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/DefaultInboundAction

### windows10endpointprotectionconfiguration.firewallProfilePublic.inboundNotificationsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/DisableInboundNotifications

### windows10endpointprotectionconfiguration.firewallProfilePublic.outboundConnectionsBlocked 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/DefaultOutboundAction

### windows10endpointprotectionconfiguration.firewallProfilePublic.policyRulesFromGroupPolicyMerged 
**CSP**: ./Device/Vendor/MSFT/Firewall  
**Offset URI**: /MdmStore/PublicProfile/AllowLocalPolicyMerge

### Windows10EndpointProtectionConfiguration.LanManagerAuthenticationLevel 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_LANManagerAuthenticationLevel

### Windows10EndpointProtectionConfiguration.LanManagerWorkstationDisableInsecureGuestLogons 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LanmanWorkstation/EnableInsecureGuestLogons

### Windows10EndpointProtectionConfiguration.LanManagerWorkstationEnableInsecureGuestLogons 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LanmanWorkstation/EnableInsecureGuestLogons

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAdministratorAccountName 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_RenameAdministratorAccount

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAdministratorElevationPromptBehavior
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_BehaviorOfTheElevationPromptForAdministrators

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowAnonymousEnumerationOfSAMAccountsAndShares 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowPKU2UAuthenticationRequests 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_AllowPKU2UAuthenticationRequests

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowRemoteCallsToSecurityAccountsManager 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_RestrictClientsAllowedToMakeRemoteCallsToSAM

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowRemoteCallsToSecurityAccountsManagerHelperBool 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_RestrictClientsAllowedToMakeRemoteCallsToSAM

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowSystemToBeShutDownWithoutHavingToLogOn 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Shutdown\_AllowSystemToBeShutDownWithoutHavingToLogOn

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowUIAccessApplicationElevation 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_AllowUIAccessApplicationsToPromptForElevation

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowUIAccessApplicationsForSecureLocations 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsAllowUndockWithoutHavingToLogon 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_AllowUndockWithoutHavingToLogon

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockMicrosoftAccounts 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_BlockMicrosoftAccounts

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockRemoteLogonWithBlankPassword 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockRemoteOpticalDriveAccess 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_RestrictCDROMAccessToLocallyLoggedOnUserOnly

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsBlockUsersInstallingPrinterDrivers 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsClearVirtualMemoryPageFile 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Shutdown\_ClearVirtualMemoryPageFile

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsClientDigitallySignCommunicationsAlways 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient\_DigitallySignCommunicationsAlways

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsClientSendUnencryptedPasswordToThirdPartySMBServers 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient\_SendUnencryptedPasswordToThirdPartySMBServers

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDetectApplicationInstallationsAndPromptForElevation 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_DetectApplicationInstallationsAndPromptForElevation

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableAdministratorAccount 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableAdministratorAccountStatus

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableClientDigitallySignCommunicationsIfServerAgrees 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkClient\_DigitallySignCommunicationsIfServerAgrees

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableGuestAccount 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableGuestAccountStatus

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableServerDigitallySignCommunicationsAlways 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkServer\_DigitallySignCommunicationsAlways

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDisableServerDigitallySignCommunicationsIfClientAgrees 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/MicrosoftNetworkServer\_DigitallySignCommunicationsIfClientAgrees

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDoNotAllowAnonymousEnumerationOfSAMAccounts 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_DoNotAllowAnonymousEnumerationOfSAMAccounts

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDoNotRequireCtrlAltDel 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DoNotRequireCTRLALTDEL

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsDoNotStoreLANManagerHashValueOnNextPasswordChange 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_DoNotStoreLANManagerHashValueOnNextPasswordChange

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsEnableAdministratorAccount 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableAdministratorAccountStatus

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsEnableGuestAccount 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_EnableGuestAccountStatus

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsFormatAndEjectOfRemovableMediaAllowedUser 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Devices\_AllowedToFormatAndEjectRemovableMedia

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsGuestAccountName 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/Accounts\_RenameGuestAccount

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsHideLastSignedInUser 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DoNotDisplayLastSignedIn

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsHideUsernameAtSignIn 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DoNotDisplayUsernameAtSignIn

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsInformationDisplayedOnLockScreen 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DisplayUserInformationWhenTheSessionIsLocked

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsInformationShownOnLockScreen 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_DisplayUserInformationWhenTheSessionIsLocked

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsLogOnMessageText 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MessageTextForUsersAttemptingToLogOn

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsLogOnMessageTitle 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MessageTitleForUsersAttemptingToLogOn

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMachineInactivityLimit 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MachineInactivityLimit

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMachineInactivityLimitInMinutes 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_MachineInactivityLimit

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMinimumSessionSecurityForNtlmSspBasedClients 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_MinimumSessionSecurityForNTLMSSPBasedClients

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsMinimumSessionSecurityForNtlmSspBasedServers 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkSecurity\_MinimumSessionSecurityForNTLMSSPBasedServers

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsOnlyElevateSignedExecutables 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_OnlyElevateExecutableFilesThatAreSignedAndValidated

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsRestrictAnonymousAccessToNamedPipesAndShares 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/NetworkAccess\_RestrictAnonymousAccessToNamedPipesAndShares

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsSmartCardRemovalBehavior 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/InteractiveLogon\_SmartCardRemovalBehavior

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsStandardUserElevationPromptBehavior 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_BehaviorOfTheElevationPromptForStandardUsers

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsSwitchToSecureDesktopWhenPromptingForElevation 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_SwitchToTheSecureDesktopWhenPromptingForElevation

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsUseAdminApprovalMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_UseAdminApprovalMode

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsUseAdminApprovalModeForAdministrators 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_RunAllAdministratorsInAdminApprovalMode

### Windows10EndpointProtectionConfiguration.LocalSecurityOptionsVirtualizeFileAndRegistryWriteFailuresToPerUserLocations 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/LocalPoliciesSecurityOptions/UserAccountControl\_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations

### Windows10EndpointProtectionConfiguration.NetworkIcmpRedirectsOverrideOspfGeneratedRoutes 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSLegacy/AllowICMPRedirectsToOverrideOSPFGeneratedRoutes

### Windows10EndpointProtectionConfiguration.NetworkIgnoreNetBiosNameReleaseRequestsExceptFromWinsServers 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSLegacy/AllowTheComputerToIgnoreNetBIOSNameReleaseRequestsExceptFromWINSServers

### Windows10EndpointProtectionConfiguration.NetworkIpSourceRoutingProtectionLevel 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSLegacy/IPSourceRoutingProtectionLevel

### Windows10EndpointProtectionConfiguration.NetworkIpV6SourceRoutingProtectionLevel 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSLegacy/IPv6SourceRoutingProtectionLevel

### Windows10EndpointProtectionConfiguration.PasswordPinLogOn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/CredentialProviders/AllowPINLogon

### Windows10EndpointProtectionConfiguration.PowerShellShellScriptBlockLogging 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsPowerShell/TurnOnPowerShellScriptBlockLogging

### Windows10EndpointProtectionConfiguration.RemoteAssistanceSolicitedSetting 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/HardenedUNCPaths

### Windows10EndpointProtectionConfiguration.RemoteDesktopServicesClientConnectionEncryptionLevel 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteDesktopServices/ClientConnectionEncryptionLevel

### Windows10EndpointProtectionConfiguration.RemoteDesktopServicesDriveRedirection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteDesktopServices/DoNotAllowDriveRedirection

### Windows10EndpointProtectionConfiguration.RemoteDesktopServicesPasswordSaving 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteDesktopServices/DoNotAllowPasswordSaving

### Windows10EndpointProtectionConfiguration.RemoteDesktopServicesPromptForPasswordUponConnection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteDesktopServices/PromptForPasswordUponConnection

### Windows10EndpointProtectionConfiguration.RemoteDesktopServicesSecureRpcCommunication 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteDesktopServices/RequireSecureRPCCommunication

### Windows10EndpointProtectionConfiguration.RemoteHostDelegationOfNonExportableCredentials 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/CredentialsDelegation/RemoteHostAllowsDelegationOfNonExportableCredentials

### Windows10EndpointProtectionConfiguration.RemoteManagementClientBasicAuthentication 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteManagement/AllowBasicAuthentication\_Client

### Windows10EndpointProtectionConfiguration.RemoteManagementClientDigestAuthentication 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteManagement/DisallowDigestAuthentication

### Windows10EndpointProtectionConfiguration.RemoteManagementClientUnencryptedTraffic 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteManagement/AllowUnencryptedTraffic\_Client

### Windows10EndpointProtectionConfiguration.RemoteManagementServiceBasicAuthentication 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteManagement/AllowBasicAuthentication\_Service

### Windows10EndpointProtectionConfiguration.RemoteManagementServiceStoringRunAsCredentials 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteManagement/DisallowStoringOfRunAsCredentials

### Windows10EndpointProtectionConfiguration.RemoteManagementServiceUnencryptedTraffic 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteManagement/AllowUnencryptedTraffic\_Service

### Windows10EndpointProtectionConfiguration.RpcUnauthenticatedClientOptions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteProcedureCall/RestrictUnauthenticatedRPCClients

### Windows10EndpointProtectionConfiguration.SecurityGuideApplyUacRestrictionsToLocalAccountsOnNetworkLogon 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/ApplyUACRestrictionsToLocalAccountsOnNetworkLogon

### Windows10EndpointProtectionConfiguration.SecurityGuideSmbV1ClientDriverStartConfiguration 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/ConfigureSMBV1ClientDriver

### Windows10EndpointProtectionConfiguration.SecurityGuideSmbV1Server 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/ConfigureSMBV1Server

### Windows10EndpointProtectionConfiguration.SecurityGuideStructuredExceptionHandlingOverwriteProtection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/EnableStructuredExceptionHandlingOverwriteProtection

### Windows10EndpointProtectionConfiguration.SecurityGuideWDigestAuthentication 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/MSSecurityGuide/WDigestAuthentication

### Windows10EndpointProtectionConfiguration.SmartScreenBlockOverrideForFiles 
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/DeviceGuard/RequirePlatformSecurityFeatures

### Windows10EndpointProtectionConfiguration.SmartScreenEnableInShell 
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/SmartScreen/EnableSmartScreenInShell

### windows10endpointprotectionconfiguration.solicitedRemoteAssistance 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/RemoteAssistance/SolicitedRemoteAssistance

### Windows10EndpointProtectionConfiguration.UserRightsAccessCredentialManagerAsTrustedCaller 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/AccessCredentialManagerAsTrustedCaller

### windows10EndpointProtectionConfiguration.UserRightsAccessFromNetwork 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/AccessFromNetwork

### Windows10EndpointProtectionConfiguration.userRightsActAsPartOfTheOperatingSystem 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ActAsPartOfTheOperatingSystem

### Windows10EndpointProtectionConfiguration.UserRightsAllowAccessFromNetwork 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/AccessFromNetwork

### Windows10EndpointProtectionConfiguration.UserRightsBackupData 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/BackupFilesAndDirectories

### Windows10EndpointProtectionConfiguration.UserRightsBlockAccessFromNetwork 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/DenyAccessFromNetwork

### Windows10EndpointProtectionConfiguration.UserRightsChangeSystemTime 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ChangeSystemTime

### Windows10EndpointProtectionConfiguration.UserRightsCreateGlobalObjects 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/CreateGlobalObjects

### Windows10EndpointProtectionConfiguration.UserRightsCreatePageFile 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/CreatePageFile

### Windows10EndpointProtectionConfiguration.UserRightsCreatePermanentSharedObjects 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/CreatePermanentSharedObjects

### Windows10EndpointProtectionConfiguration.UserRightsCreateSymbolicLinks 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/CreateSymbolicLinks

### Windows10EndpointProtectionConfiguration.UserRightsCreateToken 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/CreateToken

### Windows10EndpointProtectionConfiguration.UserRightsDebugPrograms 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/DebugPrograms

### Windows10EndpointProtectionConfiguration.UserRightsDelegation 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/EnableDelegation

### windows10EndpointProtectionConfiguration.UserRightsDenyAccessFromNetwork 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/DenyAccessFromNetwork

### Windows10EndpointProtectionConfiguration.UserRightsGenerateSecurityAudits 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/GenerateSecurityAudits

### Windows10EndpointProtectionConfiguration.UserRightsImpersonateClient 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ImpersonateClient

### Windows10EndpointProtectionConfiguration.UserRightsIncreaseSchedulingPriority 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/IncreaseSchedulingPriority

### Windows10EndpointProtectionConfiguration.UserRightsLoadUnloadDrivers 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/LoadUnloadDeviceDrivers

### Windows10EndpointProtectionConfiguration.UserRightsLocalLogOn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/AllowLocalLogOn

### Windows10EndpointProtectionConfiguration.UserRightsLockMemory 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/LockMemory

### Windows10EndpointProtectionConfiguration.UserRightsManageAuditingAndSecurityLogs 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ManageAuditingAndSecurityLog

### Windows10EndpointProtectionConfiguration.UserRightsManageVolumes 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ManageVolume

### Windows10EndpointProtectionConfiguration.UserRightsModifyFirmwareEnvironment 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ModifyFirmwareEnvironment

### Windows10EndpointProtectionConfiguration.UserRightsModifyObjectLabels 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ModifyObjectLabel

### Windows10EndpointProtectionConfiguration.UserRightsProfileSingleProcess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/ProfileSingleProcess

### Windows10EndpointProtectionConfiguration.UserRightsRegisterProcessAsService 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/DenyLocalLogOn

### Windows10EndpointProtectionConfiguration.UserRightsRemoteDesktopServicesLogOn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/DenyRemoteDesktopServicesLogOn

### Windows10EndpointProtectionConfiguration.UserRightsRemoteShutdown 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/RemoteShutdown

### Windows10EndpointProtectionConfiguration.UserRightsRestoreData 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/RestoreFilesAndDirectories

### Windows10EndpointProtectionConfiguration.UserRightsTakeOwnership 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/UserRights/TakeOwnership

### Windows10EndpointProtectionConfiguration.WindowsConnectionManagerConnectionToNonDomainNetworks 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsConnectionManager/ProhitConnectionToNonDomainNetworksWhenConnectedToDomainAuthenticatedNetwork

### Windows10EndpointProtectionConfiguration.WindowsLogOnSignInLastInteractiveUserAfterSystemInitiatedRestart 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsLogon/SignInLastInteractiveUserAutomaticallyAfterASystemInitiatedRestart

### Windows10EndpointProtectionConfiguration.XboxServicesAccessoryManagementServiceStartupMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode

### Windows10EndpointProtectionConfiguration.XboxServicesEnableXboxGameSaveTask 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/TaskScheduler/EnableXboxGameSaveTask

### Windows10EndpointProtectionConfiguration.XboxServicesLiveAuthManagerServiceStartupMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode

### Windows10EndpointProtectionConfiguration.XboxServicesLiveGameSaveServiceStartupMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/SystemServices/XboxServicesLiveGameSaveServiceStartupMode

### Windows10EndpointProtectionConfiguration.XboxServicesLiveNetworkingServiceStartupMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode

### Windows10EnterpriseModernAppManagementConfiguration.UninstallBuiltInApps
**CSP**: N/A Graph API call only
**Offset URI**: N/A Graph API call only

### Windows10GeneralConfiguration.AccountsBlockAddingNonMicrosoftAccountEmail 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Accounts/AllowAddingNonMicrosoftAccountsManually

### Windows10GeneralConfiguration.AntiTheftModeBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Security/AntiTheftMode

### Windows10GeneralConfiguration.AppManagementMSIAllowUserControlOverInstall 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/MSIAllowUserControlOverInstall

### Windows10GeneralConfiguration.AppManagementMSIAlwaysInstallWithElevatedPrivileges 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges

### Windows10GeneralConfiguration.AppsAllowTrustedAppsSideloading 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/AllowAllTrustedApps

### Windows10GeneralConfiguration.AppsBlockWindowsStoreOriginatedApps 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/DisableStoreOriginatedApps

### Windows10GeneralConfiguration.AppsMicrosoftAccountsOptional 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/AppRuntime/AllowMicrosoftAccountsToBeOptional

### Windows10GeneralConfiguration.AssignedAccessMultiModeProfiles 
**CSP**: ./Device/Vendor/MSFT/AssignedAccess  
**Offset URI**: /Configuration

### Windows10GeneralConfiguration.AssignedAccessSingleModeAppUserModelId 
**CSP**: ./Device/Vendor/MSFT/AssignedAccess  
**Offset URI**: /Configuration

### Windows10GeneralConfiguration.AssignedAccessSingleModeUserName 
**CSP**: ./Device/Vendor/MSFT/AssignedAccess  
**Offset URI**: /Configuration

### Windows10GeneralConfiguration.AuthenticationAllowFIDODevice 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Authentication/AllowFidoDeviceSignon

### Windows10GeneralConfiguration.AuthenticationAllowSecondaryDevice 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Authentication/AllowSecondaryAuthenticationDevice

### Windows10GeneralConfiguration.AuthenticationPreferredAzureADTenantDomainName 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Authentication/PreferredAadTenantDomainName

### Windows10GeneralConfiguration.AuthenticationWebSignIn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Authentication/EnableWebSignIn

### Windows10GeneralConfiguration.AutoPlayDefaultAutoRunBehavior 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Autoplay/SetDefaultAutoRunBehavior

### Windows10GeneralConfiguration.AutoPlayForNonVolumeDevices 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Autoplay/DisallowAutoplayForNonVolumeDevices

### Windows10GeneralConfiguration.AutoPlayMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Autoplay/TurnOffAutoPlay

### Windows10GeneralConfiguration.BluetoothAllowedServices 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Bluetooth/ServicesAllowedList

### Windows10GeneralConfiguration.BluetoothBlockAdvertising 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Bluetooth/AllowAdvertising

### Windows10GeneralConfiguration.BluetoothBlockDiscoverableMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Bluetooth/AllowDiscoverableMode

### Windows10GeneralConfiguration.BluetoothBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowBluetooth

### Windows10GeneralConfiguration.BluetoothBlockPrePairing 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Bluetooth/AllowPrepairing

### Windows10GeneralConfiguration.BluetoothBlockPromptedProximalConnections 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Bluetooth/AllowPromptedProximalConnections

### Windows10GeneralConfiguration.BluetoothDeviceName 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Bluetooth/LocalDeviceName

### windows10generalconfiguration.bootStartDriverInitialization 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/System/BootStartDriverInitialization

### Windows10GeneralConfiguration.CameraBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Camera/AllowCamera

### Windows10GeneralConfiguration.CellularBlockDataWhenRoaming 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowCellularDataRoaming

### Windows10GeneralConfiguration.CellularBlockVpn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowVPNOverCellular

### Windows10GeneralConfiguration.CellularBlockVpnWhenRoaming 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowVPNRoamingOverCellular

### Windows10GeneralConfiguration.CellularData 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowCellularData

### Windows10GeneralConfiguration.CertificatesBlockManualRootCertificateInstallation 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Security/AllowManualRootCertificateInstallation

### Windows10GeneralConfiguration.ConnectedDevicesServiceBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowConnectedDevices

### Windows10GeneralConfiguration.CopyPasteBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowCopyPaste

### Windows10GeneralConfiguration.CortanaBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/AboveLock/AllowCortanaAboveLock

### Windows10GeneralConfiguration.CryptographyAllowFipsAlgorithmPolicy 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Cryptography/AllowFipsAlgorithmPolicy

### Windows10GeneralConfiguration.DataProtectionBlockDirectMemoryAccess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DataProtection/AllowDirectMemoryAccess

### Windows10GeneralConfiguration.DefenderBlockEndUserAccess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowUserUIAccess

### Windows10GeneralConfiguration.DefenderBlockOnAccessProtection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowOnAccessProtection

### Windows10GeneralConfiguration.DefenderCloudBlockLevel 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/CloudBlockLevel

### Windows10GeneralConfiguration.DefenderCloudExtendedTimeout 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/CloudExtendedTimeout

### Windows10GeneralConfiguration.DefenderCloudExtendedTimeoutInSeconds 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/CloudExtendedTimeout

### Windows10GeneralConfiguration.DefenderDaysBeforeDeletingQuarantinedMalware 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/DaysToRetainCleanedMalware

### Windows10GeneralConfiguration.DefenderDetectedMalwareActions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ThreatSeverityDefaultAction

### Windows10GeneralConfiguration.DefenderFileExtensionsToExclude 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ExcludedExtensions

### Windows10GeneralConfiguration.DefenderFilesAndFoldersToExclude 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ExcludedPaths

### Windows10GeneralConfiguration.DefenderMonitorFileActivity 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowRealtimeMonitoring

### Windows10GeneralConfiguration.DefenderPotentiallyUnwantedAppAction 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/PUAProtection

### Windows10GeneralConfiguration.DefenderPotentiallyUnwantedAppActionSetting 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/PUAProtection

### Windows10GeneralConfiguration.DefenderProcessesToExclude 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ExcludedProcesses

### Windows10GeneralConfiguration.DefenderPromptForSampleSubmission 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/SubmitSamplesConsent

### Windows10GeneralConfiguration.DefenderRequireBehaviorMonitoring 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowBehaviorMonitoring

### Windows10GeneralConfiguration.DefenderRequireCloudProtection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowCloudProtection

### Windows10GeneralConfiguration.DefenderRequireNetworkInspectionSystem 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowIntrusionPreventionSystem

### Windows10GeneralConfiguration.DefenderRequireRealTimeMonitoring 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowRealtimeMonitoring

### Windows10GeneralConfiguration.DefenderScanArchiveFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowArchiveScanning

### Windows10GeneralConfiguration.DefenderScanDownloads 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowIOAVProtection

### Windows10GeneralConfiguration.DefenderScanIncomingMail 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowScanningNetworkFiles

### Windows10GeneralConfiguration.DefenderScanMappedNetworkDrivesDuringFullScan 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowFullScanOnMappedNetworkDrives

### Windows10GeneralConfiguration.DefenderScanMaxCpu 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AvgCPULoadFactor

### Windows10GeneralConfiguration.DefenderScanNetworkFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowScanningNetworkFiles

### Windows10GeneralConfiguration.DefenderScanRemovableDrivesDuringFullScan 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowFullScanRemovableDriveScanning

### Windows10GeneralConfiguration.DefenderScanScriptsLoadedInInternetExplorer 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/AllowScriptScanning

### Windows10GeneralConfiguration.DefenderScanType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ScanParameter

### Windows10GeneralConfiguration.DefenderScheduledQuickScanTime 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ScheduleQuickScanTime

### Windows10GeneralConfiguration.DefenderScheduledScanTime 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ScheduleScanTime

### Windows10GeneralConfiguration.DefenderScheduleScanDay 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ScheduleScanDay

### Windows10GeneralConfiguration.DefenderSignatureUpdateIntervalInHours 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/SignatureUpdateInterval

### Windows10GeneralConfiguration.DefenderSubmitSamplesConsentType 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/SubmitSamplesConsent

### Windows10GeneralConfiguration.DefenderSystemScanSchedule 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Defender/ScheduleScanDay

### Windows10GeneralConfiguration.DeveloperUnlockSetting 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/AllowDeveloperUnlock

### Windows10GeneralConfiguration.DeviceManagementBlockFactoryResetOnMobile 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/System/AllowUserToResetPhone

### Windows10GeneralConfiguration.DeviceManagementBlockManualUnenroll 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowManualMDMUnenrollment

### Windows10GeneralConfiguration.DiagnosticsDataSubmissionMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/System/AllowTelemetry

### Windows10GeneralConfiguration.DisplayAppListWithGdiDPIScalingTurnedOff 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Display/TurnOffGdiDPIScalingForApps

### Windows10GeneralConfiguration.DisplayAppListWithGdiDPIScalingTurnedOn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Display/TurnOnGdiDPIScalingForApps

### Windows10GeneralConfiguration.EdgeAllowStartPagesModification 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/HomePages

### Windows10GeneralConfiguration.EdgeBlockAccessToAboutFlags 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventAccessToAboutFlagsInMicrosoftEdge

### Windows10GeneralConfiguration.EdgeBlockAddressBarDropdown 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowAddressBarDropdown

### Windows10GeneralConfiguration.EdgeBlockAutofill 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowAutofill

### Windows10GeneralConfiguration.EdgeBlockCompatibilityList 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowMicrosoftCompatibilityList

### Windows10GeneralConfiguration.EdgeBlockDeveloperTools 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowDeveloperTools

### Windows10GeneralConfiguration.EdgeBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowBrowser

### Windows10GeneralConfiguration.EdgeBlockEditFavorites 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/LockdownFavorites

### Windows10GeneralConfiguration.EdgeBlockExtensions 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowExtensions

### Windows10GeneralConfiguration.EdgeBlockFullScreenMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowFullScreenMode

### Windows10GeneralConfiguration.EdgeBlockInPrivateBrowsing 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowInPrivate

### Windows10GeneralConfiguration.EdgeBlockLiveTileDataCollection 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventLiveTileDataCollection

### Windows10GeneralConfiguration.EdgeBlockPasswordManager 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowPasswordManager

### Windows10GeneralConfiguration.EdgeBlockPopups 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowPopups

### Windows10GeneralConfiguration.EdgeBlockPrelaunch 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowPrelaunch

### Windows10GeneralConfiguration.EdgeBlockPrinting 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowPrinting

### Windows10GeneralConfiguration.EdgeBlockSavingHistory 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowSavingHistory

### Windows10GeneralConfiguration.EdgeBlockSearchSuggestions 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowSearchSuggestionsinAddressBar

### Windows10GeneralConfiguration.EdgeBlockSendingDoNotTrackHeader 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowDoNotTrack

### Windows10GeneralConfiguration.EdgeBlockSendingIntranetTrafficToInternetExplorer 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SendIntranetTraffictoInternetExplorer

### Windows10GeneralConfiguration.EdgeBlockSideloadingExtensions 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowSideloadingOfExtensions

### Windows10GeneralConfiguration.EdgeBlockTabPreloading 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowTabPreloading

### Windows10GeneralConfiguration.EdgeBlockWebContentOnNewTabPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowWebContentOnNewTabPage

### Windows10GeneralConfiguration.EdgeClearBrowsingDataOnExit 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ClearBrowsingDataOnExit

### Windows10GeneralConfiguration.EdgeCookiePolicy 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowCookies

### Windows10GeneralConfiguration.EdgeDisableFirstRunPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventFirstRunPage

### Windows10GeneralConfiguration.EdgeEnterpriseModeSiteListLocation 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/EnterpriseSiteListServiceUrl

### Windows10GeneralConfiguration.EdgeFavoritesBarVisibility 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ConfigureFavoritesBar

### Windows10GeneralConfiguration.EdgeFavoritesListLocation 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ProvisionFavorites

### Windows10GeneralConfiguration.EdgeFirstRunUrl 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/FirstRunURL

### Windows10GeneralConfiguration.EdgeHomeButtonConfiguration 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SetHomeButtonURL

### Windows10GeneralConfiguration.EdgeHomeButtonConfigurationEnabled 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ConfigureHomeButton

### Windows10GeneralConfiguration.EdgeHomepageUrls 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SetHomeButtonURL

### Windows10GeneralConfiguration.EdgeNewTabPageURL 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SetNewTabPageURL

### Windows10GeneralConfiguration.EdgeOpensWith 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ConfigureOpenMicrosoftEdgeWith

### Windows10GeneralConfiguration.EdgePreventCertificateErrorOverride 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventCertErrorOverrides

### Windows10GeneralConfiguration.EdgeRequireSmartScreen 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/AllowSmartScreen

### Windows10GeneralConfiguration.EdgeSearchEngine 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SetDefaultSearchEngine

### Windows10GeneralConfiguration.EdgeSendIntranetTrafficToInternetExplorer 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SendIntranetTraffictoInternetExplorer

### Windows10GeneralConfiguration.EdgeShowMessageWhenOpeningInternetExplorerSites 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ShowMessageWhenOpeningSitesInInternetExplorer

### Windows10GeneralConfiguration.EdgeSyncFavoritesWithInternetExplorer 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/SyncFavoritesBetweenIEAndMicrosoftEdge

### Windows10GeneralConfiguration.EdgeTelemetryForMicrosoft365Analytics 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ConfigureTelemetryForMicrosoft365Analytics

### Windows10GeneralConfiguration.EnableAutomaticRedeployment 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/CredentialProviders/DisableAutomaticReDeploymentCredentials

### Windows10GeneralConfiguration.EnterpriseCloudPrintDiscoveryEndPoint 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint

### Windows10GeneralConfiguration.EnterpriseCloudPrintDiscoveryMaxLimit 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit

### Windows10GeneralConfiguration.EnterpriseCloudPrintMopriaDiscoveryResourceIdentifier 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId

### Windows10GeneralConfiguration.EnterpriseCloudPrintOAuthAuthority 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority

### Windows10GeneralConfiguration.EnterpriseCloudPrintOAuthClientIdentifier 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority

### Windows10GeneralConfiguration.EnterpriseCloudPrintResourceIdentifier 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/EnterpriseCloudPrint/CloudPrintResourceId

### Windows10GeneralConfiguration.ExperienceBlockConsumerSpecificFeatures 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsConsumerFeatures

### Windows10GeneralConfiguration.ExperienceBlockDeviceDiscovery 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowDeviceDiscovery

### Windows10GeneralConfiguration.ExperienceBlockErrorDialogWhenNoSIM 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowSIMErrorDialogPromptWhenNoSIM

### Windows10GeneralConfiguration.ExperienceBlockTaskSwitcher 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowTaskSwitcher

### Windows10GeneralConfiguration.ExperienceBlockWindowsSpotlight 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsSpotlight

### Windows10GeneralConfiguration.ExperienceDoNotSyncBrowserSettings 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/DoNotSyncBrowserSettings

### Windows10GeneralConfiguration.GameDvrBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/AllowGameDVR

### Windows10GeneralConfiguration.HardwareDeviceInstallationByDeviceIdentifiers 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs

### Windows10GeneralConfiguration.HardwareDeviceInstallationBySetupClasses 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses

### Windows10GeneralConfiguration.InkWorkspaceAccess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsInkWorkspace/AllowWindowsInkWorkspace

### Windows10GeneralConfiguration.InkWorkspaceAccessState 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsInkWorkspace/AllowWindowsInkWorkspace

### Windows10GeneralConfiguration.InkWorkspaceBlockSuggestedApps 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsInkWorkspace/AllowSuggestedAppsInWindowsInkWorkspace

### Windows10GeneralConfiguration.InternetExplorerActiveXControlsInProtectedMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DoNotAllowActiveXControlsInProtectedMode

### Windows10GeneralConfiguration.InternetExplorerAutoComplete 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/AllowAutoComplete

### Windows10GeneralConfiguration.InternetExplorerBlockOutdatedActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DoNotBlockOutdatedActiveXControls

### Windows10GeneralConfiguration.InternetExplorerBypassSmartScreenWarnings 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableBypassOfSmartScreenWarnings

### Windows10GeneralConfiguration.InternetExplorerBypassSmartScreenWarningsAboutUncommonFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableBypassOfSmartScreenWarningsAboutUncommonFiles

### Windows10GeneralConfiguration.InternetExplorerCertificateAddressMismatchWarning 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/AllowCertificateAddressMismatchWarning

### Windows10GeneralConfiguration.InternetExplorerCheckServerCertificateRevocation 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/CheckServerCertificateRevocation

### Windows10GeneralConfiguration.InternetExplorerCheckSignaturesOnDownloadedPrograms 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/CheckSignaturesOnDownloadedPrograms

### Windows10GeneralConfiguration.InternetExplorerCrashDetection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableCrashDetection

### Windows10GeneralConfiguration.InternetExplorerDisableProcessesInEnhancedProtectedMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableProcessesInEnhancedProtectedMode

### Windows10GeneralConfiguration.InternetExplorerDownloadEnclosures 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableEnclosureDownloading

### Windows10GeneralConfiguration.InternetExplorerEncryptionSupport 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableEncryptionSupport

### Windows10GeneralConfiguration.InternetExplorerEnhancedProtectedMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/AllowEnhancedProtectedMode

### Windows10GeneralConfiguration.InternetExplorerFallbackToSsl3 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/AllowFallbackToSSL3

### Windows10GeneralConfiguration.InternetExplorerIgnoreCertificateErrors 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableIgnoringCertificateErrors

### Windows10GeneralConfiguration.InternetExplorerIncludeAllNetworkPaths 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/IncludeAllNetworkPaths

### Windows10GeneralConfiguration.InternetExplorerInternetZoneAccessToDataSources 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowAccessToDataSources

### Windows10GeneralConfiguration.InternetExplorerInternetZoneAllowOnlyApprovedDomainsToUseActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseActiveXControls

### Windows10GeneralConfiguration.InternetExplorerInternetZoneAllowOnlyApprovedDomainsToUseTdcActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl

### Windows10GeneralConfiguration.InternetExplorerInternetZoneAllowVBScriptToRun 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowVBScriptToRunInInternetExplorer

### Windows10GeneralConfiguration.InternetExplorerInternetZoneAutomaticPromptForFileDownloads 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowAutomaticPromptingForFileDownloads

### Windows10GeneralConfiguration.InternetExplorerInternetZoneCopyAndPasteViaScript 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowCopyPasteViaScript

### Windows10GeneralConfiguration.InternetExplorerInternetZoneCrossSiteScriptingFilter 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableCrossSiteScriptingFilter

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneDoNotRunAntimalwareAgainstActiveXControls

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDotNetFrameworkReliantComponents 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowNETFrameworkReliantComponents

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDownloadSignedActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneDownloadSignedActiveXControls

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDownloadUnsignedActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneDownloadUnsignedActiveXControls

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDragAndDropOrCopyAndPasteFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowDragAndDropCopyAndPasteFiles

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDragContentFromDifferentDomainsAcrossWindows 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows

### Windows10GeneralConfiguration.InternetExplorerInternetZoneDragContentFromDifferentDomainsWithinWindows 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows

### Windows10GeneralConfiguration.InternetExplorerInternetZoneIncludeLocalPathWhenUploadingFilesToServer 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneIncludeLocalPathWhenUploadingFilesToServer

### Windows10GeneralConfiguration.InternetExplorerInternetZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneInitializeAndScriptActiveXControls

### Windows10GeneralConfiguration.InternetExplorerInternetZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneJavaPermissions


### Windows10GeneralConfiguration.InternetExplorerInternetZoneLaunchApplicationsAndFilesInAnIFrame 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneLaunchingApplicationsAndFilesInIFRAME

### Windows10GeneralConfiguration.InternetExplorerInternetZoneLessPrivilegedSites 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowLessPrivilegedSites

### Windows10GeneralConfiguration.InternetExplorerInternetZoneLoadingOfXamlFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowLoadingOfXAMLFiles

### Windows10GeneralConfiguration.InternetExplorerInternetZoneLogonOptions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneLogonOptions

### Windows10GeneralConfiguration.InternetExplorerInternetZoneNavigateWindowsAndFramesAcrossDifferentDomains 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneNavigateWindowsAndFrames

### Windows10GeneralConfiguration.InternetExplorerInternetZonePopupBlocker 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneUsePopupBlocker

### Windows10GeneralConfiguration.InternetExplorerInternetZoneProtectedMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneEnableProtectedMode

### Windows10GeneralConfiguration.InternetExplorerInternetZoneRunDotNetFrameworkReliantComponentsSignedWithAuthenticode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode

### Windows10GeneralConfiguration.InternetExplorerInternetZoneScriptingOfWebBrowserControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowScriptingOfInternetExplorerWebBrowserControls

### Windows10GeneralConfiguration.InternetExplorerInternetZoneScriptInitiatedWindows 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowScriptInitiatedWindows

### Windows10GeneralConfiguration.InternetExplorerInternetZoneScriptlets 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowScriptlets

### Windows10GeneralConfiguration.InternetExplorerInternetZoneSecurityWarningForPotentiallyUnsafeFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneShowSecurityWarningForPotentiallyUnsafeFiles

### Windows10GeneralConfiguration.InternetExplorerInternetZoneSmartScreen 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowSmartScreenIE

### Windows10GeneralConfiguration.InternetExplorerInternetZoneUpdatesToStatusBarViaScript 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowUpdatesToStatusBarViaScript

### Windows10GeneralConfiguration.InternetExplorerInternetZoneUserDataPersistence 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/InternetZoneAllowUserDataPersistence

### Windows10GeneralConfiguration.InternetExplorerIntranetZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/IntranetZoneDoNotRunAntimalwareAgainstActiveXControls

### Windows10GeneralConfiguration.InternetExplorerIntranetZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/IntranetZoneInitializeAndScriptActiveXControls

### Windows10GeneralConfiguration.InternetExplorerIntranetZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/IntranetZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerLocalMachineZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LocalMachineZoneDoNotRunAntimalwareAgainstActiveXControls

### Windows10GeneralConfiguration.InternetExplorerLocalMachineZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LocalMachineZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerLockedDownInternetZoneSmartScreen 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LockedDownInternetZoneAllowSmartScreenIE

### Windows10GeneralConfiguration.InternetExplorerLockedDownIntranetZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LockedDownIntranetJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerLockedDownLocalMachineZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LockedDownLocalMachineZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerLockedDownRestrictedZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LockedDownRestrictedSitesZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerLockedDownRestrictedZoneSmartScreen 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LockedDownRestrictedSitesZoneAllowSmartScreenIE

### Windows10GeneralConfiguration.InternetExplorerLockedDownTrustedZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/LockedDownTrustedSitesZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerPreventManagingSmartScreenFilter 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/PreventManagingSmartScreenFilter

### Windows10GeneralConfiguration.InternetExplorerPreventPerUserInstallationOfActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/PreventPerUserInstallationOfActiveXControls

### Windows10GeneralConfiguration.InternetExplorerProcessesConsistentMimeHandling 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/ConsistentMimeHandlingInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesMimeSniffingSafetyFeature 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/MimeSniffingSafetyFeatureInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesMKProtocolSecurityRestriction 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/MKProtocolSecurityRestrictionInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesNotificationBar 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/NotificationBarInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesProtectionFromZoneElevation 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/ProtectionFromZoneElevationInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesRestrictActiveXInstall 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictActiveXInstallInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesRestrictFileDownload 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictFileDownloadInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerProcessesScriptedWindowSecurityRestrictions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/ScriptedWindowSecurityRestrictionsInternetExplorerProcesses

### Windows10GeneralConfiguration.InternetExplorerRemoveRunThisTimeButtonForOutdatedActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RemoveRunThisTimeButtonForOutdatedActiveXControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAccessToDataSources 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowAccessToDataSources

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneActiveScripting 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowActiveScripting

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAllowOnlyApprovedDomainsToUseActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseActiveXControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAllowOnlyApprovedDomainsToUseTdcActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAllowVBScriptToRun 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowVBScriptToRunInInternetExplorer

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneAutomaticPromptForFileDownloads 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowAutomaticPromptingForFileDownloads

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneBinaryAndScriptBehaviors 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowBinaryAndScriptBehaviors

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneCopyAndPasteViaScript 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowCopyPasteViaScript

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneCrossSiteScriptingFilter 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneEnableCrossSiteScriptingFilter

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneDoNotRunAntimalwareAgainstActiveXControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDotNetFrameworkReliantComponents 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowNETFrameworkReliantComponents

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDownloadSignedActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneDownloadSignedActiveXControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDownloadUnsignedActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneDownloadUnsignedActiveXControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDragAndDropOrCopyAndPasteFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowDragAndDropCopyAndPasteFiles

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDragContentFromDifferentDomainsAcrossWindows 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneDragContentFromDifferentDomainsWithinWindows 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneFileDownloads 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowFileDownloads

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneIncludeLocalPathWhenUploadingFilesToServer 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneIncludeLocalPathWhenUploadingFilesToServer

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneInitializeAndScriptActiveXControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLaunchApplicationsAndFilesInAnIFrame 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneLaunchingApplicationsAndFilesInIFRAME

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLessPrivilegedSites 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowLessPrivilegedSites

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLoadingOfXamlFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowLoadingOfXAMLFiles

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneLogonOptions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneLogonOptions

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneMetaRefresh 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowMETAREFRESH

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneNavigateWindowsAndFramesAcrossDifferentDomains 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneNavigateWindowsAndFrames

### Windows10GeneralConfiguration.InternetExplorerRestrictedZonePopupBlocker 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneUsePopupBlocker

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneProtectedMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneTurnOnProtectedMode

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneRunActiveXControlsAndPlugins 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneRunActiveXControlsAndPlugins

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneRunDotNetFrameworkReliantComponentsSignedWithAuthenticode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptActiveXControlsMarkedSafeForScripting 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneScriptActiveXControlsMarkedSafeForScripting

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptingOfJavaApplets 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneScriptingOfJavaApplets

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptingOfWebBrowserControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowScriptingOfInternetExplorerWebBrowserControls

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptInitiatedWindows 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowScriptInitiatedWindows

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneScriptlets 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowScriptlets

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneSecurityWarningForPotentiallyUnsafeFiles 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneShowSecurityWarningForPotentiallyUnsafeFiles

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneSmartScreen 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowSmartScreenIE

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneUpdatesToStatusBarViaScript 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowUpdatesToStatusBarViaScript

### Windows10GeneralConfiguration.InternetExplorerRestrictedZoneUserDataPersistence 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/RestrictedSitesZoneAllowUserDataPersistence

### Windows10GeneralConfiguration.InternetExplorerSecuritySettingsCheck 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DisableSecuritySettingsCheck

### Windows10GeneralConfiguration.InternetExplorerSecurityZonesUseOnlyMachineSettings 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/SecurityZonesUseOnlyMachineSettings

### Windows10GeneralConfiguration.InternetExplorerSoftwareWhenSignatureIsInvalid 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/AllowSoftwareWhenSignatureIsInvalid

### Windows10GeneralConfiguration.InternetExplorerTrustedZoneDoNotRunAntimalwareAgainstActiveXControls 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/TrustedSitesZoneDoNotRunAntimalwareAgainstActiveXControls

### Windows10GeneralConfiguration.InternetExplorerTrustedZoneInitializeAndScriptActiveXControlsNotMarkedAsSafe 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/TrustedSitesZoneInitializeAndScriptActiveXControls

### Windows10GeneralConfiguration.InternetExplorerTrustedZoneJavaPermissions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/TrustedSitesZoneJavaPermissions

### Windows10GeneralConfiguration.InternetExplorerUseActiveXInstallerService 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/SpecifyUseOfActiveXInstallerService

### Windows10GeneralConfiguration.InternetExplorerUsersAddingSites 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DoNotAllowUsersToAddSites

### Windows10GeneralConfiguration.InternetExplorerUsersChangingPolicies 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/InternetExplorer/DoNotAllowUsersToChangePolicies

### Windows10GeneralConfiguration.InternetSharingBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WiFi/AllowInternetSharing

### Windows10GeneralConfiguration.LocationServicesBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/System/AllowLocation

### Windows10GeneralConfiguration.LockScreenAllowTimeoutConfiguration 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/AllowScreenTimeoutWhileLockedUser/Config

### Windows10GeneralConfiguration.LockScreenBlockActionCenterNotifications 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/AboveLock/AllowActionCenterNotifications

### Windows10GeneralConfiguration.LockScreenBlockCortana 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/AboveLock/AllowCortanaAboveLock

### Windows10GeneralConfiguration.LockScreenBlockToastNotifications 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/AboveLock/AllowToasts

### Windows10GeneralConfiguration.LockScreenCamera 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/PreventEnablingLockScreenCamera

### Windows10GeneralConfiguration.LockScreenHideNetworkSelectionUI 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsLogon/DontDisplayNetworkSelectionUI

### Windows10GeneralConfiguration.LockScreenSlideShow 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/PreventLockScreenSlideShow

### Windows10GeneralConfiguration.LockScreenTimeoutInSeconds 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/ScreenTimeoutWhileLocked

### Windows10GeneralConfiguration.LogonBlockFastUserSwitching 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsLogon/HideFastUserSwitching

### Windows10GeneralConfiguration.MessagingBlockMMS 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Messaging/AllowMMS

### Windows10GeneralConfiguration.MessagingBlockRichCommunicationServices 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Messaging/AllowRCS

### Windows10GeneralConfiguration.MessagingBlockSync 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Messaging/AllowMessageSync

### Windows10GeneralConfiguration.MicrosoftAccountBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Accounts/AllowMicrosoftAccountConnection

### Windows10GeneralConfiguration.MicrosoftAccountBlockSettingsSync 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowSyncMySettings

### Windows10GeneralConfiguration.MicrosoftAccountSignInAssistantSettings 
**CSP**: ./Device/Vendor/MSFT/Accounts  
**Offset URI**: /AllowMicrosoftAccountSignInAssistant

### Windows10GeneralConfiguration.NetworkProxyApplySettingsDeviceWide 
**CSP**: ./Device/Vendor/MSFT/NetworkProxy  
**Offset URI**: /ProxySettingsPerUser

### Windows10GeneralConfiguration.NetworkProxyAutomaticConfigurationUrl 
**CSP**: ./Device/Vendor/MSFT/NetworkProxy  
**Offset URI**: /SetupScriptUrl

### Windows10GeneralConfiguration.NetworkProxyDisableAutoDetect 
**CSP**: ./Device/Vendor/MSFT/NetworkProxy  
**Offset URI**: /AutoDetect

### Windows10GeneralConfiguration.NetworkProxyServer 
**CSP**: ./Vendor/MSFT/NetworkProxy  
**Offset URI**: /ProxyAddress, /Exceptions and /UseProxyForLocalAddresses

### Windows10GeneralConfiguration.NfcBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowNFC

### Windows10GeneralConfiguration.OneDriveDisableFileSync 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/System/DisableOneDriveFileSync

### Windows10GeneralConfiguration.PasswordBlockSimple 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/AllowSimpleDevicePassword

### Windows10GeneralConfiguration.PasswordExpirationDays 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/DevicePasswordExpiration

### Windows10GeneralConfiguration.PasswordMinimumAgeInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/MinimumPasswordAge

### Windows10GeneralConfiguration.PasswordMinimumCharacterSetCount 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/MinDevicePasswordComplexCharacters

### Windows10GeneralConfiguration.PasswordMinimumLength 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/MinDevicePasswordLength

### Windows10GeneralConfiguration.PasswordMinutesOfInactivityBeforeScreenTimeout 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/MaxInactivityTimeDeviceLock

### Windows10GeneralConfiguration.PasswordPreviousPasswordBlockCount 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/DevicePasswordHistory

### Windows10GeneralConfiguration.PasswordRequired 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/DevicePasswordEnabled

### Windows10GeneralConfiguration.PasswordRequiredType 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/AlphanumericDevicePasswordRequired

### Windows10GeneralConfiguration.PasswordRequireWhenResumeFromIdleState 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/AllowIdleReturnWithoutPassword

### Windows10GeneralConfiguration.PasswordSignInFailureCountBeforeFactoryReset 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceLock/MaxDevicePasswordFailedAttempts

### Windows10GeneralConfiguration.PersonalizationDesktopImageUrl 
**CSP**: ./Device/Vendor/MSFT/Personalization  
**Offset URI**: /DesktopImageUrl

### Windows10GeneralConfiguration.PersonalizationLockScreenImageUrl 
**CSP**: ./Device/Vendor/MSFT/Personalization  
**Offset URI**: /LockScreenImageUrl

### Windows10GeneralConfiguration.PowerRequirePasswordOnWakeWhileOnBattery 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Power/RequirePasswordWhenComputerWakesOnBattery

### Windows10GeneralConfiguration.PowerRequirePasswordOnWakeWhilePluggedIn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Power/RequirePasswordWhenComputerWakesPluggedIn

### Windows10GeneralConfiguration.PowerStandbyStatesWhenSleepingWhileOnBattery 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Power/AllowStandbyStatesWhenSleepingOnBattery

### Windows10GeneralConfiguration.PowerStandbyStatesWhenSleepingWhilePluggedIn 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Power/AllowStandbyWhenSleepingPluggedIn

### windows10generalconfiguration.preventInstallationOfMatchingDeviceIDs 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceIDs

### windows10generalconfiguration.preventInstallationOfMatchingDeviceSetupClasses 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeviceInstallation/PreventInstallationOfMatchingDeviceSetupClasses

### Windows10GeneralConfiguration.PrinterBlockAddition 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Education/PreventAddingNewPrinters

### Windows10GeneralConfiguration.PrinterDefaultName 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Education/DefaultPrinterName

### Windows10GeneralConfiguration.PrinterNames 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Education/PrinterNames

### Windows10GeneralConfiguration.PrivacyAdvertisingId 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Privacy/DisableAdvertisingID

### Windows10GeneralConfiguration.PrivacyAutoAcceptPairingAndConsentPrompts 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts

### Windows10GeneralConfiguration.PrivacyBlockActivityFeed 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Privacy/EnableActivityFeed

### Windows10GeneralConfiguration.PrivacyBlockInputPersonalization 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Privacy/AllowInputPersonalization

### Windows10GeneralConfiguration.PrivacyBlockPublishUserActivities 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Privacy/PublishUserActivities

### Windows10GeneralConfiguration.SafeSearchFilter 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/SafeSearchPermissions

### Windows10GeneralConfiguration.ScreenCaptureBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowScreenCapture

### Windows10GeneralConfiguration.SearchBlockDiacritics 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/AllowUsingDiacritics

### Windows10GeneralConfiguration.SearchBlockWebResults 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/DoNotUseWebResults

### Windows10GeneralConfiguration.SearchDisableAutoLanguageDetection 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/AlwaysUseAutoLangDetection

### Windows10GeneralConfiguration.SearchDisableIndexerBackoff 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/DisableBackoff

### Windows10GeneralConfiguration.SearchDisableIndexingEncryptedItems 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/AllowIndexingEncryptedStoresOrItems

### Windows10GeneralConfiguration.SearchDisableIndexingRemovableDrive 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/DisableRemovableDriveIndexing

### Windows10GeneralConfiguration.SearchDisableLocation 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/AllowSearchToUseLocation

### Windows10GeneralConfiguration.SearchDisableUseLocation 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/AllowSearchToUseLocation

### Windows10GeneralConfiguration.SearchEnableAutomaticIndexSizeManangement 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/PreventIndexingLowDiskSpaceMB

### Windows10GeneralConfiguration.SearchEnableRemoteQueries 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Search/PreventRemoteQueries

### Windows10GeneralConfiguration.SecurityBlockAzureADJoinedDevicesAutoEncryption 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices

### Windows10GeneralConfiguration.SettingsBlockAccountsPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockAddProvisioningPackage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Security/AllowAddProvisioningPackage

### Windows10GeneralConfiguration.SettingsBlockAppsPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockChangeLanguage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/AllowLanguage

### Windows10GeneralConfiguration.SettingsBlockChangePowerSleep 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/AllowPowerSleep

### Windows10GeneralConfiguration.SettingsBlockChangeRegion 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/AllowRegion

### Windows10GeneralConfiguration.SettingsBlockChangeSystemTime 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/AllowDateTime

### Windows10GeneralConfiguration.SettingsBlockDevicesPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockEaseOfAccessPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockEditDeviceName 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/AllowEditDeviceName

### Windows10GeneralConfiguration.SettingsBlockGamingPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockNetworkInternetPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockPersonalizationPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockPrivacyPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockRemoveProvisioningPackage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Security/AllowRemoveProvisioningPackage

### Windows10GeneralConfiguration.SettingsBlockSystemPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockTimeLanguagePage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SettingsBlockUpdateSecurityPage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Settings/PageVisibilityList

### Windows10GeneralConfiguration.SharedUserAppDataAllowed 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/AllowSharedUserAppData

### Windows10GeneralConfiguration.SmartScreenBlockPromptOverride 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventSmartScreenPromptOverride

### Windows10GeneralConfiguration.SmartScreenBlockPromptOverrideForFiles 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventSmartScreenPromptOverrideForFiles

### Windows10GeneralConfiguration.SmartScreenEnableAppInstallControl 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/SmartScreen/EnableAppInstallControl

### Windows10GeneralConfiguration.StartBlockUnpinningAppsFromTaskbar 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/NoPinningToTaskbar

### Windows10GeneralConfiguration.StartMenuAppListVisibility 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideAppList

### Windows10GeneralConfiguration.StartMenuHideChangeAccountSettings 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideChangeAccountSettings

### Windows10GeneralConfiguration.StartMenuHideFrequentlyUsedApps 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideFrequentlyUsedApps

### Windows10GeneralConfiguration.StartMenuHideHibernate 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideHibernate

### Windows10GeneralConfiguration.StartMenuHideLock 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideLock

### Windows10GeneralConfiguration.StartMenuHidePowerButton 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HidePowerButton

### Windows10GeneralConfiguration.StartMenuHideRecentJumpLists 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideRecentJumplists

### Windows10GeneralConfiguration.StartMenuHideRecentlyAddedApps 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideRecentlyAddedApps

### Windows10GeneralConfiguration.StartMenuHideRestartOptions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideRestart

### Windows10GeneralConfiguration.StartMenuHideShutDown 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideShutDown

### Windows10GeneralConfiguration.StartMenuHideSignOut 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideSignOut

### Windows10GeneralConfiguration.StartMenuHideSleep 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideSleep

### Windows10GeneralConfiguration.StartMenuHideSwitchAccount 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideSwitchAccount

### Windows10GeneralConfiguration.StartMenuHideUserTile 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/HideUserTile

### Windows10GeneralConfiguration.StartMenuLayoutEdgeAssetsXml 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/ImportEdgeAssets

### Windows10GeneralConfiguration.StartMenuLayoutXml 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/StartLayout

### Windows10GeneralConfiguration.StartMenuMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/ForceStartSize

### Windows10GeneralConfiguration.StartMenuPinnedFolderDocuments 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderDocuments

### Windows10GeneralConfiguration.StartMenuPinnedFolderDownloads 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderDownloads

### Windows10GeneralConfiguration.StartMenuPinnedFolderFileExplorer 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderFileExplorer

### Windows10GeneralConfiguration.StartMenuPinnedFolderHomeGroup 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderHomeGroup

### Windows10GeneralConfiguration.StartMenuPinnedFolderMusic 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderMusic

### Windows10GeneralConfiguration.StartMenuPinnedFolderNetwork 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderNetwork

### Windows10GeneralConfiguration.StartMenuPinnedFolderPersonalFolder 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderPersonalFolder

### Windows10GeneralConfiguration.StartMenuPinnedFolderPictures 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderPictures

### Windows10GeneralConfiguration.StartMenuPinnedFolderSettings 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderSettings

### Windows10GeneralConfiguration.StartMenuPinnedFolderVideos 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Start/AllowPinnedFolderVideos

### Windows10GeneralConfiguration.StorageBlockRemovableStorage 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/System/AllowStorageCard

### Windows10GeneralConfiguration.StorageRequireMobileDeviceEncryption 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Security/RequireDeviceEncryption

### Windows10GeneralConfiguration.StorageRestrictAppDataToSystemVolume 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/RestrictAppDataToSystemVolume

### Windows10GeneralConfiguration.StorageRestrictAppInstallToSystemVolume 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/RestrictAppToSystemVolume

### Windows10GeneralConfiguration.SystemBootStartDriverInitialization 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/System/BootStartDriverInitialization

### Windows10GeneralConfiguration.SystemTelemetryProxyServer 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/System/TelemetryProxy

### Windows10GeneralConfiguration.TaskManagerBlockEndTask 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/TaskManager/AllowEndTask

### Windows10GeneralConfiguration.TenantLockdownRequireNetworkDuringOutOfBoxExperience 
**CSP**: ./Vendor/MSFT/TenantLockdown  
**Offset URI**: /RequireNetworkInOOBE

### Windows10GeneralConfiguration.UsbBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Connectivity/AllowUSBConnection

### Windows10GeneralConfiguration.VoiceRecordingBlocked 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowVoiceRecording

### Windows10GeneralConfiguration.WebRtcBlockLocalhostIpAddress 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/PreventUsingLocalHostIPAddressForWebRTC

### Windows10GeneralConfiguration.WiFiBlockAutomaticConnectHotspots 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WiFi/AllowAutoConnectToWiFiSenseHotspots

### Windows10GeneralConfiguration.WiFiBlocked 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Wifi/AllowWiFi

### Windows10GeneralConfiguration.WiFiBlockManualConfiguration 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WiFi/AllowManualWiFi/Configuration

### Windows10GeneralConfiguration.WiFiScanInterval 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WiFi/WLANScanMode

### Windows10GeneralConfiguration.WindowsLogOnLocalUsersOnDomainJoinedComputers 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/WindowsLogon/EnumerateLocalUsersOnDomainJoinedComputers

### Windows10GeneralConfiguration.WindowsSpotlightBlockConsumerSpecificFeatures 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsConsumerFeatures

### Windows10GeneralConfiguration.WindowsSpotlightBlocked 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsSpotlight

### Windows10GeneralConfiguration.WindowsSpotlightBlockOnActionCenter 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsSpotlightOnActionCenter

### Windows10GeneralConfiguration.WindowsSpotlightBlockTailoredExperiences 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowTailoredExperiencesWithDiagnosticData

### Windows10GeneralConfiguration.WindowsSpotlightBlockThirdPartyNotifications 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowThirdPartySuggestionsInWindowsSpotlight

### Windows10GeneralConfiguration.WindowsSpotlightBlockWelcomeExperience 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsSpotlightWindowsWelcomeExperience

### Windows10GeneralConfiguration.WindowsSpotlightBlockWindowsTips 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/AllowWindowsTips

### Windows10GeneralConfiguration.WindowsSpotlightConfigureOnLockScreen 
**CSP**: ./User/Vendor/MSFT/Policy  
**Offset URI**: /Config/Experience/ConfigureWindowsSpotlightOnLockScreen

### Windows10GeneralConfiguration.WindowsStoreBlockAutoUpdate 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/AllowAppStoreAutoUpdate

### Windows10GeneralConfiguration.WindowsStoreBlocked 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/AllowStore

### Windows10GeneralConfiguration.WindowsStoreEnablePrivateStoreOnly 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/ApplicationManagement/RequirePrivateStoreOnly

### Windows10GeneralConfiguration.WirelessDisplayBlockProjectionToThisDevice 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WirelessDisplay/AllowProjectionToPC

### Windows10GeneralConfiguration.WirelessDisplayBlockUserInputFromReceiver 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver

### Windows10GeneralConfiguration.WirelessDisplayRequirePinForPairing 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/WirelessDisplay/RequirePINForPairing

### Windows10NetworkBoundaryConfiguration.WindowsNetworkIsolationPolicy 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/NetworkIsolation/EnterpriseCloudResources, /Config/NetworkIsolation/EnterpriseIPRange, /Config/NetworkIsolation/EnterpriseIPRangesAreAuthoritative, /Config/NetworkIsolation/EnterpriseInternalProxyServers, /Config/NetworkIsolation/EnterpriseNetworkDomainNames, /Config/NetworkIsolation/EnterpriseProxyServers, /Config/NetworkIsolation/EnterpriseProxyServersAreAuthoritative, /Config/NetworkIsolation/NeutralResources

### Windows10PolicyOverrideConfiguration.PreferMdmOverGroupPolicy 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/ControlPolicyConflict/MDMWinsOverGP

### Windows10SecureAssessmentConfiguration.AllowPrinting 
**CSP**: ./Vendor/MSFT/SecureAssessment  
**Offset URI**: /RequirePrinting

### Windows10SecureAssessmentConfiguration.AllowScreenCapture 
**CSP**: ./Vendor/MSFT/SecureAssessment  
**Offset URI**: /AllowScreenMonitoring

### Windows10SecureAssessmentConfiguration.AllowTextSuggestion 
**CSP**: ./Vendor/MSFT/SecureAssessment  
**Offset URI**: /AllowTextSuggestions

### Windows10SecureAssessmentConfiguration.ConfigurationAccount 
**CSP**: ./Vendor/MSFT/SecureAssessment  
**Offset URI**: /TesterAccount

### Windows10SecureAssessmentConfiguration.ConfigurationAccountType 
**CSP**: ./Vendor/MSFT/SecureAssessment  
**Offset URI**: /TesterAccount

### Windows10SecureAssessmentConfiguration.LaunchUri 
**CSP**: ./Vendor/MSFT/SecureAssessment  
**Offset URI**: /LaunchURI

### Windows10TeamGeneralConfiguration.AzureOperationalInsightsBlockTelemetry 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /MOMAgent/WorkspaceID and /MOMAgent/WorkspaceKey

### Windows10TeamGeneralConfiguration.AzureOperationalInsightsWorkspaceId 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /MOMAgent/WorkspaceID

### Windows10TeamGeneralConfiguration.AzureOperationalInsightsWorkspaceKey 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /MOMAgent/WorkspaceKey

### Windows10TeamGeneralConfiguration.ConnectAppBlockAutoLaunch 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/Connect/AutoLaunch

### Windows10TeamGeneralConfiguration.DeviceAccountBlockExchangeServices 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /DeviceAccount/Email

### Windows10TeamGeneralConfiguration.DeviceAccountEmailAddress 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /DeviceAccount/Email

### Windows10TeamGeneralConfiguration.DeviceAccountExchangeServerAddress 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /DeviceAccount/ExchangeServer

### Windows10TeamGeneralConfiguration.DeviceAccountRequirePasswordRotation 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /DeviceAccount/PasswordRotationEnabled

### Windows10TeamGeneralConfiguration.DeviceAccountSessionInitiationProtocolAddress 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /DeviceAccount/SipAddress

### Windows10TeamGeneralConfiguration.MaintenanceWindowBlocked 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /MaintenanceHoursSimple/Hours/Duration and /MaintenanceHoursSimple/Hours/StartTime

### Windows10TeamGeneralConfiguration.MaintenanceWindowDurationInHours 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /MaintenanceHoursSimple/Hours/Duration

### Windows10TeamGeneralConfiguration.MaintenanceWindowStartTime 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /MaintenanceHoursSimple/Hours/StartTime

### Windows10TeamGeneralConfiguration.MiracastBlocked 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/WirelessProjection/Enabled

### Windows10TeamGeneralConfiguration.MiracastChannel 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/WirelessProjection/Channel

### Windows10TeamGeneralConfiguration.MiracastRequirePin 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/WirelessProjection/PINRequired

### Windows10TeamGeneralConfiguration.SettingsBlockMyMeetingsAndFiles 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/DoNotShowMyMeetingsAndFiles

### Windows10TeamGeneralConfiguration.SettingsBlockSessionResume 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/AllowSessionResume

### Windows10TeamGeneralConfiguration.SettingsBlockSigninSuggestions 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/DisableSigninSuggestions

### Windows10TeamGeneralConfiguration.SettingsDefaultVolume 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/DefaultVolume

### Windows10TeamGeneralConfiguration.SettingsScreenTimeoutInMinutes 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/ScreenTimeout

### Windows10TeamGeneralConfiguration.SettingsSessionTimeoutInMinutes 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/SessionTimeout

### Windows10TeamGeneralConfiguration.SettingsSleepTimeoutInMinutes 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /Properties/SleepTimeout

### Windows10TeamGeneralConfiguration.WelcomeScreenBackgroundImageUrl 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/Welcome/CurrentBackgroundPath

### Windows10TeamGeneralConfiguration.WelcomeScreenBlockAutomaticWakeUp 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/Welcome/AutoWakeScreen

### Windows10TeamGeneralConfiguration.WelcomeScreenMeetingInformation 
**CSP**: ./Vendor/MSFT/SurfaceHub  
**Offset URI**: /InBoxApps/Welcome/MeetingInfoOption

### WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOffboardingBlob 
**CSP**: ./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Offboarding 

### WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOffboardingFilename
**CSP**: ./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Offboarding 

### WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOnboardingBlob 
**CSP**: ./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Onboarding 

### WindowsDefenderAdvancedThreatProtectionConfiguration.AdvancedThreatProtectionOnboardingFilename 
**CSP**: ./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Onboarding 

### WindowsDefenderAdvancedThreatProtectionConfiguration.AllowSampleSharing 
**CSP**: ./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Configuration/SampleSharing

### WindowsDefenderAdvancedThreatProtectionConfiguration.EnableExpeditedTelemetryReporting 
**CSP**: ./Device/Vendor/MSFT/WindowsAdvancedThreatProtection  
**Offset URI**: /Configuration/TelemetryReportingFrequency

### WindowsDeliveryOptimizationConfiguration.DeliveryOptimizationMode 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/DeliveryOptimization/DODownloadMode

### WindowsIdentityProtectionConfiguration.EnhancedAntiSpoofingForFacialFeaturesEnabled 
**CSP**: ./Device/Vendor/MSFT/PassportForWork  
**Offset URI**: /Biometrics/FacialFeaturesUseEnhancedAntiSpoofing

### WindowsIdentityProtectionConfiguration.PinExpirationInDays 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/Expiration

### WindowsIdentityProtectionConfiguration.PinLowercaseCharactersUsage 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/LowercaseLetters

### WindowsIdentityProtectionConfiguration.PinMaximumLength 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/MaximumPINLength

### WindowsIdentityProtectionConfiguration.PinMinimumLength 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/MinimumPINLength

### WindowsIdentityProtectionConfiguration.PinPreviousBlockCount 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/History

### WindowsIdentityProtectionConfiguration.PinRecoveryEnabled 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/EnablePinRecovery

### WindowsIdentityProtectionConfiguration.PinSpecialCharactersUsage 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/SpecialCharacters

### WindowsIdentityProtectionConfiguration.PinUppercaseCharactersUsage
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/PINComplexity/UppercaseLetters

### WindowsIdentityProtectionConfiguration.SecurityDeviceRequired 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/RequireSecurityDevice

### WindowsIdentityProtectionConfiguration.UnlockWithBiometricsEnabled 
**CSP**: ./Device/Vendor/MSFT/PassportForWork  
**Offset URI**: /Biometrics/UseBiometrics

### WindowsIdentityProtectionConfiguration.UseCertificatesForOnPremisesAuthEnabled 
**CSP**: ./Device/Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/UseCertificateForOnPremAuth

### WindowsIdentityProtectionConfiguration.WindowsHelloForBusinessBlocked 
**CSP**: ./Vendor/MSFT/PassportForWork  
**Offset URI**: /{AADTenantId}/Policies/UsePassportForWork

### WindowsKioskConfiguration.EdgeKioskEnablePublicBrowsing 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ConfigureKioskMode

### WindowsKioskConfiguration.EdgeKioskResetAfterIdleTimeInMinutes 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Browser/ConfigureKioskResetAfterIdleTimeout

### WindowsKioskConfiguration.KioskBrowserBlockedUrlExceptions 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/BlockedUrlExceptions

### WindowsKioskConfiguration.KioskBrowserBlockedURLs 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/BlockedUrls

### WindowsKioskConfiguration.KioskBrowserDefaultUrl 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/DefaultUrl

### WindowsKioskConfiguration.KioskBrowserEnableEndSessionButton 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/EnableEndSessionButton

### WindowsKioskConfiguration.KioskBrowserEnableHomeButton 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/EnableHomeButton

### WindowsKioskConfiguration.KioskBrowserEnableNavigationButtons 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/EnableNavigationButtons

### WindowsKioskConfiguration.KioskBrowserRestartOnIdleTimeInMinutes 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/KioskBrowser/KioskBrowserRestartOnIdleTimeInMinutes

### WindowsUpdateForBusinessConfiguration.AutomaticUpdateMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/AllowAutoUpdate

### WindowsUpdateForBusinessConfiguration.AutoRestartNotificationDismissal 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/AutoRestartRequiredNotificationDismissal

### WindowsUpdateForBusinessConfiguration.BusinessReadyUpdatesOnly 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/BranchReadinessLevel

### WindowsUpdateForBusinessConfiguration.DeliveryOptimizationMode 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/DeliveryOptimization/DODownloadMode

### WindowsUpdateForBusinessConfiguration.DriversExcluded 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/ExcludeWUDriversInQualityUpdate

### WindowsUpdateForBusinessConfiguration.EngagedRestartDeadlineForFeatureUpdatesInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/EngagedRestartDeadlineForFeatureUpdates

### WindowsUpdateForBusinessConfiguration.EngagedRestartDeadlineInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/EngagedRestartDeadline

### WindowsUpdateForBusinessConfiguration.EngagedRestartSnoozeScheduleForFeatureUpdatesInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/EngagedRestartSnoozeScheduleForFeatureUpdates

### WindowsUpdateForBusinessConfiguration.EngagedRestartSnoozeScheduleInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/EngagedRestartSnoozeSchedule

### WindowsUpdateForBusinessConfiguration.EngagedRestartTransitionScheduleForFeatureUpdatesInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/EngagedRestartTransitionScheduleForFeatureUpdates

### WindowsUpdateForBusinessConfiguration.EngagedRestartTransitionScheduleInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/EngagedRestartTransitionSchedule

### WindowsUpdateForBusinessConfiguration.FeatureUpdatesDeferralPeriodInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/DeferFeatureUpdatesPeriodInDays

### WindowsUpdateForBusinessConfiguration.FeatureUpdatesPaused 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/PauseFeatureUpdates

### WindowsUpdateForBusinessConfiguration.FeatureUpdatesPauseStartDateTime 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/PauseFeatureUpdatesStartTime

### WindowsUpdateForBusinessConfiguration.FeatureUpdatesRollbackStartDateTime
**CSP**: N/A - Graph API only 
**Offset URI**: N/A - Graph API only

### WindowsUpdateForBusinessConfiguration.FeatureUpdatesWillBeRolledBack 
**CSP**: N/A - Graph API only 
**Offset URI**: N/A - Graph API only

### WindowsUpdateForBusinessConfiguration.FeatureUpdatesRollbackWindowInDays
**CSP**: N/A - Graph API only 
**Offset URI**: N/A - Graph API only

### WindowsUpdateForBusinessConfiguration.InstallationSchedule
**CSP**: ./Device/Vendor/MSFT/Policy
**Offset URI**: /Config/Update/ActiveHoursStart, /Config/Update/ActiveHoursEnd, /Config/Update/ScheduledInstallDay,  /Config/Update/ScheduledInstallTime

### WindowsUpdateForBusinessConfiguration.MicrosoftUpdateServiceAllowed 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/AllowMUUpdateService

### WindowsUpdateForBusinessConfiguration.PreviewBuildSetting 
**CSP**: ./Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/ManagePreviewBuilds

### WindowsUpdateForBusinessConfiguration.QualityUpdatesDeferralPeriodInDays 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/DeferQualityUpdatesPeriodInDays

### WindowsUpdateForBusinessConfiguration.QualityUpdatesPaused 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/PauseQualityUpdates

### WindowsUpdateForBusinessConfiguration.QualityUpdatesPauseStartDateTime 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/PauseQualityUpdatesStartTime

### WindowsUpdateForBusinessConfiguration.QualityUpdatesRollbackStartDateTime
**CSP**: N/A - Graph API only 
**Offset URI**: N/A - Graph API only

### WindowsUpdateForBusinessConfiguration.QualityUpdatesWillBeRolledBack 
**CSP**: N/A - Graph API only 
**Offset URI**: N/A - Graph API only

### WindowsUpdateForBusinessConfiguration.ScheduleImminentRestartWarningInMinutes 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/ScheduleImminentRestartWarning

### WindowsUpdateForBusinessConfiguration.ScheduleRestartWarningInHours 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/ScheduleRestartWarning

### WindowsUpdateForBusinessConfiguration.SkipChecksBeforeRestart 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/SetEDURestart

### WindowsUpdateForBusinessConfiguration.UpdateWeeks 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/ScheduledInstallEveryWeek, /Config/Update/ScheduledInstallFirstWeek, /Config/Update/ScheduledInstallFourthWeek, /Config/Update/ScheduledInstallSecondWeek, /Config/Update/ScheduledInstallThirdWeek

### WindowsUpdateForBusinessConfiguration.UserPauseAccess 
**CSP**: ./Device/Vendor/MSFT/Policy  
**Offset URI**: /Config/Update/SetDisablePauseUXAccess


## Next steps

- [Device configuration overview](../configuration/device-profiles.md)
- [configuration service provider reference](/windows/client-management/mdm/configuration-service-provider-reference) (opens another Docs site)