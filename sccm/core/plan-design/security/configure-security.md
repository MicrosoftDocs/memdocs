---
title: "Configure security in System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: 5
author: Brenduns

---
# Configure security in System Center Configuration Manager
Use the information in this topic to help you configure the following security-related options for System Center Configuration Manager:  

-   [Configure Settings for Client PKI Certificates](#BKMK_ConfigureClientPKI)  

-   [Configure Signing and Encryption](#BKMK_ConfigureSigningEncryption)  

-   [Configure Role-Based Administration](#BKMK_ConfigureRBA)  

-   [Manage Accounts that are Used by Configuration Manager](#BKMK_ManageAccounts)  

##  <a name="BKMK_ConfigureClientPKI"></a> Configure settings for client PKI certificates  
If you want to use public key infrastructure (PKI) certificates for client connections to site systems that use Internet Information Services (IIS), use the following procedure to configure settings for these certificates.  

#### To configure client PKI certificate settings  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, click **Sites**, and then click the primary site to configure.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**, and then click the **Client Computer Communication** tab.  

    This tab is available on a primary site only. If you do not see the **Client Computer Communication** tab, check that you are not connected to a central administration site or a secondary site.  

4.  Click **HTTPS only** when you want clients that are assigned to the site to always use a client PKI certificate when they connect to site systems that use IIS. Or, click **HTTPS or HTTP** when you do not require clients to use PKI certificates.  

5.  If you selected **HTTPS or HTTP**, click **Use client PKI certificate (client authentication capability) when available** when you want to use a client PKI certificate for HTTP connections. The client uses this certificate instead of a self-signed certificate to authenticate itself to site systems. This option is automatically selected if you select **HTTPS only**.  

    When clients are detected to be on the Internet, or they are configured for Internet-only client management, they always use a client PKI certificate.  

6.  Click **Modify** to configure your chosen client selection method for when more than one valid PKI client certificate is available on a client, and then click **OK**.  

    For more information about the client certificate selection method, see [Planning for PKI client certificate selection](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Select or clear the check box for clients to check the Certificate Revocation list (CRL).  

    For more information about CRL checking for clients, see [Planning for PKI certificate revocation](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  If you must specify trusted root certification authority (CA) certificates for clients, click **Set**, import the root CA certificate files, and then click **OK**.  

    For more information about this setting, see [Planning for the PKI Trusted Root certificates and the Certificate Issuers List](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Click **OK** to close the properties dialog box for the site.  

Repeat this procedure for all primary sites in the hierarchy.  

##  <a name="BKMK_ConfigureSigningEncryption"></a> Configure Signing and Encryption  
Configure the most secure signing and encryption settings for site systems that all clients in the site can support. These settings are especially important when you let clients communicate with site systems by using self-signed certificates over HTTP.  

#### To configure signing and encryption for a site  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, click **Sites**, and then click the primary site to configure.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**, and then click the **Signing and Encryption** tab.  

    This tab is available on a primary site only. If you do not see the **Signing and Encryption** tab, check that you are not connected to a central administration site or a secondary site.  

4.  Configure the signing and encryption options that you want, and then click **OK**.  

    > [!WARNING]  
    >  Do not select **Require SHA-256** without first verifying that all clients that might be assigned to the site can support this hash algorithm, or they have a valid PKI client authentication certificate. You might have to install updates or hotfixes on clients to support SHA-256. For example, computers that run Windows Server 2003 SP2 must install a hotfix that is referenced in the [KB article 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  If you select this option and clients cannot support SHA-256 and use self-signed certificates, Configuration Manager rejects them. In this scenario, the SMS_MP_CONTROL_MANAGER component logs the message ID 5443.  

5.  Click **OK** to close the **Properties** dialog box for the site.  

Repeat this procedure for all primary sites in the hierarchy.  

##  <a name="BKMK_ConfigureRBA"></a> Configure role-based administration  
Role-based administration combines security roles, security scopes, and assigned collections to define the administrative scope for each administrative user. An administrative scope includes the objects that an administrative user can view in the Configuration Manager console, and the tasks related to those objects that the administrative user has permission to perform. Role-based administration configurations are applied at each site in a hierarchy.  

The following links are to the relevant sections from the [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md) topic:  

-   [Create custom security roles](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configure security roles](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configure security scopes for an object](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configure collections to manage security](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Create a new administrative user](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modify the administrative scope of an administrative user](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  Your own administrative scope defines the objects and settings that you can assign when you configure role-based administration for another administrative user. For information about planning for role-based administration, see [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="BKMK_ManageAccounts"></a> Manage accounts that are used by Configuration Manager  
Configuration Manager supports Windows accounts for many different tasks and uses.  

Use the following procedure to view which accounts are configured for different tasks, and to manage the password that Configuration Manager uses for each account.  

#### To manage accounts that are used by Configuration Manager  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Security**, and then click **Accounts** to view the accounts that are configured for Configuration Manager.  

3.  To change the password for an account that is configured for Configuration Manager, select the account.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  Click **Set** to open the **Windows User Account** dialog box and specify the new password for Configuration Manager to use for the account.  

    > [!NOTE]  
    >  The password that you specify must match the password that is specified for the account in Active Directory Users and Computers.  

6.  Click **OK** to complete the procedure.  

