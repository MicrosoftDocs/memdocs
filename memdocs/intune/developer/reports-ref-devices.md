---
# required metadata
title: Devices - Intune Data Warehouse
titleSuffix: Microsoft Intune
description: Reference article for the Devices category of entity collections in the Intune Data Warehouse API.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: 6955E12D-70D7-4802-AE3B-8B276F01FA4F

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---

# Reference for devices entities

The **devices** category contains entities for mobile devices that track information such as:

- Device type
- Device enrollment and registration status
- Device ownership
- Device management state
- Device membership to Microsoft Entra status
- Enrollment status
- Historic information about the device
- Inventory of apps on the device

## deviceTypes

The **deviceTypes** entity represents the device type referenced by other data warehouse entities. The device type typically describes either the device model, manufacturer, or a combination of both.

| Property  | Description |
|---------|------------|
| deviceTypeID |Unique identifier of the device type |
| deviceTypeKey |Unique identifier of the device type in the data warehouse - surrogate key |
| deviceTypeName |Device type |

### Example

| deviceTypeID  | Name | Description |
|---------|------------|--------|
| 0 |Desktop |Windows Desktop device |
| 1 |WindowsRT |WindowsRT device |
| 2 |WinMO6 |Windows Mobile 6.0 device |
| 3 |Nokia |Nokia device |
| 4 |WindowsPhone |Windows Phone device |
| 5 |Mac |Mac device |
| 6 |WinCE |Windows CE device |
| 7 |WinEmbedded |Windows Embedded device |
| 8 |IPhone |iPhone device |
| 9 |IPad |iPad device |
| 10 |IPod |iPod device |
| 11 |Android |Android device-managed using Device Administrator |
| 12 |ISocConsumer |iSoc Consumer device |
| 14 |MacMDM |OS X device managed with the built-in MDM agent |
| 15 |HoloLens |HoloLens device |
| 16 |SurfaceHub |Surface Hub device |
| 17 |AndroidForWork |Android device-managed using Android Profile Owner |
| 100 |Blackberry |Blackberry Device |
| 101 |Palm |Palm device |
| 255 |Unknown |Unknown device type |

## enrollmentActivities 
The **enrollmentActivity** entity indicates the activity of a device enrollment.

| Property                      | Description                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | Key of the date when this enrollment activity was recorded.               |
| deviceEnrollmentTypeKey       | Key of the type of the enrollment.                                        |
| deviceTypeKey                 | Key of the type of device.                                                |
| enrollmentEventStatusKey      | Key of the status indicating the success or failure of the enrollment.    |
| enrollmentFailureCategoryKey  | Key of the enrollment failure category (if the enrollment failed).        |
| enrollmentFailureReasonKey    | Key of the enrollment failure reason (if the enrollment failed).          |
| osVersion                     | The operating system version of the device.                               |
| count                         | Total count of enrollment activities matching the classifications above.  |

## enrollmentEventStatuses 
The **enrollmentEventStatus** entity indicates the result of a device enrollment.

| Property                   | Description                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | Unique identifier of the enrollment status in the data warehouse (surrogate key)  |
| enrollmentEventStatusName  | The name of the enrollment status. See examples below.                            |

### Example

| enrollmentEventStatusName  | Description                            |
|----------------------------|----------------------------------------|
| Success                    | A successful device enrollment         |
| Failed                     | A failed device enrollment             |
| Not Available              | The enrollment status is unavailable.  |

## enrollmentFailureCategories 
The **EnrollmentFailureCategory** entity indicates why a device enrollment failed. 

| Property                       | Description                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| enrollmentFailureCategoryKey   | Unique identifier of the enrollment failure category in the data warehouse (surrogate key)  |
| enrollmentFailureCategoryName  | The name of the enrollment failure category. See examples below.                            |

### Example

