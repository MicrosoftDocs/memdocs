---
title: OS Deployment Site Role Configuration
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 15ddea9d-e13a-4be2-a3f6-20eba1e4a678
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
description: Learn about the different operating system deployment site roles and how to configure these roles by using the SMS_SiteControlFile class.
ms.reviewer: mstewart,aaroncz 
---
# About Operating System Deployment Site Role Configuration
The following two site roles are of particular importance to Operating System Deployment in Configuration Manager.  

## State Migration Point Site Role  
 The state migration point (SMP) is a Configuration Manager site role that provides a secure location to store user state information before an operating system deployment. You can store the user state on the SMP while the operating system deployment proceeds and then restore the user state to the new computer from the SMP. Each SMP site role can only be a member of one Configuration Manager site.  

## PXE Service Point Site Role  
 You use the PXE protocol to initiate operating system deployments to Configuration Manager clients. Configuration Manager uses the PXE service point site role to initiate the operating system deployment process. The PXE service point must be configured to respond to PXE boot requests made by Configuration Manager clients on the network and then interact with Configuration Manager infrastructure to determine the appropriate installation actions to take.  

## Programming the Site Roles  
 Most information about Configuration Manager site roles is stored in the Configuration Manager site control file.  

 You can make updates to the site control file through Windows Management Instrumentation (WMI) by using the [SMS_SiteControlFile](../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md) class. In managed code, `IResultObject` allows access to the site control file. For more information, see [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md).  

 The properties you will need to access are stored as system resources in the site control file. For example, the following site control file section shows the properties for the PXE service point site role.  

```  
BEGIN_SYSTEM_RESOURCE_USE  
    RESOURCE<Windows NT Server><["Display=\\SERVERNAME\"]MSWNET:["SMS_SITE=ABC"]\\SERVERNAME\>  
    ROLE<SMS PXE Service Point>  
    PROPERTY <Server Remote Name><><><0>  
    PROPERTY <IsActive><><><1>  
    PROPERTY <BindPolicy><><><1>  
    PROPERTY <ResponseDelay><><><15>  
    PROPERTY <PXEPassword><><><0>  
    PROPERTY <AuthType><><><0>  
    PROPERTY <UserName><><><0>  
    PROPERTY <CertificateType><><><0>  
    PROPERTY <CertificateExpirationDate><128568119567070000><><0>  
    PROPERTY <CertificateFile><><><0>  
    PROPERTY <PXECertGUID><XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX><><0>  
    BEGIN_PROPERTY_LIST  
        <BindExcept>  
        <11:11:11:11:11:11>  
        <22:22:22:22:22:22>  
    END_PROPERTY_LIST  
    BEGIN_PROPERTY_LIST  
        <Objects Polled By Site Status>  
        <["Display=\\SERVERNAME\C$\Program Files\Microsoft Configuration Manager\"]MSWNET:["SMS_SITE=ABC"]\\SERVERNAME\C$\Program Files\Microsoft Configuration Manager\>  
    END_PROPERTY_LIST  
END_SYSTEM_RESOURCE_USE  
```  

 When you have access to the site control file, the various properties are stored as embedded properties or in embedded property lists. For example `UserName` in the sample above is an embedded property. Other properties are stored as embedded property lists. In the example above, the MAC addresses in `BindExcept` are stored in an embedded property list.  

## See Also  
 [About the site control file](../core/understand/about-the-configuration-manager-site-control-file.md)
 [How to Set the Restore-Only Mode for a State Migration Point](../../develop/osd/how-to-set-the-restore-only-mode-for-a-state-migration-point.md)   
 [How to Track Operating System Deployment Migrations in Configuration Manager](../../develop/osd/how-to-track-operating-system-deployment-migrations.md)   
 [About OS deployment site role configuration](about-operating-system-deployment-site-role-configuration.md)
