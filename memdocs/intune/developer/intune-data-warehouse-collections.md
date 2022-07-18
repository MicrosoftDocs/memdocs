---
# required metadata
title:  Intune Data Warehouse Collections
titleSuffix: Microsoft Intune 
description: The Intune Data Warehouse collections provide details related to the Data Warehouse API.
keywords: 
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 29f09230-dc56-43db-b599-d961967bda49

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune
ms.collection: M365-identity-device-management
---

# Intune Data Warehouse Collections

The following Intune Data Warehouse collections provides the properties, descriptions, and examples for v1.0 collections of the Data Warehouse API entities. 

## appRevisions
The **appRevision** entity lists all the versions of apps.

|          Property          |                                      Description                                      |                Example               |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------|
| appKey                     | Unique identifier of the App.                                                         | 123                                  |
| applicationId              | Unique identifier of the App -   similar to AppKey, but this key is a natural.        | b66bc706-ffff-7437-0340-032819502773 |
| revision                   | The version as mentioned by admin   during uploading of the binary.                   | 2                                    |
| title                      | Title of the app.                                                                     | Excel                                |
| publisher                  | Publisher of the app.                                                                 | Microsoft                            |
| uploadState                | Upload state of the app.                                                              | 1                                    |
| appTypeKey                 | Reference to AppType described in   the following section.                            | 1                                    |
| vppProgramTypeKey          | Reference to VppProgramType   described below.                                        | 30876                                |
| creationTime               | The time when this revision was   created.                                            | 11/23/2016 0:00                      |
| modifiedTime               | Last time anything related to this   revision was changed.                            | 11/23/2016 0:00                      |
| size                       | Size of the binary in bytes.                                                          | 120,392,000                          |
| startDateInclusiveUTC      | Date and time in UTC when this App   revision was created in the data warehouse.      | 11/23/2016 0:00                      |
| endDateExclusiveUTC        | Date and time in UTC when this app   revision became obsolete.                        | 11/23/2016 0:00                      |
| isCurrent                  | Indicates whether this App version   is current or not in the data warehouse.         | True/False                           |
| rowLastModifiedDateTimeUTC | Date and time in UTC when this app   version was last modified in the data warehouse. | 11/23/2016 0:00                      |

## appTypes
The **appType** entity lists the installation source of an app.

> [!NOTE]
> Win32 apps are not included in the Intune Data Warehouse.


|   Property  |        Description        |
|-------------|---------------------------|
| appTypeID   | ID for the type           |
| appTypeKey  | Surrogate key for the key |
| appTypeName | App type                  |

### Example

| AppTypeID |                Name               |                     Description                     |
|-----------|-----------------------------------|-----------------------------------------------------|
| 0         | Android   store app               | An   Android store app.                             |
| 1         | Android   LOB app                 | An   Android line-of-business app.                  |
| 2         | Managed   Android store app (MAM) | An   Android store app that has management enabled. |
| 3         | iOS   store app                   | An   iOS store app.                                 |
| 4         | iOS   LOB app                     | An   iOS line-of-business app.                      |
| 5         | Managed   iOS store app (MAM)     | An   iOSstore app that is management enabled.       |
| 6         | Microsoft 365 Apps for enterprise        | The   Microsoft 365 Apps for Windows 10.     |
| 7         | Web   app                         | A   web app.                                        |
| 8         | Windows   Phone 8.1 store app     | A   Windows phone 8.1 store app.                    |
| 9         | Windows   store app               | A   Windows store app.                              |
| 10        | Windows   LOB apps                | A   Windows AppX line-of-business app.              |
| 11        | Windows   Mobile MSI              | An   MSI line-of-business app.                      |
| 12        | Windows   Phone LOB app           | A   Windows phone line-of-business app.             |

## compliancePolicyStatusDeviceActivities
The following table summarizes the assignment status of compliance policies to devices. It lists the count of devices found in each compliance state.

|    Property   |                                                                                      Description                                                                                     |  Example |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey       | Date   key when the summary was created for the compliance policy.                                                                                                                   | 20161204 |
| unknown       | Number   of devices that are offline or failed to communicate with Intune or Azure AD   for other reasons.                                                                           | 5        |
| notApplicable | Number   of devices where device compliance policies targeted by the admin are not   applicable.                                                                                     | 201      |
| compliant     | Number   of devices that successfully applied one or more device compliance policies   targeted by the admin.                                                                        | 4083     |
| inGracePeriod | Number   of devices that are not compliant but that are in the grace-period defined by   the admin.                                                                                  | 57       |
| nonCompliant  | Number   of devices that failed to apply one or more device compliance policies   targeted by the admin or where the user hasn't complied with the policies   targeted by the admin. | 43       |
|    error      |    Number of   devices that failed to communicate with Intune or Azure AD, and returned an   error message.                                                                          |    3     |

## compliancePolicyStatusDevicePerPolicyActivities
The following table summarizes the assignment status of compliance policies to devices on a per policy and a per policy type basis. It lists the count of devices found in each compliance state for each assigned compliance policy.

|      Property     |                                                                                      Description                                                                                     |  Example |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey           | Date   key when the summary was created for the compliance policy.                                                                                                                   | 20161219 |
| policyKey         | Key   for the compliance policy for which the summary was created.                                                                                                                   | 10178    |
| policyPlatformKey | Key   for the platform type of the compliance policy for which the summary was   created.                                                                                            | 5        |
| unknown           | Number   of devices that are offline or failed to communicate with Intune or Azure AD   for other reasons.                                                                           | 13       |
| notApplicable     | Number   of devices where device compliance policies targeted by the admin are not   applicable.                                                                                     | 3        |
| compliant         | Number   of devices that successfully applied one or more device compliance policies   targeted by the admin.                                                                        | 45       |
| inGracePeriod     | Number   of devices that are not compliant but that are in the grace-period defined by   the admin.                                                                                  | 3        |
| nonCompliant      | Number   of devices that failed to apply one or more device compliance policies   targeted by the admin or where the user hasn't complied with the policies   targeted by the admin. | 7        |
| error             | Number   of devices that failed to communicate with Intune or Azure AD, and returned   an error message.                                                                             | 3        |
## complianceStates

