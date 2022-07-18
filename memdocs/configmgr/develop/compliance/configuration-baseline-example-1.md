---
title: "Configuration Baseline Example 1"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 488ff3c1-2bc0-49a0-b925-ab6f41c9561f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: "This Baseline Configuration Item Instance example references an application configuration item that checks whether the Configuration Manager client and Notepad are installed on systems that are running Windows XP SP2." 

---
# Configuration Baseline Example 1
The following Baseline Configuration Item Instance example references an application configuration item that checks whether the Configuration Manager client and Notepad.exe are installed on systems that are running Windows XP SP2.  

## Configuration Baseline Example  

```xml
<?xml version="1.0" encoding="utf-8"?>  

<!--   
The root element for any DCM Digest document is the DesiredConfigurationDigest element referenced below.  All of the XML elements/attributes are defined in the DCM Digest schema definition namespace.  
-->  

<DesiredConfigurationDigest xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration">  

<!--   
Every digest must contain exactly one configuration item. Specifically one of the following: an application, operatingsystem, general or baseline.  
This is a baseline configuration item.  
The baseline configuration item provides a way to group other configuration items (including other baselines) for deployment to clients. Other types of configuration items cannot be directly deployed to clients, they must be referenced within a baseline configuration item, which is then deployed to clients.  

The unique identify of the configuration item is the combination of the attributes AuthoringScopeID, LogicalName and Version.   
Each attribute is part of the unique identity of the configuration item; the actual identity is AuthoringScopeID + LogicalName + Version.  

AuthoringScopeID (string) - This attribute corresponds to the author's namespace or identity.  
LogicalName (string) - This attribute identifies the configuration item within the authoring scope.  
Version (string) - This attribute specifies the version of the configuration item.  
-->  

    <Baseline AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="Baseline_ab095740-707a-46b6-8408-a72be147514c" Version="1">  
        <Annotation>  
            <DisplayName Text="Sample Baseline" />  
            <Description Text="A baseline that includes the sample CI." />  
        </Annotation>  

<!--  
Only application and general configuration item references can be used in the RequiredItems section.  

Below is a reference to an application configuration item that checks to see whether the Configuration Manager 2007 client is installed on the system. The application configuration item can be found in the Application Configuration Item Schema Example 1 (link below)  
-->  

        <RequiredItems>  
            <ApplicationReference AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="Application_5cb68ff1-a234-41ed-a7d4-14174d8108b7" Version="1" />  
        </RequiredItems>  

<!--  
Only application configuration item references can appear in ProhibitedItems.  
-->  

        <ProhibitedItems>  
        </ProhibitedItems>  

<!--  
Only application configuration items can appear in OptionalItems.  

Below is a reference to an application configuration item that checks to see whether Notepad.exe is installed on the system. The application configuration item can be found in the Application Configuration Item Schema Example 2 (link below)  
-->  

        <OptionalItems>  
            <ApplicationReference AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="Application_171bae6f-5661-4bb8-a703-270b131e4c4c" Version="1" />  
        </OptionalItems>  

<!--  
Only operating system configuration items can appear in OperatingSystems.    
At least one of the operating systems in the referenced OperationSystem configuration items must be detected on the targeted computer.  

Below is a reference to an operating system configuration item that checks to see whether Windows XP SP2 is installed on the system. The application configuration item can be found in the Operating System Configuration Item Schema Example 1 (link below)  
-->  

        <OperatingSystems>  
            <OperatingSystemReference AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="OperatingSystem_8aa19644-7801-411c-a7fa-8e7a33d0d8fe" Version="3" />  
        </OperatingSystems>  

<!--   
Only SoftwareUpdates and SoftwareUpdateBundles can appear in SoftwareUpdates. Software Updates configuration items are created and administered through the Software Updates Management feature in Configuration Manager. The Software Updates configuration items can be referenced in configuration baselines; however, they should not be directly authored via DCM or the DCM Digest.  
 -->  

        <SoftwareUpdates>  
        </SoftwareUpdates>  

<!-- Only baseline configuration item references can appear in Baselines.  References to other baselines. -->  
        <Baselines>  
        </Baselines>  

<!--  
Only references to content defined as System Definition Model language (SDM) can appear in OtherConfigurationItems.  
-->  

        <OtherConfigurationItems>  
        </OtherConfigurationItems>  

    </Baseline>  
</DesiredConfigurationDigest>  
```  

## See Also  
[About authoring configuration baselines and items](about-authoring-configuration-baselines-and-configuration-items.md)
