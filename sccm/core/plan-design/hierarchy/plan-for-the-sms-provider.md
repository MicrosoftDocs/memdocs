---
title: Plan for the SMS Provider
titleSuffix: Configuration Manager
description: Learn about the SMS Provider site system role in Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Plan for the SMS Provider 

*Applies to: System Center Configuration Manager (Current Branch)*

To manage Configuration Manager, you use a Configuration Manager console that connects to an instance of the **SMS Provider**. By default, an SMS Provider installs on the site server when you install a central administration site or primary site. 



##  <a name="BKMK_PlanSMSProv"></a> About the SMS Provider  

The SMS Provider is a Windows Management Instrumentation (WMI) provider that assigns **read** and **write** access to the Configuration Manager database at a site.  

- Each central administration site and primary site require at least one SMS Provider. You can install additional providers as needed.  

- The **SMS Admins** security group provides access to the SMS Provider. Configuration Manager automatically creates this group on the site server, and on each computer where you install an instance of the SMS Provider. For more information, see [SMS Admins](/sccm/core/plan-design/hierarchy/accounts#sms-admins).  

- Secondary sites don't support the SMS Provider role.  

Configuration Manager administrative users use an SMS Provider to access information that's stored in the database. To do so, admins can use the Configuration Manager console, Resource Explorer, tools, and custom scripts. The SMS Provider doesn't interact with Configuration Manager clients. When a Configuration Manager console connects to a site, it queries WMI on the site server to locate an instance of the SMS Provider to use.  

The SMS Provider helps enforce Configuration Manager security. It returns only the information that the console user is authorized to view.  

Starting in version 1810, the SMS Provider now provides read-only API interoperability access to WMI over HTTPS, called the **administration service**. This REST API can be used in place of a custom web service to access information from the site. For more information, see [Administration service](#bkmk_admin-service). 

> [!IMPORTANT]  
>  When each instance of the SMS Provider for a site is offline, Configuration Manager consoles can't connect to the site.  

For more information about how to manage the SMS Provider, see [Manage the SMS Provider](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).  



## Installation prerequisites  

 To support the SMS Provider, the target server must meet the following prerequisites:  

-   In the same domain as the site server and the site database site systems  

-   Can't have a site system role from a different site  

-   Can't already have an SMS Provider from any site  

-   Run a supported OS version  

-   At least 650 MB of free disk space to support the Windows ADK components. For more information about Windows ADK and the SMS Provider, see [OS deployment requirements](#BKMK_WAIKforSMSProv).  

-   Enable Windows server role **Web Server (IIS)**  

    > [!Note]  
    > Every SMS Provider attempts to install the [administration service](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service), which requires a certificate. This service has a dependency on IIS to bind that certificate to HTTPS port 443. If you enable [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http), then the site binds that certificate using IIS APIs. If your site uses PKI, you need to manually bind a PKI certificate in IIS on the SMS Provider.  


##  <a name="bkmk_location"></a> Locations  

When you install a site, you automatically install the first SMS Provider for the site. You can specify any of the following supported locations for the SMS Provider:  

-   The site server  

-   The site database server  

-   Another server, which meets the [installation prerequisites](#installation-prerequisites)  


To view the locations of each SMS Provider for a site: 

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the **Sites** node.  

2. Select the desired site from the list, and then choose **Properties** in the ribbon.  

3. On the **General** tab of the site **Properties**, view the **SMS Provider location** field.    


Each SMS Provider supports simultaneous connections from multiple requests. The only limitations on these connections are the number of server connections that are available to Windows, and the available resources on the server to service the connection requests.  

After you install a site, you can run Configuration Manager setup on the site server again. Use setup to change the location of an existing SMS Provider, or to install additional SMS Providers at that site. Install only one SMS Provider on a computer. A computer can't host an SMS Provider from more than one site.  


### Choosing a location 

The following sections describe the advantages and disadvantages of installing an SMS Provider on each supported location:  

#### Configuration Manager site server

- **Advantages:**  

    -   The SMS Provider doesn't use the system resources of the site database computer.  

    -   This location can provide better performance than an SMS Provider located on a computer other than the site server or site database computer.  

- **Disadvantages:**  

    -   The SMS Provider uses system and network resources that could be dedicated to site server operations.  


#### SQL Server that hosts the site database

- **Advantages:**  

    -   The SMS Provider doesn't use system resources on the site server.  

    -   This location can provide the best performance of the three locations, if sufficient server resources are available.  

- **Disadvantages:**  

    -   The SMS Provider uses system and network resources that could be dedicated to site database operations.  

    -   When the site database is hosted on a clustered instance of SQL Server, you can't use this location.  


#### Computer other than the site server or site database server

- **Advantages:**  

    -   SMS Provider doesn't use site server or site database system resources.  

    -   This type of location lets you deploy additional SMS Providers to provide high availability for connections.  

- **Disadvantages:**  

    -   The SMS Provider performance might be reduced. This behavior is due to the additional network activity that it requires to coordinate with the site server and the site database computer.  

    -   This server must be always accessible to the site database server, and to all computers with the Configuration Manager console installed.  

    -   This location can use system resources that would otherwise be dedicated to other services.  



## <a name="bkmk_auth"></a> Authentication
<!--1357013-->

Starting in version 1810, you can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. It applies to all components that access the SMS Provider. For example, the Configuration Manager console, SDK methods, and Windows PowerShell cmdlets. 


### Configure authentication

To configure this setting, first sign in to Windows with the intended authentication level. 

> [!Important]  
> This configuration is a hierarchy-wide setting. Before you change this setting, make sure that all Configuration Manager administrators can sign in to Windows with the required authentication level. 

To configure this setting, use the following steps:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2. Select **Hierarchy Settings** in the ribbon.  

3. Switch to the **Authentication** tab. Select the desired [authentication level](#authentication-levels), and then select **OK**.  

    - Only when necessary, select **Add** to exclude specific users or groups. For more information, see [Exclusions](#exclusions).  


### Authentication levels

The following levels are available:

- **Windows authentication**: Require authentication with Active Directory domain credentials. This setting is the previous behavior, and the current default setting. When you update the site, there's no change to the authentication level.  

- **Certificate authentication**: Require authentication with a valid certificate that's issued by a trusted PKI certificate authority. You don't configure this certificate in Configuration Manager. Configuration Manager requires the administrator to be signed into Windows using PKI.  

- **Windows Hello for Business authentication**: Require authentication with strong two-factor authentication that's tied to a device and uses biometrics or a PIN. For more information, see [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).   


### Exclusions

From the **Authentication** tab of Hierarchy Settings, you can also exclude certain users or groups. Use this option sparingly. For example, when specific users require access to the Configuration Manager console, but can't authenticate to Windows at the required level. It may also be necessary for automation or services that run under the context of a system account.



##  <a name="BKMK_SMSProvLanguages"></a> About SMS Provider languages  

The SMS Provider operates independently of the display language of the server where you install it.  

When an administrative user or Configuration Manager process requests data by using the SMS Provider, it attempts to return that data in a format that matches the OS language of the requesting computer.

The way it attempts to match the language is indirect. The SMS Provider doesn't translate information from one language to another. When it returns data for display in the Configuration Manager console, the display language of the data depends on the source of the object and type of storage.  

When Configuration Manager stores data for an object in the database, the available languages depend on the following factors:  

-   Configuration Manager stores objects that it creates by using support for multiple languages. It stores the object in the site database by using the languages that you configure for the site when you run setup. The Configuration Manager console displays these objects in the display language of the requesting computer, when that language is available for the object. If the console can't display the object in the display language of the requesting computer, it displays the object in the default language, which is English.  

-   Configuration Manager stores objects that an administrative user creates by using the language that was used to create the object. These objects display in the Configuration Manager console in this same language. The SMS Provider can't translate them, and they don't have multiple language options.  



##  <a name="BKMK_MultiSMSProv"></a> Use multiple SMS Providers  

 After a site completes installation, you can install additional SMS Providers for the site. To install additional SMS Providers, run Configuration Manager setup on the site server. 

Consider installing additional SMS Providers when any of the following are true:  

- Many administrative users need to use the Configuration Manager console and connect to a site at the same time.  

- You use the Configuration Manager SDK, or other products, that might introduce frequent calls to the SMS Provider.  

- You have a business requirement for high availability of the SMS Provider.  

When you install multiple SMS Providers at a site, and a connection request is made, the site randomly assigns each new connection request to use an installed SMS Provider. You can't specify the SMS Provider to use with a specific connection session.  

> [!NOTE]  
>  Consider the advantages and disadvantages of each SMS Provider location. For more information, see [Locations](#bkmk_location). Balance these considerations with the information that you can't control which SMS Provider is used for each new connection.  

When you first connect a Configuration Manager console to a site, the connection queries WMI on the site server. This query identifies an instance of the SMS Provider that the console uses. This specific instance of the SMS Provider remains in use by the console until the session ends. If the session ends because the SMS Provider server is unavailable on the network, when you reconnect the console to the site, it repeats the initial query. It's possible the site assigns the same SMS Provider instance that's not available. If this behavior occurs, attempt to reconnect the console until the site returns an available SMS Provider.  



##  <a name="BKMK_SMSProvNamespace"></a> About the SMS Provider namespace  

The Configuration Manager WMI schema defines the structure of the SMS Provider. Schema namespaces describe the location of Configuration Manager data within the SMS Provider schema. The following table contains some of the common namespaces that the SMS Provider uses:  

|Namespace|Description|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|The SMS Provider, which is extensively used by the Configuration Manager console, Resource Explorer, Configuration Manager tools, and scripts.|  
|`Root\SMS\SMS_ProviderLocation`|The location of the SMS Provider computers for a site.|  
|`Root\CIMv2`|The location inventoried for WMI namespace information during hardware and software inventory.|  
|`Root\CCM`|Configuration Manager client configuration policies and client data.|  
|`Root\CIMv2\SMS`|The location of inventory reporting classes that the inventory client agent collects. Clients compile these settings during computer policy evaluation. These settings are based on the client settings configuration for the computer.|  



##  <a name="BKMK_WAIKforSMSProv"></a> OS deployment requirements

The computer where you install an instance of the SMS Provider requires a supported version of the Windows ADK.  

For more information about this requirement, see [Infrastructure requirements for OS deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10) and [Support for Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

When you manage OS deployments, the Windows ADK allows the SMS Provider to complete various tasks, such as:  

-   View WIM file details  

-   Add driver files to existing boot images  

-   Create boot ISO files  


The Windows ADK installation can require up to 650 MB of free disk space on each computer that installs the SMS Provider. This high disk space requirement is necessary for Configuration Manager to install the Windows PE boot images.  



## <a name="bkmk_admin-service"></a> Administration service
<!--3607711, fka 1321523-->

> [!Note]  
> In this version of Configuration Manager, the SMS Provider API is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  

Starting in version 1810, the SMS Provider provides read-only API interoperability access to WMI over HTTPS, called the **administration service**. This REST API can be used in place of a custom web service to access information from the site.

The **administration service** URL format is `https://<servername>/AdminService/wmi/<ClassName>` where `<servername>` is the the server where the SMS Provider is installed and `<ClassName>` is a valid Configuration Manager WMI class name. In version 1810, this class name doesn't include the `SMS_` prefix. In version 1902 and later, this class name is the same as the WMI class name. 

For example:
- 1810: `https://servername/AdminService/wmi/Site`
- 1902 and later: `https://servername/AdminService/wmi/SMS_Site`

> [!Note]  
> The administration service class names are case-sensitive. Make sure to use the proper capitalization, for example SMS_Site.

Make direct calls to this service with the Windows PowerShell cmdlet [Invoke-RestMethod](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-restmethod).

> [!Tip]  
> You can use this cmdlet in a task sequence. This action lets you access information from the site without requiring a custom web service to interface with the WMI provider. 

You can also use it to access site data from PowerBI using the OData connector option. 

The administration service logs its activity to the **adminservice.log** file.

### Enable the administration service through the CMG

The **SMS Provider** appears as a role with an option to allow communication over the cloud management gateway (CMG). The current use for this setting is to enable application approvals via email from a remote device. For more information, see [Approve applications](/sccm/apps/deploy-use/app-approval).

#### Prerequisites
- The server that hosts the SMS Provider requires .NET 4.5.2 or later.  

- Enable the SMS Provider to use a certificate. Use one of the following options:  

    - Enable [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http) (recommended)  

        > [!Note]  
        > When the site creates a certificate for the SMS Provider, it won't be trusted by the web browser on the client. Based on your security settings, accessing the REST provider, you may see a security warning.  

    - Manually bind a PKI-based certificate to port 443 in IIS on the server that hosts the SMS Provider role  

#### Process to enable the API through the CMG
1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node.  

2. Select the server with the **SMS Provider** role.  

3. In the details pane, select the **SMS Provider** role, and select **Properties** in the ribbon on the **Site Role** tab.  

4. Select the option to **Allow Configuration Manager cloud management gateway traffic for administration service**.  

