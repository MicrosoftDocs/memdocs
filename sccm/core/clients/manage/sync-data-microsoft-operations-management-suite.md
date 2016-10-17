---
title: "Sync data | Microsoft Operations Management Suite | System Center Configuration Manager"
description: "Sync data from System Center Configuration Manager to Microsoft Operations Management Suite."
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: nbigman
ms.author: nbigman
manager: angrobe
---
# Sync data from Configuration Manager to the Microsoft Operations Management Suite*Applies to: System Center Configuration Manager (Current Branch)*
You can use the Microsoft Operations Management Suite (OMS) Connector to sync data such as your collections from System Center Configuration Manager to OMS. This makes data from your Configuration Manager deployment visible in OMS.

## Add an OMS connection to Configuration Manager

In order to add an OMS connection, your Configuration Manager environment must first configure a [service connection point](../../../core/servers/deploy/configure/about-the-service-connection-point.md) in an [online mode](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). When you add an OMS connection to your environment, it will also install the Microsoft Monitoring Agent on the machine running this site system role.
1.  In the **Administration** workspace, select **OMS Connector**. In the ribbon, click on "Create connection to Operations Management Suite". This opens the **Connection to Operation Management Suite Wizard**. Select **Next**.
2.  On the **General** screen, confirm that you have the following information, then select **Next**.

    * Registered Configuration Manager as a “Web Application and/or Web API” management tool, and that you have the [client ID from this registration](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
    * Created a client key for the registered management tool in Azure Active Directory.
    * In the Azure Management Portal, provided the registered web app with permission to access OMS, as described in [Provide Configuration Manager with permissions to OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

3.  On the **Azure Active Directory** screen, configure your connection settings to OMS by providing your **Tenant**, **Client ID**, and **Client Secret Key**, then select **Next**.
4.  On the **OMS Connection Configuration** screen, provide your connection settings by filling in your **Azure subscription**, **Azure resource group**, and **Operations Management Suite Workspace**.
5.  Verify your connection settings on the **Summary** screen, then select **Next**. The **Progress** screen will show the connection status, then should **Complete**.

> [!NOTE]
> You must connect OMS to the top-tier site in your hierarchy. If you connect OMS to a standalone primary site and then add a central administration site to your environment, you must delete and recreate the OMS connection within the new hierarchy.

After you have linked Configuration Manager to OMS, you can add or remove collections, and view the properties of the OMS connection.

## Viewing Microsoft Operations Management Suite connection properties in Configuration Manager

1.  Navigate to **Cloud Services**, then select **OMS Connector** to open the **OMS Connection Properties** page.
2.  Within this page there are two tabs:
  * The **Azure Active Directory** tab shows your **Tenant**, **Client ID**, **Client secret key expiration**, and allows you to **Verify** your **Client secret key** if it has expired.
  * The **OMS Connection Properties** tab shows your **Azure subscription**, **Azure resource group**, **Operations Management Suite Workspace**, and a list of **Device collections that Operations Management Suite can get data for**. Use the **Add** and **Remove** buttons to modify which collections are allowed.
