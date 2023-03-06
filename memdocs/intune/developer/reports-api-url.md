---
# required metadata
title: Intune Data Warehouse API endpoint
titleSuffix: Microsoft Intune 
description: This reference topic describes the Microsoft Intune Data Warehouse API URL structure. Filter examples are provided.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/06/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: A7A174EC-109D-4BB8-B460-F53AA2D033E6

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier3
- M365-identity-device-management
---
# Intune Data Warehouse API endpoint

You can use the Intune Data Warehouse API with an account with specific role-based access controls and Azure AD credentials. You will then authorize your REST client with Azure AD using OAuth 2.0. And finally, you will form a meaningful URL to call a data warehouse resource.

[!INCLUDE [reports-credential-reqs](../includes/reports-credential-reqs.md)]

## Authorization

Azure Active Directory (Azure AD) uses OAuth 2.0 to enable you to authorize access to web applications and web APIs in your Azure AD tenant. This guide is language independent, and describes how to send and receive HTTP messages without using any open-source libraries. The OAuth 2.0 authorization code flow is described in [section 4.1](https://tools.ietf.org/html/rfc6749#section-4.1) of the OAuth 2.0 specification.

For more information, see [Authorize access to web applications using OAuth 2.0 and Azure Active Directory](/azure/active-directory/develop/active-directory-protocols-oauth-code).

## API URL structure

The Data Warehouse API endpoints read the entities for each set. The API supports a **GET** HTTP verb, and a subset of query options.

The URL for Intune uses the following format:  
`https://fef.{location}.manage.microsoft.com/ReportingService/DataWarehouseFEService/{entity-collection}?api-version={api-version}`

> [!NOTE]
> In the above URL, replace  `{location}`, `{entity-collection}`, and `{api-version}` based on the details provided in the table below.

The URL contains the following elements:

| Element | Example | Description |
|-------------------|------------|--------------------------------------------------------------------------------------------------------------------|
| location | msua06 | The base URL can be found by viewing the Data Warehouse API blade in the [Microsoft Intune admin center](https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/ReportingMenu/dataWarehouse). |
| entity-collection | devicePropertyHistories | The name of the OData entity collection. For more information on collections and entities in the data model, see [Data Model](reports-ref-data-model.md). |
| api-version | beta | Version is the version of the API to access. For more information, see [Version](reports-api-url.md#api-version-information). |
| maxhistorydays | 7 | (Optional) The maximum number of days of history to retrieve. This parameter can be supplied to any collection, but will only take effect for collections that include `dateKey` as a part of their key property. See [DateKey Range Filters](reports-api-url.md#datekey-range-filters) for more information. |

## API version information

You can now use the v1.0 version of the Intune Data Warehouse by setting the query parameter `api-version=v1.0`. Updates to collections in the Data Warehouse are additive in nature and do not break existing scenarios.

You can try out the latest functionality of the Data Warehouse by using the beta version. To use the beta version, your URL must contain the query parameter `api-version=beta`. The beta version offers features before they are made generally available as a supported service. As Intune adds new features, the beta version may change behavior and data contracts. Any custom code or reporting tools dependent on the beta version may break with ongoing updates.

## OData query options

The current version supports the following OData query parameters: `$filter`, `$select`, `$skip,` and `$top`. In `$filter`, only `DateKey` or `RowLastModifiedDateTimeUTC` may be supported when the columns are applicable, and other properties would trigger a bad request.

## DateKey Range Filters

`DateKey` range filters may be used to limit the amount of data to download for some of the collections with `dateKey` as a key property. The `DateKey` filter can be used to optimize service performance by providing the following `$filter` query parameter:

1. `DateKey` alone in the `$filter`, supporting the `lt/le/eq/ge/gt` operators and joining with the logic operator `and`, where they can be mapped to a begin date and/or end date.
2. `maxhistorydays` is supplied as custom query option.<br>

## Filter examples

> [!NOTE]
> The filter examples assume today is 2/21/2018.

|                             Filter                             |           Performance Optimization           |                                          Description                                          |
|----------------------------------------------------------------|----------------------------------------------|-----------------------------------------------------------------------------------------------|
|    `maxhistorydays=7`                                            |    Full                                      |    Return data with `DateKey` between 20180214 and 20180221.                                     |
|    `$filter=DateKey eq 20180214`                                 |    Full                                      |    Return data with `DateKey` equal to 20180214.                                                    |
|    `$filter=DateKey ge 20180214 and DateKey lt 20180221`         |    Full                                      |    Return data with `DateKey` between 20180214 and 20180220.                                     |
|    `maxhistorydays=7&$filter=DateKey eq 20180214`                |    Full                                      |    Return data with `DateKey` equal to 20180214. `maxhistorydays` is ignored.                            |
|    `$filter=RowLastModifiedDateTimeUTC ge 2018-02-21T23:18:51.3277273Z`                                |    Full                                       |    Return data with `RowLastModifiedDateTimeUTC` is greater than or equal to `2018-02-21T23:18:51.3277273Z`                             |
