---
title: Task sequence variable reference
titleSuffix: Configuration Manager
description: Learn about the variables to control and customize a Configuration Manager task sequence.
ms.date: 04/08/2022
ms.service: configuration-manager
ms.subservice: osd
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Task sequence variables

*Applies to: Configuration Manager (current branch)*

This article is a reference for all of the available variables in alphabetical order. Use the browser **Find** function (typically **CTRL** + **F**) to find a specific variable. The variable notes if it's specific to particular step. The article on [task sequence steps](task-sequence-steps.md) includes the list of variables specific to each step.

For more information, see [Using task sequence variables](using-task-sequence-variables.md).

## <a name="bkmk_tsvar"></a> Task sequence variable reference

### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

The task sequence scans the computer's hard drives for a previous operating system installation when Windows PE starts. The Windows folder location is stored in this variable. You can configure your task sequence to retrieve this value from the environment and use it to specify the same Windows folder location to use for the new operating system installation.

### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

The task sequence scans the computer's hard drives for a previous operating system installation when Windows PE starts. The hard drive location for where the operating system is installed is stored in this variable. You can configure your task sequence to retrieve this value from the environment and use it to specify the same hard drive location to use for the new operating system.

### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Applies to the [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState) step.*

(input)

Specifies the package ID of the Configuration Manager package that contains the USMT files. This variable is required.

### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Applies to the [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState) step.*

(input)

Specifies the package ID of the Configuration Manager package that contains the USMT files. This variable is required.

### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Stores the current running task sequence deployment unique ID. It uses the same format as a Configuration Manager software distribution deployment ID. If the task sequence is running from stand-alone media, this variable is undefined.

#### Example

`ABC20001`

### <a name="SMSTSAppInstallNeeds"></a> _SMSTSAppInstallNeedsRetry

Starting this Configuration Manager 2211 HFRU Kb 16643863 and above

