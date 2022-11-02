---
# required metadata

title: Use Graph APIs to export Intune Reports | Microsoft Docs
description: Learn about exporting Intune reports using Graph APIs.
keywords: 
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Export Intune reports using Graph APIs

All reports that have been migrated to the Intune reporting infrastructure will be available for export from a single top-level export API. You must use the Microsoft Graph API to make the HTTP call. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources. 

> [!NOTE]
> For information about making REST API calls, including tools for interacting with Microsoft Graph, see [Use the Microsoft Graph API](/graph/use-the-api).

Microsoft Endpoint Manager will export reports using the following Microsoft Graph API endpoint:

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
    "filter":"(OwnerType eq '1')", 
    "localizationType": "LocalizedValuesAsAdditionalColumn", 
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
    ]
} 
```

> [!NOTE]
> To retrieve data, select specific columns, such as those specified in the above example. Do not build automation around default columns of any report export. You should build your automation to explicitly select relevant columns.

### Response example

Based on the above POST request, Graph returns a response message. The response message is the data that you requested or the result of the operation.

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter":"(OwnerType eq '1')", 
    "localizationType": "LocalizedValuesAsAdditionalColumn", 
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
You can then use the `id` field to query the status of the export with a GET request: 

For example:
```https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('Devices_05e62361-783b-4cec-b635-0aed0ecf14a3') ```

You will need to continue calling this URL until you get a response with a `status: completed` attribute. It will look like the following example:

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter":"(OwnerType eq '1')", 
    "localizationType": "LocalizedValuesAsAdditionalColumn", 
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

There are four main parameters you can submit in your request body to define the export request: 

- `reportName`: Required. This parameter is the name of the report you want to specify.  
- `filter`: Not required for most reports. Note that the filter parameter is a string.
- `select`: Not required. Specify which columns from the report you want. Only valid column names relevant to the report you are calling will be accepted.  
- `localizationType`: This parameter controls localization behavior for the report. Possible values are `LocalizedValuesAsAdditionalColumn` and `ReplaceLocalizableValues`.

## Localization behavior

The `localizationType` parameter controls localization behavior for the report. The possible values for this parameter are `LocalizedValuesAsAdditionalColumn` and `ReplaceLocalizableValues`.

### LocalizedValuesAsAdditionalColumn report value

This value for the `localizationType` parameter is the default value. It will be inserted automatically if the `localizationType` parameter is not specified. This value specifies that Intune provides two columns for each localizable column.
- *enum value*:  The *enum value* column contains either a raw string, or a set of numbers that don't change, regardless of locale. This column will be under the original column name (see example).
- *localized string value*: This column  will be the original column name with _loc appended. It will contain string values that are human readable, and locale conditional (see example).

#### Example

|         OS  |            OS_loc        |
|-|-|
|         1  |            Windows        |
|         1  |            Windows        |
|         1  |            Windows        |
|         2  |            iOS        |
|         3  |            Android        |
|         4  |            Mac        |


### ReplaceLocalizableValues report value

ReplaceLocalizableValues report value will only return one column per localized attribute. This column will contain the original column name with the localized values.

#### Example 

|         OS        |
|-|
|         Windows        |
|         Windows        |
|         Windows        |
|         iOS        |
|         Android        |
|         Mac        |

For columns without localized values, only a single column with the true column name and the true column values are returned.  

> [!IMPORTANT]
> The `localizationType` parameter is relevant for any export experience hosted by Intune's reporting infrastructure with a few exceptions. The`Devices` and `DevicesWithInventory` report types will not honor the `localizationType` parameter due to legacy compatibility requirements.

## Next steps

- [Microsoft Graph documentation](/graph/)
- [Intune reports](./reports.md)
