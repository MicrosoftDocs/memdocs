---
title: Audit logs for Microsoft Intune cloud PKI  
titleSuffix: Microsoft Intune 
description: Get audit logs for Microsoft cloud public key infrastructure (PKI) activity in the admin center.   
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/26/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: wicale  
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection:
- tier1
- M365-identity-device-management
- certificates
- IntuneSuite
- sub-intune-suite
---
# Microsoft Cloud PKI audit logs  

This article describes how to access and utilize audit logs for Microsoft Cloud PKI admin actions. *Intune audit logs* are records of actions invoked by Intune administrators and authorized users. Audit logs provide information about who performed what action, when it occurred, and other data points relating to the actions executed. You can use the Microsoft PKI audit logs to monitor the creation, access, deletion, and modification of certification authorities and issued certificates in Intune.  

## Available logs  

Audit logs are available for the following actions on CAs and certificates:  

| Audit action | Purpose |
| -------------------------- | ----------------- |
|Create CloudCertificationAuthority| This action creates a new CA in Intune Cloud PKI.|
| Search CloudCertificationAuthority| This action searches for CAs available in Intune Cloud PKI. |
|Get CloudCertificationAuthority | This action retrieves a specific CA by its ID in Intune Cloud PKI |
|Patch CloudCertificationAuthority | This action updates the properties of an existing CA in Intune Cloud PKI |
| Delete CloudCertificationAuthority|This action deletes an existing CA in Intune Cloud PKI. |
|Search CloudCertificationAuthorityLeafCertificate | This action retrieves all leaf certificates issued by a specific CA in the Cloud PKI service. |
|RevokeLeafCertAsync CloudCertificationAuthorityLeafCertificate | This action revokes a specific leaf certificate issued by a CA in the Cloud PKI service. |
|UploadExternallySignedCertificationAuthorityCertificateAsync CloudCertificationAuthority| This action uploads an externally signed CA certificate to an existing CA in Intune Cloud PKI. |
|ChangeCloudCertificationAuthorityStatusAsync CloudCertificationAuthority| This action changes the status of an existing CA in Intune Cloud PKI. |
|RevokeCloudCertificationAuthorityCertificateAsync CloudCertificationAuthority | This action revokes the CA certificate of an existing CA in Intune Cloud PKI, which renders it invalid. |  

## Prerequisites

To access the audit logs for Intune Cloud PKI, you must have:

- An Intune Cloud PKI license.
- An Intune service administrator role.
- An access token for the Microsoft Graph API.

You must also be assigned the following Microsoft Graph API permissions:  

- *DeviceManagementApps.Read.All*
- *DeviceManagementApps.ReadWrite.All*  

## Access logs

You can access the audit logs for Microsoft Cloud PKI in the Microsoft Intune admin center or through the Microsoft Graph API.

### Microsoft Intune admin center  

In the admin center, go to **Tenant Administration** > **Audit Logs**.

### Microsoft Graph API

The Microsoft Graph API is a unified endpoint that enables you to access data and services across Microsoft 365, including Cloud PKI. You can use the Microsoft Graph API to query, filter, and export the audit logs for Cloud PKI actions.

1. Make a GET request to ``https://graph.microsoft.com/beta/deviceManagement/auditEvents``.

2. Use the `$filter` query parameter to filter the audit logs. Available filters include:
   - activityType
   - activityDateTime  
   - displayName  
   - ID properties

For example, you can use the following query to filter the audit logs by the Intune Cloud PKI category and the CreateCaAsync action:  

`GET  https://graph.microsoft.com/beta/deviceManagement/auditEvents?$filter=activityType eq 'Create CloudCertificationAuthority'`  

As another example, the following query requests audit revocation logs between the dates of January 9 and January 10.

`GET https://graph.microsoft.com/beta/deviceManagement/auditEvents?$filter=activityType eq 'RevokeLeafCertAsync CloudCertificationAuthorityLeafCertificate' and %20activityDateTime%20gt%202024-01-09T00:00:00Z%20and%20activityDateTime%20le%202024-01-11T00:00:00Z&$orderby=activityDateTime%20desc`  