| enrollmentFailureCategoryName   | Description                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| Not Applicable                  | The enrollment failure category isn't applicable.                                                            |
| Not Available                   | The enrollment failure category isn't available.                                                             |
| Unknown                         | Unknown error.                                                                                                |
| Authentication                  | Authentication failed.                                                                                        |
| Authorization                   | Call was authenticated, but not authorized to enroll.                                                         |
| AccountValidation               | Failed to validate the account for enrollment. (Account blocked, enrollment not enabled)                      |
| UserValidation                  | User couldn't be validated. (User doesn't exist, missing license)                                           |
| DeviceNotSupported              | Device isn't supported for mobile device management.                                                         |
| InMaintenance                   | Account is in maintenance.                                                                                    |
| BadRequest                      | Client sent a request that isn't understood/supported by the service.                                        |
| FeatureNotSupported             | Feature(s) used by this enrollment aren't supported for this account.                                        |
| EnrollmentRestrictionsEnforced  | Enrollment restrictions configured by admin blocked this enrollment.                                          |
| ClientDisconnected              | Client timed out or enrollment was aborted by end user.                                                        |
| UserAbandonment                 | Enrollment was abandoned by end user. (End user started onboarding but failed to complete it in timely manner)  |

## enrollmentFailureReasons  
The **EnrollmentFailureReason** entity indicates a more detailed reason for a device enrollment failure within a given failure category.  

| Property                     | Description                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| enrollmentFailureReasonKey   | Unique identifier of the enrollment failure reason in the data warehouse (surrogate key)  |
| enrollmentFailureReasonName  | The name of the enrollment failure reason. See examples below.                            |

### Example

| enrollmentFailureReasonName      | Description                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Not Applicable                   | The enrollment failure reason isn't applicable.                                                                                                                                                       |
| Not Available                    | The enrollment failure reason isn't available.                                                                                                                                                        |
| Unknown                          | Unknown Error.                                                                                                                                                                                         |
| UserNotLicensed                  | The user wasn't found in Intune or doesn't have a valid license.                                                                                                                                     |
| UserUnknown                      | User isn't known to Intune.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Only one user can enroll a device. This device was previously enrolled by another user.                                                                                                                |
| EnrollmentOnboardingIssue        | Intune mobile device management (MDM) authority isn't configured yet.                                                                                                                                 |
| AppleChallengeIssue              | The iOS management profile installation was delayed or failed.                                                                                                                                         |
| AppleOnboardingIssue             | An Apple MDM push certificate is required to enroll into Intune.                                                                                                                                       |
| DeviceCap                        | The user attempted to enroll more devices than maximum allowed.                                                                                                                                        |
| AuthenticationRequirementNotMet  | Intune enrollment service failed to authorize this request.                                                                                                                                            |
| UnsupportedDeviceType            | This device doesn't meet minimum requirements for Intune enrollment.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | This device failed to enroll due to a configured enrollment restriction rule.                                                                                                                          |
| BulkDeviceNotPreregistered       | This device's international mobile equipment identifier (IMEI) or serial number wasn't found.  Without this identifier, devices are recognized as personal-owned devices which are currently blocked.  |
| FeatureNotSupported              | The user was attempting to access a feature that isn't yet released for all customers or isn't compatible with your Intune configuration.                                                            |
| UserAbandonment                  | Enrollment was abandoned by end user. (End user started onboarding but failed to complete it in timely manner)                                                                                           |
| APNSCertificateExpired           | Apple devices can't be managed with an expired Apple MDM push certificate.                                                                                                                            |
## ownerTypes

The **ownerType** entity indicates whether a device is corporate, personally owned, or unknown.

| Property  | Description | Example |
|---------|------------|--------|
| ownerTypeID |Unique identifier of the owner type. | |
| ownerTypeKey |Unique identifier of the owner type in the data warehouse - surrogate key. | |
| ownerTypeName |Represents the owner type of the devices:  <br>Company - device is enterprise owned. <br>Personal - device is personally owned (BYOD).  <br>Unknown - no information on this device. |Company Personal Unknown |

