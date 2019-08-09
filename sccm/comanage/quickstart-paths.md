---
title: Paths to co-management
titleSuffix: Configuration Manager
description: Understand the prerequisites for the two primary ways for you to setup co-management.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Paths to co-management

There are two primary ways for you to set up co-management. It's important to understand the prerequisites for each path. They each require some combination of Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune, and Windows 10. 

1. [Auto-enroll existing Configuration Manager-managed devices into Intune](#bkmk_path1)  
2. [Bootstrap the Configuration Manager client with modern provisioning](#bkmk_path2)  

![Diagram of co-management paths](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Path 1: Auto-enroll existing clients

Taking this path can get your existing Configuration Manager-managed devices quickly enrolled into Intune. The management of these devices from Configuration Manager is no different from before you enable co-management. Now you get all the cloud-based benefits. This path is transparent to your users.

Here's what you need to set it up:
- Hybrid Azure AD
    - One of the following [Azure AD hybrid identity options](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Password hash synchronization](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) with [Seamless Single Sign-on (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Pass-through authentication](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) with [Seamless Single Sign-on (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Federated SSO (with Active Directory Federation Services (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium license
    - Configure hybrid Azure AD-join (choose one option):
        - For managed domains
        - For federated domains
- Client agent setting for hybrid Azure AD-join
- Configure auto-enrollment of devices to Intune
- Assign Intune user licenses
- Enable co-management in Configuration Manager

For a tutorial on this path, see [Tutorial: Enable co-management for existing Configuration Manager clients](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Path 2: Bootstrap with modern provisioning

Here's what you need to set it up:

1. [Setup enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Create the cloud services in Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configure the management point and clients to use the cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Use Intune to deploy the Configuration Manager client](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> A tutorial for this path is coming soon.

