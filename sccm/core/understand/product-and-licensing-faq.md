---
title: Product and licensing FAQ
titleSuffix: Configuration Manager
description: Find answers for common product and license questions for System Center Configuration Manager.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Frequently asked questions for Configuration Manager branches and licensing

*Applies to: System Center Configuration Manager (Current Branch), System Center Configuration Manager (Long-Term Servicing Branch)*

This FAQ addresses common licensing questions about Configuration Manager current branch and the long-term servicing branch (LTSB) versions, available through Microsoft Volume Licensing programs. This article is for informational purposes. It doesn't supersede or replace any documentation covering System Center Configuration Manager licensing. For more information, see the product licensing for [System Center 2016](https://www.microsoft.com/en-us/licensing/product-licensing/system-center-2016.aspx)<!-- this link doesn't work without some language code --> and the [Product Terms](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). The Product Terms describe the use terms for all Microsoft products in Volume Licensing.

For more information about Configuration Manager features, see the [product page](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).



### <a name="bkmk_cb"></a> What's current branch?  

The current branch is the production-ready build of Configuration Manager that provides an active servicing model. This servicing model is like the experience with Windows 10. This approach supports customers who are moving at a "cloud cadence" and wish to innovate more quickly. With the current branch servicing model, you continue to receive new features and functionality. For this reason, only customers with active Software Assurance on Configuration Manager licenses, or with equivalent subscription rights, may install and use the current branch of Configuration Manager.


### <a name="bkmk_ltsb"></a> What's the long-term servicing branch (LTSB)?  

The LTSB is a production-ready build of Configuration Manager. It's intended for customers who allow Software Assurance or equivalent subscription rights to expire. When compared to the current branch, the LTSB has [reduced functionality](/sccm/core/understand/introduction-to-the-ltsb#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Customers who allow Software Assurance or equivalent subscription rights to expire must uninstall the current branch of Configuration Manager. Customers who have perpetual license rights to Configuration Manager may then install and use the LTSB build of the Configuration Manager version that's current at the time of expiration.


### <a name="bkmk_licensing-acronyms"></a> I've seen *SA* and *L&SA* used in licensing content. What do these acronyms mean in regard to Configuration Manager?    

Both **Software Assurance** (SA) and **License and Software Assurance** (L&SA) are license options that grant rights to use Configuration Manager. SA is an option for a customer that's renewing SA coverage from a prior agreement. L&SA is an option for a customer buying a new license and SA coverage.