|      Property      |                       Description                      |
|--------------------|--------------------------------------------------------|
| complianceStatus   | Compliance status of devices with   mdmStatusKey       |
| complianceStateKey | Compliance key to match device and   compliance status |
| complianceStateID  | The ID to match this compliance   state                |

### Example

|  complianceStatus  |                       Description                      |
|--------------------|--------------------------------------------------------|
|    Unknown         |    Unknown.                                                                        |
|    Compliant       |    Compliant.                                                                      |
|    Noncompliant    |       Device is non-compliant and is blocked from corporate resources.             |
|    Conflict        |    Conflict with other rules.                                                      |
|    Error           |       Error.                                                                       |
|    ConfigManager   |    Managed by Config Manager.                                                      |
|    InGracePeriod   |       Device is non-compliant but still has access to corporate resources          |

## dates
The **date** entity represents dates that are referenced across multiple data warehouse entities.

|     Property    |                       Description                      |    Example    |
|-----------------|--------------------------------------------------------|---------------|
| dateKey         | Unique identifier for this date in the data warehouse. | 20160703      |
| fullDate        | This date represented in full Date/Time format.        | 7/3/2016 0:00 |
| dayOfWeek       | Day of week                                            | 1             |
| dayOfMonth      | Day of month                                           | 3             |
| dayOfYear       | Day of year                                            | 185           |
| weekOfYear      | Week of year                                           | 28            |
| monthOfYear     | Month of the year                                      | 7             |
| calendarQuarter | Calendar quarter                                       | 3             |
| calendarYear    | Calendar year                                          | 2016          |
| dateKey         | Unique identifier for this date in the data warehouse. | 20160703      |
| fullDate        | This date represented in full Date/Time format.        | 7/3/2016 0:00 |
| dayOfWeek       | Day of week                                            | 1             |
| dayOfMonth      | Day of month                                           | 3             |
| dayOfYear       | Day of year                                            | 185           |
| weekOfYear      | Week of year                                           | 28            |
| monthOfYear     | Month of the year                                      | 7             |
| calendarQuarter | Calendar quarter                                       | 3             |
| calendarYear    | Calendar year                                          | 2016          |

## deviceCategories

|      Property      |                                    Description                                   |                Example               |
|--------------------|----------------------------------------------------------------------------------|--------------------------------------|
| deviceCategoryID   | Unique identifier for the device category.                                       | fb415ba2-7c08-41f6-a5e5-685b50da2c4c |
| deviceCategoryKey  | Unique identifier of the device category in the data   warehouse - surrogate key | 1                                    |
| deviceCategoryName | Display name for the device category.                                            | Smartphones                          |

## deviceConfigurationProfileDeviceActivities
The **DeviceConfigurationProfileDeviceActivity** entity lists the number of devices in the succeeded, pending, failed, or error state per day. The number reflects the Device configuration profiles assigned to the entity. For example, if a device is in the succeeded state for all its assigned policies, it increments the succeeded counter up one for that day. If a device has two profiles assigned to it, one in the succeeded state and another in an error state, the entity increments the Succeeded counter and place the device in the error state. The entity lists how many devices are in which state on a given day over the last 30 days.

|  Property |                                          Description                                          |  Example |
|-----------|-----------------------------------------------------------------------------------------------|----------|
| dateKey   | Date Key when the Device Configuration Profile check-in   was recorded in the data warehouse. | 20160703 |
| pending   | Number of unique Devices in pending state.                                                    | 123      |
| succeeded | Number of unique Devices in success state.                                                    | 12       |
| error     | Number of unique Devices in error state.                                                      | 10       |
| failed    | Number of unique Devices in failed state.                                                     | 2        |

## deviceConfigurationProfileUserActivities 
The **DeviceConfigurationProfileUserActivity** entity lists the number of users in the succeeded, pending, failed, or error state per day. The number reflects the Device configuration profiles assigned to the entity. For example, if a user is in the succeeded state for all their assigned policies, it moves up the succeeded counter by one for that day. If a user has two profiles assigned to them, one in the succeeded state and the other is in an error state, the user in the error state is counted. The **DeviceConfigurationProfileUserActivity** entity lists how many users are in which state on a given day over the last 30 days. 

| Property  | Description  | Example  |
|------------|----------------------------------------------------------------------------------------------|-----------|
| dateKey  | Date Key when the Device Configuration Profile check-in was recorded in the data warehouse.  | 20160703  |
| pending  | Number of unique Users in pending state.  | 123  |
| succeeded  | Number of unique Users in success state.  | 12  |
| error  | Number of unique Users in error state.  | 10  |
| failed  | Number of unique Users in failed state.  | 2  |

## devicePropertyHistories

|          Property          |                                                                                      Description                                                                                     |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dateKey                    | Reference to date table indicating the day.                                                                                                                                          |
| deviceKey                  | Unique identifier of the device in the data warehouse -   surrogate key. This is a reference to the Device table that contains the   Intune device ID.                               |
| deviceName                 | Name of the device on platforms that allow naming a   device. On other platforms, Intune creates a name from other properties. This   attribute cannot be available for all devices. |
| deviceRegistrationStateKey | Key of the device registration state attribute for this   device.                                                                                                                    |
| ownerTypeKey               | Key of the owner type attribute for this device:   corporate, personal, or unknown.                                                                                                  |
| managementStateKey         | Key of the management state associated with this device,   indicating latest state of a remote action or if it was jailbroken/rooted.                                                |
| azureADRegistered          | Whether the device is Azure Active Directory registered.                                                                                                                             |
| complianceStateKey         | A key to ComplianceState.                                                                                                                                                            |
| oSVersion                  | OS version.                                                                                                                                                                          |
| jailBroken                 | Whether the device is jail broken or rooted.                                                                                                                                         |
| deviceCategoryKey          | Key of device category attribute for this device.                                                                                                                                    |
| physicalMemoryInBytes      | The physical memory in bytes.                                                                                                                                    |
| totalStorageSpaceInBytes      | Total storage capacity in bytes.                                                                                                                                    |


