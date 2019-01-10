---
title: Use Azure AD for co-management
titleSuffix: Configuration Manager
description: With Azure AD you can take advantage of improved productivity for your users and security for your resources, across both cloud and on-prem environments
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Use Azure AD for co-management

In the cloud, identity is the new control plane. Azure Active Directory (Azure AD) allows you to link your users, devices, and applications across both cloud and on-premises environments. Registering your devices to Azure AD enables you to improve productivity for your users and security for your resources. Having devices in Azure AD is the foundation for both co-management and device-based conditional access. 

For more information on device-based conditional access, see [How To: Require managed devices for cloud app access with conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

<!--update with final video for this quickstart, with some intro text-->
> [!VIDEO https://www.youtube.com/embed/gA5q0_3bxPs]

Azure AD provides two options for company-owned devices to suit your organization's needs:  

- **Azure AD-joined device**: Join your Windows 10 devices to Azure AD without needing to join them to your on-premises Active Directory  

    - Supports Windows 10

    - Set up without requiring any additional configuration to your on-premises environments  

    - By enabling a few settings in Azure AD, you can enable your users to join devices to Azure AD through the Windows setup experience (OOBE)  

    - For more information, see [How to: Plan your Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Hybrid Azure AD-joined device**: Join your existing domain-joined devices to Azure AD  

    - Supports Windows 10, Windows 8.1, and Windows 7

    - Set up using AD FS claims or Azure AD Connect  

    - For Windows 10 the join happens in the machine context, so your users don't have to take extra steps  

    - For more information, see [How to plan your hybrid Azure Active Directory join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Both options provide similar functionality for users. It's flexible for you to choose either one based on your needs. For example, you can [access your on-premises resources](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) from Azure AD-joined machines even though they aren't joined to Active Directory. 

You can join devices to Azure AD in various environments, no matter your [authentication method](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). For example, federated authentication, or cloud authentication. 

If you already have an on-premises Active Directory, setting up either option is straightforward. 



## Benefits

Joining devices to Azure AD provides the following benefits to your organization:

#### Single sign on to cloud resources
On devices joined to Azure AD, users get a seamless experience accessing any cloud or on-premises resources. Once users sign in to a Windows machine that's joined to Azure AD, they get single sign-on to all applications without any additional sign-in prompts.  

#### Windows Hello for Business
Windows Hello for Business brings strong password-less authentication to Windows 10. By joining your devices to Azure AD, you can enable Windows Hello for Business across your user base for both cloud and on-premises resources. Windows Hello for Business eliminates the problem of remembering complex passwords or inadvertently exposing them by providing a sign-in process that's both simple and secure. 

For more information, see [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### Device-based conditional access
Enable conditional access based on the device state to better protect your organization's data. Device-based conditional access requires a managed device. This device must be a compliant device or a hybrid Azure AD-joined device. For Azure AD-joined devices, you need Intune to mark the device as compliant. But for hybrid Azure AD-joined devices, the device state itself is used to evaluate conditional access. Co-management provides you the additional advantage of evaluating compliance through Intune for hybrid Azure AD-joined devices to make sure the device configuration is intact. 

For more information on device-based conditional access, see [How To: Require managed devices for cloud app access with conditional access](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### Automatic device licensing
All Windows 10 devices joined to Azure AD go through license checks. These checks enable you to automatically upgrade them from Pro to Enterprise through the Microsoft cloud. When you remove the relevant subscription from the user, the device automatically downgrades its license. This feature provides a single pane of control for managing Windows licenses, without any complicated processes or on-premises systems.

#### Self-service functionality
Self-service functionality includes self-service password reset and Bitlocker recovery key. Azure AD also provides options directly to the user to reset their password or access BitLocker recovery keys. Users can use Azure AD to reset their passwords directly from the Windows lock screen, instead of from a web browser. These features reduce friction for users and help cut helpdesk costs for your organization.  

For more information, see [Quickstart: Self-service password reset](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### Enterprise state roaming
All devices joined to Azure AD can sync their settings to the cloud. Any device to which a user signs in syncs all their settings for a more productive experience.  



## Value proposition

Joining your devices to Azure AD through either method accelerates your digital transformation. It enables more functionality provided by Microsoft 365. Your users will have better experiences, and you'll have greater security for your data. 

Azure AD provides several options to ease your work load, for example:

- Manage all the device identities in your organization from a single place  

- Lower your helpdesk costs by enabling self-service password reset. Then users can reset their passwords from the Windows 10 lock screen on their device at any time.  



## Configure

If you already have an on-premises Active Directory environment, and you want to join your domain-joined devices to Azure AD, configure hybrid Azure AD-joined devices. For more information, [How to plan your hybrid Azure Active Directory join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

Configuration Manager has a client setting to [Automatically register new Windows 10 domain-joined devices with Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). For more information on configuring client settings, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).

If you want to configure Azure AD-join for your devices without also joining them to your on-premises domain, review the considerations for Azure AD-join in your environment. Once you decided to go with Azure AD join, you have many options to deploy it based on your organization’s needs. For more information, see the following articles:
- [How to: Plan your Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Understand your provisioning options](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