> [!Note]  
> For the `ownerTypeName` in AzureAD when creating Dynamic Groups for devices, you need to set the filter value `deviceOwnership` as `Company`. For more information, see [Rules for devices](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## managementStates

The **managementStates** entity provides details on the state of the device. Detail can be useful in the cases where remote actions are applied, the device is jailbroken, or rooted.

| Property  | Description |
|---------|------------|
| managementStateID | Unique identifier of the management state. |
| managementStateKey | Unique identifier of the management state in the data warehouse - surrogate key. |
| managementStateName | Indicates the state of the remote action applied to this device. |

### Example

| managementStateID  | Name | Description |
|---------|------------|--------|
| 0 |Managed | Managed with no pending remote actions. |
| 1 |RetirePending | There's a retire command pending for the device. |
| 2 |RetireFailed | The retire command failed on the device. |
| 3 |WipePending | There's a wipe command pending for the device. |
| 4 |WipeFailed | The wipe command failed on the device. |
| 5 |Unhealthy | Unhealthy state. |
| 6 |DeletePending | There's a delete command pending for the device. |
| 7 |RetireIssued | A retire command has been issued to the device. |
| 8 |WipeIssued | A wipe command has been issued. |
| 9 |WipeCanceled | Wipe command has been canceled. |
| 10 |RetireCanceled | Retire command has been canceled. |
| 11 |Discovered | The device is newly discovered by Intune, once it checks in for the first time it moves to -Managed- state. |

## managementAgentTypes

The **ManagementAgentType** entity represents the agents used to manage a device.

| Property  | Description |
|---------|------------|
| managementAgentTypeID | Unique identifier of the management agent type. |
| managementAgentTypeKey | Unique identifier of the management agent type in the data warehouse - surrogate key. |
| managementAgentTypeName |Indicates what kind of agent is used to manage the device. |

### Example

| ManagementAgentTypeID  | Name | Description |
|---------|------------|--------|
| 1 |EAS | The device is managed through Exchange Active Sync. |
| 2 |MDM | The device is managed using an MDM agent. |
| 3 |EasMdm | The device is managed by both Exchange Active Sync and an MDM agent. |
| 4 |IntuneClient | The device is managed by the Intune PC agent. |
| 5 |EasIntuneClient | The device is managed by both Exchange Active Sync and the Intune PC agent. |
| 8 |ConfigManagerClient | The device is managed by the Configuration Manager agent. |
| 16 |Unknown | Unknown management agent type. |
| 2048 |IntuneAosp |  The device is managed by Intune's MDM for AOSP (Android Open Source Project) devices. |

## devices

The **devices** entity lists all enrolled devices under management and their corresponding properties.

|          Property          |                                                                                       Description                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| deviceKey                  | Unique   identifier of the device in the data warehouse - surrogate key.                                                                                                               |
| deviceId                   | Unique   identifier of the device.                                                                                                                                                     |
| deviceName                 | Name   of the device on platforms that allow naming a device. On other platforms,   Intune creates a name from other properties. This attribute can't be   available for all devices. |
| deviceTypeKey              | Key   of the device type attribute for this device.                                                                                                                                    |
| deviceRegistrationState    | Key   of the client registration state attribute for this device.                                                                                                                      |
| ownerTypeKey               | Key   of the owner type attribute for this device: corporate, personal, or unknown.                                                                                                    |
| enrolledDateTime           | Date   and time that this device was enrolled.                                                                                                                                         |
| lastSyncDateTime           | Last known device check-in with   Intune.                                                                                                                                              |
| managementAgentKey         | Key of the management agent   associated with this device.                                                                                                                             |
| managementStateKey         | Key of the management state   associated with this device, indicating latest state of a remote action or if   it was jailbroken/rooted.                                                |
| azureADDeviceId            | The   Azure deviceID for this device.                                                                                                                                                  |
| azureADRegistered          | Whether the device is Microsoft Entra registered.                                                                                                                             |
| deviceCategoryKey          | Key of the category associated   with this device.                                                                                                                                     |
| deviceEnrollmentType       | Key of the enrollment type   associated with this device, indicating method of enrollment.                                                                                             |
| complianceStateKey         | Key of the Compliance state   associated with this device.                                                                                                                             |
| osVersion                  | Operating system version of the device.                                                                                                                                                |
| easDeviceId                | Exchange ActiveSync ID of the device.                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Unique Identifier for the user   associated with the device.                                                                                                                           |
| rowLastModifiedDateTimeUTC | Date and time in UTC when this   device was last modified in the data warehouse.                                                                                                       |
| manufacturer               | Manufacturer of the device                                                                                                                                                             |
| model                      | Model of the device                                                                                                                                                                    |
| operatingSystem            | Operating system of the device. Windows, iOS/iPadOS,   etc.                                                                                                                                   |
| isDeleted                  | Binary   to show whether the device is deleted or not.                                                                                                                                 |
| androidSecurityPatchLevel  | Android security patch level                                                                                                                                                           |
| MEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Device supervised status                                                                                                                                                               |
| freeStorageSpaceInBytes    | Free Storage in Bytes.                                                                                                                                                                 |
| totalStorageSpaceInBytes   | Total Storage in Bytes.                                                                                                                                                                |
| encryptionState            | Encryption state on the   device.                                                                                                                                                      |
| subscriberCarrier          | Subscriber carrier of the device                                                                                                                                                       |
| phoneNumber                | Phone number of the device                                                                                                                                                             |
| IMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Cellular technology of the   device                                                                                                                                                    |
| WiFiMacAddress             | Wi-Fi MAC                                                                                                                                                                              |
| ICCD                       | Integrated Circuit Card Identifier                                                                                                                                                     |
| windowsOsEdition           | Windows Operating System edition.                                                                                                                             |
| ethernetMacAddress           | The unique network identifier of this device.                                                                                                                                        |
| model                      | The device model.                                                                                                                                                                      |
| office365Version           | The version of Microsoft 365 that is installed on the device. `Office365Version` is only collected when the Intune management extension agent is installed on a Windows machine. The admin must also create and assign a PowerShell or Win32 App for the agent to be installed. For more information, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md) and [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).<p>**NOTE**:<br>There's a known issue with the Intune Data Warehouse **devices** table. The `office365Version` property for the device record may be null. This property is currently under maintenance and may be subject to deprecation. Therefore, you should consider not using this property value for reporting purposes.                                                                                                                               |
| SubnetAddressV4Wifi           | The subnet address for IPV4 Wifi connection.                                                                                                                             |
| IpAddressV4Wifi           | The IP address for IPV4 Wifi connection.                                                                                                                             |

