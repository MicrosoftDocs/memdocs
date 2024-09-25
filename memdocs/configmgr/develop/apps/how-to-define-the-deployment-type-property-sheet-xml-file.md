---
description: Learn how to create and define the custom deployment type property page XML file for use within Configuration Manager.
title: Define the Deployment Type Property Sheet XML File
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: dd5151b2-09f0-4c8d-ad5f-727b8b3d4e56
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Define the Deployment Type Property Sheet XML File
To define the custom deployment type property page XML file, create an XML file based on the `https://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework` schema. The XML file for the deployment type property sheet should be named \<*TechnologyID*>DeploymentTypePropertySheet.xml.  

### To define the deployment type property page XML file  

1.  Create a deployment type property sheet XML file.  

     The following example from the RPC sample project shows how to define the deployment type property sheet XML file.  

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>   
    <SmsFormData xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" FormatVersion="1" xmlns="https://schemas.microsoft.com/SystemsManagementServer/2005/03/ConsoleFramework">  
      <Form Id="f1908d6f-1ef8-4304-a229-c521c8e33713" FormType="PropertySheet">  
        <Resources>  
          <Title Name="_AppTitle" />  
          <Icon Name="_AppIcon" />  
        </Resources>  
        <Assembly Name="AdminUI.DeploymentType.Rdp.dll" Namespace="RdpTechnology.AdminConsole"/>  
        <Pages>  
          <Page VendorId="Partner Company Name" Id="{8A248387-62CB-4253-8255-47E9723BC40D}" Type="RdpDeploymentTechnologyPageControl" />  
        </Pages>  
      </Form>  
    </SmsFormData>  
    ```  

## See Also  
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
