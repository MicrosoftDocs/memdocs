---
title: "How to Define the Resources"
titleSuffix: "Configuration Manager"
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
ms.assetid: 29a19b45-0413-4cb1-a74a-4c38cdc84118searchScope: - ConfigMgr SDK
caps.latest.revision: 18
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Define the Resources
To support the Installer, a custom XML schema should be included as part of the assembly. The schema file (XSD) file must be included as a resource in the assembly.  

> [!IMPORTANT]
>  The custom XML schema name must use the following naming convention:  
>   
>  1.  \<*InstallerClassName*>_XmlSchema.xsd  
>   
>  In the case of the RDP sample, the Installer implementation is called RdpInstaller, therefore the XML schema file for that technology is called RdpInstaller_XmlSchema.xsd.  

 As part of the resource documentation, a localizable title and description the technology should be created.  

> [!IMPORTANT]
>  The Title and Desciption should use the following naming conventions:  
>   
>  1.  \<*DeploymentTechnologyClassName*>_Title  
> 2.  \<*DeploymentTechnologyClassName*>_Description  

### To define a custom schema file  

1.  Create the custom schema file.  

     The following example from the RDP sample project demonstrates how to define a custom schema file.  

    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema id="RdpInstaller" version="1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/SystemsManagement/2009/ApplicationManagement" xmlns="http://schemas.microsoft.com/SystemsManagement/2009/ApplicationManagement" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:complexType name="RdpInstaller">  
        <xs:complexContent mixed="false">  
          <xs:extension base="Installer">  
            <xs:sequence>  
              <xs:element name="InstallFolder" type="string256" />  
              <xs:element name="Filename" type="string256" />  
              <xs:element name="ConstructRdpOnClient" type="xs:byte" />  
              <xs:element name="FullAddress" type="string256" minOccurs="0" />  
              <xs:element name="RemoteApplication" type="string256" minOccurs="0" />  
              <xs:element name="FullScreen" type="xs:byte" minOccurs="0" />  
              <xs:element name="DesktopWidth" type="int" minOccurs="0" />  
              <xs:element name="DesktopHeight" type="int" minOccurs="0" />  
              <xs:element name="AudioMode" type="string64" minOccurs="0" />  
              <xs:element name="RemoteServerName" type="string64" minOccurs="0" />  
              <xs:element name="RemoteServerPort" type="string64" minOccurs="0" />  
              <xs:element name="KeyboardMode" type="int" minOccurs="0" />  
              <xs:element name="RedirectPrinters" type="xs:byte" minOccurs="0" />  
              <xs:element name="RedirectSmartCards" type="xs:byte" minOccurs="0" />  
              <xs:element name="Username" type="string64" minOccurs="0" />  
              <xs:element name="ContentFilename" type="string256" minOccurs="0" />  
            </xs:sequence>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  
    </xs:schema>  
    ```  

#### Namespaces  
 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement.Serialization  

#### Assemblies  
 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

## .NET Framework Security  

## See Also  
 [How to Define the Hosting Technology](../../develop/apps/how-to-define-the-hosting-technology.md)   
 [How To Define the Installer Technology](../../develop/apps/how-to-define-the-installer-technology.md)   
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