> [!NOTE]
> For more information about Windows SKU enum values,  see [Device properties](../fundamentals/filters-device-properties.md#managed-device-properties).

## devicePropertyHistories

The **devicePropertyHistory** entity has the same properties as the devices table and daily snapshots of each device record per day for the past 60 days. The DateKey column indicates the day for each row.

|          Property          |                                                                                      Description                                                                                     |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dateKey                    | Reference to date table indicating the day.                                                                                                                                          |
| deviceKey                  | Unique identifier of the device in the data warehouse -  surrogate key. This is a reference to the Device table that contains the   Intune device ID.                               |
| deviceName                 | Name of the device on platforms that allow naming a   device. On other platforms, Intune creates a name from other properties. This   attribute can't be available for all devices. |
| deviceRegistrationStateKey | Key of the device registration state attribute for this   device.                                                                                                                    |
| ownerTypeKey               | Key of the owner type attribute for this device:   corporate, personal, or unknown.                                                                                                  |
| managementStateKey         | Key of the management state associated with this device,   indicating latest state of a remote action or if it was jailbroken/rooted.                                                |
| azureADRegistered          | Whether the device is Microsoft Entra registered.                                                                                                                             |
| complianceStateKey         | A key to ComplianceState.                                                                                                                                                            |
| OSVersion                  | OS version.                                                                                                                                                                          |
| jailBroken                 | Whether the device is jail broken or rooted.                                                                                                                                         |
| deviceCategoryKey          | Key of device category attribute for this device. 
| physicalMemoryInBytes      | The physical memory in bytes.                                                                                                                                                          |
| totalStorageSpaceInBytes   | Total storage capacity in bytes.                                                                                                                                                                |
