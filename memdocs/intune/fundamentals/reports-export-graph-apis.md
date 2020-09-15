---
# required metadata

title: Use Graph APIs to export Intune Reports | Microsoft Docs
description: Learn about exporting Intune reports using Graph APIs.
keywords: 
ms.author: erikre
author: Erikre
manager: dougeby
ms.date: 09/15/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: [ALIAS]
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Export Intune reports using Graph APIs

All reports that have been migrated to the Intune reporting infrastructure will be available for export from a single top level export API. You must use the Microsoft Graph API to make the HTTP call. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources. 

> [!NOTE]
> For information about making REST API calls, including tools for interacting with Microsoft Graph, see [Use the Microsoft Graph API](https://docs.microsoft.com/graph/use-the-api).

Microsoft Intune Reports use the following Microsoft Graph API endpoint:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```
## Example devices report request and response

When making the request, you must provide a `reportName` parameter as part of the request body based on the report that you would like to export. Below is an example of an export request for the **Devices** report. You must use the POST HTTP method on your request. The POST method is used to create a new resource or perform an action.

### Request example

The below request contains the HTTP method used on the request to Microsoft Graph.

```http
{ 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "localization": "true", 
    "ColumnName": "ui" 
} 
```
### Reponse example

Based on the above POST request, Graph returns a response message. The response message is the data that you requested or the result of the operation.

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "notStarted", 
    "url": null, 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "0001-01-01T00:00:00Z" 
} 
```
You can then use the "id" field to query the status of the export with a GET request: 

For example:
```https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('Devices_05e62361-783b-4cec-b635-0aed0ecf14a3') ```

You will need to continue calling this URL until you get a response with a `status: completed` attribute. It will look like the following example:

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "completed", 
    "url": "https://amsua0702repexpstorage.blob.core.windows.net/cec055a4-97f0-4889-b790-dc7ad0d12c29/Devices_05e62361-783b-4cec-b635-0aed0ecf14a3.zip?sv=2019-02-02&sr=b&sig=%2BP%2B4gGiZf0YzlQRuAV5Ji9Beorg4nnOtP%2F7bbFGH7GY%3D&skoid=1db6df02-4c8b-4cb3-8394-7ac2390642f8&sktid=72f988bf-86f1-41af-91ab-2d7cd011db47&skt=2020-08-19T03%3A48%3A32Z&ske=2020-08-19T09%3A44%3A23Z&sks=b&skv=2019-02-02&se=2020-08-19T09%3A44%3A23Z&sp=r", 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "2020-08-19T09:44:23.8540289Z" 
} 
```
You can then directly download the compressed CSV from the `url` field.  

## Report parameters

There are three main parameters you can submit in your request body to define the export request: 

- `reportName`: Required. This is the name of the report you want to specify.  
- `filter`: Not required for most reports. Reports that do require a filter are listed here: 
    - `DeviceInstallStatus`: Required filter is `ApplicationId`.
    - `UserInstallStatus`: Required filter is `ApplicationId`.
    - `OrgDeviceInstallStatus`: Required filter is `ApplicationId`.
- `select`: Not required. If you don't specify a `select` value you will receive a default set of columns, which for most reports is the entire dataset. 

## Available reports

The following table contains the possible values for the `reportName` parameter. These are the currently available reports for export.

| `reportName` parameter values |
|-|
| DeviceCompliance |
| DeviceNonCompliance |
| Devices |

Each of the listed reports is described below.

### DeviceCompliance report

The following table contains the possible output when calling the `DeviceCompliance` report:

| Return value | Description |
|-|-|
|         DeviceId  | Unique identifier of the device. |
|            IntuneDeviceId   | Intune device ID. |
| AadDeviceId   | Azure AD device ID. |
| DeviceName   | Name of the device. |
| DeviceType   | Type of the device. |
| OSDescription   | OS description. |
|            OSVersion   | OS version. |
| OwnerType   | Type of device owner. |
| LastContact   | Latest sync DateTime. |
| InGracePeriodUntil   | Remaining amount of grace period. |
| IMEI   | International mobile equipment identifier (IMEI) of the device. |
|            SerialNumber   | Serial number of the device. |
| ManagementAgents   | Management agents  associated with   the device. |
| PrimaryUser   | Primary user of the device. |
| UserId   | User's ID. |
| UPN   | User Principal Name. |
|            UserEmail   | User's email address. |
| UserName   | User's name. |
| DeviceHealthThreatLevel   | Device health threat level. |
| RetireAfterDatetime   | DateTime value for retirement. |
| PartnerDeviceId   | Partner device ID. |
|            ComplianceState   | Compliance state. |
| OS        | OS of the device. |

You can choose to filter the `DeviceCompliance` report's output based on the following columns:
- `ComplianceState`
- `OS` 
- `OwnerType`
- `DeviceType` 

### DeviceNonCompliance report

The following table contains the possible output when calling the `DeviceNonCompliance` report:

| Return value | Description |
|-|-|
|         DeviceId  | Unique identifier of the device. |
|            IntuneDeviceId   | Intune device ID. |
| AadDeviceId   | Azure AD device ID. |
| DeviceName   | Name of the device. |
| DeviceType   | Type of the device. |
| OSDescription   | OS description. |
|            OSVersion   | OS version. |
| OwnerType   | Type of device owner. |
| LastContact   | Latest sync DateTime. |
| InGracePeriodUntil   | Remaining amount of grace period. |
| IMEI   | International mobile equipment identifier (IMEI) of the device. |
|            SerialNumber   | Serial number of the device. |
| ManagementAgents   | Management agents  associated with   the device. |
| PrimaryUser   | Primary user of the device. |
| UserId   | User's ID. |
| UPN   | User Principal Name. |
|            UserEmail   | User's email address. |
| UserName   | User's name. |
| DeviceHealthThreatLevel   | Device health threat level. |
| RetireAfterDatetime   | DateTime value for retirement. |
| PartnerDeviceId   | Partner device ID. |
|            ComplianceState   | Compliance state. |
| OS        | OS of the device. |

You can choose to filter the `DeviceNonCompliance` report's output based on the following columns:
- `OS` 
- `OwnerType`
- `DeviceType` 
- `UserId`
- `ComplianceState`

### Devices report

The following table contains the possible output when calling the `Devices` report:

| Return value | Description |
|-|-|
|         DeviceId  | Unique identifier of the device. |
| DeviceName  | Name of the device. |
| DeviceType  | Type of the device. |
| ClientRegistrationStatus  | Registatrion status of the client device. |
|            OwnerType  | Type of device owner. |
| CreatedDate  | Report date created. |
| LastContact  | Latest sync DateTime. |
| ManagementAgents  | Management agents  associated with   the device. |
| ManagementState  | Management state  associated with   the device. |
|            ReferenceId  | Report reference ID. |
| CategoryId  | Report category ID. |
| EnrollmentType  | Enrollment type of the device. |
| CertExpirationDate  | Expiration date of the cert. |
| MDMStatus  | Status of device management. |
|            OSVersion  | OS version of the device. |
| GraphDeviceIsManaged  | Management state  associated with   the device. |
| EasID  | Exchange Active Sync ID. |
| SerialNumber  | Serial number of the device. |
| EnrolledByUser  | Enrolled by user. |
|            Manufacturer  | Device manufacturer. |
| Model  | Device model. |
| OSDescription  | OS description. |
| IsManaged  | Management state of the device. |
| EasActivationStatus  | Exchange Active Sync activation status. |
|            IMEI  | International mobile equipment identifier (IMEI) of the device. |
| EasLastSyncSuccessUtc  | Exchange Active Sync successful sync. |
| EasStateReason  | Exchange Active Sync state and reason. |
| EasAccessState  | Exchange Active Sync access state. |
| EncryptionStatus  | Encryption status. |
|            SupervisedStatus  | Supervised status. |
| PhoneNumberE164Format  | Phone number. |
| InGracePeriodUntil  | Remaining amount of grace period. |
| AndroidPatchLevel  | Android patch level. |
| WifiMacAddress  | Wifi mac address. |
|            SCCMCoManagementFeatures  | Configuratiom Mgr management features. |
| MEID  | Mobile equipment ID. |
| SubscriberCarrierNetwork  | Subscriber carrier network. |
| StorageTotal  | Total storage. |
| StorageFree  | Free storage. |
|            ManagedDeviceName  | Managed device name. |
| LastLoggedOnUserUPN  | Last  UPN. |
| MDMWinsOverGPStartTime  | MDM start time. |
| StagedDeviceType  | Staged device type. |
| UserApprovedEnrollment  | User approved enrollment. |
|            ExtendedProperties  | Extended properties. |
| EntitySource  | Entity source. |
| PrimaryUser  | Primary user. |
| CategoryName  | Category name. |
| UserId  | User id. |
|            UPN  |  |
| UserEmail  | User user email. |
| UserName  | User user name. |
| RetireAfterDatetime  | Retire after datetime. |
| PartnerDeviceId  | Partner device id. |
|            HasUnlockToken  | Has unlock token. |
| CompliantState  | Compliant compliant state. |
| ManagedBy  | Managed managed by. |
| Ownership  | User Principal Name. |
| DeviceState  | Device state. |
|            DeviceRegistrationState  | Device registration state. |
| SupervisedStatusString  | Supervised status string. |
| EncryptionStatusString  | Encryption status string. |
| OS  | Operating system. |
| SkuFamily  | SKU family. |
|            JoinType  | Join type. |
| PhoneNumber  | Phone number. |
| JailBroken  | Jail broken device. |
| EasActivationStatusString        | Exchange Active Sync status string. |

You can choose to filter the `DeviceNonCompliance` report's output based on the following columns:
- `OwnerType`
- `DeviceType` 
- `ManagementAgents`
- `CategoryName` 
- `ManagementState` 
- `CompliantState` 
- `JailBroken` 
- `LastContact` 
- `CreatedDate` 
- `EnrollmentType` 

## Next steps

- [Microsoft Graph documenation](https://docs.microsoft.com/graph/)
- [Intune reports](https://docs.microsoft.com/mem/intune/fundamentals/reports)