*Applies to the [Install Application](task-sequence-steps.md#BKMK_InstallApplication) step.*

This value is set to true if the previous application failed to install and is required to be retried.

This value is set to false otherwise.

### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the asset tag for the computer.

### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

If the current running task sequence references a boot image package, this variable stores the boot image package ID. If the task sequence doesn't reference a boot image package, this variable isn't set.

#### Example

`ABC00001`  

### <a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

The task sequence sets this variable when it detects a computer that's in UEFI mode.

### <a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
The task sequence sets this variable when it caches content on the local drive. The variable contains the path to the cache. If this variable doesn't exist, then there's no cache.

### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Stores the value of Configuration Manager client GUID. If the task sequence is running from standalone media, this variable isn't set.

#### Example

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Specifies the name of the currently running task sequence step. This variable is set before the task sequence manager runs each individual step.

#### Example

`run command line`

### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the default gateways used by the computer.

### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

If the current task sequence is running in download-on-demand mode, this variable is `true`. Download-on-demand mode means the task sequence manager downloads content locally only when it must access the content.

### <a name="SMSTSInWinPE"></a> _SMSTSInWinPE

When the current task sequence step is running in Windows PE, this variable is `true`. Test this task sequence variable to determine the current OS environment.

### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the IP addresses used by the computer.

### <a name="SMSTSLastActionName"></a> _SMSTSLastActionName

Stores the name of the last action that was run. This variable relates to **_SMSTSLastActionRetCode**. The task sequence logs these values to the smsts.log file. This variable is beneficial when troubleshooting a task sequence. When a step fails, a custom script can include the step name along with the return code.

### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Stores the return code from the last action that was run. This variable can be used as a condition to determine if the next step is run.

#### Example

`0`

### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- If the last step succeeded, this variable is `true`.  

- If the last step failed, it's `false`.  

- If the task sequence skipped the last action, because the step is disabled or the associated condition evaluated to **false**, this variable isn't reset. It still holds the value for the previous action.  

### <a name="SMSTSLastContentDownloadLocation"></a> _SMSTSLastContentDownloadLocation

<!-- 2840337 -->
This variable contains the last location where the task sequence downloaded or attempted to download content. Inspect this variable instead of parsing the client logs for this content location.

### <a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Specifies that the task sequence started via one of the following methods:  

- **SMS**: The Configuration Manager client, such as when a user starts it from Software Center
- **UFD**: Legacy USB media
- **UFD+FORMAT**: Newer USB media
- **CD**: A bootable CD
- **DVD**: A bootable DVD
- **PXE**: Network boot with PXE
- **HD**: Prestaged media on a hard disk

### <a name="SMSTSLogPath"></a> _SMSTSLogPath

Stores the full path of the log directory. Use this value to determine where the task sequence steps log their actions. This value isn't set when a hard drive isn't available.

### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the MAC addresses used by the computer.

### <a name="SMSTSMachineName"></a> _SMSTSMachineName

Stores and specifies the computer name. Stores the name of the computer that the task sequence uses to log all status messages. To change the computer name in the new OS, use the [OSDComputerName](#OSDComputerName-input) variable.

### <a name="SMSTSMake"></a> _SMSTSMake

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the make of the computer.

### <a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Specifies the path defined by the [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) variable. This path specifies where the task sequence stores temporary cache files on the destination computer while it's running. When you define SMSTSLocalDataDrive before the task sequence starts, such as by setting a collection variable, Configuration Manager then defines the _SMSTSMDataPath variable once the task sequence starts.

### <a name="SMSTSMediaType"></a> _SMSTSMediaType

Specifies the type of media used to initiate the installation, which includes:

- `BootMedia`: Boot Media
- `FullMedia`: Full Media
- `PXE`: PXE
- `OEMMedia`: Prestaged Media

### <a name="SMSTSModel"></a> _SMSTSModel

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the model of the computer.

### <a name="SMSTSMP"></a> _SMSTSMP

Stores the URL or IP address of a Configuration Manager management point.

### <a name="SMSTSMPPort"></a> _SMSTSMPPort

Stores the port number of a Configuration Manager management point.

### <a name="SMSTSOrgName"></a> _SMSTSOrgName

Stores the branding title name that the task sequence displays in the progress dialog.

### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Applies to the [Upgrade operating system](task-sequence-steps.md#BKMK_UpgradeOS) step.*

Stores the exit code value that Windows Setup returns to indicate success or failure. This variable is useful with the `/Compat` command-line option.

#### Example

On the completion of a compat-only scan, take action in later steps depending on the failure or success exit code. On success, initiate the upgrade. Or set a marker in the environment to collect with hardware inventory. For example, add a file or set a registry key. Use this marker to create a collection of computers that are ready to upgrade, or that require action before upgrade.

### <a name="SMSTSPackageID"></a> _SMSTSPackageID

Stores the current running task sequence ID. This ID uses the same format as a Configuration Manager package ID.

#### Example

`HJT00001`

### <a name="SMSTSPackageName"></a> _SMSTSPackageName

Stores the current running task sequence name. A Configuration Manager administrator specifies this name when creating the task sequence.

#### Example

`Deploy Windows 10 task sequence`

### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Set to `true` if the current task sequence is running in run-from-distribution-point mode. This mode means the task sequence manager obtains required package shares from distribution point.

### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the serial number of the computer.

### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Specifies whether Windows Setup performed a rollback operation during an in-place upgrade. The variable values can be `true` or `false`.

### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Stores the site code of the Configuration Manager site.

#### Example

`ABC`

### <a name="SMSTSTimezone"></a> _SMSTSTimezone

This variable stores the time zone information in the following format:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### Example

For the time zone **Eastern Time (US and Canada)**:

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="SMSTSType"></a> _SMSTSType

Specifies the type of the current running task sequence. It can have one of the following values:  

- **1**: A generic task sequence
- **2**: An OS deployment task sequence

### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

When the task sequence uses HTTPS to communicate with the management point, this variable specifies whether it uses the certificate revocation list (CRL).

### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Specifies whether a user started the task sequence. This variable is set only if the task sequence is started from Software Center. For example, if [_SMSTSLaunchMode](#SMSTSLaunchMode) is set to `SMS`.

This variable can have the following values:  

- `true`: Specifies that the task sequence is manually started by a user from Software Center.  

- `false`: Specifies that the task sequence is initiated automatically by the Configuration Manager scheduler.

### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Specifies whether the task sequence uses SSL to communicate with the Configuration Manager management point. If you configure your site systems for HTTPS, the value is set to `true`.

### <a name="SMSTSUUID"></a> _SMSTSUUID

*Applies to the [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables) step.*

Specifies the UUID of the computer.

### <a name="SMSTSWTG"></a> _SMSTSWTG

Specifies if the computer is running as a Windows To Go device.

### <a name="TSCRMEMORY"></a> _TS_CRMEMORY

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Minimum memory (MB)** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRSPEED"></a> _TS_CRSPEED

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Minimum processor speed (MHz)** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRDISK"></a> _TS_CRDISK

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Minimum free disk space (MB)** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCROSTYPE"></a> _TS_CROSTYPE

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Current OS to be refreshed is** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRARCH"></a> _TS_CRARCH

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Architecture of current OS** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRMINOSVER"></a> _TS_CRMINOSVER

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Minimum OS version** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRMAXOSVER"></a> _TS_CRMAXOSVER

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Maximum OS version** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRCLIENTMINVER"></a> _TS_CRCLIENTMINVER

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Minimum client version** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCROSLANGUAGE"></a> _TS_CROSLANGUAGE

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Language of current OS** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRACPOWER"></a> _TS_CRACPOWER

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **AC power plugged in** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRNETWORK"></a> _TS_CRNETWORK

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Network adapter connected** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRUEFI"></a> _TS_CRUEFI

<!--6452769-->

*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Computer is in UEFI mode** check returned BIOS (`0`) or UEFI (`1`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRWIRED"></a> _TS_CRWIRED

<!--6005561-->
*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **Network adapter is not wireless** check returned true (`1`) or false (`0`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRTPMACTIVATED"></a> _TS_CRTPMACTIVATED

*Starting in version 2111* <!--9575077-->

*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **TPM 2.0 or above is activated** check returned inactive (`0`) or active (`1`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSCRTPMENABLED"></a> _TS_CRTPMENABLED

*Starting in version 2111* <!--9575077-->

*Applies to the [Check Readiness](task-sequence-steps.md#BKMK_CheckReadiness) step.*

A read-only variable for whether the **TPM 2.0 or above is enabled** check returned disabled (`0`) or enabled (`1`). If you don't enable the check, the value of this read-only variable is blank.

### <a name="TSAppInstallStatus"></a> _TSAppInstallStatus

The task sequence sets this variable with the installation status for the application during the [Install Application](task-sequence-steps.md#BKMK_InstallApplication) step. It sets one of the following values:  

- **Undefined**: The Install Application step hasn't run.  

- **Error**: At least one application failed because of an error during the Install Application step.  

- **Warning**: No errors occurred during the Install Application step. One or more applications, or a required dependency, didn't install because a requirement wasn't met.  

- **Success**: There are no errors or warnings detected during the Install Application step.  

### <a name="TSSecureBoot"></a> _TSSecureBoot

<!--5842295-->

Use this variable to determine the state of secure boot on a UEFI-enabled device. The variable can have one of the following values:

- `NA`: The associated registry value doesn't exist, which means the device doesn't support secure boot.
- `Enabled`: The device has secure boot enabled.
- `Disabled`: The device has secure boot disabled.

### <a name="OSDAdapter"></a> OSDAdapter

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

This task sequence variable is an *array* variable. Each element in the array represents the settings for a single network adapter on the computer. Access the settings for each adapter by combining the array variable name with the zero-based network adapter index and the property name.

If the Apply Network Settings step configures multiple network adapters, it defines the properties for the *second* network adapter by using the index **1** in the variable name. For example: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, and OSDAdapter1DNSDomain.

Use the following variable names to define the properties of the *first* network adapter for the step to configure:

#### OSDAdapter0EnableDHCP

This setting is required. Possible values are `True` or `False`. For example:

`true`: enable Dynamic Host Configuration Protocol (DHCP) for the adapter

#### OSDAdapter0IPAddressList

Comma-delimited list of IP addresses for the adapter. This property is ignored unless **EnableDHCP** is set to `false`. This setting is required.

#### OSDAdapter0SubnetMask

Comma-delimited list of subnet masks. This property is ignored unless **EnableDHCP** is set to `false`. This setting is required.

#### OSDAdapter0Gateways

Comma-delimited list of IP gateway addresses. This property is ignored unless **EnableDHCP** is set to `false`. This setting is required.

#### OSDAdapter0DNSDomain

Domain Name System (DNS) domain for the adapter.

#### OSDAdapter0DNSServerList

Comma-delimited list of DNS servers for the adapter. This setting is required.

#### OSDAdapter0EnableDNSRegistration

Set to `true` to register the IP address for the adapter in DNS.

#### OSDAdapter0EnableFullDNSRegistration

Set to `true` to register the IP address for the adapter in DNS under the full DNS name for the computer.

#### OSDAdapter0EnableIPProtocolFiltering

Set to `true` to enable IP protocol filtering on the adapter.

#### OSDAdapter0IPProtocolFilterList

Comma-delimited list of protocols allowed to run over IP. This property is ignored if **EnableIPProtocolFiltering** is set to `false`.

#### OSDAdapter0EnableTCPFiltering

Set to `true` to enable TCP port filtering for the adapter.

#### OSDAdapter0TCPFilterPortList

Comma-delimited list of ports to be granted access permissions for TCP. This property is ignored if **EnableTCPFiltering** is set to `false`.

#### OSDAdapter0TcpipNetbiosOptions

Options for NetBIOS over TCP/IP. Possible values are as follows:  

- `0`: Use NetBIOS settings from DHCP server  
- `1`: Enable NetBIOS over TCP/IP  
- `2`: Disable NetBIOS over TCP/IP  

<!--
#### OSDAdapter0EnableWINS

Set to `true` to use WINS for name resolution.

#### OSDAdapter0WINSServerList

Comma-delimited list of WINS server IP addresses. This property is ignored unless **EnableWINS** is set to `true`.
-->

#### OSDAdapter0MacAddress

MAC address used to match settings to the physical network adapter.

#### OSDAdapter0Name

The name of the network connection as it appears in the network connections control panel program. The name is between 0 and 255 characters long.

#### OSDAdapter0Index

Index of the network adapter settings in the array of settings.

#### Example

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="OSDAdapterCount"></a> OSDAdapterCount

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies the number of network adapters installed on the destination computer. When you set the **OSDAdapterCount** value, also set all the configuration options for each adapter.

For example, if you set the **OSDAdapter0TCPIPNetbiosOptions** value for the first adapter, then you must configure all the values for that adapter.

If you don't specify this value, the task sequence ignores all **OSDAdapter** values.

### <a name="OSDAppInstallRetries"></a> OSDAppInstallRetries

Starting this Configuration Manager 2211 HFRU Kb 16643863 and above

*Applies to the [Install Application](task-sequence-steps.md#BKMK_InstallApplication) step.*

(input)

Specifies the number of times the task sequence step tries to install an application in the case of failure. The value must be specified to trigger a retry in the case of application installation failure. Application installation retry is attempted ONLY when 'Install Next Application on Failure' option is not selected on the task.

Defaults to 0 and task sequence does not retry application installation by default. 

### <a name="OSDAppInstallRetryTimeout"></a> OSDAppInstallRetryTimeout

Starting this Configuration Manager 2211 HFRU Kb 16643863 and above

*Applies to the [Install Application](task-sequence-steps.md#BKMK_InstallApplication) step.*

(input)

Specifies the time in milliseconds, that the task sequence should wait before retrying an application installation on failure. The value defaults to 30 seconds (30000 milliseconds). For example, specify a value of 45000 for a retry delay of 45 seconds.

### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*Applies to the [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage) step.*

(input)

Specifies the content ID of the mass storage device driver to install from the driver package. If this variable isn't specified, no mass storage driver is installed.

### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Applies to the [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage) step.*

(input)

Specifies whether a mass storage device driver is installed, this variable must be **scsi**.

If [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) is set, this variable is required.

### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Applies to the [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage) step.*

(input)

Specifies the boot critical ID of the mass storage device driver to install. This ID is listed in the **scsi** section of the device driver's txtsetup.oem file.

If [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) is set, this variable is required.

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Applies to the [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage) step.*

(input)

Specifies the INF file of the mass storage driver to install.

If [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) is set, this variable is required.

### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Applies to the [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers) step.*

(input)

If there are multiple device drivers in the driver catalog that are compatible with a hardware device, this variable determines the step's action.

#### Valid values

- `true` (default): Only install the best device driver  

- `false`: Installs all compatible device drivers, and Windows chooses the best driver to use  

### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Applies to the [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers) step.*

(input)

A comma-delimited list of the driver catalog category unique IDs. The **Auto Apply Driver** step only considers the drivers in at least one of the specified categories. This value is optional, and it's not set by default. Obtain the available category IDs by enumerating the list of **SMS_CategoryInstance** objects on the site.

### OSDBitLockerPIN
<!-- MEMDOcs #764 -->
*Applies to the [Enable BitLocker](task-sequence-steps.md#enable-bitlocker) step.*

Specify the PIN for BitLocker encryption. This variable is only valid if the BitLocker mode is **TPM and PIN**.

### <a name="OSDBitLockerRebootCount"></a> OSDBitLockerRebootCount

*Applies to the [Disable BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker) step.*

<!-- 4512937 -->
Use this variable to set the number of restarts after which to resume protection.

#### Valid values

An integer from `1` to `15`.

### <a name="OSDBitLockerRebootCountOverride"></a> OSDBitLockerRebootCountOverride

*Applies to the [Disable BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker) step.*

<!-- 4512937 -->
Set this value to override the count set by the step or the [OSDBitLockerRebootCount](#OSDBitLockerRebootCount) variable. While the other methods only accept values 1 to 15, if you set this variable to 0, BitLocker remains disabled indefinitely. This variable is useful when the task sequence sets one value, but you want to set a separate value on a per-device or per-collection basis.

#### Valid values

An integer from `0` to `15`.

### OSDBitLockerRecoveryPassword

*Applies to the [Enable BitLocker](task-sequence-steps.md#enable-bitlocker) step.*

(input)

Instead of generating a random recovery password, the **Enable BitLocker** step uses the specified value as the recovery password. The value must be a valid numerical BitLocker recovery password.

### OSDBitLockerStartupKey

*Applies to the [Enable BitLocker](task-sequence-steps.md#enable-bitlocker) step.*

(input)

Instead of generating a random startup key for the key management option **Startup Key on USB only,** the **Enable BitLocker** step uses the Trusted Platform Module (TPM) as the startup key. The value must be a valid, 256-bit Base64-encoded BitLocker startup key.

### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

(input)

Specifies a Windows account name that has permissions to store the captured image on a network share ([OSDCaptureDestination](#OSDCaptureDestination)). Also specify the [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

For more information on the capture OS image account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

(input)

Specifies the password for the Windows account ([OSDCaptureAccount](#OSDCaptureAccount)) used to store the captured image on a network share ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

(input)

Specifies the location where the task sequence saves the captured OS image. The maximum directory name length is 255 characters. If the network share requires authentication, specify the [OSDCaptureAccount](#OSDCaptureAccount) and [OSDCaptureAccountPassword](#OSDCaptureAccountPassword) variables.

### <a name="OSDComputerName-input"></a> OSDComputerName (input)

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the name of the destination computer.

#### Example

`%_SMSTSMachineName%` (default)

### <a name="OSDComputerName-output"></a> OSDComputerName (output)

*Applies to the [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings) step.*

Set to the NetBIOS name of the computer. The value is set only if the [OSDMigrateComputerName](#OSDMigrateComputerName) variable is set to `true`.

### <a name="OSDConfigFileName"></a> OSDConfigFileName

*Applies to the [Apply OS Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) step.*

(input)

Specifies the file name of the OS deployment answer file associated with the OS deployment image package.  

### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Applies to the [Apply Data Image](task-sequence-steps.md#BKMK_ApplyDataImage) step.*

(input)

Specifies the index value of the image that's applied to the destination computer.

### <a name="OSDDiskIndex"></a> OSDDiskIndex

*Applies to the [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk) step.*

(input)

Specifies the physical disk number to be partitioned.

In version 2010 and earlier, this number can't be larger than 99. In version 2103 and later, the maximum number is 10,000. This change helps support storage area network (SAN) scenarios.<!-- 9528541 -->

### <a name="OSDDNSDomain"></a> OSDDNSDomain

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies the primary DNS server that the destination computer uses.

### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies the DNS search order for the destination computer.

### <a name="OSDDomainName"></a> OSDDomainName

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies the name of the Active Directory domain that the destination computer joins. The specified value must be a valid Active Directory Domain Services domain name.

### <a name="OSDDomainOUName"></a> OSDDomainOUName

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies the RFC 1779 format name of the organizational unit (OU) that the destination computer joins. If specified, the value must contain the full path.

#### Example

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
_Applies to the [Install Package](task-sequence-steps.md#BKMK_InstallPackage) and [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) steps._

(input)

To prevent potentially sensitive data from being displayed or logged, set this variable to `TRUE`. This variable masks the program name in the **smsts.log** during an **Install Package** step.

When you set this variable to `TRUE`, it also hides the command line from the **Run Command Line** step in the log file.<!--3654172-->

### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies whether TCP/IP filtering is enabled.

#### Valid values

- `true`  
- `false` (default)  

### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Applies to the [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk) step.*

(input)

Specifies whether to create an EFI partition on a GPT hard disk. EFI-based computers use this partition as the startup disk.

#### Valid values

- `true`  
- `false` (default)

### <a name="OSDImageCreator"></a> OSDImageCreator

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

(input)

An optional name of the user who created the image. This name is stored in the WIM file. The maximum length of the user name is 255 characters.

### <a name="OSDImageDescription"></a> OSDImageDescription

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

(input)

An optional user-defined description of the captured OS image. This description is stored in the WIM file. The maximum length of the description is 255 characters.

### <a name="OSDImageIndex"></a> OSDImageIndex

*Applies to the [Apply OS Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) step.*

(input)

Specifies the image index value of the WIM file that's applied to the destination computer.

### <a name="OSDImageVersion"></a> OSDImageVersion

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

(input)

An optional user-defined version number to assign to the captured OS image. This version number is stored in the WIM file. This value can be any combination of alphanumeric characters with a maximum length of 32.

### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Applies to the [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage) step.*

(input)

Specifies additional options to add to the DISM command line when applying a driver package. The task sequence doesn't verify the command-line options.

To use this variable, enable the setting, **Install driver package via running DISM with recurse option**, on the **Apply Driver Package** step.

For more information, see [DISM command-line options](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="OSDJoinAccount"></a> OSDJoinAccount

*Applies to the following steps:*  

- [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(input)

Specifies the domain user account that's used to add the destination computer to the domain. This variable is required when joining a domain.

For more information on the task sequence domain joining account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Applies to the [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) step.*

(input)

Specifies the name of an Active Directory domain the destination computer joins. The length of the domain name must be between 1 and 255 characters.

### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Applies to the [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) step.*

(input)

Specifies the RFC 1779 format name of the organizational unit (OU) that the destination computer joins. If specified, the value must contain the full path. The length of the OU name must be between 0 and 32,767 characters. This value isn't set if the [OSDJoinType](#OSDJoinType) variable is set to `1` (join workgroup).

#### Example

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="OSDJoinPassword"></a> OSDJoinPassword

*Applies to the following steps:*  

- [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(input)

Specifies the password for the [OSDJoinAccount](#OSDJoinAccount) that the destination computer uses to join the Active Directory domain. If the task sequence environment doesn't include this variable, then Windows Setup tries a blank password. If the variable [OSDJoinType](#OSDJoinType) variable is set to `0` (join domain), this value is required.

### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Applies to the [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) step.*

(input)

Specifies whether to skip restarting after the destination computer joins the domain or workgroup.

#### Valid values

- `true`  
- `false`  

### <a name="OSDJoinType"></a> OSDJoinType

*Applies to the [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) step.*

(input)

Specifies whether the destination computer joins a Windows domain or a workgroup.

#### Valid values

- `0`: Join the destination computer to a Windows domain  
- `1`: Join the destination computer to a workgroup  

### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Applies to the [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) step.*

(input)

Specifies the name of a workgroup that the destination computer joins. The length of the workgroup name must be between 1 and 32 characters.

### <a name="OSDKeepActivation"></a> OSDKeepActivation

*Applies to the [Prepare Windows for Capture](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) step.*

(input)

Specifies whether sysprep keeps or resets the product activation flag.

#### Valid values

- `true`: keep the activation flag
- `false` (default): reset the activation flag

### <a name="OsdLayeredDriver"></a> OsdLayeredDriver

_Starting in version 2107_<!--9735002-->

_Applies to the [Apply OS Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) step_

Specify an integer value for the layered driver to install with Windows. For more information, see the [LayeredDriver](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-winpe-layereddriver) Windows setting.

#### Valid values for OsdLayeredDriver

| Value | Keyboard driver |
|---------|---------|
| `0` | Do not specify (default) |
| `1` | PC/AT Enhanced keyboard (101/102-key) |
| `2` | Korean PC/AT 101-Key Compatible keyboard or the Microsoft Natural keyboard (type 1) |
| `3` | Korean PC/AT 101-Key Compatible keyboard or the Microsoft Natural keyboard (type 2) |
| `4` | Korean PC/AT 101-Key Compatible keyboard or the Microsoft Natural keyboard (type 3) |
| `5` | Korean keyboard (103/106-key) |
| `6` | Japanese keyboard (106/109-key) |

### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

(input)

Specifies the local Administrator account password. If you enable the option to **Randomly generate the local administrator password and disable the account on all supported platforms**, then the step ignores this variable. The specified value must be between 1 and 255 characters.

### <a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
_Applies to the [Run PowerShell Script](task-sequence-steps.md#BKMK_RunPowerShellScript) step._

(input)

To prevent potentially sensitive data from being logged, the **Run PowerShell Script** step doesn't log script parameters in the **smsts.log** file. To include the script parameters in the task sequence log, set this variable to **TRUE**.

### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Applies to the [Capture Network Settings](task-sequence-steps.md#BKMK_CaptureNetworkSettings) step.*

(input)

Specifies whether the task sequence captures the network adapter information. This information includes configuration settings for TCP/IP and DNS.

#### Valid values

- `true` (default)
- `false`

### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*Applies to the [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState) step.*

(input)

Specify additional command-line options for the user state migration tool (USMT) that the task sequence uses to capture user state. The step doesn't expose these settings in the task sequence editor. Specify these options as a string, which the task sequence appends to the automatically generated USMT command line for ScanState.

The USMT options specified with this task sequence variable aren't validated for accuracy prior to running the task sequence.

For more information on available options, see [ScanState Syntax](/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*Applies to the [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState) step.*

(input)

Specifies additional command-line options for the user state migration tool (USMT) that the task sequence uses when restoring the user state. Specify the additional options as a string, which the task sequence appends to the automatically generated USMT command line for LoadState.

The USMT options specified with this task sequence variable aren't validated for accuracy prior to running the task sequence.

For more information on available options, see [LoadState Syntax](/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Applies to the [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings) step.*

(input)

Specifies whether the computer name is migrated.

#### Valid values

- `true` (default). The [OSDComputerName (output)](#OSDComputerName-output) variable is set to the NetBIOS name of the computer.  
- `false`  

### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Applies to the [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState) step.*

(input)

Specifies the configuration files used to control the capture of user profiles. This variable is used only if [OSDMigrateMode](#OSDMigrateMode) is set to `Advanced`. This comma-delimited list value is set to perform customized user profile migration.

#### Example

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Applies to the [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState) step.*

(input)

If USMT can't capture some files, this variable allows the user state capture to proceed.

#### Valid values

- `true` (default)  
- `false`  

### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Applies to the [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState) step.*

(input)

Continue the process, even if USMT can't restore some files.

#### Valid values

- `true` (default)  
- `false`  

### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Applies to the following steps:*  

- [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState)  

(input)

Enables verbose logging for USMT. The step requires this value.

#### Valid values

- `true`  
- `false` (default)  

### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Applies to the [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState) step.*

(input)

Specifies whether the local computer account is restored.

#### Valid values

- `true`  
- `false` (default)  

### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Applies to the [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState) step.*

(input)

If the [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) variable is `true`, this variable must contain the password assigned to *all* migrated local accounts. USMT assigns the same password to all migrated local accounts. Consider this password as temporary, and change it later by some other method.

### <a name="OSDMigrateMode"></a> OSDMigrateMode

*Applies to the [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState) step.*

(input)

Allows you to customize the files that USMT captures.

#### Valid values

- `Simple`: The task sequence only uses the standard USMT configuration files  

- `Advanced`: The task sequence variable [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) specifies the configuration files that USMT uses  

### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Applies to the [Capture Network Settings](task-sequence-steps.md#BKMK_CaptureNetworkSettings) step.*

(input)

Specifies whether the task sequence migrates the workgroup or domain membership information.

#### Valid values

- `true` (default)
- `false`

### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Applies to the [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings) step.*

(input)

Specifies whether the step migrates user and organization information.

#### Valid values

- `true` (default). The [OSDRegisteredOrgName (output)](#OSDRegisteredOrgName-output) variable is set to the registered organization name of the computer.  
- `false`  

### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Applies to the [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState) step.*

(input)

Specifies whether encrypted files are captured.

#### Valid values

- `true`  
- `false` (default)  

### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Applies to the [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings) step.*

(input)

Specifies whether the computer time zone is migrated.

#### Valid values

- `true` (default). The variable [OSDTimeZone (output)](#OSDTimeZone-output) is set to the time zone of the computer.  
- `false`  

### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies whether the destination computer joins an Active Directory domain or a workgroup.

#### Value values

- `0`: Join an Active Directory domain  
- `1`: Join a workgroup

### <a name="OSDPartitions"></a> OSDPartitions

*Applies to the [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk) step.*

(input)

This task sequence variable is an array variable of partition settings. Each element in the array represents the settings for a single partition on the hard disk. Access the settings defined for each partition by combining the array variable name with the zero-based disk partition number and the property name.

Use the following variable names to define the properties for the *first* partition that this step creates on the hard disk:

#### OSDPartitions0Type

Specifies the type of partition. This property is required. Valid values are `Primary`, `Extended`, `Logical`, and `Hidden`.

#### OSDPartitions0FileSystem

Specifies the type of file system to use when formatting the partition. This property is optional. If you don't specify a file system, the step doesn't format the partition. Valid values are `FAT32` and `NTFS`.

#### OSDPartitions0Bootable

Specifies whether the partition is bootable. This property is required. If this value is set to `TRUE` for MBR disks, then the step marks this partition as active.

#### OSDPartitions0QuickFormat

Specifies the type of format that is used. This property is required. If this value is set to `TRUE`, the step performs a quick format. Otherwise, the step performs a full format.

#### OSDPartitions0VolumeName

Specifies the name that's assigned to the volume when it's formatted. This property is optional.

#### OSDPartitions0Size

Specifies the size of the partition. This property is optional. If this property isn't specified, the partition is created using all remaining free space. Units are specified by the **OSDPartitions0SizeUnits** variable.

#### OSDPartitions0SizeUnits

The step uses these units to interpret the **OSDPartitions0Size** variable. This property is optional. Valid values are `MB` (default), `GB`, and `Percent`.

#### OSDPartitions0VolumeLetterVariable

When this step creates partitions, it always uses the next available drive letter in Windows PE. Use this optional property to specify the name of another task sequence variable. The step uses this variable to save the new drive letter for future reference.

If you define multiple partitions with this task sequence step, the properties for the *second* partition are defined by using the **1** index in the variable name. For example: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, and **OSDPartitions1VolumeName**.

### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Applies to the [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk) step.*

(input)

Specifies the partition style to use when partitioning the disk.

#### Valid values

- `GPT`: Use the GUID Partition Table style
- `MBR`: Use the master boot record partition style

### <a name="OSDProductKey"></a> OSDProductKey

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

(input)

Specifies the Windows product key. The specified value must be between 1 and 255 characters.

### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

(input)

Specifies a randomly generated password for the local Administrator account in the new OS.

#### Valid values

- `true` (default): Windows Setup disables the local Administrator account on the target computer  

- `false`: Windows Setup enables the local administrator account on the target computer, and sets the account password to the value of [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### OSDRecoveryKeyPollingFrequency
<!--10454717-->
_Applies to the [Enable BitLocker](task-sequence-steps.md#enable-bitlocker) step._

_Applies to version 2203 and later._

The frequency, in seconds, that the BitLocker action will poll the site database for recovery key escrow status. Minimum value is 15 seconds. Default value is 300 seconds (5 minutes).

### OSDRecoveryKeyPollingTimeout
<!--10454717-->
_Applies to the [Enable BitLocker](task-sequence-steps.md#enable-bitlocker) step._

_Applies to version 2203 and later._

The maximum number of seconds for the BitLocker action to wait for the recovery key to be escrowed to the site database. Minimum value is 30 seconds. Default value is 1800 seconds (30 minutes).

### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (input)

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the default registered organization name in the new OS. The specified value must be between 1 and 255 characters.

### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (output)

*Applies to the [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings) step.*

Set to the registered organization name of the computer. The value is set only if the [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) variable is set to `true`.

### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

(input)

Specifies the default registered user name in the new OS. The specified value must be between 1 and 255 characters.

### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

(input)

Specifies the maximum number of connections allowed. The specified number must be in the range between 5 and 9999 connections.

### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

(input)

Specifies the Windows Server license mode that's used.

#### Valid values

- `PerSeat`
- `PerServer`

### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Applies to the [Upgrade Operating System](task-sequence-steps.md#BKMK_UpgradeOS) step.*

(input)

Specifies the additional command-line options that are added to Windows Setup during an upgrade. The task sequence doesn't verify the command-line options.

For more information, see [Windows Setup Command-Line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Applies to the [Request State Store](task-sequence-steps.md#BKMK_RequestStateStore) step.*

(input)

When the computer account fails to connect to the state migration point, this variable specifies whether the task sequence falls back to use the network access account (NAA).

For more information on the network access account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### Valid values

- `true`  
- `false` (default)  

### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Applies to the [Request State Store](task-sequence-steps.md#BKMK_RequestStateStore) step.*

(input)

Specifies the number of times that the task sequence step tries to find a state migration point before the step fails. The specified count must be between 0 and 600.

### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Applies to the [Request State Store](task-sequence-steps.md#BKMK_RequestStateStore) step.*

(input)

Specifies the number of seconds that the task sequence step waits between retry attempts. The number of seconds can be a maximum of 30 characters.

### <a name="OSDStateStorePath"></a> OSDStateStorePath

*Applies to the following steps:*  

- [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Release State Store](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Request State Store](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState)  

(input)

The network share or local path name of the folder where the task sequence saves or restores the user state. There is no default value.

### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Applies to the [Apply OS Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) step.*

(output)

Specifies the drive letter of the partition that contains the OS files after the image is applied.

### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (input)

*Applies to the [Capture OS Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) step.*

Specifies the path to the Windows directory of the installed OS on the reference computer. The task sequence verifies it as a supported OS for capture by Configuration Manager.

### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (output)

*Applies to the [Prepare Windows for Capture](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) step.*

Specifies the path to the Windows directory of the installed OS on the reference computer. The task sequence verifies it as a supported OS for capture by Configuration Manager.

### <a name="OSDTimeZone-input"></a> OSDTimeZone (input)

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the default time zone setting that's used in the new OS.

Set the value of this variable to the language invariant name of time zone. For example, use the string in the `Std` value for a time zone under the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.

### <a name="OSDTimeZone-output"></a> OSDTimeZone (output)

*Applies to the [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings) step.*

Set to the time zone of the computer. The value is set only if the [OSDMigrateTimeZone](#OSDMigrateTimeZone) variable is set to `true`.

### <a name="OSDWindowsSettingsInputLocale"></a> OSDWindowsSettingsInputLocale

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the default input locale setting that's used in the new OS.

For more information on the Windows setup answer file value, see [Microsoft-Windows-International-Core - InputLocale](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="OSDWindowsSettingsSystemLocale"></a> OSDWindowsSettingsSystemLocale

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the default system locale setting that's used in the new OS.

For more information on the Windows setup answer file value, see [Microsoft-Windows-International-Core - SystemLocale](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="OSDWindowsSettingsUILanguage"></a> OSDWindowsSettingsUILanguage

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the default user interface language setting that's used in the new OS.

For more information on the Windows setup answer file value, see [Microsoft-Windows-International-Core - UILanguage](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="OSDWindowsSettingsUILanguageFallback"></a> OSDWindowsSettingsUILanguageFallback

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the fallback user interface language setting that's used in the new OS.

For more information on the Windows setup answer file value, see [Microsoft-Windows-International-Core - UILanguageFallback](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="OSDWindowsSettingsUserLocale"></a> OSDWindowsSettingsUserLocale

*Applies to the [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings) step.*

Specifies the default user locale setting that's used in the new OS.

For more information on the Windows setup answer file value, see [Microsoft-Windows-International-Core - UserLocale](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Applies to the [Apply Data Image](task-sequence-steps.md#BKMK_ApplyDataImage) step.*

(input)

Specifies whether to delete the files located on the destination partition.

#### Valid values

- `true` (default)
- `false`

### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Applies to the [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings) step.*

(input)

Specifies the name of the workgroup that the destination computer joins.

Specify either this variable or the [OSDDomainName](#OSDDomainName) variable. The workgroup name can be a maximum of 32 characters.

### <a name="SetupCompletePause"></a> SetupCompletePause

*Applies to the [Upgrade Operating System](task-sequence-steps.md#BKMK_UpgradeOS) step.*

<!-- 4680263 -->

Use this variable to address timing issues with the Window 10 in-place upgrade task sequence on high performance devices when Windows setup is complete. When you assign a value in seconds to this variable, the Windows setup process delays that amount of time before it starts the task sequence. This timeout provides the Configuration Manager client additional time to initialize.

The following log entries are common examples of this issue that you can remediate with this variable:

- The TSManager component records entries similar to the following errors in the **smsts.log**:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Windows setup records entries similar to the following errors in the **setupcomplete.log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Applies to the [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) step.*

(input)

Specifies the client installation properties that the task sequence uses when installing the Configuration Manager client.

For more information, see [About client installation parameters and properties](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Applies to the [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) step.*

(input)

Specifies the user account that is used to connect to the network share in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Specify the account password with the [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) value.

For more information on the task sequence network folder connection account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).

### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Applies to the [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) step.*

(input)

Specifies the network drive letter to connect to. This value is optional. If it's not specified, then the network connection isn't mapped to a drive letter. If this value is specified, the value must be in the range from D to Z. Don't use X, it's the drive letter used by Windows PE during the Windows PE phase.

#### Examples

- `D:`  
- `E:`  

### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Applies to the [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) step.*

(input)

Specifies the password for the [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) that is used to connect to the network share in [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Applies to the [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) step.*

(input)

Specifies the network path for the connection. If you need to map this path to a drive letter, use the [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) value.

#### Example

`\\server\share`

### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Applies to the [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) step.*

(input)

Specifies whether to install all updates or only mandatory updates.

#### Valid values

- `All`  
- `Mandatory`  

### <a name="SMSRebootMessage"></a> SMSRebootMessage

*Applies to the [Restart Computer](task-sequence-steps.md#BKMK_RestartComputer) step.*

(input)

Specifies the message to be displayed to users before restarting the destination computer. If this variable isn't set, the default message text is displayed. The specified message can't exceed 512 characters.

#### Example

`Save your work before the computer restarts.`  

### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Applies to the [Restart Computer](task-sequence-steps.md#BKMK_RestartComputer) step.*

(input)

Specifies the number of seconds that the warning is displayed to the user before the computer restarts.

#### Examples

- `0` (default): Don't display a reboot message  
- `60`: Display the warning for one minute  

### SMSTSAllowTokenAuthURLForACP

<!-- 13788624 -->
_Applies to version 2203 and later_

When you use the [SMSTSDownloadProgram](#smstsdownloadprogram) variable to use an alternate content provider, set this variable to `true` to allow it to use token authentication. If you don't set this variable or set it to `false`, it skips any token authentication sources. The alternate content provider has to support token authentication.

For more information, see [CMG client authentication](../../core/clients/manage/cmg/plan-client-authentication.md#site-token).

### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

The number of seconds to wait before the client attempts to download the policy since the last attempt that returned no policies. By default, the client waits **0** seconds before retrying.

You can set this variable by using a prestart command from media or PXE.

### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

The number of times a client attempts to download the policy after no policies are found on the first attempt. By default, the client retries **0** times.

You can set this variable by using a prestart command from media or PXE.

### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Specifies how a task sequence associates users with the destination computer. Set the variable to one of the following values:  

- **Auto**: When the task sequence deploys the OS to the destination computer, it creates a relationship between the specified users and destination computer.  

- **Pending**: The task sequence creates a relationship between the specified users and the destination computer. An administrator must approve the relationship to set it.  

- **Disabled**: The task sequence doesn't associate users with the destination computer when it deploys the OS.

### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
In disconnected scenarios, the task sequence engine repeatedly tries to send status messages to the management point. This behavior in this scenario causes delays in task sequence processing.

Set this variable to `true` and the task sequence engine doesn't attempt to send status messages after the first message fails to send. This first attempt includes multiple retries.

When the task sequence restarts, the value of this variable persists. However, the task sequence tries sending an initial status message. This first attempt includes multiple retries. If successful, the task sequence continues sending status regardless of the value of this variable. If status fails to send, the task sequence uses the value of this variable.

> [!NOTE]  
> [Task sequence status reporting](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) relies upon these status messages to display the progress, history, and details of each step. If status messages fail to send, they're not queued. When connectivity is restored to the management point, they're not sent at a later time. This behavior results in task sequence status reporting to be incomplete and missing items.

### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Applies to the [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step.*

(input)

By default on a 64-bit OS, the task sequence locates and runs the program in the command line using the WOW64 file system redirector. This behavior allows the command to find 32-bit versions of OS programs and DLLs. Setting this variable to `true` disables the use of the WOW64 file system redirector. The command finds native 64-bit versions of OS programs and DLLs. This variable has no effect when running on a 32-bit OS.

### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

This variable contains the abort code value for the external program downloader. This program is specified in the [SMSTSDownloadProgram](#smstsdownloadprogram) variable. If the program returns an error code equal to the value of the SMSTSDownloadAbortCode variable, then the content download fails and no other download method is attempted.

### SMSTSDownloadProgram

Use this variable to specify an alternate content provider (ACP). An ACP is a downloader program that's used to download content. The task sequence uses the ACP instead of the default Configuration Manager downloader. As part of the content download process, the task sequence checks this variable. If specified, the task sequence runs the program to download the content.

### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

The number of times that Configuration Manager attempts to download content from a distribution point. By default, the client retries **2** times.

### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

The number of seconds that Configuration Manager waits before it retries to download content from a distribution point. By default, the client waits **15** seconds before retrying.

### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Applies to the [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers) step.*

When requesting the driver catalog, this variable is the number of seconds the task sequence waits for the HTTP server connection. If the connection takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **60** seconds.

### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Applies to the [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers) step.*

When requesting the driver catalog, this variable is the number of seconds the task sequence waits for a response. If the connection takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **480** seconds.

### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Applies to the [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers) step.*

When requesting the driver catalog, this variable is the number of seconds the task sequence waits for HTTP name resolution. If the connection takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **60** seconds.

### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Applies to the [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers) step.*

When sending a request for the driver catalog, this variable is the number of seconds the task sequence waits to send the request. If the request takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **60** seconds.

### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

When an error occurs in a task sequence, it displays a dialog box with the error. The task sequence automatically dismisses it after the number of seconds specified by this variable. By default, this value is **900** seconds (15 minutes).

### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

Use this variable to change the display language of a language neutral boot image.

### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Specifies where the task sequence stores temporary cache files on the destination computer while it's running.

Set this variable before the task sequence starts, such as by setting a collection variable. Once the task sequence starts, Configuration Manager defines the [_SMSTSMDataPath](#SMSTSMDataPath) variable based on what the SMSTSLocalDataDrive variable was defined to.

### <a name="SMSTSMP"></a> SMSTSMP

Use this variable to specify the URL or IP address of the Configuration Manager management point.

### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Applies to the following steps:*  

- [Install Application](task-sequence-steps.md#BKMK_InstallApplication)  
- [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(input)

If the client isn't on the intranet, use this variable to enable repeated MPList requests to refresh the client. By default, this variable is set to `True`.

When clients are on the internet, set this variable to `False` to avoid unnecessary delays.

### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Applies to the following steps:*  

- [Install Application](task-sequence-steps.md#BKMK_InstallApplication)  
- [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(input)

If the task sequence fails to retrieve the management point list (MPList) from location services, this variable specifies how many milliseconds it waits before it retries the step. By default, the task sequence waits `60000` milliseconds (60 seconds) before it retries. It retries up to three times.

### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Use this variable to enable the client to use Windows PE peer cache. Setting this variable to `true` enables this functionality.

### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

A custom network port that Windows PE peer cache uses for the initial broadcast. The default port configured in client settings is **8004**.

### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

Use this variable to temporarily persist content in the task sequence cache. This variable is different from [SMSTSPreserveContent](#SMSTSPreserveContent), which keeps content in the Configuration Manager client cache after the task sequence is complete. SMSTSPersistContent uses the task sequence cache, SMSTSPreserveContent uses the Configuration Manager client cache.

### <a name="SMSTSPostAction"></a> SMSTSPostAction

Specifies a command that's run after the task sequence completes. Just before exiting the task sequence, the TSManager process spawns the specified post action. It doesn't wait or record any status, just exits after calling that command.<!-- MEMDocs #719 -->

For example, specify `shutdown.exe /r /t 30 /f` to restart the computer 30 seconds after the task sequence completes.

### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Forces the task sequence to run a specific targeted deployment on the destination computer. Set this variable through a prestart command from media or PXE. If this variable is set, the task sequence overrides any required deployments.

### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

This variable flags the content in the task sequence to be kept in the Configuration Manager client cache after the deployment. This variable is different from [SMSTSPersistContent](#SMSTSPersistContent), which only keeps the content for the duration of the task sequence. SMSTSPersistContent uses the task sequence cache, SMSTSPreserveContent uses the Configuration Manager client cache. Set SMSTSPreserveContent to `true` to enable this functionality.

### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Specifies how many seconds to wait before the computer restarts. If this variable is zero (0), the task sequence manager doesn't display a notification dialog before reboot.

#### Example

- `0`: don't display a notification  

- `60`: display a notification for one minute  

### <a name="SMSTSRebootDelayNext"></a> SMSTSRebootDelayNext

<!--4447680-->
Use this variable with the existing [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) variable. If you want any later reboots to happen with a different timeout than the first, set SMSTSRebootDelayNext to a different value in seconds.

#### Example

You want to give users a 60-minute reboot notification at the start of a Windows in-place upgrade task sequence. After that first long timeout, you want additional timeouts to only be 60 seconds. Set SMSTSRebootDelay to `3600`, and SMSTSRebootDelayNext to `60`.  


### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Specifies the message to display in the restart notification dialog. If this variable isn't set, a default message appears.

#### Example

`The task sequence is restarting this computer`

### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

Indicates that a restart is requested after the current task sequence step is completed. If the task sequence step requires a restart to complete the action, set this variable. After the computer restarts, the task sequence continues to run from the next task sequence step.

- `HD`: Restart to the installed OS
- `WinPE`: Restart to the associated boot image

### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Requests a retry after the current task sequence step is completed. If this task sequence variable is set, also configure the [SMSTSRebootRequested](#SMSTSRebootRequested) variable. After the computer is restarted, the task sequence manager reruns the same task sequence step.

### <a name="SMSTSRunCommandLineAsUser"></a> SMSTSRunCommandLineAsUser

<!-- 5573175 -->
*Applies to the [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step.*

Use task sequence variables to configure the user context for the **Run Command Line** step. You don't need to configure the **Run Command Line** step with a placeholder account to use the [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) and [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) variables.

Configure `SMSTSRunCommandLineAsUser` with one of the following values:

- `true`: Any further **Run Command Line** steps run in the context of the user specified in `SMSTSRunCommandLineUserName`.

- `false`: Any further **Run Command Line** steps run in the context that you configured on the step.

### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Applies to the [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step.*

(input)

Specifies the account by which the command line is run. The value is a string of the form username for a local account or domain\username for a domain one. Specify the account password with the [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) variable.

> [!NOTE]
> Use the [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) variable with this variable to configure the user context for this step.

For more information on the task sequence run-as account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword

*Applies to the [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step.*

(input)

Specifies the password for the account specified by the [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) variable.

### <a name="SMSTSRunPowerShellAsUser"></a> SMSTSRunPowerShellAsUser

<!-- 5573175 -->  
*Applies to the [Run PowerShell Script](task-sequence-steps.md#BKMK_RunPowerShellScript) step.*

Use task sequence variables to configure the user context for the **Run PowerShell Script** step. You don't need to configure the **Run PowerShell Script** step with a placeholder account to use the [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) and [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) variables.

Configure `SMSTSRunPowerShellAsUser` with one of the following values:

- `true`: Any further **Run PowerShell Script** steps run in the context of the user specified in `SMSTSRunPowerShellUserName`.

- `false`: Any further **Run PowerShell Script** steps run in the context that you configured on the step.

### <a name="SMSTSRunPowerShellUserName"></a> SMSTSRunPowerShellUserName

*Applies to the [Run PowerShell Script](task-sequence-steps.md#BKMK_RunPowerShellScript) step.*

(input)

Specifies the account by which the PowerShell script is run. The value is a string of the form username or domain\username. Specify the account password with the [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) variable.

> [!NOTE]
> To use these variables, configure the **Run PowerShell Script** step with the setting to **Run this step as the following account**. When you enable this option, if you're setting the user name and password with variables, specify any value for the account.

For more information on the task sequence run-as account, see [Accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="SMSTSRunPowerShellUserPassword"></a> SMSTSRunPowerShellUserPassword

*Applies to the [Run PowerShell Script](task-sequence-steps.md#BKMK_RunPowerShellScript) step.*

(input)

Specifies the password for the account specified by the [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) variable.

### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Applies to the [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) step.*

(input)

Control the timeout for the software updates scan during this step. For example, if you expect numerous updates during the scan, increase the value. The default value is `3600` seconds (60 minutes). The variable value is set in seconds.

### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Specifies the primary users of the destination computer by using the following format: `<DomainName>\<UserName>`. Separate multiple users by using a comma (`,`). For more information, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).

#### Example

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### SMSTSWaitCcmexecOperationalTimeout

(input)

Use this variable to control the timeout period for the task sequence to wait for the SMS Agent Host service (ccmexec) to completely start. Specify this value in seconds. The default timeout period is 30 minutes, or 1800 seconds.

#### Examples of SMSTSWaitCcmexecOperationalTimeout

- `1800` (default): 30 minutes
- `300`: The task sequence waits five minutes for ccmexec to start

### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Applies to the [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) step.*

(input)

This optional task sequence variable controls client behavior when a software update installation triggered by the **Install Software Updates** task requires multiple restarts. Set this variable before the **Install Software Updates** step to prevent a task sequence from failing because of multiple restarts from software update installation.

This variable is useful when a single **Install Software Updates** task sequence step installs software updates that need multiple restarts to finish installing.

Set the **SMSTSWaitForSecondReboot** value in seconds to specify how long the task sequence pauses on this step while the computer restarts. Allow sufficient time in case there's multiple restarts. For example, if you set **SMSTSWaitForSecondReboot** to `600`, the task sequence pauses for 10 minutes after a restart before additional steps run.

The **SMSTSWaitForSecondReboot** variable is intended for use with the **Install Software Updates** task, but can be set anywhere in the task sequence to introduce delays after reboots initiated by tasks other than the **Install Software Updates** task. For this reason, when this variable is set before the **Install Software Updates** task, it's advisable to also set it again after the **Install Software Updates** task with a value of `0`. This resets the variable and prevents unnecessary delays during the task sequence. If there are multiple **Install Software Updates** tasks in the task sequence, define the variable to the desired value before the first **Install Software Updates** task, and then reset it back to `0` after the last **Install Software Updates** task.

> [!NOTE]
>
> This variable only applies to OSD task sequences that deploys an OS. It doesn't work with any task sequence that doesn't utilize the **Setup Windows and ConfigMgr** task, such as stand-alone task sequences or in-place upgrade task sequences. <!-- 2839998 -->

### <a name="TSDebugMode"></a> TSDebugMode

<!--3612274-->
Set this variable to `TRUE` on a collection or computer object to which the task sequence is deployed. Any device that has this variable set will put any task sequence deployed to it into debug mode.

For more information, see [Debug a task sequence](../deploy-use/debug-task-sequence.md).

### <a name="TSDebugOnError"></a> TSDebugOnError

<!-- 5012536 -->
Set this variable to `TRUE` to automatically start the [task sequence debugger](../deploy-use/debug-task-sequence.md) when the task sequence returns an error.

Set this variable using:

- The [Set Task Sequence Variable](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step

- A collection variable. For more information, see [How to set variables](using-task-sequence-variables.md#bkmk_set).

### <a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Use this variable to control when the task sequence displays progress to end users. To hide or display progress at different times, set this variable multiple times in a task sequence.  

- `true`: Hide task sequence progress  

- `false`: Display task sequence progress  

### <a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Applies to the [Install Application](task-sequence-steps.md#BKMK_InstallApplication) step.*

(input)

Specify whether the task sequence engine considers a detected warning as an error during this step. The task sequence sets the [_TSAppInstallStatus](#TSAppInstallStatus) variable to `Warning` when one or more applications, or a required dependency, didn't install because it didn't meet a requirement. When you set this variable to `True`, and the task sequence sets **_TSAppInstallStatus** to `Warning`, the outcome is an error. A value of `False` is the default behavior.

### <a name="TSProgressInfoLevel"></a> TSProgressInfoLevel

<!--5932692-->  

Specify this variable to control the type of information that the task sequence progress window displays. Use the following values for this variable:

- `1`: Include the current step and total steps to the progress text. For example, **2 of 10**.
- `2`: Include the current step, total steps, and percentage completed. For example, **2 of 10 (20% complete)**.
- `3`: Include the percentage completed. For example, **(20% complete)**.

### <a name="TSUEFIDrive"></a> TSUEFIDrive

Use on the properties of a FAT32 partition in the **Variable** field. When the task sequence detects this variable, it prepares the disk for transition to UEFI before it restarts the computer. For more information, see [Task sequence steps to manage BIOS to UEFI conversion](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

### <a name="WorkingDirectory"></a> WorkingDirectory

*Applies to the [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine) step.*

(input)

Specifies the starting directory for a command-line action. The specified directory name can't exceed 255 characters.

#### Examples

- `C:\`  
- `%SystemRoot%`  


## Deprecated variables

The following variables are deprecated:

- **OSDAllowUnsignedDriver**: Isn't used when deploying Windows Vista and later operating systems
- **OSDBuildStorageDriverList**: Only applies to Windows XP and Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: Only needed when deploying Windows XP or Windows Server 2003
- **OSDInstallEditionIndex**: Not needed post-Windows Vista
- **OSDPreserveDriveLetter**: For more information, see [OSDPreserveDriveLetter](#osdpreservedriveletter)

### OSDPreserveDriveLetter

> [!Important]
> This task sequence variable is deprecated.
>
> During an OS deployment, by default, Windows Setup determines the best drive letter to use (typically C:).

*Previous behavior*: when applying an image, the OSDPreverveDriveLetter variable determines whether the task sequence uses the drive letter captured in the image file (WIM). Set the value for this variable to `false` to use the location that you specify for the **Destination** setting in the **Apply Operating System** task sequence step. For more information, see [Apply OS image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## See also

- [Task sequence steps](task-sequence-steps.md)
- [Using task sequence variables](using-task-sequence-variables.md)
- [Planning considerations for automating tasks](../plan-design/planning-considerations-for-automating-tasks.md)
