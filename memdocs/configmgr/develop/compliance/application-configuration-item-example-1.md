---
title: "Application Configuration Item Example 1"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: adc63f00-8fcf-4212-910a-26ae9154d574
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Application Configuration Item Example 1
The following Application Configuration Item Instance example determines whether the Configuration Manager client is installed on the system by using Microsoft Windows Installer-based detection.  

## Application Configuration Item Example  

```xml
<?xml version="1.0" encoding="utf-8"?>  

<!--   
The root element for any DCM Digest document is the DesiredConfigurationDigest element referenced below.  All of the XML elements/attributes are defined in the DCM Digest schema definition namespace.  
-->  

<DesiredConfigurationDigest xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration">  

<!--  
Every DCM Digest must contain exactly one configuration item. Specifically one of the following: an application, operatingsystem, general or baseline.  
This digest defines an application configuration item.    

The unique identity of the configuration item is the combination of the attributes AuthoringScopeID, LogicalName and Version.   
Each attribute is part of the unique identity of the configuration item; the actual identity is AuthoringScopeID + LogicalName + Version.  

AuthoringScopeID (string) - This attribute corresponds to the author's namespace or identity.  
LogicalName (string) - This attribute identifies the configuration item within the authoring scope.  
Version (string) - This attribute specifies the version of the configuration item.  
-->  

    <Application AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="Application_5cb68ff1-a234-41ed-a7d4-14174d8108b7" Version="1" Is64Bit="false">  
        <Annotation>  
            <DisplayName Text="Configuration Manager Client" />  
            <Description Text="Configuration Manager Client (Windows Installer-based detection)" />  
        </Annotation>  

<!--  
There are no parts defined for this configuration item.  
Parts are physical things with fixed lists of properties.Mandatory element tag for the section of the DCM Digest used to define Object parts, including:  
File  
Folder  
Assembly (registered in the Global Assembly Cache (GAC))  
RegistryKey  
-->  

        <Parts>  
            <ParentReferences />  
        </Parts>  

<!--  
There are no settings defined for this configuration item.   
Settings are configurable name/value pairs which influence the behavior of hardware and software. DCM can discover settings using any of the supported providers, including:  
Registry  
WMI (WQL query)  
Microsoft SQL Server (SQL query)  
Active Directory (LDAP)  
XML (XPath query)  
IIS Metabase  
Script (JScript/VBScript/PowerShell)  
-->  

        <Settings>  

<!--  
RootComplexSetting is the root container for all settings. Every configuration item has one of these, even if there are no actual settings defined.  
-->  
            <RootComplexSetting />  

        </Settings>  

<!--  
This application is discovered via Windows Installer-based discovery. If it does exist (is discovered) the system then discovers the parts and settings. Finally, the system evaluates the rules (if any) defined against the part property values and the setting values.  
-->  

        <MsiDiscoveryInfo IsPerUser="false" ProductCode="{D7D7EE27-817F-481D-865F-F5755FA89E2E}" Version="4.00.5507.0000" />  

    </Application>  
</DesiredConfigurationDigest>  
```  

## See Also  
[About authoring configuration baselines and items](about-authoring-configuration-baselines-and-configuration-items.md)
