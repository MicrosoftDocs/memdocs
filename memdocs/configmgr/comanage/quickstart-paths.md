---
title: Paths to co-management
titleSuffix: Configuration Manager
description: Understand the prerequisites for the two primary ways for you to setup co-management.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Paths to co-management

There are two primary ways for you to set up co-management. It's important to understand the prerequisites for each path. They each require some combination of Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune, and Windows 10 or later.

1. [Auto-enroll existing Configuration Manager-managed devices into Intune](#bkmk_path1)  

2. [Bootstrap the Configuration Manager client with modern provisioning](#bkmk_path2)  

>[!Tip]
> As we talk with our customers that are using Microsoft Endpoint Manager to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and hybrid Azure Active Directory (AD) joined devices. Many customers confuse these two topics – the first is a management option, while the second is an identity option. See the blog post [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog aims to clarify Hybrid Azure AD Join and co-management, how they work together but are not the same thing.



## <a name="bkmk_path1"></a> Path 1: Auto-enroll existing clients

Taking this path can get your existing Configuration Manager-managed devices quickly enrolled into Intune. The management of these devices from Configuration Manager is no different from before you enable co-management. Now you get all the cloud-based benefits. This path is transparent to your users.

Here's what you need to set it up:
- Hybrid Azure AD
    - One of the following [Azure AD hybrid identity options](/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Password hash synchronization](/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) with [Seamless Single Sign-on (SSO)](/azure/active-directory/hybrid/how-to-connect-sso)
       - [Pass-through authentication](/azure/active-directory/hybrid/how-to-connect-pta) with [Seamless Single Sign-on (SSO)](/azure/active-directory/hybrid/how-to-connect-sso)
       - [Federated SSO (with Active Directory Federation Services (AD FS))](/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium license
    - Configure hybrid Azure AD-join (choose one option):
        - For managed domains
        - For federated domains
- Client agent setting for hybrid Azure AD-join
- Configure auto-enrollment of devices to Intune
- Enable co-management in Configuration Manager

For a tutorial on this path, see [Tutorial: Enable co-management for existing Configuration Manager clients](tutorial-co-manage-clients.md).

## <a name="bkmk_path2"></a> Path 2: Bootstrap with modern provisioning

This path is for those devices that are first enrolled with Intune. They are cloud-first devices and use Intune to install the Configuration Manager client.

Here's what you need to set it up:

1. [Setup enhanced HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Create the cloud services in Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Configure the management point and clients to use the cloud management gateway](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Use Intune to deploy the Configuration Manager client](how-to-prepare-Win10.md)  

For a tutorial on this path, see [Tutorial: Enable co-management for new internet-based devices](tutorial-co-manage-new-devices.md).
