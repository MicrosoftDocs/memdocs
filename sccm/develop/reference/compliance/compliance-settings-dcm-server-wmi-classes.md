---
title: "Compliance Settings Classes"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4dbfce7f-1b58-4998-9b38-f5f3c3ba77c6
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration Manager Compliance Settings (DCM) Server WMI Classes
In System Center Configuration Manager, compliance settings (DCM) server Windows Management Instrumentation (WMI) classes, assist you in assessing computer compliance by considering a number of configurations, for example, installation and configuration of the correct versions of Microsoft Windows operating systems. You can also use these classes to check for compliance with software updates and security settings.  

 The main classes supporting the compliance settings feature are:  

- [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md), representing a generic configuration item.  

- [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md), representing information for a baseline configuration item.  

- [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md), representing an assignment of a baseline configuration item.  

  For more information, see Desired Configuration Management Configuration Baselines and Configuration Items.  

> [!NOTE]
>  Some of the classes that are defined for desired configuration management, for example, [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md), are specific to baseline configuration items. Some of the classes can also be used to reference software update configuration items, although applications use the software updates feature to manipulate these items. For more information, see [Configuration Manager Software Updates](../../../develop/sum/software-updates.md).  

 The System Center Configuration Manager server class schema is a set of WMI classes that represent the objects on a server running Configuration Manager. Each Configuration Manager class is a template for a managed object and all instances of the object use the template. Classes can contain properties and methods. The properties describe the class data, and the methods typically perform data management. For more information about developing applications using these classes, see [About Configuration Manager SDK Requirements](../../../develop/core/reqs/about-configuration-manager-sdk-requirements.md).  

## Compliance Settings (DCM) Server WMI Classes  

-   [SMS_AdvancedThreatProtectionSettings Server WMI Class](../../../develop/reference/compliance/sms_advancedthreatprotectionsettings-server-wmi-class.md)  

-   [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)  

-   [SMS_Category_LocalizedProperties Server WMI Class](../../../develop/reference/compliance/sms_category_localizedproperties-server-wmi-class.md)  

-   [SMS_CategoryInstance Server WMI Class](../../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md)  

-   [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md)  

-   [SMS_CategoryInstanceMembership Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancemembership-server-wmi-class.md)  

-   [SMS_CI_ComplianceHistory Server WMI Class](../../../develop/reference/compliance/sms_ci_compliancehistory-server-wmi-class.md)  

-   [SMS_CI_ComplianceSummary Server WMI Class](../../../develop/reference/compliance/sms_ci_compliancesummary-server-wmi-class.md)  

-   [SMS_CI_CurrentComplianceStatus Server WMI Class](../../../develop/reference/compliance/sms_ci_currentcompliancestatus-server-wmi-class.md)  

-   [SMS_CI_LocalizedEulas Server WMI Class](../../../develop/reference/compliance/sms_ci_localizedeulas-server-wmi-class.md)  

-   [SMS_CI_LocalizedProperties Server WMI Class](../../../develop/reference/compliance/sms_ci_localizedproperties-server-wmi-class.md)  

-   [SMS_CIAssignmentBaseClass Server WMI Class](../../../develop/reference/compliance/sms_ciassignmentbaseclass-server-wmi-class.md)  

-   [SMS_CIAssignmentToCI Server WMI Class](../../../develop/reference/compliance/sms_ciassignmenttoci-server-wmi-class.md)  

-   [SMS_CIRelation_Flat Server WMI Class](../../../develop/reference/compliance/sms_cirelation_flat-server-wmi-class.md)  

-   [SMS_CIContentPackage Server WMI Class](../../../develop/reference/compliance/sms_cicontentpackage-server-wmi-class.md)  

-   [SMS_CompliancePolicySettings Server WMI Class](../../../develop/reference/compliance/sms_compliancepolicysettings-server-wmi-class.md)  

-   [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md)  

-   [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)  

-   [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md)  

-   [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md)  

-   [SMS_ConfigurationItemRules Server WMI Class](../../../develop/reference/compliance/sms_configurationitemrules-server-wmi-class.md)  

-   [SMS_ConfigurationItemSettings Server WMI Class](../../../develop/reference/compliance/sms_configurationitemsettings-server-wmi-class.md)  

-   [SMS_ConfigurationItemSettingReference Server WMI Class](../../../develop/reference/compliance/sms_configurationitemsettingreference-server-wmi-class.md)  

-   [SMS_ConfigurationPlatform Server WMI Class](../../../develop/reference/compliance/sms_configurationplatform-server-wmi-class.md)  

-   [SMS_ConfigurationPolicy Server WMI Class](../../../develop/reference/compliance/sms_configurationpolicy-server-wmi-class.md)  

-   [SMS_ConfigurationPolicyAssignment Server WMI Class](../../../develop/reference/compliance/sms_configurationpolicyassignment-server-wmi-class.md)  

-   [SMS_ConfigurationPolicyBase Server WMI Class](../../../develop/reference/compliance/sms_configurationpolicybase-server-wmi-class.md)  

-   [SMS_DCMDeploymentCompliantAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantassetdetails-server-wmi-class.md)  

-   [SMS_DCMDeploymentCompliantDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantdetailsperasset-server-wmi-class.md)  

-   [SMS_DCMDeploymentCompliantStatus Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentcompliantstatus-server-wmi-class.md)  

-   [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md)  

-   [SMS_DCMDeploymentErrorDetailsPerAsset Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrordetailsperasset-server-wmi-class.md)  

-   [SMS_DCMDeploymentErrorStatus Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorstatus-server-wmi-class.md)  

-   [SMS_DCMDeploymentNonCompliantAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentnoncompliantassetdetails-server-wmi-class.md)  

-   [SMS_DCMDeploymentNonCompliantStatus Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymentnoncompliantstatus-server-wmi-class.md)  

-   [SMS_G_System_CI_ComplianceState Server WMI Class](../../../develop/reference/compliance/sms_g_system_ci_compliancestate-server-wmi-class.md)  

-   [SMS_HealthAttestationDetails Server WMI Class](../../../develop/reference/compliance/sms_healthattestationdetails-server-wmi-class.md)  

-   [SMS_MAMPolicyTemplate Server WMI Class](../../../develop/reference/compliance/sms_mampolicytemplate-server-wmi-class.md)  

-   [SMS_PassportForWorkProfileSettings Server WMI Class](../../../develop/reference/compliance/sms_passportforworkprofilesettings-server-wmi-class.md)  

-   [SMS_PfxCertificateSettings Server WMI Class](../../../develop/reference/compliance/sms_pfxcertificatesettings-server-wmi-class.md)  

-   [SMS_SDMPackageLocalizedData Server WMI Class](../../../develop/reference/compliance/sms_sdmpackagelocalizeddata-server-wmi-class.md)  

-   [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md)  

-   [SMS_TermsAndConditionsSettings Server WMI Class](../../../develop/reference/compliance/sms_termsandconditionssettings-server-wmi-class.md)  

-   [SMS_UserStateManagementSettings Server WMI Class](../../../develop/reference/compliance/sms_userstatemanagementsettings-server-wmi-class.md)  

-   [SMS_WSfBConfigurationData Server WMI Class](../../../develop/reference/compliance/sms_wsfbconfigurationdata-server-wmi-class.md)  

## See Also  
 [Configuration Manager Compliance Settings (DCM)](../../../develop/compliance/compliance-settings-dcm.md)   
 [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md)
