---
title: Install the client with Azure AD
titleSuffix: Configuration Manager
description: Install and assign the Configuration Manager client on Windows devices using Azure Active Directory for authentication
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Install and assign Configuration Manager clients using Azure AD for authentication

To install the Configuration Manager client on Windows devices using Azure Active Directory (Azure AD) authentication, integrate Configuration Manager with Azure AD. Clients can be on the intranet communicating directly with an HTTPS-enabled management point or any management point in a site enabled for Enhanced HTTP. They can also be internet-based communicating through the CMG or with an Internet-based management point. This process uses Azure AD to authenticate clients to the Configuration Manager site. Azure AD replaces the need to configure and use client authentication certificates.

Setting up Azure AD may be easier for some customers than setting up a public key infrastructure for certificate-based authentication. There are features that require you onboard the site to Azure AD, but don't necessarily require the clients to be Azure AD-joined.<!-- SCCMDocs issue 1259 --> For more information, see the following articles:

- [Plan for Azure Active Directory](../../plan-design/security/plan-for-security.md#azure-active-directory)
- [Use Azure AD for co-management](../../../comanage/quickstart-hybrid-aad.md)

## Before you begin

- An Azure AD tenant is a prerequisite  

- Device requirements:  

  - A supported version of Windows 10 or later

  - Joined to Azure AD, either pure cloud domain-joined, or hybrid Azure AD-joined  

- User requirements:  

  - The signed in user must be an Azure AD identity.

  - If the user is a federated or synchronized identity, configure both Configuration Manager [Active Directory user discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) and [Azure AD user discovery](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc). For more information about hybrid identities, see [Define a hybrid identity adoption strategy](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->

- In addition to the [existing prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#management-point) for the management point site system role, also enable **ASP.NET 4.5** on this server. Include any other options that are automatically selected when enabling ASP.NET 4.5.  

- Determine whether your management point needs HTTPS. For more information, see [Enable management point for HTTPS](../manage/cmg/configure-authentication.md#enable-management-point-for-https).

- Optionally set up a [cloud management gateway](../manage/cmg/overview.md) (CMG) to deploy internet-based clients. For on-premises clients that authenticate with Azure AD, you don't need a CMG.  

> [!TIP]
> Configuration Manager extends its support for internet-based devices that don't often connect to the internal network, aren't able to join Azure Active Directory (Azure AD), and don't have a method to install a PKI-issued certificate. For more information, see [Token-based authentication for CMG](deploy-clients-cmg-token.md).<!--5686290-->

## Configure Azure Services for Cloud Management

Connect your Configuration Manager site to Azure AD as the first step. For details of this process, see [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md). Create a connection to the **Cloud Management** service.

Enable [Azure AD User Discovery](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) as part of onboarding to **Cloud Management**.

After you complete these actions, your Configuration Manager site is connected to Azure AD.

> [!NOTE]
> If your devices are in an Azure AD tenant that's separate from the tenant with a subscription for the CMG compute resources, starting in version 2010 you can disable authentication for tenants not associated with users and devices. For more information, see [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md#disable-authentication).<!--8537319-->

## Configure client settings

These client settings help configure Windows devices to be hybrid-joined. They also enable internet-based clients to use the CMG.

1. Configure the following client settings in the **Cloud Services** group. For more information, see [How to configure client settings](configure-client-settings.md).

    - **Allow access to cloud distribution point**: Enable this setting to help internet-based devices get the required content to install the Configuration Manager client. Devices can get the content from the CMG.<!--495533-->  

    - **Automatically register new Windows 10 or later domain joined devices with Azure Active Directory**: Set to **Yes** or **No**. The default setting is **Yes**. This behavior is also the default in Windows.

        > [!TIP]
        > Hybrid-joined devices are joined to an on-premises Active Directory domain and registered with Azure AD. For more information, see [Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid).<!-- MEMDocs#325 -->

    - **Enable clients to use a cloud management gateway**: Set to **Yes** (default), or **No**.  

2. Deploy the client settings to the required collection of devices. Don't deploy these settings to user collections.

To confirm the device is hybrid-joined, run `dsregcmd.exe /status` in a command prompt. If the device is Azure AD-joined or hybrid-joined, the **AzureAdjoined** field in the results shows **YES**. For more information, see [dsregcmd command - device state](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

## Install and register the client using Azure AD identity

To manually install the client using Azure AD identity, first review the general process on [How to install clients manually](deploy-clients-to-windows-computers.md#BKMK_Manual).

> [!Note]  
> The device needs access to the internet to contact Azure AD, but doesn't need to be internet-based.

The following example shows the general structure of the command line:
`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSITECODE=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

For more information, see [Client installation properties](about-client-installation-properties.md).

The `/mp` parameter and `CCMHOSTNAME` property specify one of the following, depending upon the scenario:

- On-premises management point. Only specify the `/mp` parameter. The `CCMHOSTNAME` property isn't required.
- Cloud management gateway
- Internet-based management point

The `SMSMP` property specifies the on-premises management point. It's not required. It's recommended for Azure AD-joined devices that roam onto the intranet, so they can find an on-premises management point.

This example uses a cloud management gateway. It replaces sample values:
`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

The site publishes additional Azure AD information to the cloud management gateway (CMG). An Azure AD-joined client gets this information from the CMG during the ccmsetup process, using the same tenant to which it's joined. This behavior further simplifies installing the client in an environment with more than one Azure AD tenant. The only two required ccmsetup properties are `CCMHOSTNAME` and `SMSSITECODE`.<!--3607731-->

To automate the client install using Azure AD identity via Microsoft Intune, see [How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

## Next steps

Once complete, you can continue to [monitor and manage clients](../manage/monitor-clients.md).
