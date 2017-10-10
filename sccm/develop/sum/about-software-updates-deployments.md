---
title: "Software Updates Deployments"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "12/30/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: f421edfe-d1c6-4fec-a5d1-d1399d4a3a82
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---

# About Software Updates Deployments
Software updates are delivered to client computers in System Center Configuration Manager by creating software update deployments. It is a multistep process to create software update deployments by using the Configuration Manager SDK interfaces. A basic approach to deploying software updates, by using the Configuration Manager SDK interfaces, is outlined below.  

> [!NOTE]
>  General information about Software Updates can be found in the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt346023.aspx) under [Deploy and manage software updates in System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt634340.aspx).  

 Coding examples (in C# and VBScript) for individual steps of the deployment process are included in the [Software Updates Deployments](../../develop/sum/software-updates-deployments.md) section of the Configuration Manager SDK.  

> [!NOTE]
>  Deleting updates or update bundles is not supported by the Configuration Manager SDK.  

 Select which software updates to install.  
 This can be something such as running a query to identify which updates should be installed.  

 For information about queries that use criteria, such as selecting software updates for a specific knowledge base article, or selecting software updates that are a specific severity level, see [How to Enumerate Updates Matching a Specific Criteria](../../develop/sum/how-to-enumerate-updates-matching-a-specific-criteria.md).  

 Obtain the configuration item identification (CI_ID) values.  
 The CI_ID value identifies the software updates information across several classes. For the purposes of using the Configuration Manager SDK interfaces, the CI_ID value is vital.  

 The CI_ID value is a property of several classes and can be readily identified by using the [SMS_SoftwareUpdate](../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md) class.  

 For more information about a number of queries that include the CI_ID, see [How to Enumerate Updates Matching a Specific Criteria](../../develop/sum/how-to-enumerate-updates-matching-a-specific-criteria.md).  

 Download the software update content.  
 Software update content must be downloaded manually. To identify which contents must be downloaded, query the [SMS_CIToContent](../../develop/reference/sum/sms_citocontent-server-wmi-class.md) class and obtain the list of `ContentID` properties that match the specific language criteria. After you have the list of `ContentID` properties, you can obtain the associated download URL and the related properties for the content files from the [SMS_CIContentFiles](../../develop/reference/sum/sms_cicontentfiles-server-wmi-class.md) class by using the `ContentID` properties you obtained earlier.  

 Create a software updates deployment package.  
 The software updates deployment package holds the software updates content. For information about creating a deployment package, see [How to Create a Deployment Package](../../develop/sum/how-to-create-a-deployment-package.md).  

 Add update content to the software updates package.  
 After a software updates deployment package has been created, software updates contents can be added to the package by using the [AddUpdateContent](../../develop/reference/sum/addupdatecontent-method-in-class-sms_softwareupdatespackage.md) method in the [SMS_SoftwareUpdatesPackage](../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md) class. For information about adding software updates content to a deployment package, see [How to Add Updates to a Deployment Package](../../develop/sum/how-to-add-updates-to-a-deployment-package.md).  

 Create a software updates deployment to distribute the software updates.  
 Distribute software updates by creating a software updates deployment. For information about the process for creating a software updates deployment, see [How to Configure and Deploy Updates](../../develop/sum/how-to-configure-and-deploy-updates.md).  

## See Also  
 [Configuration Manager SDK](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Updates](../../develop/sum/software-updates.md)   
 [How to Enumerate Updates Matching a Specific Criteria](../../develop/sum/how-to-enumerate-updates-matching-a-specific-criteria.md)   
 [How to Create an Update List](../../develop/sum/how-to-create-an-update-list.md)   
 [How to Create a Deployment Package](../../develop/sum/how-to-create-a-deployment-package.md)   
 [How to Add Updates to a Deployment Package](../../develop/sum/how-to-add-updates-to-a-deployment-package.md)   
 [How to Delete Updates from a Deployment Package](../../develop/sum/how-to-delete-updates-from-a-deployment-package.md)   
 [How to Configure and Deploy Updates](../../develop/sum/how-to-configure-and-deploy-updates.md)