- **Software Assurance (SA)**: Customers must have active SA on Configuration Manager licenses, or equivalent subscription rights, in order to install and use the current branch option of Configuration Manager.    

    - While SA is optional for some Microsoft products, the only way to get rights to use Configuration Manager current branch is with SA *or equivalent subscription rights*. For more information, see the [Software Assurance FAQ](https://www.microsoft.com/en-us/licensing/licensing-programs/FAQ-Software-Assurance.aspx).<!--this link doesn't work without some language code-->

- **Microsoft License and Software Assurance (L&SA)**: Customers buying new licenses for Configuration Manager must acquire L&SA (the license and SA coverage).   

    - The SA grants rights to use the current branch.

    - If your SA expires, and you still have a license for Configuration Manager, you can no longer use the current branch. For more information, see the FAQ [If my SA expires and I had L&SA, what do I get?](#bkmk_sa-expires)

For more information about license offerings, see [Ways to buy](https://www.microsoft.com/en-us/licensing/licensing-programs)<!--this link doesn't work without some language code--> and [Licensing Product Terms](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  


### <a name="bkmk_equiv-sub"></a> I read the term "equivalent subscription", what programs does that refer to?   

Equivalent subscriptions refer to programs like [Enterprise Mobility + Security](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) or [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). There can be others, but these programs are the most common. The Microsoft Volume Licensing Product Terms refers to these programs as Management License Equivalent Licenses.


### <a name="bkmk_ems-expires"></a> I have Enterprise Mobility + Security and it expired, what must I do now?  

EMS grants rights to use Configuration Manager current branch and long-term service branch. When these rights expire, you no longer have rights to use either branch and must uninstall.  


### <a name="bkmk_sa-expires"></a> If my SA expires, and I had L&SA, what do I get?   

If your SA expired after October 1, 2016, depending on what program you acquired L&SA under, you could retain a perpetual license to use the LTSB. If you currently use the current branch, you must uninstall it, and then install the LTSB. There's no support to migrate or convert to the LTSB from the current branch.

If your SA expired before October 1, 2016, and you retained a perpetual license to Configuration Manager, then your only option for ongoing use is to install and use System Center 2012 R2 Configuration Manager and its available service packs. You're required to uninstall the current branch when your SA expires, and reinstall that earlier version of the product. There's no support to migrate to or downgrade from Configuration Manager current branch to prior versions of Configuration Manager.   

If you use System Center Endpoint Protection, and your SA expires, you must uninstall it. System Center Endpoint Protection offers no *L (License)* rights, and no perpetual rights.<!--506238--> 


### <a name="bkmk_owncb"></a> Do I "own" the current branch?   

No. You're licensed to use the current branch while you have active SA. For example, via *L&SA*, when *SA* expires, you then have only *L (License)* rights, which don't include rights to use the current branch. If your L provides perpetual rights, you can use the Configuration Manager LTSB in place of the current branch. If your SA expired prior to October 1, 2016, you can also use System Center 2012 R2 Configuration Manager.


### <a name="bkmk_standalone"></a> Can I purchase Configuration Manager standalone without SA?      

No. The only way to get rights to use Configuration Manager is to acquire a license with SA or through an equivalent subscription. There are developer programs like MSDN where Configuration Manager is offered for development and test purposes, but not production usage.


### <a name="bkmk_update-rights"></a> I see updates for Configuration Manager offered from within my console, like version 1810. Do I have rights to install it?   

If you have active *SA*, you do have rights. If you don't have active SA, uninstall the current branch, and then install the LTSB of Configuration Manager. The LTSB doesn't receive updates for incremental versions of Configuration Manager, but does receive security updates based on the Support Lifecycle.


### <a name="bkmk_csp"></a> I have purchased EMS or Microsoft 365 through a Cloud Solution Provider (CSP), do I have rights to use Configuration Manager? 

Yes, you have rights to use Configuration Manager to manage clients covered by the EMS license. First download and install the [evaluation software](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Then contact Microsoft Support to obtain the license key.<!--issue472--> When you talk with Microsoft Support, ask them to reference the internal article ID 4033838.<!-- SCCMDocs issue 493 --> 


### <a name="bkmk_expiration-date"></a> Is my subscription end-date the same as an SA expiration date?    

If *SA* or your subscription is active, you have use rights for Configuration Manager current branch. An active subscription is equivalent of having active *SA*, but no perpetual *"L" (license)*. Once your subscription is over, uninstall the current branch. At this time, you don't have rights to use the LTSB.  


### <a name="bkmk_sql"></a> What are the use rights associated with the SQL technology provided with Configuration Manager?    

All of the System Center products include SQL Server technology. Microsoft's licensing terms for these products allow customer use of SQL Server technology only to support System Center components. SQL Server client access licenses are not required for that use. 
 
Approved use rights for the SQL capabilities with Configuration Manager include:
 - Site database role
 - Windows Server Update Services (WSUS) for software update point role
 - SQL Server Reporting Services (SSRS) for reporting point role
 - Data warehouse service point role
 - Database replicas for management point roles
 - SQL Server Always On 

The SQL Server license that's included with Configuration Manager supports each instance of SQL Server that you install to host a database for Configuration Manager. However, only databases for Configuration Manager in the preceding list can run on that SQL Server when you use this license. If a database for any additional Microsoft or third-party product shares the SQL Server, you must have a separate license for that SQL Server instance. 
 <!-- sms500967 -->


### <a name="bkmk_opmdm"></a> Does on-premises mobile device management (MDM) require an Intune subscription?

In versions 1806 and earlier, to start using on-premises MDM, you need a Microsoft Intune subscription. The subscription is only required to track licensing of the devices and isn't used to manage or store management information for the devices. All management data is stored in your organization using the on-premises Configuration Manager infrastructure.  

Starting in version 1810, an Intune connection is no longer required for new on-premises MDM deployments.<!--3607730, fka 1359124--> Your organization still requires Intune licenses to use this feature. You can't currently remove the Intune connection from existing on-premises MDM deployments. For more information, see the [Intune support blog post](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

