---
title: OS Configuration Item Example 1
titleSuffix: Configuration Manager
description: Example 1 for Operating System Configuration Item
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: bee6d39d-fbf9-451e-bd3a-0330cc57d910
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Operating System Configuration Item Example 1
In Configuration Manager, the following Operating System Configuration Item Schema example checks for Windows XP SP2.  

## Operating System Configuration Item Example  

```xml
<?xml version="1.0" encoding="utf-8"?>  

<!--   
The root element for any DCM Digest document is the DesiredConfigurationDigest element referenced below.  All of the XML elements/attributes are defined in the DCM Digest schema definition namespace.  
-->  

<DesiredConfigurationDigest xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration">  

<!--  
Every DCM Digest must contain exactly one configuration item. Specifically one of the following: an application, operatingsystem, general or baseline.  
This digest defines an operating system configuration item.    

The unique identify of the configuration item is the combination of the attributes AuthoringScopeID, LogicalName and Version.   
Each attribute is part of the unique identity of the configuration item; the actual identity is AuthoringScopeID + LogicalName + Version.  

AuthoringScopeID (string) - This attribute corresponds to the author's namespace or identity.  
LogicalName (string) - This attribute identifies the configuration item within the authoring scope.  
Version (string) - This attribute specifies the version of the configuration item.  
-->  

    <OperatingSystem AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="OperatingSystem_c745714d-1063-4dec-8447-a9414ec030e7" Version="1">  
        <Annotation>  
            <DisplayName Text="My WinXp SP2 Operating System CI" />  
            <Description Text="Simple Operating System detection." />  
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
OperatingSystem identifies how to determine whether or not this operating system exists on the system. If it does exist (is discovered), then the system discovers the parts and settings. Finally, the system evaluates the rules(if any) defined against the part property values and the setting values.  
-->  
        <OperatingSystemDiscoveryInfo BuildVersion="2600" MajorVersion="5" MinorVersion="10" ServicePackMajorVersion="2" ServicePackMinorVersion="0" />  
    </OperatingSystem>  
</DesiredConfigurationDigest>  
```  

## See Also  
[About authoring configuration baselines and items](about-authoring-configuration-baselines-and-configuration-items.md)
