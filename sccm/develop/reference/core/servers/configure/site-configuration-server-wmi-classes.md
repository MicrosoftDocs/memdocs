---
title: "Site Configuration Server WMI Classes"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: fac9263e-4e47-4e15-b07a-27a39c9ecd74searchScope: - ConfigMgr SDK
caps.latest.revision: 21
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Site Configuration Server WMI Classes
This section contains detailed reference information about the site configuration server Windows Management Instrumentation (WMI) classes in System Center Configuration Manager. These classes include classes that relate to an installation of Configuration Manager that consists of one or more computers running the Configuration Manager components.  

 You can configure the components of a site at any time to enhance the management of your site. Configuration information is contained in the install map and the site control file.  

 When you install Configuration Manager, it creates an install map that describes the initial configuration of the installed features for the server, client, and Configuration Manager console. The install map configuration data is read-only and uses the following classes:  

-   [SMS_SiteInstallMap Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallmap-server-wmi-class.md)  

-   [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)  

-   [SMS_SiteInstallItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitem-server-wmi-class.md)  

-   [SMS_SystemResourceList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)  

-   [SMS_UINAL_ResourceInfo Server WMI Class](../../../../../develop/reference/misc/sms_uinal_resourceinfo-server-wmi-class.md)  

 Classes that are derived from `SMS_SiteInstallItem` use the naming convention `SMS_SII_*`**.** Classes that are derived from `SMS_SiteInstallItemBase` use the naming convention `SMS_SIIB_*`.  

 The site control file describes the current configuration of the site and its components. Use the following classes to manage the site control file and the site configuration data:  

-   [SMS_SiteControlFile Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md)  

-   [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)  

 Classes that are derived from `SMS_SiteControlItem` use the naming convention `SMS_SCI_*`. Use these classes to access and modify the configuration items that are contained in the site control file.For information about managing the site control file and changing component configuration, see [Configuration Manager Site Control File](../../../../../develop/core/understand/site-control-file.md).  

## Site Configuration Server WMI Classes  

-   [SMS_Boundary Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundary-server-wmi-class.md)  

-   [SMS_BoundaryGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundarygroup-server-wmi-class.md)  

-   [SMS_BoundaryGroupMembers Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundarygroupmembers-server-wmi-class.md)  

-   [SMS_BoundaryGroupRelationships Server WMI Class](../../../../../develop/reference/core/servers/configure/sms-boundarygrouprelationships-server-wmi-class.md)

-   [SMS_BoundaryGroupSiteSystems Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_boundarygroupsitesystems-server-wmi-class.md)  

-   [SMS_Client_Reg_MultiString_List Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_client_reg_multistring_list-server-wmi-class.md)  

-   [SMS_CMSiteConfiguration Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_cmsiteconfiguration-server-wmi-class.md)  

-   [SMS_DefaultBoundaryGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms-defaultboundarygroup-server-wmi-class.md)

-   [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md)  

-   [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md)  

-   [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)  

-   [SMS_RcmSqlControl](../../../../../develop/reference/core/servers/configure/sms_rcmsqlcontrol-server-wmi-class.md)  

-   [SMS_RcmSqlControlProperty](../../../../../develop/reference/core/servers/configure/sms_rcmsqlcontrolproperty-server-wmi-class.md)  

-   [SMS_ReplicationGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_replicationgroup-server-wmi-class.md)  

-   [SMS_ReplicationLinkStatus Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_replicationlinkstatus-server-wmi-class.md)  

-   [SMS_ReplicationLinkSummary Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_replicationlinksummary-server-wmi-class.md)  

-   [SMS_SCI_Address Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_address-server-wmi-class.md)  

-   [SMS_SCI_ClientComp Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md)  

-   [SMS_SCI_ClientConfig Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_clientconfig-server-wmi-class.md)  

-   [SMS_SCI_Component Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)  

-   [SMS_SCI_Configuration Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_configuration-server-wmi-class.md)  

-   [SMS_SCI_FileDefinition Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_filedefinition-server-wmi-class.md)  

-   [SMS_SCI_MaintenanceTask Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_maintenancetask-server-wmi-class.md)  

-   [SMS_SCI_SiteDefinition Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_sitedefinition-server-wmi-class.md)  

-   [SMS_SCI_SQLTask Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_sqltask-server-wmi-class.md)  

-   [SMS_SCI_SysResUse Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)  

-   [SMS_SII_Property Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_property-server-wmi-class.md)  

-   [SMS_SII_PropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sii_propertylist-server-wmi-class.md)  

-   [SMS_SIIB_AddressType Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siib_addresstype-server-wmi-class.md)  

-   [SMS_SIIB_Component_FileList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siib_component_filelist-server-wmi-class.md)  

-   [SMS_SIIB_Configuration Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siib_configuration-server-wmi-class.md)  

-   [SMS_SIIB_Generic_Configuration Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siib_generic_configuration-server-wmi-class.md)  

-   [SMS_SIIB_SenderType Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siib_sendertype-server-wmi-class.md)  

-   [SMS_SIIB_SysResRole Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siib_sysresrole-server-wmi-class.md)  

-   [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)  

-   [SMS_SiteAndSubsites Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteandsubsites-server-wmi-class.md)  

-   [SMS_SiteControlDaySchedule Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontroldayschedule-server-wmi-class.md)  

-   [SMS_SiteControlFile Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md)  

-   [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)  

-   [SMS_SiteInstallItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitem-server-wmi-class.md)  

-   [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)  

-   [SMS_SiteInstallMap Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallmap-server-wmi-class.md)  

-   [SMS_SystemResourceList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)  

-   [SMS_SCFToSCI_a Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scftosci_a-server-wmi-class.md)  

-   [SMS_SCFToSite_a Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scftosite_a-server-wmi-class.md)  

-   [SMS_SiteToSubSite_a Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitetosubsite_a-server-wmi-class.md)  

-   [SMS_SiteToSiteID_a Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitetositeid_a-server-wmi-class.md)  

## See Also  
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
