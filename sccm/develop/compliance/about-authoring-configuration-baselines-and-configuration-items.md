---
title: "About Authoring Configuration Baselines and Items"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 39e47528-ea59-4d32-8baf-d017d3a44426searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Authoring Configuration Baselines and Configuration Items
System Center Configuration Manager supports the authoring of configuration data, which consists of configuration baselines and configuration items, in the System Center Configuration Manager console. Configuration Manager is able to present this configuration data in a user-friendly format called DCM Digest, which is a specialized XML document that Configuration Manager uses. You can author configuration data by using the Configuration Manager console, or by directly authoring a DCM Digest XML file.  

 Configuration data that is created with the Configuration Manager console can be exported into a .cab (cabinet) file. When configuration data is imported into Configuration Manager, the format can be the following:  

-   DCM Digest XML only.  

## Authoring Configuration Data  
 You can create configuration data in the following ways:  

-   You can create configuration data externally with an XML editor and then import it into Configuration Manager if it is first packaged as a .cab file.  

> [!NOTE]
>  See a discussion of configuration item authoring in the document provided as part of the System Center Configuration Manager 2007 Software Development Kit (SDK) download (Compliance_Settings_Digest_Authoring.doc).  

-   You can create configuration data within Configuration Manager by using the following wizards:  

    -   Create Application Configuration Item Wizard  

    -   Create Operating System Configuration Item Wizard  

    -   Create Configuration Baseline  

> [!IMPORTANT]
>  Software Updates configuration items are created and administered through the Software Updates Management feature in Configuration Manager. The Software Updates configuration items can be referenced by configuration baselines; however, they should not be directly authored by using Desired Configuration Management or the DCM Digest.  

 You can also import configuration data that has been published by Microsoft and other software vendors and solution providers as Best Practices configurations. You can download Best Practices configuration data from [http://go.microsoft.com/fwlink/?LinkId=71837](http://go.microsoft.com/fwlink/?LinkId=71837).  

> [!NOTE]
>  Published configuration data can be digitally signed so that you can verify the publishing source and be sure that the data has not been tampered with. If the digital signature verification check fails, you will be warned and prompted to continue with the import. It is recommended you import only configuration data from external sources if it has a valid digital signature from a trusted publisher.  

 After the configuration data is imported into the Configuration Manager site, it can then be copied and edited in the Configuration Manager console.  

## See Also  
 [Authoring Compliance Settings Configuration Baselines and Configuration Items](../../develop/compliance/authoring-compliance-settings-configuration-baselines-and-configuration-items.md)
