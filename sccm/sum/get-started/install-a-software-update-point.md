---

title: Install and configure a software update point
titleSuffix: "Configuration Manager"
description: "Primary sites require a software update point on the central administration site for software updates compliance assessment and to deploy software updates to clients."
keywords:
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/30/2017
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396


---


# Install and configure a software update point  

*Applies to: System Center Configuration Manager (Current Branch)*


> [!IMPORTANT]  
>  Before you install the software update point site system role, you must verify that the server meets the required dependencies and determines the software update point infrastructure on the site. For more information about how to plan for software updates and to determine your software update point infrastructure, see [Plan for software updates](../plan-design/plan-for-software-updates.md).  

 The software update point is required on the central administration site and on the primary sites in order to enable software updates compliance assessment and to deploy software updates to clients. The software update point is optional on secondary sites. The software update point site system role must be created on a server that has WSUS installed. The software update point interacts with the WSUS services to configure the software update settings and to request synchronization of software updates metadata. When you have a Configuration Manager hierarchy, install and configure the software update point on the central administration site first, then on child primary sites, and then optionally, on secondary sites. When you have a stand-alone primary site, not a central administration site, install and configure the software update point on the primary site first, and then optionally, on secondary sites. Some settings are only available when you configure the software update point on a top-level site. There are different options that you must consider depending on where you installed the software update point.  

> [!IMPORTANT]  
>  You can install more than one software update points on a site. The first software update point that you install is configured as the synchronization source, which synchronizes the updates from Microsoft Update or from the upstream synchronization source. The other software update points on the site are configured as replicas of the first software update point. Therefore, some settings are not available after you install and configure the initial software update point.  

