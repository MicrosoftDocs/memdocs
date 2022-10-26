---
title: Configuration Manager Site Control File
description: Site control in Configuration Manager defines the settings for a specific site.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1283e2a3-d4e2-4fba-a6c3-7dcd94598a0d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About the Configuration Manager Site Control File
Site control in Configuration Manager defines the settings for a specific site. The settings for each site are contained in the database and are accessed through Windows Management Instrumentation (WMI) when working with scripting languages, and through the managed SMS Provider library when working with a managed language.  

> [!NOTE]
>  Previous releases of Configuration Manager had a physical file that was processed for site settings referred to as the site control file. Configuration Manager stores site settings directly in the site database; however, very little has changed when programmatically configuring a site.  

The site control file in Configuration Manager is an ASCII text file (Sitectrl.ct0) that contains the configuration of each site. There are two types of site control files:  

- Actual site control file - A working copy of the site control file that is stored in the Configuration Manager site database and in the inbox in the site control manager.  

- Delta site control file - Contains the proposed site control file changes that are to be processed.  

  The site control file is stored on each site server in the site control manager inbox.  

  On the primary site, there is a copy of the site control file for the current site in the database. The primary site also has a copy of the site control file for all lower level sites in the hierarchy, including secondary sites.  

  Each child site passes a copy of its site control file to its parent site. Each parent site passes a copy of the site control file for itself and for each of its child sites up the hierarchy. Therefore, the central site's database contains copies of the site control files of every Configuration Manager site in the hierarchy.  

## Site Control File Format  
 The site control file is a collection of resource definitions that contain embedded properties, embedded property lists and multi-string lists. The following example shows a section of site control file that defines client component information. The resource is declared by the BEGIN_CLIENT_COMPONENT. The embedded properties are denoted by PROPERTY and have a name and value. The property lists are denoted by the BEGIN_PROPERTY_LIST section and list a property list name and several property names and associated values. The multi-string lists are denoted by the BEGIN_CLIENT_REG_MULTI_STRING_LIST and provide a list of string values.  

```  
BEGIN_CLIENT_COMPONENT  
    <SMS Client Base Components>  
    <65537>  
    SITE_KEY_FLAGS <1>  
    PROPERTY <Component Verify Interval><REG_SZ><00011700001000F0><0>  
    PROPERTY <Component Maintenance Interval (minutes)><REG_DWORD><><1500>  
    BEGIN_PROPERTY_LIST  
        <Copy Queue>  
        <(REG_DWORD)Item Lifetime=11520>  
        <(REG_DWORD)Wakeup cycle=1380>  
    END_PROPERTY_LIST  
    BEGIN_CLIENT_REG_MULTI_STRING_LIST  
        <Retry Sequence><Copy Queue>  
        SITE_KEY_FLAGS <1>  
        <15>  
        <30>  
        <60>  
        <360>  
    END_CLIENT_REG_MULTI_STRING_LIST  
END_CLIENT_COMPONENT  
```  

 The provider has several Windows Management Instrumentation (WMI) classes that represent resources in the site control file. For example, [SMS_SCI_Component Server WMI Class](../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md) holds information on the server components stored on a Configuration Manager site server. These classes derive from [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md). For more information, see [Configuration Manager Site Configuration Server WMI Classes &#91;reference&#93;](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md).  

 The following example is the declaration for [SMS_SCI_ClientConfig Server WMI Class](../../../develop/reference/core/servers/configure/sms_sci_clientconfig-server-wmi-class.md).  

```  
Class SMS_SCI_ClientConfig : SMS_SiteControlItem   
{  
     String ClientConfigName;  
     UInt32 FileType;  
     UInt32 Flags;  
     String ItemName;  
     String ItemType;  
     String Platforms[];  
     SMS_EmbeddedPropertyList PropLists[];  
     SMS_EmbeddedProperty Props[];  
     SMS_Client_Reg_MultiString_List RegMultiStringLists[];  
     String SiteCode;  
};  
```  

 The declaration includes declarations for the embedded property, property list, and multi string list declarations.  

 You access the embedded properties, property lists, and multi-string lists by using the following classes:  

|Type|WMI Class|  
|----------|---------------|  
|Embedded property|[SMS_EmbeddedProperty Server WMI Class](../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)|  
|Embedded property list|[SMS_EmbeddedPropertyList Server WMI Class](../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) (array)|  
|Multi-string list|[SMS_Client_Reg_MultiString_List Server WMI Class](../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md) (array)|  

 This documentation has the following topic that describes the embedded properties:  

 [How to Read a Configuration Manager Site Control File Embedded Property List](../../../develop/core/understand/how-to-read-a-configuration-manager-site-control-file-embedded-property-list.md)  

## Using the Site Control File  
 How you access the site control file differs depending on whether you are using WMI or the managed provider.  

### WMI  
 When you are using WMI, you use the `SMS_SiteControlFile` class methods to manage changes to the site control file. Writing to the site control file is managed by using session contextual information that you supply. This is used to enable concurrent writing to the site control file for multiple applications. For more information, see [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md) If you are only reading from the site control file you can query it without setting up a session.   

### Managed Provider  
 In almost all cases, your code does not have to lock or commit changes to the Configuration Manager site control file because the managed Configuration Manager library takes care of this for you. As a result, programming the Configuration Manager site control file is fundamentally the same as programming Configuration Manager objects. This is different from accessing the Configuration Manager site control file through WMI where you explicitly have to get a session handle and commit any changes you make.  

 For more information, see, [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md).  

## See Also  
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
