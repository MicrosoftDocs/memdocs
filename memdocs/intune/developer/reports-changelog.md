---
# required metadata
title: Intune Data Warehouse Change log 
titleSuffix: Microsoft Intune
description: This topic provides a list of changes for the Microsoft Intune Data Warehouse API.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/01/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: E85DBB2D-67BB-4E10-82D6-E43046B9C43C

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Change log for the Intune Data Warehouse API

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Keep current on updates to the Intune Data Warehouse.

## 2202
_Released Feburary 2022_

The  `applicationInventory` entity has been removed from the Intune Data Warehouse. A new dataset is now available in the UI and via Intune's export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

## 2105
_Released May 2021_

The `IntuneAosp` property value is now supported in the `managementAgentType` enum. The `ManagementAgentTypeID` value for this property is `2048`.  It represents the device type that is managed by Intune's MDM for AOSP (Android Open Source Project) devices. For related information, see [managementAgentType](../developer/reports-ref-devices.md#managementagenttypes) in the beta section of the Intune Data Warehouse API.

## 2103
_Released March 2021_

The  `applicationInventory`  entity will be removed from the Intune Data Warehouse with the 2107 update of Intune. We are introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

## 2007 
_Released July 2020_

### v1.0 changes

The following table lists the added property to the [device](../developer/intune-data-warehouse-collections.md#devices) entity in the Intune Data Warehouse.

|    Collection                          |    Change     |    Description information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    ethernetMacAddress    |    Added    |    The unique network identifier of this device.                                                                                                                                                                                                                                                                     |
|    office365Version    |    Added    |    The version of Microsoft 365 that is installed on the device.                                                                                                                                                                                                                                                                     |

The following table lists the added property to the [devicePropertyHistories](../developer/intune-data-warehouse-collections.md#devicepropertyhistories) entity in the Intune Data Warehouse.

|    Collection                          |    Change     |    Description information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    physicalMemoryInBytes    |    Added    |    The physical memory in bytes.                                                                                                                                                                                                                                                                     |
|    totalStorageSpaceInBytes    |    Added    |    Total storage capacity in bytes.                                                                                                                                                                                                                                                                     |

## 2004 
_Released April 2020_

### v1.0 changes

The following table lists the added property to the [devices](../developer/intune-data-warehouse-collections.md#devices) entity in the Intune Data Warehouse.

|    Collection                          |    Change     |    Description information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    windowsOsEdition     |    Added    |    Windows Operating System edition.                                                                                                                                                                                                                                                                     |

### Beta changes

The following table lists the added property to the **device** entity in the Intune Data Warehouse.

|    Collection                          |    Change     |    Description information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    windowsOsEdition     |    Added    |    Windows Operating System edition.                                                                                                                                                                                                                                                                     |

## 2003 
_Released March 2020_

### Beta changes

The following table lists the added properties to the **device** entity in the Intune Data Warehouse.

|    Collection                          |    Change     |    Description information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    ethernetMacAddress    |    Added    |    The unique network identifier of this device.                                                                                                                                                                                                                                                                     |
|    model    |    Added    |    The device model.                                                                                                                                                                                                                                                                     |
|    office365Version    |    Added    |    The version of Microsoft 365 that is installed on the device.                                                                                                                                                                                                                                                                     |

The following table lists the added properties to the **devicePropertyHistory** entity in the Intune Data Warehouse.

|    Collection                          |    Change     |    Description information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    physicalMemoryInBytes    |    Added    |    The physical memory in bytes.                                                                                                                                                                                                                                                                     |
|    totalStorageSpaceInBytes     |    Added    |    Total Storage in bytes.                                                                                                                                                                                                                                                                     |

## 1903 (Part 2)
_Released April 2019_

### Beta changes

The following table lists the recent removed collections and the replacements collections in the Intune Data Warehouse.

|    Collection                          |    Change     |    Additional information                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    mobileAppDeviceUserInstallStatus    |    Removed    |    Use   [mobileAppInstallStatusCounts](intune-data-warehouse-collections.md#mobileappinstallstatuscounts)   instead.                                                                                                                                                                                                                                                                     |
|    enrollmentTypes                     |    Removed    |    Use   [deviceEnrollmentTypes](intune-data-warehouse-collections.md#deviceenrollmenttypes)   instead.                                                                                                                                                                                                                                                                                      |
|    mdmStatuses                         |    Removed    |    Use [complianceStates](intune-data-warehouse-collections.md#compliancestates)   instead.                                                                                                                                                                                                                                                                                               |
|    workPlaceJoinStateTypes             |    Removed    |    Use the `azureAdRegistered`   property in the [devices](intune-data-warehouse-collections.md#devices) and   [devicePropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories)   collections instead.                                                                                                                                                                                                             |
|    clientRegistrationStateTypes        |    Removed    |    Use   [deviceRegistrationStates](intune-data-warehouse-collections.md#deviceregistrationstates)   instead.                                                                                                                                                                                                                                                                             |
|    currentUser                         |    Removed    |    Use the   [users](intune-data-warehouse-collections.md#users) collection instead.                                                                                                                                                                                                                                                                                                      |
|    mdmDeviceInventoryHistories         |    Removed    |    Many of the properties were   redundant or can now be found in the   [devicePropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories)   or [devices](intune-data-warehouse-collections.md#devices) collections. Any **mdmDeviceInventoryHistories** properties not already listed with these two   collections are no longer available. See details below.    |

The following table lists the old properties formerly found in the **mdmDeviceInventoryHistories** collection and the change/replacement. Any properties that were in **mdmDeviceInventoryHistories** but not listed below have been removed.

|    Old property                |    Change/replacement                                                           |
|--------------------------------|---------------------------------------------------------------------------------|
|    cellularTechnology          |    cellularTechnology in devices collection                                     |
|    deviceClientId              |    deviceId in devices collection                                               |
|    deviceManufacturer          |    manufacturer in devices collection                                           |
|    deviceModel                 |    model in devices collection                                                  |
|    deviceName                  |    deviceName in devices collection                                             |
|    deviceOsPlatform            |    deviceTypeKey in devices collection                                          |
|    deviceOsVersion             |    osVersion in devicePropertyHistories collection                              |
|    deviceType                  |    deviceTypeKey in devices collection, referencing   deviceTypes collection    |
|    encryptionState             |    encryptionState property in the devices collection                           |
|    exchangeActiveSyncId        |    easDeviceId property in the devices collection                               |
|    exchangeDeviceId            |    easDeviceId in devices collection                                            |
|    imei                        |    imei in devices collection                                                   |
|    isSupervised                |    isSupervised property in the devices collection                              |
|    jailBroken                  |    jailBroken in devicePropertyHistories collection                             |
|    meid                        |    meid property in the devices collection                                      |
|    oem                         |    manufacturer in devices collection                                           |
|    osName                      |    deviceTypeKey in devices collection, referencing   deviceTypes collection    |
|    phoneNumber                 |    phoneNumber in devices collection                                            |
|    platformType                |    model in devices collection                                                  |
|    product                     |    deviceTypeKey in devices collection                                          |
|    productVersion              |    osVersion in devicePropertyHistories collection                              |
|    serialNumber                |    serialNumber in devices collection                                           |
|    storageFree                 |    freeStorageSpaceInBytes property in the devices collection                   |
|    storageTotal                |    totalStorageSpaceInBytes property in the devices   collection                |
|    subscriberCarrierNetwork    |    subscriberCarrier property in the devices collection                         |
|    wifimac                     |    wiFiMacAddress in devices collection                                         |

The following table lists changes to properties found in the [devicePropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories) collection: 

|    Old property                  |    Change/replacement                                               |
|----------------------------------|---------------------------------------------------------------------|
|    categoryId                    |    deviceCategoryKey, referencing deviceCategories collection       |
|    certExpirationDate            |    Removed                                                          |
|    clientRegistrationStateKey    |    deviceRegistrationStateKey                                       |
|    createdDate                   |    enrolledDateTime in devices collection                           |
|    deviceTypeKey                 |    deviceTypeKey in devices collection                              |
|    easID                         |    easDeviceId in devices collection                                |
|    enrolledByUser                |    userId in devices collection                                     |
|    enrollmentTypeKey             |    deviceEnrollmentTypeKey in devices collection                    |
|    graphDeviceIsCompliant        |    Removed                                                          |
|    graphDeviceIsManaged          |    Removed                                                          |
|    lastContact                   |    lastSyncDateTime in devices collection                           |
|    lastContactNotification       |    Removed                                                          |
|    lastContactWorkplaceJoin      |    Removed                                                          |
|    lastExchangeStatusUtc         |    Removed                                                          |
|    lastModifiedDateTimeUTC       |    Removed                                                          |
|    lastPolicyUpdateUtc           |    Removed                                                          |
|    managementAgentKey            |    managementStateKey                                               |
|    manufacturer                  |    manufacturer in devices collection                               |
|    mdmStatusKey                  |    complianceStateKey, referencing complianceStates   collection    |
|    model                         |    model in devices collection                                      |
|    osFamily                      |    operatingSystem in devices collection                            |
|    osRevisionNumber              |    osVersion in devices collection                                  |
|    processorArchitecture         |    Removed                                                          |
|    referenceId                   |    azureAdDeviceId in devices collection                            |
|    serialNumber                  |    serialNumber in devices collection                               |
|    workplaceJoinStateKey         |    azureAdRegistered                                                |

The following table lists changes to properties found in the [devices](intune-data-warehouse-collections.md#devices) collection: 

|    Old property                  |    Change/replacement                                               |
|----------------------------------|---------------------------------------------------------------------|
|    categoryId                    |    deviceCategoryKey, referencing deviceCategories collection       |
|    certExpirationDate            |    Removed                                                          |
|    clientRegistrationStateKey    |    deviceRegistrationStateKey                                       |
|    createdDate                   |    enrolledDateTime                                                 |
|    easId                         |    easDeviceId                                                      |
|    enrolledByUser                |    userId                                                           |
|    enrollmentTypeKey             |    deviceEnrollmentTypeKey                                          |
|    graphDeviceIsCompliant        |    Removed                                                          |
|    graphDeviceIsManaged          |    Removed                                                          |
|    lastContact                   |    lastSyncDateTime                                                 |
|    lastContactNotification       |    Removed                                                          |
|    lastContactWorkplaceJoin      |    Removed                                                          |
|    lastExchangeStatusUtc         |    Removed                                                          |
|    lastPolicyUpdateUtc           |    Removed                                                          |
|    mdmStatusKey                  |    complianceStateKey, referencing complianceStates   collection    |
|    osFamily                      |    operatingSystem                                                  |
|    processorArchitecture         |    Removed                                                          |
|    referenceId                   |    azureAdDeviceId                                                  |
|    workplaceJoinStateKey         |    azureAdRegistered                                                |

The following table lists changes to properties found in the [enrollmentActivities](intune-data-warehouse-collections.md#enrollmentactivities) collection: 

|    Old property         |    Change/replacement         |
|-------------------------|-------------------------------|
|    enrollmentTypeKey    |    deviceEnrollmentTypeKey    |

The following table lists changes to properties found in the [mamApplications](intune-data-warehouse-collections.md#mamapplications) collection: 

|    Old property       |    Change/replacement    |
|-----------------------|--------------------------|
|    applicationKey     |    mamApplicationKey     |
|    applicationName    |    mamApplicationName    |
|    applicationId      |    mamApplicationId      |

The following table lists changes to properties found in the [mamApplicationInstances](intune-data-warehouse-collections.md#mamapplicationinstances) collection: 

|    Old property     |    Change/replacement    |
|---------------------|--------------------------|
|    applicationId    |    mamApplicationId      |
|    deviceId         |    mamDeviceId           |
|    deviceType       |    mamDeviceType         |
|    deviceName       |    mamDeviceName         |

The following table lists changes to properties found in the [mamCheckins](intune-data-warehouse-collections.md#mamcheckins) collection: 

|    Old property      |    Change/replacement    |
|----------------------|--------------------------|
|    applicationKey    |    mamApplicationKey     |

The following table lists changes to properties found in the [users](intune-data-warehouse-collections.md#users) collection: 

|    Old property             |    Change/replacement    |
|-----------------------------|--------------------------|
|    startDateInclusiveUtc    |    Removed               |
|    endDateInclusiveUtc      |    Removed               |
|    isCurrent                |    Removed               |

## 1903
_Released March 2019_

### V1.0 changes reflecting back to beta
When V1.0 was first introduced in 1808, it differed in some significant ways from the beta API. In 1903 those changes will be reflected back into the beta API version. If you have important reports that use the beta API version, we strongly recommend switching those reports to V1.0 to avoid breaking changes. Please refer to [API version information](reports-api-url.md) for more information on Data Warehouse API versions and backwards compatibility.

## 1902 
_Released February 2019_

### Power BI Compliance app

Access your Intune Data Warehouse in Power BI Online using the [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) app. With this Power BI app, you can now access and share pre-created reports without any setup and without leaving your web browser.

> [!NOTE]
> There are two additional filters you can apply to the Intune Compliance app.

#### Add additional filters to the Intune Compliance app
1. Open the [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) app in your web browsers.
2. Click **Non-Compliant Devices** and select **Non-Compliant** in the **complianceStatus** filter.
3. Click on **Unknown Devices** and select **Not Yet Available** in the **complianceStatus** filter.

## 1812 
_Released December 2018_

### Enrollment Activities Collection Released to v1.0 

The Enrollment Activities collection is now available in v1.0. You can use this collection to understand enrollment failure volume and trends in your environment. For more information, see [enrollmentActivities](intune-data-warehouse-collections.md#enrollmentactivities), [enrollmentEventStatuses](intune-data-warehouse-collections.md#enrollmenteventstatuses), [enrollmentFailureCategories](intune-data-warehouse-collections.md#enrollmentfailurecategories), and [enrollmentFailureReasons](intune-data-warehouse-collections.md#enrollmentfailurereasons).

## 1808
_Released August 2018_

### v1.0 Collections  

You can now use the v1.0 version of the Intune Data Warehouse by setting the query parameter `api-version=v1.0`. Updates to collections in the Data Warehouse are additive in nature and do not break existing scenarios.

### Enrollment Activities Collection Released to Beta

The new `Enrollment Activities` collection is released to beta. You can use this collection to understand how your enrollment is proceeding by viewing the most common failures. 


## 1805
_Released May 2018_

### Correction to device count in **Devices** collection 

A fix has been made to the **Devices** collection which may lower total device counts that filter by the attribute `isDeleted`. This drop is a result of the correction and is not an error. For more information regarding the **Devices** collection, see [Reference for device entities](reports-ref-devices.md). 


## 1801
_Released January 2018_

### Intune Data Warehouse application-only authentication <!-- 1867540 -->

You can set up an application using Azure Active Directory (Azure AD) and authenticate to the Intune Data Warehouse. For more information see, [Intune Data Warehouse application-only authentication](data-warehouse-app-only-auth.md).

### Azure AD and Intune credential requirements <!-- 2077525 -->

- An Intune license is no longer required to be assigned to the user when accessing the Intune Data Warehouse (including the API).
- The Intune role name has been changed from **Reports** to **Intune data warehouse**. 

    For more information, see [Azure AD and Intune credential requirements](reports-api-url.md#azure-ad-and-intune-credential-requirements).

### OData query options <!-- 2077711 -->

You can use <code>$select</code> as an OData query parameter. The current version supports the following OData query parameters: <code>$filter</code>, <code>$orderby</code>, <code>$select</code>, <code>$skip</code>, and <code>$top</code>. For more information, see [OData query options](reports-api-url.md#odata-query-options).

### New entities in the in Data Warehouse data model <!-- 2077804 -->

- The entity, [**MobileAppDeviceuserInstallStatus**](reports-ref-application.md), has been added. The **MobileAppDeviceUserInstallStatus** represents a mobile app install status for a given device and user.
- The entity, [**MobileAppInstallStates**](reports-ref-application.md#mobileappinstallstates), has been added. The **MobileAppInstallState** entity represents the install state for a mobile application after it has been assigned to a group containing devices, users, or both. 

## 1710
_Released November  2017_

### A new entity collection named Current User is limited to currently active user data <!-- 1544273 -->

The **Users** entity collection contains all the Azure Active Directory (Azure AD) users with assigned licenses in your enterprise. These records include user states during the data collection period, even if the user has been removed. For example, a user may be added to Intune and then removed during the course of the last month. While this user is not present at the time of the report, the user and state are present in the data. You could create a report that would show the duration of the user's historic presence in your data.

In contrast, the new **Current User** entity collection only contains users who have not been removed. The **Current User** entity collection only contains currently active users. For information about the **current user** entity collection, see [Reference for current user entity](reports-ref-data-model.md).

## 1709
_Released October  2017_

### User device association entity collection added to Intune Data Warehouse data model <!-- 1187917 -->

You can now build reports and data visualizations using the user device association information that associates user and device entity collections. The data model can be accessed through the Power BI file (PBIX) retrieved from the Data Warehouse Intune page, through the OData endpoint, or by developing a custom client. For more information, see the [User Device Association](reports-ref-user-device.md).

### New entities in the in Data Warehouse data model <!-- 1479526 -->

- The entity, [**UserDeviceAssociation**](reports-ref-user-device.md), added. **UserDeviceAssociation** contains user device associations in your organization. You can now build reports and data visualizations using the user device association information that associates user and device entity collections.  
- The entity, [**IntuneManagementExtension**](reports-ref-intunemanagementextension.md), added. **IntuneManagementExtension** contains entities for mobile devices that track information such as version and installation status.

## Next steps
- Learn [what's new each week in Intune](../fundamentals/whats-new.md). You can also find out about upcoming changes, important notices about the service, and information about past releases.
- Read the [Microsoft Intune Blog](https://www.microsoft.com/microsoft-365/blog/microsoft-intune/).
