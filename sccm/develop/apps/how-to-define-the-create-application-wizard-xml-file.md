---
title: "How to Define the Create Application Wizard XML File"
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
ms.assetid: 5e09cee5-b251-42d0-b927-e1d6019f3695searchScope: - ConfigMgr SDK
caps.latest.revision: 20
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Define the Create Application Wizard XML File
To define the custom deployment technology XML file, create an XML file based on the `http://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework` schema. The XML file for the Create Application Wizard should be named, CreateApp_\<*TechnologyID*>.xml.  

### To define the create application wizard XML file  

1.  Create a Create Application Wizard XML file.  

     The following example from the RDP sample project shows how to define the Create Application Wizard XML file. Note that wizards are not extensible for the UI.  However, by creating this custom deployment technology XML, the contents of the wizard now include the ability to create a RDP deployment type.  

    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <SmsFormData xmlns="http://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework" FormatVersion="1">  
      <Form Id="{FD19DEC6-81ED-447B-9D88-3AAD7DE499F1}" CustomData="CreateApp" FormType="PropertySheet" ForceRefresh="true">  
        <Pages>  
          <Page Assembly="AdminUI.DeploymentType.Rdp.dll" Namespace="RdpTechnology.AdminConsole" VendorId="Partner Company Name" Id="{6802BC91-30EF-49A5-80F6-D4902CD5181C}" Type="RdpDeploymentTechnologyPageControl" />  
        </Pages>  
      </Form>  
    </SmsFormData>  
    ```  

## See Also  
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
