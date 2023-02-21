---
# required metadata
title: Connect to the Data Warehouse with Power BI
titleSuffix: Microsoft Intune
description: You can download a file for use with Microsoft Power BI that allows you to load interactive, dynamically generated reports for your Microsoft Intune tenant.
keywords: Intune Data Warehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/24/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 5E5A35D3-88F8-441B-8A0B-C5D7A1E5137B

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

# Connect to the Data Warehouse with Power BI

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

You can use the Power BI Compliance app to load interactive, dynamically generated reports for your Intune tenant. Additionally, you can load your tenant data in Power BI using the OData link. Intune provides connection settings to your tenant so that you can view the following sample reports and charts related to:  

- Devices
- Enrollment
- App protection policy
- Compliance policy
- Device configuration profiles
- Software updates
- Device inventory logs

There are also trends highlighted for the enrollment, compliance, device configuration profile, and software updates. Sample charts and reports apply user-friendly filters to the canvas. To use advanced filters, check out the **Filter** pane in Power BI Desktop.

> [!NOTE]
> Power BI template apps enable Power BI partners to build Power BI apps with little or no coding, and deploy them to any Power BI customer. For example, you can use the Power BI compliance report template in V2.0. V2.0 includes an improved design, as well as changes to the calculations and data that is being surfaced as part of the template. For more information, see [Update a template app](/power-bi/service-template-apps-install-distribute#update-a-template-app), [Intune Compliance (Data Warehouse) app](https://appsource.microsoft.com/product/power-bi/pbi_intune.intune_compliance_dw_app-preview?flightCodes=65ede247-5273-43b8-8a25-b89c7d211fbd), and [What are Power BI template apps?](/power-bi/service-template-apps-overview)

The following steps show you how to download the Power BI file and how to use the OData link with Power BI.

[!INCLUDE [reports-credential-reqs](../includes/reports-credential-reqs.md)]

## Install Power BI

Install the latest version of [Power BI Desktop](https://aka.ms/intune/datawarehouseapi/installpowerbi). For more information, see [Power BI Desktop](https://powerbi.microsoft.com/desktop).

## Load the data and reports using the Power BI Intune Compliance Data Warehouse App

The Power BI [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) app contains information for your tenant and a set of prebuilt reports based on the Data Warehouse data model.

> [!NOTE]
> The Power BI Intune Compliance Data Warehouse app is not supported for Azure Government cloud environments.

1. Navigate to the **AppSource** page of the [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) app to begin the installation process.
2. Click the **Get It Now** button, and then click **Continue**.
3. When prompted to install the Power BI app, click **Install**.
4. After the installation completes, click on the **Intune Compliance (Data Warehouse)** app tile.
5. Click the **Connect** button. The **Connect to Intune Compliance (Data Warehouse)** dialog is displayed.
6. Click the **Sign in** button.
7. Sign in with a user account that has access to the Intune Data Warehouse for the tenant that has reports you want to view.
8. To view the included dashboard, click the **Dashboards** tab, then click the **Compliance Overview** dashboard.
9. To view all the available reports, click the **Reports** tab, then click the **Compliance V1.0** report. Browse through the report pages by clicking on the tabs at the bottom.
10. To make it easy to navigate back to these reports later, click the star next to the **Compliance V1.0** report. This will add the report to your Power BI favorites.

Alternatively, you can install the app from the Microsoft Intune admin center:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Reports** > **Intune Data warehouse** > **Data warehouse**.
3. Select **Get Power BI App** to access and share pre-created Power BI reports for your tenant in the browser.
4. Follow steps 2-10 above.

## Load the data in Power BI using the OData link

With a client authenticated to Azure AD, the OData URL connects to the RESTful endpoint in the Data Warehouse API that exposes the data model to your reporting client. Follow these instructions to use Power BI Desktop to connect and create your own reports. You are not limited to Power BI Desktop, but can use your favorite analytic tool with the OData URL provided the client supports OAUTH2.0 authentication and the OData v4.0 standard.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Reports** > **Intune Data warehouse** > **Data warehouse**.
3. Retrieve the custom feed URL from the reporting blade, for example:<br>
    `https://fef.{yourtenant}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`
4. Open **Power BI Desktop**.
5. Choose **File** > **Get Data**. Select **OData feed**.
6. Choose **Basic**.
7. Type or paste the **OData URL** into the URL box.
8. Select **OK**.
9. If you have not authenticated to Azure AD for your tenant from the Power BI desktop client, type your credentials. To gain access to your data, you must authorize with Azure Active Directory (Azure AD) using OAuth 2.0.  
    1. Select **Organizational account**.  
    2. Type your username and password.  
    3. Select **Sign In.**  
    4. Select **Connect**.  
10. Select **Load**.

## Next steps

You can find the answers to questions about your environment such as the number of devices enrolled by day over the last week. You can gain insight into your Intune tenant and client population using the Intune Data Warehouse Power BI reports retrieved from the blade in the Microsoft Intune admin center. However, Intune provides a number of additional ways to extend or reuse the data. Power BI and the Intune Data Warehouse API provide additional functionality, for example:

<!-- - You can use Power BI Desktop to create additional report types with your data. For example, you could create a custom chart representing the ratio of device manufactures in your enterprise. For more information about creating custom reports with Power BI and the Intune Data Warehouse, see `BLOG POST ON POWER BI`. -->
- Your tenant data is organized to help you pull insight from your data. For more information about how the data is organized, see [Data Warehouse Data Model](reports-ref-data-model.md).
- You can also access the data from a RESTful interface and incorporate the data into your own app. For more information, see [Get data from the Data Warehouse API with a REST client](reports-proc-data-rest.md).
