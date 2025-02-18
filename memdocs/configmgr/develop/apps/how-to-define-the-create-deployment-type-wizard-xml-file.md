---
title: How to Define the Create Deployment Type Wizard XML File
description: To define the custom create deployment type wizard XML file, create an XML file based on the schema.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 249a6d47-c45f-491d-a846-8082665c6185
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Define the Create Deployment Type Wizard XML File
To define the custom create deployment type wizard XML file, create an XML file based on the `https://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework` schema. The XML file for the Create Application Wizard should be named CreateDeploymentWizard_\<*TechnologyID*>.xml.  

### To define the create deployment type wizard XML file  

1.  Create a Create Deployment Type Wizard XML file.  

     The following example from the RDP sample project demonstrates how to define the Deployment Type Wizard XML file.  

    ```xml
    <?xml version="1.0" encoding="utf-8"?>  
    <SmsFormData xmlns="https://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework" FormatVersion="1">  
      <Form Id="{FD19DEC6-81ED-447B-9D88-3AAD7DE499F1}" CustomData="CreateDT" FormType="PropertySheet" ForceRefresh="true">  
        <Pages>  
          <Page Assembly="AdminUI.DeploymentType.Rdp.dll" Namespace="RdpTechnology.AdminConsole" VendorId="Partner Company Name" Id="{6802BC91-30EF-49A5-80F6-D4902CD5181C}" Type="RdpDeploymentTechnologyPageControl" />  
        </Pages>  
      </Form>  
    </SmsFormData>  
    ```  

## See Also  
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
