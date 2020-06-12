---
title: Tenant attach data collection
titleSuffix: Configuration Manager
description: Learn about the diagnostics data that Configuration Manager collects for tenant attach features.
ms.date: 06/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 4b305a71-9ad8-4332-9692-d51554158981
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Tenant attach data collection

*Applies to: Configuration Manager (current branch)*

<!-- 6505626 -->
When you attach your Configuration Manager site with a Microsoft Intune tenant, the site sends additional data to Microsoft. This article summarizes the data that's sent.

Tenant attach allows the Microsoft Endpoint Manager admin center to be the Configuration Manager console in the cloud. The architecture allows the site to synchronize data to your Intune tenant. You can then query and present data from your on-premises environment in the cloud console in real time without active synchronization. Tenant attach uses a mixture of these methods to provide efficient up-to-date information in the cloud console.

For more general information on the data that Configuration Manager collects, see [Diagnostics and usage data for Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

> [!IMPORTANT]
> The Microsoft data handling policies are described in the [Microsoft Intune Privacy Statement](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). We only use your customer data to provide you the services you signed up for.

## Applications
<!-- 6502080 -->

For each Windows Installer (msi) deployment type:

- **ProductName**: The name of the application
- **Publisher**: The entity that published the software
- **Version**: The version of the application
- **ProductLanguage**: The language code for the application
- **ProgramID**: An identifier for the deployment type

## Device sync
<!-- 6505639 -->

For each device:

- **SMSID**: The unique identifier of your Configuration Manager hierarchy
- **AADTenantID**: The unique identifier of your Azure Active Directory (Azure AD) tenant
- **AADDeviceID**: The unique identifier of the device in Azure AD
- **Name**: The device's host name
- **DeviceOS**: The name of the device's operating system. For example, `Microsoft Windows NT Server 6.3`
- **DeviceOSBuild**: The build version of the device's operating system. For example, `10.0.19041`
- **AADPrimaryUserID**: The unique identifier of the device's primary user in Azure AD
- **PrimaryUserCount**: The number of primary users on the device
- **IsComanaged**: The co-managed state of the device
- **Model**: The device model
- **Manufacturer**: The device manufacturer
- **SerialNumber**: The device serial number
- **DomainNames**: Any domain names for the device
- **SenseID**
- **IsRevoked**
- **ApprovalStatus**: The device's approval status in Configuration Manager
- **AADIdentitySource**
- **OfficeInstallGroup**
- **SKU**
- **ProductType**

## Windows Defender Advanced Threat Protection (ATP)
<!-- 6505652 -->

For any collection that you select for ATP policy deployment:

- **CollectionId**: The unique identifier of the collection. For example, `ABC00014`
- **CollectionName**: The name of the collection. For example, `All Windows servers`
- **CollectionType**: Identifies whether it's a device or user collection.
- **CollectionSize**: A general category of size determined by the number of members. Current options are: small, medium, and large.
- **IsDeleted**: Determines whether you deleted the collection from the site.
- **PolicyId**: The unique identifier (GUID) of the policy object
- **PolicyVersion**: The version of the policy
- **PolicyState**
- **ErrorCode**
- **LastUpdateTime**
- **AssignmentVersion**
- **AssignmentState**
- **CountTargeted**: The count of devices that you target with this policy
- **CountCompliant**: The count of devices that are compliant with this policy
- **CountNonCompliant**: The count of devices that aren't compliant with this policy
- **CountFailed**: The count of devices that failed to process this policy
- **CountActivated**
- **CountEnforced**
- **LastSummaryTime**: The last time the site summarized policy compliance
- **SummaryType**: Whether summarization is for users or devices
- **SiteNumber**: An identifier for the site in your hierarchy

## See also

For more information about related privacy aspects, see the following articles:

- [Microsoft Intune Privacy Statement](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 and privacy compliance](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licensing terms and documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Security and privacy at Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/)  
- [Confidence in the trusted cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Trust Center](https://www.microsoft.com/trustcenter)  
