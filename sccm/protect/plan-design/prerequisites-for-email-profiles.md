---
title: "Prerequisites for email profiles"
titleSuffix: "Configuration Manager"
description: "Learn about email profiles in Configuration Manager and their dependencies both externally and within the product."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: mestew
ms.author: mstewart
manager: dougeby


---
# Email profile prerequisites

*Applies to: Configuration Manager (current branch)*

Email profiles in Configuration Manager have dependencies both externally, and within the product.  

## Configuration Manager dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Specific security permissions must be granted to manage email profiles|You must have the following security permissions to manage company resource access settings, such as email profiles:<br /><br /> - To view and manage alerts and reports for email profiles: **Create**, **Delete**, **Modify**, **Modify Report**, **Read**, and **Run Report** permissions for the **Alerts** object.<br /><br /> - To create and manage certificate profiles: **Author Policy**, **Modify Report**, **Read** and **Run Report** permissions for the **Certificate Profile** object.<br /><br /> - To manage email profile deployments: **Deploy Configuration Policies**, **Modify Client Status Alert**, **Read**, and **Read Resource** permissions for the **Collection** object.<br /><br /> - To manage all configuration policies: **Create**, **Delete**, **Modify**, **Read** and **Set Security Scope** permissions for the **Configuration Policy** object.<br /><br /> - To run queries that are related to email profiles: **Read** permission for the **Query** object.<br /><br /> - To view email profiles information in the Configuration Manager console: **Read** permission for the **Site** object.<br /><br /> - To view status messages for email profiles: **Read** permission for the **Status Messages** object.<br /><br /> - To create and manage email profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** permissions for the **Communications Provisioning Profile** object.<br /><br /> The **Company Resource Access Manager** security role includes these permissions that are required to manage email profiles in Configuration Manager. For more information, see [Configure security](../../core/plan-design/security/configure-security.md).|  
|Mail attribute in active directory|If you want to generate the users email address in an email profile by using the user's primary SMTP address, Configuration Manager user discovery must be configured to discover the **mail** attribute from Active Directory (this is configured by default).|  

## External dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Mail attribute in active directory|If you want to generate the users email address in an email profile by using the user's primary SMTP address, this address must exist in the **mail** attribute in Active Directory.<br /><br /> For more information, see your Windows Server documentation.|
