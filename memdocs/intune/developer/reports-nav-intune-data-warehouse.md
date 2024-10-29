---
# required metadata
title:  Intune Data Warehouse API
titleSuffix: Microsoft Intune 
description: You can use the Intune Data Warehouse API to build reports that provide insight into your enterprise mobile environment.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: 701D6CE9-43F6-4A29-8E84-E2B59931C635

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

# Microsoft Intune Data Warehouse API

The Intune Data Warehouse API lets you access your Intune data in a machine-readable format for use in your favorite analytics tool. You can use the API to build reports that provide insight into your enterprise mobile environment. The API uses the OData protocol, which follows standard patterns for:

- Request and response headers
- Status codes
- HTTP methods
- URL conventions
- Media types
- Payload formats
- Query options

The OData (Open Data Protocol) is an Organization for the Advancement of Structured Information Standards (OASIS) standard that defines the best practice for building and consuming RESTful APIs. The Intune Data Warehouse uses OData version 4.0.

This reference section provides an overview of endpoints, supported HTTP methods, return payload formats, and documentation of the Intune Data Warehouse data model.

> [!Important]  
> You can try out the latest functionality of the Data Warehouse by using the beta version. To use the beta version, your URL must contain the query parameter `api-version=beta`. The beta version offers features before they are made generally available as a supported service. As Intune adds new features, the beta version may change behavior and data contracts. Any custom code or reporting tools dependent on the beta version may break with ongoing updates. <!--If you experience problems with the beta service, follow [link to feedback process]() to report the issue or provide feedback.-->

## OData custom client

You can access the Intune Data Warehouse data model through RESTful endpoints. To gain access to your data, your client must authorize with Microsoft Entra ID using OAuth 2.0. You first set up a web app and a client app in Azure, grant permissions to the client. Your local client gets authorization and can then communicate with the Data Warehouse endpoints.

For more information, see [Get data from the Data Warehouse API with a REST client](reports-proc-data-rest.md).

> [!Note]  
> You can access the [GitHub Intune Data Warehouse repo](https://github.com/Microsoft/Intune-Data-Warehouse) on Github for code samples.

## Interacting with the API

The API requires authorization with Microsoft Entra ID. Microsoft Entra ID uses OAuth 2.0. Once authorized, you can get data from the API using an HTTP GET verb and contacting the exposed entity collections. For details see:

- [Authorization](reports-api-url.md#authorization)
- [API URL Structure](reports-api-url.md#api-url-structure)

## Intune Data Warehouse data model

OData defines an abstract data model and a protocol that let any client access information exposed by any data source. The data model documentation topic contains an explanation of the namespaces, entities, and return objects in the Intune Data Warehouse data model. For more information, see [Data Warehouse Data Model](reports-ref-data-model.md).

## Next steps

Learn more about working with Microsoft Entra ID by reading the [Authentication Scenarios for Microsoft Entra ID](/azure/active-directory/develop/active-directory-authentication-scenarios).

Find OData resources at [odata.org](https://www.odata.org).
  
Review the OData Version 4.0 standard at [OData Version 4.0](https://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html).