## deviceRegistrationStates
The **DeviceRegistrationState** entity represents the registration type referenced by other data warehouse collections. 

|           Property          |                                     Description                                     |
|-----------------------------|-------------------------------------------------------------------------------------|
| deviceRegistrationStateID   | Unique identifier for registration state                                            |
| deviceRegistrationStateKey  | Unique identifier of the registration state in the data   warehouse - surrogate key |
| deviceRegistrationStateName | Registration state                                                                  |
|    notRegistered                     |    Not registered                                                                                                                                                                  |
|    registered                        |       Registered                                                                                                                                                                   |
|    revoked                           |       State means the IT administrator has blocked the client, and the client can   be unblocked. A device can also be in the Revoked state after it is wiped or   retired.        |
|    keyConflict                       |    Key conflict                                                                                                                                                                    |
|    approvalPending                   |    Approval pending                                                                                                                                                                |
|    certificateReset                  |    Reset certificate                                                                                                                                                               |
|    notRegisteredPendingEnrollment    |    Not registered pending enrollment                                                                                                                                               |
|    unknown                           |    Unknown state                                                                                                                                                                   |

## devices
The **device** entity lists all enrolled devices under management and their corresponding properties.

|          Property          |                                                                                       Description                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| deviceKey                  | Unique   identifier of the device in the data warehouse - surrogate key.                                                                                                               |
| deviceId                   | Unique   identifier of the device.                                                                                                                                                     |
| deviceName                 | Name   of the device on platforms that allow naming a device. On other platforms,   Intune creates a name from other properties. This attribute cannot be   available for all devices. |
| deviceTypeKey              | Key   of the device type attribute for this device.                                                                                                                                    |
| deviceRegistrationState    | Key   of the client registration state attribute for this device.                                                                                                                      |
| ownerTypeKey               | Key   of the owner type attribute for this device: corporate, personal, or unknown.                                                                                                    |
| enrolledDateTime           | Date   and time that this device was enrolled.                                                                                                                                         |
| ethernetMacAddress           | The unique network identifier of this device.                                                                                                                                         |
| lastSyncDateTime           | Last known device check-in with   Intune.                                                                                                                                              |
| managementAgentKey         | Key of the management agent   associated with this device.                                                                                                                             |
| managementStateKey         | Key of the management state   associated with this device, indicating latest state of a remote action or if   it was jailbroken/rooted.                                                |
| azureADDeviceId            | The   Azure deviceID for this device.                                                                                                                                                  |
| azureADRegistered          | Whether the device is Azure Active   Directory registered.                                                                                                                             |
| deviceCategoryKey          | Key of the category associated   with this device.                                                                                                                                     |
| deviceEnrollmentType       | Key of the enrollment type   associated with this device, indicating method of enrollment.                                                                                             |
| complianceStateKey         | Key of the Compliance state   associated with this device.                                                                                                                             |
| office365Version           | The version of Microsoft 365 that is installed on the device.                                                                                                                             |
| oSVersion                  | Operating system version of the device.                                                                                                                                                |
| easDeviceId                | Exchange ActiveSync ID of the device.                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | Unique Identifier for the user   associated with the device.                                                                                                                           |
| rowLastModifiedDateTimeUTC | Date and time in UTC when this   device was last modified in the data warehouse.                                                                                                       |
| manufacturer               | Manufacturer of the device                                                                                                                                                             |
| model                      | Model of the device                                                                                                                                                                    |
| operatingSystem            | Operating system of the device. Windows, iOS/iPadOS,   etc.                                                                                                                                   |
| isDeleted                  | Binary   to show whether the device is deleted or not.                                                                                                                                 |
| androidSecurityPatchLevel  | Android security patch level                                                                                                                                                           |
| mEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | Device supervised status                                                                                                                                                               |
| freeStorageSpaceInBytes    | Free Storage in bytes.                                                                                                                                                                 |
| encryptionState            | Encryption state on the   device.                                                                                                                                                      |
| subscriberCarrier          | Subscriber carrier of the device                                                                                                                                                       |
| phoneNumber                | Phone number of the device                                                                                                                                                             |
| iMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | Cellular technology of the   device.                                                                                                                                                    |
| wiFiMacAddress             | Wi-Fi MAC.                                                                                                                                                                              |
| windowsOsEdition             | Windows Operating System edition.                                                                                                                                                                              |

