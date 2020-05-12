---
title: Set up cloud management gateway
titleSuffix: Configuration Manager
description: Use this step-by-step process for setting up a cloud management gateway (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f


---

# Set up cloud management gateway for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This process includes the steps required to set up a cloud management gateway (CMG).

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).


## Before you begin

Start by reading the article [Plan for cloud management gateway](plan-cloud-management-gateway.md). Use that article to determine your CMG design.

Use the following checklist to make sure you have the necessary information and prerequisites to create a CMG:  

- The Azure environment to use. For example, the Azure Public Cloud or the Azure US Government Cloud.  

- You need one or more certificates for CMG, depending upon your design. For more information, see [Certificates for cloud management gateway](certificates-for-cloud-management-gateway.md).  

- You need the following requirements for an [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) deployment of CMG:  

    - Integration with [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**. Azure AD user discovery isn't required.  

    - The **Microsoft.ClassicCompute** & **Microsoft.Storage** resource providers must be registered within the Azure subscription. For more information, see [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - A subscription admin needs to sign in.  

- A globally unique name for the service. This name is from the [CMG server authentication certificate](certificates-for-cloud-management-gateway.md#bkmk_serverauth).  

- If enabling CMG as a cloud distribution point, the same globally unique CMG service name chosen also needs to be available as a globally unique storage account name. This name is from the [CMG server authentication certificate](certificates-for-cloud-management-gateway.md#bkmk_serverauth).

- The Azure region for this CMG deployment.  

- How many VM instances you need for scale and redundancy.  

- If you still need to use the Azure classic service deployment in Configuration Manager version 1810 or earlier, you need the following requirements:  

    > [!Important]  
    > Starting in version 1810, classic service deployments in Azure are deprecated in Configuration Manager. Use Azure Resource Manager deployments for the cloud management gateway. For more information, see [Plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager).  
    >
    > Starting in Configuration Manager version 1902, Azure Resource Manager is the only deployment mechanism for new instances of the cloud management gateway.<!-- 3605704 -->

    - Azure subscription ID  

    - Azure management certificate  


## Set up a CMG

Do this procedure on the top-level site. That site is either a standalone primary site, or the central administration site.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Cloud Management Gateway**.  

2. Select **Create Cloud Management Gateway** in the ribbon.  

3. On the General page of the wizard, select **Sign in**. Authenticate with an Azure subscription administrator account. The wizard auto-populates the remaining fields from the information stored during the Azure AD integration prerequisite. If you own multiple subscriptions, select the **Subscription ID** of the desired subscription to use.

    > [!Note]  
    > Starting in version 1810, classic service deployments in Azure were deprecated in Configuration Manager. In version 1902 and earlier, select **Azure Resource Manager deployment** as the CMG deployment method.
    >
    > If you need to use a classic service deployment, select that option on this page. First enter your Azure **Subscription ID**. Then select **Browse**, and choose the .PFX file for the Azure management certificate.

4. Specify the **Azure environment** for this CMG. The options in the drop-down list may vary depending upon the deployment method.  

5. Select **Next**. Wait as the site tests the connection to Azure.  

6. On the Settings page of the wizard, first select **Browse** and choose the .PFX file for the CMG server authentication certificate. The name from this certificate populates the required **Service FQDN** and **Service name** fields.  

   > [!NOTE]  
   > The CMG server authentication certificate supports wildcards. If you use a wildcard certificate, replace the asterisk (`*`) in the **Service FQDN** field with the desired hostname for the CMG.<!--491233-->  

7. Select the **Region** drop-down list to choose the Azure region for this CMG.  

8. Select a **Resource Group** option.
   1. If you choose **Use existing**, then select an existing resource group from the drop-down list. The selected resource group must already exist in the region you selected in step 7. If you select an existing resource group and it is in a different region than the previously selected region, CMG will fail to provision.
   2. If you choose **Create new**, then enter the new resource group name.

9. In the **VM Instance** field, enter the number of VMs for this service. The default is one, but you can scale up to 16 VMs per CMG.  

10. Select **Certificates** to add client trusted root certificates. Add all of the certificates in the trust chain.  

    > [!Note]  
    > Starting in version 1806, when you create a CMG, you're no longer required to provide a trusted root certificate on the Settings page. This certificate isn't required when using Azure Active Directory (Azure AD) for client authentication, but used to be required in the wizard. If you're using PKI client authentication certificates, then you still must add a trusted root certificate to the CMG.<!--SCCMDocs-pr issue #2872-->  
    >
    > In version 1902 and earlier, you can only add two trusted root CAs and four intermediate (subordinate) CAs.<!-- SCCMDocs-pr#4022 -->

11. By default, the wizard enables the option to **Verify Client Certificate Revocation**. A certificate revocation list (CRL) must be publicly published for this verification to work. For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

12. Starting in version 1906, you can **Enforce TLS 1.2**. This setting only applies to the Azure cloud service VM. It doesn't apply to any on-premises Configuration Manager site servers or clients. For more information on TLS 1.2, see [How to enable TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).<!-- SCCMDocs-pr#4021 -->

13. Starting in version 1806, by default, the wizard enables the following option: **Allow CMG to function as a cloud distribution point and serve content from Azure storage**. Now a CMG can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs.  

14. Select **Next**.  

15. To monitor CMG traffic with a 14-day threshold, choose the check box to turn on the threshold alert. Then, specify the threshold, and the percentage at which to raise the different alert levels. Choose **Next** when you're done.  

16. Review the settings, and choose **Next**. Configuration Manager starts setting up the service. After you close the wizard, it will take between five to 15 minutes to provision the service completely in Azure. Check the **Status** column for the new CMG to determine when the service is ready.  

    > [!Note]  
    > To troubleshoot CMG deployments, use **CloudMgr.log** and **CMGSetup.log**. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## Configure primary site for client certificate authentication

If you're using [client authentication certificates](certificates-for-cloud-management-gateway.md#bkmk_clientauth) for clients to authenticate with the CMG, follow this procedure to configure each primary site.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**.  

2. Select the primary site to which your internet-based clients are assigned, and choose **Properties**.  

3. Switch to the **Client Computer Communication** tab of the primary site property sheet, check **Use PKI client certificate (client authentication) when available**.  

    > [!Note]
    > Starting in version 1906, this tab is called **Communication Security**.<!-- SCCMDocs#1645 -->  

4. If you don't publish a CRL, deselect the option for **Clients check the certificate revocation list (CRL) for site systems**.  


## Add the CMG connection point

The CMG connection point is the site system role for communicating with the CMG. To add the CMG connection point, follow the general instructions to [install site system roles](../../../servers/deploy/configure/install-site-system-roles.md). On the System Role Selection page of the Add Site System Role Wizard, select **Cloud management gateway connection point**. Then select the **Cloud management gateway name** to which this server connects. The wizard shows the region for the selected CMG.

> [!Important]
> The CMG connection point must have a [client authentication certificate](certificates-for-cloud-management-gateway.md#bkmk_clientauth) in some scenarios.

To troubleshoot CMG service health, use **CMGService.log** and **SMS_Cloud_ProxyConnector.log**. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## Configure client-facing roles for CMG traffic

Configure the management point and software update point site systems to accept CMG traffic. Do this procedure on the primary site, for all management points and software update points that service internet-based clients.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node. On the Home tab of the ribbon, in the View group, select **Servers with Role**. Then select **Management point** from the list.  

2. Select the site system server you want to configure for CMG traffic. Select the **Management point** role in the details pane, and then select **Properties** in the ribbon.  

3. In the Management point properties sheet under Client Connections, check the box next to **Allow Configuration Manager cloud management gateway traffic**.

    Depending upon your CMG design and Configuration Manager version, you may need to enable the **HTTPS** option. For more information, see [Enable management point for HTTPS](certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

4. Select **OK** to close the management point properties window.  

Repeat these steps for additional management points as needed, and for any software update points.


## Configure boundary groups

<!--3640932-->
Starting in version 1902, you can associate a CMG with a boundary group. This configuration allows clients to default or fallback to the CMG for client communication according to boundary group relationships.

For more information on boundary groups, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups.md).

When you [create or configure a boundary group](../../../servers/deploy/configure/boundary-group-procedures.md), on the **References** tab, add a cloud management gateway. This action associates the CMG with this boundary group.


## Configure clients for CMG

Once the CMG and site system roles are running, clients get the location of the CMG service automatically on the next location request. Clients must be on the intranet to receive the location of the CMG service, unless you [install and assign Windows 10 clients using Azure AD for authentication](../../deploy/deploy-clients-cmg-azure.md). The polling cycle for location requests is every 24 hours. If you don't want to wait for the normally scheduled location request, you can force the request by restarting the SMS Agent Host service (ccmexec.exe) on the computer.  

> [!Note]
> By default all clients receive CMG policy. Control this behavior with the client setting, [Enable clients to use a cloud management gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway).

The Configuration Manager client automatically determines whether it's on the intranet or the internet. If the client can contact a domain controller or an on-premises management point, it sets its connection type to **Currently intranet**. Otherwise, it switches to **Currently Internet**, and uses the location of the CMG service to communicate with the site.

>[!NOTE]
> You can force the client to always use the CMG regardless of whether it's on the intranet or internet. This configuration is useful for testing purposes, or for clients that you want to force to always use the CMG. Set the following registry key on the client:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> You can also specify this setting during client installation using the [CCMALWAYSINF](../../deploy/about-client-installation-properties.md#ccmalwaysinf) property.
>
> This setting will always apply, even if the client roams into a location where boundary group configurations would otherwise leverage local resources.


To verify that clients have the policy specifying the CMG, open a Windows PowerShell command prompt as an administrator on the client computer, and run the following command:
`Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

This command displays any internet-based management points the client knows about. While the CMG isn't technically an internet-based management point, clients view it as one.

> [!Note]  
> To troubleshoot CMG client traffic, use **CMGHttpHandler.log**, **CMGService.log**, and **SMS_Cloud_ProxyConnector.log**. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## Modify a CMG

After creating a CMG, you can modify some of its settings. Select the CMG in the Configuration Manager console and select **Properties**. Configure settings on the following tabs:  

#### General

- **Azure management certificate**: change the Azure management certificate for the CMG. This option is useful when updating the certificate before it expires.  

#### Settings

- **Certificate file**: change the server authentication certificate for the CMG. This option is useful when updating the certificate before it expires.  

- **VM Instance**: change the number of virtual machines that the service uses in Azure. This setting allows you to dynamically scale the service up or down based on utilization or cost considerations.  

- **Certificates**: add or remove trusted root or intermediate CA certificates. This option is useful when adding new CAs, or retiring expired certificates.  

- **Verify Client Certificate Revocation**: if you didn't originally enable this setting when creating the CMG, you can enable it afterwards once you publish the CRL. For more information, see [Publish the certificate revocation list](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

- **Allow CMG to function as a cloud distribution point and serve content from Azure storage**: Starting in version 1806, this new option is enabled by default. Now a CMG can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs.<!--1358651-->  

#### Alerts

Reconfigure the alerts at anytime after you create the CMG.


### Redeploy the service

More significant changes, such as the following configurations, require redeploying the service:

- Classic deployment method to Azure Resource Manager
- Subscription
- Service name
- Private to public PKI
- Region

Always keep at least one active CMG for internet-based clients to receive updated policy. internet-based clients can't communicate with a removed CMG. Clients don't know about a new one until they roam back to the intranet. When creating a second CMG instance in order to delete the first, also create another CMG connection point.

Clients refresh policy by default every 24 hours, so wait at least one day after creating a new CMG before you delete the old one. If clients are turned off or without an internet connection, you may need to wait longer.

If you have an existing CMG on the classic deployment method, you must deploy a new CMG to use the Azure Resource Manager deployment method.<!--509753--> There are two options:  

- If you want to reuse the same service name:  

    1. First delete the classic CMG, taking into account the guidance to always have at least one active CMG for internet-based clients.  

    2. Create a new CMG using a Resource Manager deployment. Reuse the same server authentication certificate.  

    3. Reconfigure the CMG connection point to use the new CMG instance.  

- If you want to use a new service name:  

    1. Create a new CMG using a Resource Manager deployment. Use a new server authentication certificate.  

    2. Create a new CMG connection point and link with the new CMG.  

    3. Wait at least one day for internet-based clients to receive policy about the new CMG.  

    4. Delete the classic CMG.  

> [!Tip]  
> To determine the current deployment model of a CMG:<!--SCCMDocs issue #611-->  
>
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.  
> 2. Select the CMG instance.  
> 3. In the Details pane at the bottom of the window, look for the **Deployment Model** attribute. For a Resource Manager deployment, this attribute is **Azure Resource Manager**. The legacy deployment model with the Azure management certificate displays as **Azure Service Manager**.
>
> You can also add the **Deployment Model** attribute as a column to the list view.  

### Modifications in the Azure portal

Only modify the CMG from the Configuration Manager console. Making modifications to the service or underlying VMs directly in Azure isn't supported. Any changes may be lost without notice. As with any PaaS, the service can rebuild the VMs at anytime. These rebuilds can happen for backend hardware maintenance, or to apply updates to the VM OS.

### Delete the service

If you need to delete the CMG, also do so from the Configuration Manager console. Manually removing any components in Azure causes the system to be inconsistent. This state leaves orphaned information, and unexpected behaviors may occur.


## Next steps

- [Monitor clients for cloud management gateway](monitor-clients-cloud-management-gateway.md)
- [Frequently asked questions about the cloud management gateway](cloud-management-gateway-faq.md)
