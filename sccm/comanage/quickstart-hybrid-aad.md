---
title: Use Azure AD for co-management
titleSuffix: Configuration Manager
description: Co-management requires Azure Active Directory, which allows you to link your users, devices, and applications across both cloud and on-premises environments.
ms.date: 01/15/2019
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

> [!VIDEO https://www.youtube.com/embed/gA5q0_3bxPs]

Azure AD provides two options for company-owned devices to suit your organization's needs:  

- **Azure AD-joined device**: Join your Windows 10 devices to Azure AD without needing to join them to your on-premises Active Directory  

    - Set up without requiring any additional configuration to your on-premises environments  

    - By enabling a few settings in Azure AD, you can enable your users to join devices to Azure AD through the Windows setup experience (OOBE)  

    - For more information, see [How to: Plan your Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Hybrid Azure AD-joined device**: Join your existing domain-joined PCs to Azure AD  

    - Set up using AD FS claims or Azure AD Connect  

    - Happens in the machine context, so your users don't have to take extra steps  

    - For more information, see [How to plan your hybrid Azure Active Directory join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Both options provide similar functionality for users. It's flexible for you to choose either one based on your needs. For example, you can access your on-premises resources from Azure AD-joined machines even though they aren't joined to Active Directory. 

You can join devices to Azure AD in a variety of environments, no matter your authentication method. For example, federated authentication, or cloud authentication. If you already have an on-premises Active Directory, setting up either option is straightforward. 



## Benefits

Joining devices to Azure AD provides the following benefits to your organization:

1. **Single sign-on to cloud resources**: On devices joined to Azure AD, users get a seamless experience accessing any cloud or on-premises resources. Once users sign in to a Windows machine that's joined to Azure AD, they get single sign-on to all applications without any additional sign-in prompts.  

2. **Windows Hello for Business**: Windows Hello for Business brings strong password-less authentication to Windows 10. By joining your devices to Azure AD, you can enable Windows Hello for Business across your user base for both cloud and on-premises resources. Windows Hello for Business eliminates the problem of remembering complex passwords or inadvertently exposing them by providing a sign-in process that's both simple and secure.  

3. **Device-based conditional access**: Enable conditional access based on the device state to better protect your organization's data. Device-based conditional access requires a managed device. This device must be a compliant device or a hybrid Azure AD-joined device. For Azure AD-joined devices, you need Intune to mark the device as compliant. But for hybrid Azure AD-joined devices, the device state itself is used to evaluate conditional access. Co-management provides you the additional advantage of evaluating compliance through Intune for hybrid Azure AD-joined devices to make sure the device configuration is intact.  

4. **Enterprise state roaming**: All devices joined to Azure AD can sync their settings to the cloud. Any device to which a user signs in syncs all their settings for a more productive experience.  

5. **Self-service functionality** such as self-service password reset and Bitlocker recovery key: Azure AD also provides options directly to the user to reset their password or access BitLocker recovery keys. These features reduce friction for users and help cut helpdesk costs for your organization.  



## Configure

If you already have an on-premises Active Directory environment, and you want to join your domain-joined devices to Azure AD, configure hybrid Azure AD-joined devices. For more information, [How to plan your hybrid Azure Active Directory join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 