> [!NOTE]
> For more information about Windows SKU enum values,  see [Device properties](../fundamentals/filters-device-properties.md#device-properties).

## deviceTypes
The **deviceType** entity represents the device type referenced by other data warehouse entities. The device type typically describes either the device model, manufacturer, or a combination of both.

|    Property    |                                  Description                                 |
|----------------|------------------------------------------------------------------------------|
| deviceTypeID   | Unique   identifier of the device type                                       |
| deviceTypeKey  | Unique   identifier of the device type in the data warehouse - surrogate key |
| deviceTypeName | Device   type                                                                |

### Example

| deviceTypeID |        Name       |                      Description                      |
|--------------|-------------------|-------------------------------------------------------|
| -1           | Not   Available   | The   device type is unavailable.                     |
| 0            | Desktop           | Windows   Desktop device                              |
| 1            | Windows           | Windows   device                                      |
| 2            | WinMO6            | Windows   Mobile 6.0 device                           |
| 3            | Nokia             | Nokia   device                                        |
| 4            | WindowsPhone      | Windows   Phone device                                |
| 5            | Mac               | Mac   device                                          |
| 6            | WinCE             | Windows   CE device                                   |
| 7            | WinEmbedded       | Windows   Embedded device                             |
| 8            | IPhone            | iPhone   device                                       |
| 9            | IPad              | iPad   device                                         |
| 10           | IPod              | iPod   device                                         |
| 11           | Android           | Android   device-managed using Device Administrator   |
| 12           | ISocConsumer      | iSoc   Consumer device                                |
| 13           | Unix              | Unix   Device                                         |
| 14           | MacMDM            | OS X device managed with the built-in MDM agent |
| 15           | HoloLens          | HoloLens device                                       |
| 16           | SurfaceHub        | Surface   Hub device                                  |
| 17           | AndroidForWork    | Android   device-managed using Android Profile Owner  |
| 18           | AndroidEnterprise | Android   enterprise device.                          |
| 100          | Blackberry        | Blackberry   Device                                   |
| 101          | Palm              | Palm   device                                         |
| 255          | Unknown           | Unknown   device type                                 |

## deviceEnrollmentTypes
The **deviceEnrollmentType** entity indicates how a device was enrolled. The enrollment type captures the method of enrollment. Examples list the different enrollment types and what they mean.

|         Property         |                                    Description                                    |
|--------------------------|-----------------------------------------------------------------------------------|
| deviceEnrollmentTypeID   | Unique   identifier of the enrollment type.                                       |
| deviceEnrollmentTypeKey  | Unique   identifier of the enrollment type in the data warehouse - surrogate key. |
| deviceEnrollmentTypeName | Enrollment   type name.                                                           |

### Example

| enrollmentTypeID |                Name                |                                        Description                                       |
|------------------|------------------------------------|------------------------------------------------------------------------------------------|
| 0                | Unknown                            | Enrollment   type was not collected                                                      |
| 1                | UserEnrollment                     | User driven enrollment through   BYOD channel.                                           |
| 2                | DeviceEnrollmentManager            | User enrollment with a device   enrollment manager account.                              |
| 3                | AppleBulkWithUser                  | Apple bulk enrollment with user   challenge. (DEP, Apple Configurator)                   |
| 4                | AppleBulkWithoutUser               | Apple bulk enrollment without user challenge.   (DEP, Apple Configurator, Mobile Config) |
| 5                | WindowsAzureADJoin                 | Windows 10 Azure AD Join.                                                                |
| 6                | WindowsBulkUserless                | Windows 10 Bulk enrollment through   ICD with certificate.                               |
| 7                | WindowsAutoEnrollment              | Windows 10 automatic enrollment.   (Add work account)                                    |
| 8                | WindowsBulkAzureDomainJoin         | Windows 10 bulk Azure AD Join.                                                           |
| 9                | WindowsCoManagement                | Windows 10 co-management triggered   by Autopilot or Group Policy.                       |
| 10               | WindowsAzureADJoinsUsingDeviceAuth | Windows 10 Azure AD Join using   Device Auth.                                            |

## enrollmentActivities 
The **EnrollmentActivity** entity indicates the activity of a device enrollment.

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
The **EnrollmentEventStatus** entity indicates the result of a device enrollment.

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
| Not Applicable                  | The enrollment failure category is not applicable.                                                            |
| Not Available                   | The enrollment failure category is not available.                                                             |
| Unknown                         | Unknown error.                                                                                                |
| Authentication                  | Authentication failed.                                                                                        |
| Authorization                   | Call was authenticated, but not authorized to enroll.                                                         |
| AccountValidation               | Failed to validate the account for enrollment. (Account blocked, enrollment not enabled)                      |
| UserValidation                  | User could not be validated. (User does not exist, missing license)                                           |
| DeviceNotSupported              | Device is not supported for mobile device management.                                                         |
| InMaintenance                   | Account is in maintenance.                                                                                    |
| BadRequest                      | Client sent a request that is not understood/supported by the service.                                        |
| FeatureNotSupported             | Feature(s) used by this enrollment are not supported for this account.                                        |
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
| Not Applicable                   | The enrollment failure reason is not applicable.                                                                                                                                                       |
| Not Available                    | The enrollment failure reason is not available.                                                                                                                                                        |
| Unknown                          | Unknown Error.                                                                                                                                                                                         |
| UserNotLicensed                  | The user was not found in Intune or does not have a valid license.                                                                                                                                     |
| UserUnknown                      | User is not known to Intune.                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | Only one user can enroll a device. This device was previously enrolled by another user.                                                                                                                |
| EnrollmentOnboardingIssue        | Intune mobile device management (MDM) authority is not configured yet.                                                                                                                                 |
| AppleChallengeIssue              | The iOS management profile installation was delayed or failed.                                                                                                                                         |
| AppleOnboardingIssue             | An Apple MDM push certificate is required to enroll into Intune.                                                                                                                                       |
| DeviceCap                        | The user attempted to enroll more devices than maximum allowed.                                                                                                                                        |
| AuthenticationRequirementNotMet  | Intune enrollment service failed to authorize this request.                                                                                                                                            |
| UnsupportedDeviceType            | This device does not meet minimum requirements for Intune enrollment.                                                                                                                                  |
| EnrollmentCriteriaNotMet         | This device failed to enroll due to a configured enrollment restriction rule.                                                                                                                          |
| BulkDeviceNotPreregistered       | This device's international mobile equipment identifier (IMEI) or serial number wasn't found.  Without this identifier, devices are recognized as personal-owned devices which are currently blocked.  |
| FeatureNotSupported              | The user was attempting to access a feature that is not yet released for all customers or is not compatible with your Intune configuration.                                                            |
| UserAbandonment                  | Enrollment was abandoned by end user. (End user started onboarding but failed to complete it in timely manner)                                                                                           |
| APNSCertificateExpired           | Apple devices cannot be managed with an expired Apple MDM push certificate.                                                                                                                            |

## intuneManagementExtensions
The **intuneManagementExtension** lists the **intuneManagementExtension** health on each Windows 10 device per day. The data is retained for the last 60 days.

|       Property      |                          Description                          | Example |
|---------------------|---------------------------------------------------------------|---------|
| dateKey             | Unique identifier of the Date.                                | 123     |
| tenantKey           | Unique identifier of the Tenant.                              | 456     |
| deviceKey           | Unique identifier of the Device.                              | 789     |
| extensionVersionKey | Unique identifier of the IntuneManagementExtension   version. | 1       |
| extensionStateKey   | Unique identifier of health state.                            | 2       |

## intuneManagementExtensionHealthStates
The **IntuneManagementExtensionHealthState** lists all possible health states of the **IntuneManagementExtension**.

|      Property     |                   Description                  | Example |
|-------------------|------------------------------------------------|---------|
| extensionStateKey | Unique   identifier of health state.           | 2       |
| extensionState    | Health   state of a IntuneManagementExtension. | Healthy |

## intuneManagementExtensionVersions
The **IntuneManagementExtensionVersion** entity lists all the versions used by **IntuneManagementExtension**.

|       Property      |                          Description                          | Example |
|---------------------|---------------------------------------------------------------|---------|
| extensionVersionKey | Unique identifier of the IntuneManagementExtension   version. | 1       |
| extensionVersion    | The 4 digit version number.                                   | 1.0.2.0 |

## MamApplications

The **MamApplication** entity lists Line-of-Business (LOB) apps that are managed through Mobile Application Management (MAM) without enrollment in your enterprise.

| Property | Description | Example |
|---------|------------|--------|
| mamApplicationKey |Unique identifier of the MAM application. | 432 |
| mamApplicationName |Name of the MAM application. |MAM Application Example Name |
| mamApplicationId |Application ID of the MAM application. | 123 |
| isDeleted |Indicates whether this MAM app record has been updated. <br>True- MAM app has a new record with updated fields in this table. <br>False- the latest record for this MAM app. |True/False |
| startDateInclusiveUTC |Date and time in UTC when this MAM app was created in the data warehouse. |11/23/2016 12:00:00 AM |
| deletedDateUTC |Date and time in UTC when IsDeleted changed to True. |11/23/2016 12:00:00 AM |
| rowLastModifiedDateTimeUTC |Date and time in UTC when this MAM app was last modified in the data warehouse. |11/23/2016 12:00:00 AM |


## MamApplicationInstances

The **MamApplicationInstance** entity lists managed Mobile Application Management (MAM) apps as singular instances per user per device. All users and devices listed with in the entity are protected, as in, they have at least one MAM Policy assigned to them.


|          Property          |                                                                                                  Description                                                                                                  |               Example                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   applicationInstanceKey   |                                                               Unique identifier of the MAM app instance in the data warehouse - surrogate key.                                                                |                 123                  |
|           userId           |                                                                              User ID of the user who has this MAM app installed.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              Unique identifier of the MAM app instance - similar to ApplicationInstanceKey, but the identifier is a natural key.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Application ID of the Mam Application for which this Mam Application Instance was created.   | 11/23/2016 12:00:00 AM   |
|     applicationVersion     |                                                                                     Application version of this MAM app.                                                                                      |                  2                   |
|        createdDate         |                                                                 Date when this record of the MAM app instance was created. Value can be null.                                                                 |        11/23/2016 12:00:00 AM        |
|          platform          |                                                                          Platform of the device on which this MAM app is installed.                                                                           |                  2                   |
|      platformVersion       |                                                                      Platform version of the device on which this MAM app is installed.                                                                       |                 2.2                  |
|         sdkVersion         |                                                                            The MAM SDK version that this MAM app was wrapped with.                                                                            |                 3.2                  |
| mamDeviceId | Device ID of the device with which MAM Application Instance is associated with.   | 11/23/2016 12:00:00 AM   |
| mamDeviceType | Device type of the device with which MAM Application Instance is associated with.   | 11/23/2016 12:00:00 AM   |
| mamDeviceName | Device name of the device with which MAM Application Instance is associated with.   | 11/23/2016 12:00:00 AM   |
|         isDeleted          | Indicates whether this MAM app instance record has been updated. <br>True- this MAM app instance has a new record with updated fields in this table. <br>False - the latest record for this MAM app instance. |              True/False              |
|   startDateInclusiveUtc    |                                                              Date and time in UTC when this MAM app instance was created in the data warehouse.                                                               |        11/23/2016 12:00:00 AM        |
|       deletedDateUtc       |                                                                             Date and time in UTC when IsDeleted changed to True.                                                                              |        11/23/2016 12:00:00 AM        |
| rowLastModifiedDateTimeUtc |                                                           Date and time in UTC when this MAM app instance was last modified in the data warehouse.                                                            |        11/23/2016 12:00:00 AM        |

## MamCheckins

The **MamCheckin** entity represents data gathered when a Mobile Application Management (MAM) app instance has checked in with the Intune Service. 

> [!Note]  
> When an app instance checks in multiple times a day, the data warehouse stores it as single check-in.

| Property | Description | Example |
|---------|------------|--------|
| dateKey |Date Key when the MAM app check-in was recorded in the data warehouse. | 20160703 |
| applicationInstanceKey |Key of the app instance associated with this MAM app check-in. | 123 |
| userKey |Key of the user associated with this MAM app check-in. | 4323 |
| mamApplicationKey |Application Key of Application associated with MAM Application check in. | 432 |
| deviceHealthKey |Key of DeviceHealth associated with this MAM app check-in. | 321 |
| platformKey |Represents the platform of the device associated with this MAM app check-in. |123 |
| lastCheckInDate |Date and time when this MAM app last checked in. Value can be null. |11/23/2016 12:00:00 AM |

## MamDeviceHealths

The **MamDeviceHealth** entity represents devices that have Mobile Application Management (MAM) policies deployed to them even if they are jailbroken.

| Property | Description | Example |
|---------|------------|--------|
| deviceHealthKey |Unique identifier of the device and its associated health in the data warehouse - surrogate key. |123 |
| deviceHealth |Unique identifier of the device and its associated health - similar to DeviceHealthKey, but the identifier is a natural key. |b66bc706-ffff-7777-0340-032819502773 |
| deviceHealthName |Represents the status of the device. <br>Not available - no information on this device. <br>Healthy - device is not jailbroken. <br>Unhealthy - device is jailbroken. |Not Available Healthy Unhealthy |
| rowLastModifiedDateTimeUtc |Date and time in UTC when this specific MAM Device Health was last modified in the data warehouse. |11/23/2016 12:00:00 AM |

## MamPlatforms

The **MamPlatform** entity lists platform names and types on which a Mobile Application Management (MAM) app was installed.


|          Property          |                                    Description                                    |                         Example                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        platformKey         |     Unique identifier of the platform in the data warehouse - surrogate key.      |                           123                           |
|          platform          | Unique identifier of the platform - similar to PlatformKey, but is a natural key. |                           123                           |
|        platformName        |                                   Platform name                                   | Not Available <br>None <br>Windows <br>IOS <br>Android. |
| rowLastModifiedDateTimeUtc | Date and time in UTC when this platform was last modified in the data warehouse.  |                 11/23/2016 12:00:00 AM                  |

## managementAgentTypes
The **managementAgentType** entity represents the agents used to manage a device.

|         Property        |                                       Description                                       |
|-------------------------|-----------------------------------------------------------------------------------------|
| managementAgentTypeID   | Unique identifier of the management agent type.                                         |
| managementAgentTypeKey  | Unique identifier of the management agent type in the data   warehouse - surrogate key. |
| managementAgentTypeName | Indicates what kind of agent is used to manage the device.                              |

### Example

| ManagementAgentTypeID |                Name               |                                  Description                                 |
|-----------------------|-----------------------------------|------------------------------------------------------------------------------|
| 1                     | EAS                               | The   device is managed through Exchange Active Sync                         |
| 2                     | MDM                               | The   device is managed using an MDM agent                                   |
| 3                     | EasMdm                            | The   device is managed by both Exchange Active Sync and an MDM agent        |
| 4                     | IntuneClient                      | The   device is managed by the Intune PC agent                               |
| 5                     | EasIntuneClient                   | The   device is managed by both Exchange Active Sync and the Intune PC agent |
| 8                     | ConfigManagerClient               | The   device is managed by the Configuration Manager agent     |
| 10                    | ConfigurationManagerClientMdm     | The device is managed by   Configuration Manager and MDM.                    |
| 11                    | ConfigurationManagerCLientMdmEas  | The device is managed by   Configuration Manager, MDM and Exchange Active Sync.               |
| 16                    | Unknown                           | Unknown   management agent type                                              |
| 64                    | GoogleCloudDevicePolicyController |  The device is managed by Google's CloudDPC.                                 |

## managementStates
The **ManagementState** entity provides details on the state of the device. Detail can be useful in the cases where remote actions are applied, the device is jailbroken, or rooted.

|       Property      |                                     Description                                    |
|---------------------|------------------------------------------------------------------------------------|
| managementStateID   | Unique   identifier of the management state.                                       |
| managementStateKey  | Unique   identifier of the management state in the data warehouse - surrogate key. |
| managementStateName | Indicates   the state of the remote action applied to this device.                 |

### Example

| managementStateID |      Name      |                                                   Description                                                   |
|-------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| 0                 | Managed        | Managed   with no pending remote actions.                                                                       |
| 1                 | RetirePending  | There   is a retire command pending for the device.                                                             |
| 2                 | RetireFailed   | The   retire command failed on the device.                                                                      |
| 3                 | WipePending    | There   is a wipe command pending for the device.                                                               |
| 4                 | WipeFailed     | The   wipe command failed on the device.                                                                        |
| 5                 | Unhealthy      | Unhealthy   state.                                                                                              |
| 6                 | DeletePending  | There   is a delete command pending for the device.                                                             |
| 7                 | RetireIssued   | A   retire command has been issued to the device.                                                               |
| 8                 | WipeIssued     | A   wipe command has been issued.                                                                               |
| 9                 | WipeCanceled   | Wipe   command has been canceled.                                                                               |
| 10                | RetireCanceled | Retire   command has been canceled.                                                                             |
| 11                | Discovered     | The   device is newly discovered by Intune, once it checks in for the first time it   moves to -Managed- state. |

## mobileAppInstallStates
The MobileAppInstallState entity represents the install state for a mobile application after it has been assigned to a group containing devices, users or both.

|       Property      |                        Description                       |
|---------------------|----------------------------------------------------------|
| appInstallStateKey  | The unique ID of the app install state for your account. |
| appInstallState     | Enum value of the app install state.                     |
| appInstallStateName | Name of the app install state.                           |

## mobileAppInstallStatusCounts
Represents a mobile app install status for a given target device type using Mobile Application Management through Microsoft Intune.

|      Property      |                                                          Description                                                          |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| dateKey            | Key of the date when the app install status was recorded.                                                                     |
| appKey             | Key of the mobile app used to identify an instance of   AppRevision.                                                          |
| deviceTypeKey      | Key of the Device Type associated with the Mobile   Application.                                                              |
| appInstallStateKey | Key of the app install state used to identify an instance   of MobileAppInstallState.                                         |
| errorCode          | The error code returned by the app installer, the mobile   platform or the service pertaining to the installation of the app. |
| count              | Total count.                                                                                                                  |

## ownerTypes
The **ownerType** entity indicates whether a device is corporate, personally owned, or unknown.

|    Property   |                                                                                     Description                                                                                    |           Example          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| ownerTypeID   | Unique identifier of the owner type.                                                                                                                                               |                            |
| ownerTypeKey  | Unique identifier of the owner type in the data warehouse   - surrogate key.                                                                                                       |                            |
| ownerTypeName | Represents the owner type of the devices:  Corporate  -   Device is enterprise owned.  Personal -   Device is personally owned (BYOD).   Unknown  -   No information on this device. | Corporate   Personal Unknown |

> [!Note]  
> For the `ownerTypeName` filter in AzureAD when creating Dynamic Groups for devices, you need to set the value `deviceOwnership` as `Company`. For more information, see [Rules for devices](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices). 

## policies
The **Policy** entity lists device configuration profiles, app configuration profiles, and compliance policies. You can assign the policies with Mobile Device Management (MDM) to a group in your enterprise.

|          Property          |                                                                       Description                                                                      |                Example               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| policyKey                  | Unique Key to represent the policy in the data warehouse.                                                                                              | 123                                  |
| policyId                   | Unique identifier of the Policy in the data warehouse.                                                                                                 | b66bc706-ffff-7437-0340-032819502773 |
| policyName                 | Name of the Policy.                                                                                                                                    | "Windows 10 Baseline"                |
| policyVersion              | Version of the Policy. When the policy is edited or   changed, a newer version is created.                                                             | 1, 2, 3                              |
| isDeleted                  | Indicates whether the Policy record has been   updated.  True - Policy has a new record with updated fields.  False- The latest record for the policy. | True/False                           |
| startDateInclusiveUTC      | Date and time in UTC when the policy was created in the   data warehouse.                                                                              | 11/23/2016 0:00                      |
| deletedDateUTC             | Date and time in UTC when IsDeleted changed to True.                                                                                                   | 11/23/2016 0:00                      |
| rowLastModifiedDateTimeUTC | Date and time in UTC when the policy was last modified in   the data warehouse.                                                                        | 11/23/2016 0:00                      |

## policyDeviceActivities
The following table lists the number of devices in the succeeded, pending, failed, or error state per day. The number reflects the data per Policy Type profiles. For example, if a device is in the succeeded state for all its assigned policies, it increments the succeeded counter up one for that day. If a device has two profiles assigned to it, one in the succeeded state and another in an error state, the entity increments the Succeeded counter and place the device in the error state. The **policyDeviceActivity** entity lists how many devices are in which state on a given day over the last 30 days.

|  Property |                                           Description                                           |        Example        |
|-----------|-------------------------------------------------------------------------------------------------|-----------------------|
| dateKey   | Date   Key when the Device Configuration Profile check-in was recorded in the data   warehouse. | 20160703              |
| pending   | Number   of unique Devices in pending state.                                                    | 123                   |
| succeeded | Number   of unique Devices in success state.                                                    | 12                    |
| policyKey | Policy   Key, can be joined with Policy to get the policyName.                                  | Windows   10 baseline |
| error     | Number   of unique Devices in error state.                                                      | 10                    |
| failed    | Number   of unique Devices in failed state.                                                     | 2                     |

## policyPlatformTypes

|        Property        |                      Description                      |     Example    |
|------------------------|-------------------------------------------------------|----------------|
| policyPlatformTypeKey  | The unique key for the policy   platform type.        | 20170519       |
| policyPlatformTypeId   | The unique identifier for the   policy platform type. | 1              |
| policyPlatformTypeName | The name for the policy platform   type.              | AndroidForWork |

## policyTypeActivities
The **PolicyTypeActivity** entity lists the cumulative number of devices in the succeeded, pending, failed, or error state. It lists these states with respect to a device configuration profile, app configuration profile, or compliance policy per day.

|    Property   |                                          Description                                          |           Example           |
|---------------|-----------------------------------------------------------------------------------------------|-----------------------------|
| dateKey       | Date Key when the device Configuration profile check-in   was recorded in the data warehouse. | 20160703                    |
| policyKey     | Policy Key, can be joined with Policy to get the   policyName.                                | Windows 10 baseline         |
| policyTypeKey | Type of Policy Key, can be joined with Policy Type to get   the policy type name.             | Windows10 Compliance Policy |
| pending       | Number of unique devices in pending state.                                                    | 123                         |
| succeeded     | Number of unique devices in success state.                                                    | 12                          |
| error         | Number of unique devices in error state.                                                      | 10                          |
| failed        | Number of unique devices in failed state.                                                     | 2                           |

## policyTypes
The **PolicyType** entity lists types of device configuration profiles, app configuration profiles, and Compliance policies. You can assign the policies with Mobile Device Management (MDM) to a group in your enterprise.

|    Property    |                       Description                      |            Example            |
|----------------|--------------------------------------------------------|-------------------------------|
| policyTypeId   | Unique identifier of the policy in the source system.  | 123                           |
| policyTypeKey  | Unique identifier of the policy in the data warehouse. | 1                             |
| policyTypeName | Name of the policy type.                               | Windows 10 Compliance policy. |

## policyUserActivities
The following table lists the number of users in the succeeded, pending, failed, or error state per day. The number reflects the data per Policy Type profiles. For example, if a user is in the succeeded state for all their assigned policies, it moves up the succeeded counter by one for that day. If a user has two profiles assigned to them, one in the succeeded state and the other is in an error state, the user in the error state is counted. The **PolicyUserActivity** entity lists how many users are in which state on a given day over the last 30 days.

|  Property |                                          Description                                          |       Example       |
|-----------|-----------------------------------------------------------------------------------------------|---------------------|
| dateKey   | Date Key when the Device Configuration Profile check-in   was recorded in the data warehouse. | 20160703            |
| pending   | Number of unique Devices in pending state.                                                    | 123                 |
| succeeded | Number of unique Devices in success state.                                                    | 12                  |
| policyKey | Policy Key, can be joined with Policy to get the   policyName.                                | Windows 10 baseline |
| error     | Number of unique Devices in error state.                                                      | 10                  |

## termsAndConditions
A **termsAndConditions** entity represents the metadata and contents of a given Terms and Conditions (T&C) policy. The contents of  T&C policies are presented to users upon their first attempt to enroll into Intune and subsequently upon edits where an administrator has required re-acceptance. They enable administrators to communicate the provisions to which a user must agree in order to have devices enrolled into Intune.

|    Property        |    Description    |    Example        |
|----------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
|    termsAndConditionsKey    |    A key corresponding to an entry in the   'userTermsAndConditionsAcceptances' collection    |    123    |
|    termsAndCondidionsId    |    The ID for this termsAndConditions entry    |    276edcb7-7440-4339-b6c5-8b6fc556fee6    |
|    termsAndConditionsVersion    |    The version of this terms and conditions entry    |    1    |
|    name    |    The name of this termsAndConditions entry.        |    Intune terms of use     |
|    description    |    The description for these terms and conditions.     |         |
|    title    |    The title for these terms and conditions.     |    Device management corporate policy        |
|    summaryOfTerms    |    The summary of terms given to the user.     |    I agree to the terms and conditions.    |
|    termsAndConditionsBodyText    |    The body of text for these terms and conditions.       |    *Device encryption* Enforcement of 6 digits PIN    |
|    isDeleted    |    True or false value for whether this value is   deleted.     |    False    |
|    startDateInclusiveUTC    |    The start date of these terms and conditions.     |    8/23/2018 4:01:34 AM    |
|    endDateEclusiveUTC    |    The end date of these terms and conditions.     |    12/31/9999 12:00:00 AM    |

## userDeviceAssociations
The **UserDeviceAssociation** entity contains user device associations in your organization.

|        Name        |                                             Description                                            |     Example     |
|--------------------|----------------------------------------------------------------------------------------------------|-----------------|
| userKey            | Unique identifier of the user in the data warehouse.   (Surrogate key).                            | 123             |
| deviceKey          | Unique identifier of the device in the data warehouse.                                             | 123             |
| createdDateTimeUTC | Date and time when the user device association was   created. Uses UTC format.                     | 11/23/2016 0:00 |
| isDeleted          | Indicates that the user unenrolled that device, and that   the association is not current anymore. | True/False      |
| endedDateTimeUTC   | Date and time in UTC when IsDeleted changed to True.                                               | 6/23/2017 0:00  |

## users
The **user** entity lists all the Azure Active Directory (Azure AD) users with assigned licenses in your enterprise.

The **user** entity collection contains user data. These records include user states during the data collection period, even if the user has been removed. For example, a user may be added to Intune and then removed during the course of the last month. While this user is not present at the time of the report, the user and state are present in the data from the prior month. You could create a report that would show the duration of the user's historic presence in your data.

|          Property          |                                                                                                           Description                                                                                                          |                Example               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | Unique identifier of the user in the data warehouse -   surrogate key.                                                                                                                                                         | 123                                  |
| userId                     | Unique identifier of the user - similar to UserKey, but is   a natural key.                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| userEmail                  | Email address of the user.                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | User principal name of the user.                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | Display name of the user.                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | Specifies if this user is Intune licensed or not.                                                                                                                                                                              | True/False                           |
| isDeleted                  | Indicates whether all of the user's licenses have expired   and whether the user was therefore removed from Intune. For a single record,   this flag does not change. Instead, a new record is created for a new user   state. | True/False                           |
| rowLastModifiedDateTimeUTC | Date and time in UTC when the record was last modified in   the data warehouse                                                                                                                                                 | 11/23/2016 0:00                      |

## userTermsAndConditionsAcceptances
A **userTermsAndConditionsAcceptance** entity represents the acceptance status of a given Terms and Conditions (T&C) policy by a given user. Users must accept the most up-to-date version of the terms in order to retain access to the Company Portal.

|    Property    |    Description    |    Example    |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------|
|    dateKey    |    A key corresponding to a date values in the   'dates' collection.     |    20180823    |
|    userKey    |    A user key mapping to a user in the 'users'   collection.     |    20000    |
|    termsAndConditionsKey    |    A key corresponding to an entry in the   'termsAndConditions' collection    |    1    |
|    acceptedDateTimeUTC    |    The time that the user accepted these terms and   conditions    |    8/23/2018 4:01:34 AM    |
|    lastModifiedDateTimeUTC    |    The last time that this entry was modified.     |    8/23/2018 4:01:34 AM    |

## vppProgramTypes 
The **vppProgramType** entity lists possible VPP program types for an app.

|      Property      |          Description         |
|--------------------|------------------------------|
| vppProgramTypeID   | ID   for the type.           |
| vppProgramTypeKey  | Surrogate   key for the key. |
| vppProgramTypeName | VPP   Program type.          |

### Example

|             VppProgramID             |         Name        | Description                |
|--------------------------------------|---------------------|----------------------------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Microsoft           | Microsoft's   VPP program. |
| 00000000-0000-0000-0000-000000000000 | Not   Yet Available | Default   value, No VPP.   |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple               | Apple's   VPP program.     |

## Next steps

For more about the Intune Data Warehouse, see [Data Warehouse data model](reports-ref-data-model.md).