> [!IMPORTANT]  
>  It is not supported to install the software update point site system role on a server that has been configured and used as a standalone WSUS server or using a software update point to directly manage WSUS clients. Existing WSUS servers are only supported as upstream synchronization sources for the active software update point. See [Synchronize from an upstream data source location](#BKMK_wsussync)

 You can add the software update point site system role to an existing site system server or you can create a new one. On the **System Role Selection** page of the **Create Site System Server Wizard** or **Add Site System Roles Wizard** , depending on whether you add the site system role to a new or existing site server, select **Software update point**, and then configure the software update point settings in the wizard. The settings are different depending on the version of Configuration Manager that you use. For more information about how to install site system roles, see [Install site system roles](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Use the following sections for information about the software update point settings on a site.  

## Proxy server settings  
 You can configure the proxy server settings on different pages of the **Create Site System Server Wizard** or **Add Site System Roles Wizard** depending on the version of Configuration Manager that you use.  

-   You must configure the proxy server, and then specify when to use the proxy server for software updates. Configure the following settings:  

    -   Configure the proxy server settings on the **Proxy** page of the wizard or on the **Proxy** tab in Site system Properties. The proxy server settings are site system specific, which means that all site system roles use the proxy server settings that you specify.  

    -   Specify whether to use the proxy server when Configuration Manager synchronizes the software updates and when it downloads content by using an automatic deployment rule. Configure the software update point proxy server settings on the **Proxy and Account Settings** page of the wizard or on the **Proxy and Account Settings** tab in Software update point Properties.  

        > [!NOTE]  
        >  The **Use a proxy when downloading content by using automatic deployment rules** setting is available but it is not used for a software update point on a secondary site. Only the software update point on the central administration site and primary site downloads content from the Microsoft Update page.  

> [!IMPORTANT]  
>  By default, the **Local System** account for the server on which an automatic deployment rule was created is used to connect to the Internet and download software updates when the automatic deployment rules run. When this account does not have access to the Internet, software updates fail to download and the following entry is logged to ruleengine.log: **Failed to download the update from internet. Error = 12007**. Configure the credentials to connect to the proxy server when the Local System account does not have Internet access.  


## WSUS settings  
 You must configure WSUS settings on different pages of the **Create Site System Server Wizard** or **Add Site System Roles Wizard** depending on the version of Configuration Manager that you use, and in some cases, only in the properties for the software update point, also known as Software Update Point Component Properties. Use the information in the following sections to configure the WSUS settings.  

### <a name="BKMK_wsusport"></a>WSUS port settings  
 You must configure the WSUS port settings on the Software Update Point page of the wizard or in the properties of the software update point. Use the following procedure to determine the port settings used by WSUS.  

#### To determine the port settings used in IIS  

 1.  On the WSUS server, open Internet Information Services (IIS) Manager.  

 2.  Expand **Sites**, right-click the Web site for the WSUS server, and then click **Edit Bindings**. In the Site Bindings dialog, the HTTP and HTTPS port values are displayed in the **Port** column.


### Configure SSL communications to WSUS  
 You can configure SSL communication on the **General** page of the wizard or on the **General** tab in the properties of the software update point.  

 For more information about how to use SSL, see [Decide whether to configure WSUS to use SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### WSUS Server Connection Account  
 You can configure an account to be used by the site server when it connects to WSUS that runs on the software update point. When you do not configure this account, the Configuration Manager uses the computer account for the site server to connect to WSUS. Configure the WSUS Server Connection Account on the **Proxy and Account Settings** page of the wizard, or on the **Proxy and Account Settings** tab in Software update point Properties.  You can configure the account in different places of the wizard depending on the version of Configuration Manager that you use.  

 For more information about Configuration Manager accounts, see [Accounts used in System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## Synchronization source  
 You can configure the upstream synchronization source for software updates synchronization on the **Synchronization Source** page of the wizard, or on the on the **Sync Settings** tab in Software Update Point Component Properties. Your options for the synchronization source vary depending on the site.  

 Use the following table for the available options when you configure the software update point at a site.  

|Site|Available synchronization source options|  
|----------|----------------------------------------------|  
|-   Central administration site<br />-   Stand-alone primary site|-   Synchronize from the Microsoft Update website<br />-   Synchronize from an upstream data source location<br />-   Do not synchronize from Microsoft Update or upstream data source|  
|-   Additional software update points at a site<br />-   Child primary site<br />-   Secondary site|-   Synchronize from an upstream data source location|  

 The following list provides more information about each option that you can use as the synchronization source:  

-   **Synchronize from Microsoft Update**: Use this setting to synchronize software updates metadata from Microsoft Update. The central administration site must have Internet access; otherwise, synchronization will fail. This setting is available only when you configure the software update point on the top-level site.  

    > [!NOTE]  
    >  When there is a firewall between the software update point and the Internet, the firewall might need to be configured to accept the HTTP and HTTPS ports that are used for the WSUS Web site. You can also choose to restrict access on the firewall to limited domains. For more information about how to plan for a firewall that supports software updates, see [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **<a name="BKMK_wsussync"></a>Synchronize from an upstream data source location**: Use this setting to synchronize software updates metadata from the upstream synchronization source. The child primary sites and secondary sites are automatically configured to use the parent site URL for this setting. You have the option to synchronize software updates from an existing WSUS server. Specify a URL, such as https://WSUSServer:8531, where 8531 is the port that is used to connect to the WSUS server.  

-   **Do not synchronize from Microsoft Update or upstream data source**: Use this setting to manually synchronize software updates when the software update point at the top-level site is disconnected from the Internet. For more information, see [Synchronize software updates from a disconnected software update point](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  When there is a firewall between the software update point and the Internet, the firewall might need to be configured to accept the HTTP and HTTPS ports that are used for the WSUS Web site. You can also choose to restrict access on the firewall to limited domains. For more information about how to plan for a firewall that supports software updates, see [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 You can also configure whether to create WSUS reporting events on the **Synchronization Source** page of the wizard or on the on the **Sync Settings** tab in Software Update Point Component Properties. Configuration Manager does not use these events; therefore, you will normally choose the default setting **Do not create WSUS reporting events**.  

## Synchronization schedule  
 Configure the synchronization schedule on the **Synchronization Schedule** page of the wizard or in the Software Update Point Component Properties. This setting is configured only on the software update point at the top-level site.  

 If you enable the schedule, you can configure a recurring simple or custom synchronization schedule. When you configure a simple schedule, the start time is based on the local time for the computer that runs the Configuration Manager console at the time when you create the schedule. When you configure the start time for a custom schedule, it is based on the local time for the computer that runs the Configuration Manager console.  

> [!TIP]  
>  Schedule software updates synchronization to run by using a time-frame that is appropriate for your environment. One typical scenario is to set the software updates synchronization schedule to run shortly after the Microsoft regular security update release on the second Tuesday of each month, which is normally referred to as Patch Tuesday. Another typical scenario is to set the software updates synchronization schedule to run daily when you use software updates to deliver the Endpoint Protection definition and engine updates.  

> [!NOTE]  
>  When you choose not to enable software updates synchronization on a schedule, you can manually synchronize software updates from the **All Software Updates** or **Software Update Groups** node in the Software Library workspace. For more information, see [synchronize software updates](synchronize-software-updates.md).  

## Supersedence rules  
 Configure the supersedence settings on the **Supersedence Rules** page of the wizard or on the **Supersedence Rules** tab in Software Update Point Component Properties. You can configure the supersedence rules only on the top-level site.  

 On this page, you can specify that the superseded software updates are immediately expired, which prevents them from being included in new deployments and flags the existing deployments to indicate that the superseded software updates contain one or more expired software updates. Or, you can specify a period of time before the superseded software updates are expired, which allows you to continue to deploy them. For more information, see [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  The **Supersedence Rules** page of the wizard is available only when you configure the first software update point at the site. This page is not displayed when you install additional software update points.  

## Classifications  
 Configure the classifications settings on the **Classifications** page of the wizard, or the on the **Classifications** tab in Software Update Point Component Properties. For more information about software update classifications, see [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  The **Classifications** page of the wizard is available only when you configure the first software update point at the site. This page is not displayed when you install additional software update points.  

> [!TIP]  
>  When you first install the software update point on the top-level site, clear all of the software updates classifications. After the initial software updates synchronization, configure the classifications from an updated list, and then re-initiate synchronization. This setting is configured only on the software update point at the top-level site.  

## Products  
 Configure the product settings on the **Products** page of the wizard, or the on the **Products** tab in Software Update Point Component Properties.  

> [!NOTE]  
>  The **Products** page of the wizard is available only when you configure the first software update point at the site. This page is not displayed when you install additional software update points.  

> [!TIP]  
>  When you first install the software update point on the top-level site, clear all of the products. After the initial software updates synchronization, configure the products from an updated list, and then re-initiate synchronization. This setting is configured only on the software update point at the top-level site.  

## Languages  
 Configure the language settings on the **Languages** page of the wizard, or the on the **Languages** tab in Software Update Point Component Properties. Specify the languages for which you want to synchronize software update files and summary details. The **Software Update File** setting is configured at each software update point in the Configuration Manager hierarchy. The **Summary Details** settings are configured only on the top-level software update point. For more information, see [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  The **Languages** page of the wizard is available only when you install the software update point at the central administration site. You can configure the Software Update File languages at child sites from the **Languages** tab in Software Update Point Component Properties.  

## Next steps
You installed the software update point starting at the top-most site in your Configuration Manager hierarchy. Repeat the procedures in this topic to install the software update point on child sites.

Once you have your software update points installed, go to [synchronize software updates](synchronize-software-updates.md).
