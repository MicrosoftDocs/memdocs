---
title: Desktop Analytics data privacy
titleSuffix: Configuration Manager
description: Desktop Analytics is committed to customer data privacy
ms.date: 07/07/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# Desktop Analytics data privacy

Desktop Analytics is fully committed to customer data privacy, centering on these tenets:

- **Transparency:** We fully document the Windows diagnostic events. Review them with your company's security and compliance teams. The Windows Diagnostic Data Viewer lets you see diagnostic data sent from a given device. For more information, see [Diagnostic Data Viewer overview](/windows/configuration/diagnostic-data-viewer-overview).

- **Control:** You control the level of diagnostic data to share with Microsoft.

- **Security:** Microsoft protects your data with strong security and encryption.

- **Trust:** Desktop Analytics supports the Microsoft [Privacy Statement](https://privacy.microsoft.com/privacystatement) and [Online Service Terms](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

For more information, see [Windows 10 & privacy compliance: A guide for IT and compliance professionals](/windows/privacy/windows-10-and-privacy-compliance).

## Data flow

The following illustration shows how diagnostic data flows from individual devices through the Diagnostic Data Service, transient storage, and to your Log Analytics workspace:

:::image type="content" source="media/da-data-flow.png" alt-text="Diagram illustrating flow of diagnostic data from devices.":::

1. You sign in to the Microsoft Intune admin center, and onboard to Desktop Analytics. You create the Azure AD app to connect with Configuration Manager. When you set up Desktop Analytics, you create an Azure Log Analytics workspace in the location of your choice.

2. You connect Configuration Manager and enroll devices.

    1. You configure the Desktop Analytics cloud service in Configuration Manager with the Azure AD app details.

    2. Within 15 minutes, and every hour after, Configuration Manager synchronizes via the Intune microservice the following data with Desktop Analytics using your tenant ID. The site sends all data over an encrypted HTTPS channel to your Endpoint Manager account in the public cloud.

      - Information about device collections necessary to [create deployment plans](create-deployment-plans.md). This information includes collection ID, support ID, collection name, and device count.
      - Information required to [enroll devices](enroll-devices.md). This information includes collection ID, SMS unique identifier, OS build version, device name, and serial number.
      - Information from the [monitor connection health](monitor-connection-health.md) dashboard. This information includes the count of devices per health state, and device properties.
      - Information about deployment plans, which includes the collection ID, deployment ID, pilot or production deployment type, and count of devices per upgrade decision.

    3. Configuration Manager sets the commercial ID, diagnostic data level, and other settings for the devices in the target collection. This configuration specifies the devices to appear in your Desktop Analytics workspace.

    4. You deploy compatibility updates to all target devices.

3. Devices send diagnostic data to the Microsoft Diagnostic Data Management service for Windows. All diagnostic data is encrypted over HTTPS and uses certificate pinning during transfer from the device to this service. The Microsoft Data Management Service is hosted in the United States. For more information, see [How Microsoft handles diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#how-microsoft-handles-diagnostic-data).

    Application faults, kernel faults, unresponsive applications, and other application-specific issues use the Windows Error Reporting API to send application-specific problem reports to Microsoft. For more information about this dataflow, see [Using WER](/windows/win32/wer/using-wer).

4. Each day, Microsoft produces a snapshot of IT-focused insights. This snapshot combines the diagnostic data from Windows with your input for the enrolled devices. This process happens in transient storage, which is only used by Desktop Analytics. The transient storage is hosted in Microsoft data centers in the United States with a 28-day retention period. All data is sent over an HTTPS-encrypted channel. The snapshots are segregated by commercial ID.

5. The snapshots are then copied to your Azure Log Analytics workspace. This data transfer happens over HTTPS through the webhook ingestion protocol, which is a feature of Log Analytics. Desktop Analytics doesn't have any read or write permissions to your Log Analytics storage. Desktop Analytics calls the webhook API with a shared access signature (SAS) URI. Then Log Analytics gets the data from the storage tables over HTTPS.

6. Desktop Analytics stores your input in Log Analytics storage. These configurations include deployment plans and asset decisions for upgrade and importance.

## Other resources

For privacy-related frequently asked questions for Desktop Analytics, see [Privacy FAQ](/mem/configmgr/desktop-analytics/faq#privacy).

For more information about related privacy aspects, see the following articles:

- [Windows 10 & privacy compliance: A guide for IT and compliance professionals](/windows/privacy/windows-10-and-privacy-compliance)

- [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

- [Changes to Windows diagnostic data collection](/windows/privacy/changes-to-windows-diagnostic-data-collection)

- [Windows 7, Windows 8, and Windows 8.1 appraiser diagnostic data events and fields](/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)

- [Windows 10 version 1809 basic level Windows diagnostic events and fields](/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)

- [Windows 10 version 1709 enhanced diagnostic data events and fields used by Desktop Analytics](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)

- [Windows Setup error reporting](/windows/deployment/upgrade/windows-error-reporting)

- [Diagnostic Data Viewer overview](/windows/privacy/diagnostic-data-viewer-overview)

- [Licensing terms and documentation](https://www.microsoft.com/licensing/terms)

- [Log Analytics data security](/azure/azure-monitor/logs/data-security)

- [Security and privacy at Microsoft Azure data centers](https://azure.microsoft.com/global-infrastructure/)

- [Confidence in the trusted cloud](https://azure.microsoft.com/overview/trusted-cloud/)

- [Trust Center](https://www.microsoft.com/trustcenter)

Separate from Desktop Analytics, Configuration Manager sends diagnostic and usage data to Microsoft. Microsoft uses this data to improve the installation experience, quality, and security of future releases of Configuration Manager. For more information, see [Diagnostics and usage data for Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
