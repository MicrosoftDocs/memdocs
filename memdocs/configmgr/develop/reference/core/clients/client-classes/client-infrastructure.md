---
description: Learn all about the infrastructure of Configuration Manager including Control Panel, client framework and data transfer, and policy functionality.
title: "Client Infrastructure"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1d9da14b-2239-4e8e-a4f4-1761014f6740
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Client Infrastructure
This section provides reference information for the Configuration Manager client infrastructure, including Control Panel, client framework and data transfer, and policy functionality.  

## In This Section  
 Client Control Panel COM Automation  
 > [!IMPORTANT]
>  The Client Control Panel COM Automation interface has been removed or deprecated in Configuration Manager SP1. Use the feature-related client WMI class instead.

[Client Framework and Data Transfer Client WMI Classes](#client-framework-and-data-transfer-client-wmi-classes) describes the Client Configuration Manager (CCM) framework and data transfer classes in Configuration Manager for the client.

[Policy Agent Client WMI Classes](#policy-agent-client-wmi-classes) describes the classes used to manage policy on client computers and devices.

## Client Framework and Data Transfer Client WMI Classes  
The following framework and data transfer classes are used in Configuration Manager for the client.

[CCM_Messaging_Configuration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_messaging_configuration-client-wmi-class.md)  
Supports messaging-related settings that are exposed to administrators.  

[CCM_Service_BITSConfiguration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_service_bitsconfiguration-client-wmi-class.md)  
Supports Background Intelligent Transfer Service (BITS)-related settings used by CCMEXEC for uploading and downloading message payloads.  

[CCM_Service_EndpointConfiguration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_service_endpointconfiguration-client-wmi-class.md)  
Supports endpoint configuration for the CCMEXEC service.  

[CCM_Service_GlobalConfiguration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_service_globalconfiguration-client-wmi-class.md)  
Supports global configuration for the CCMEXEC service.  

[CCM_Service_HostedClass Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_service_hostedclass-client-wmi-class.md)  
Configures a COM class to be hosted in the CCMEXEC service.  

[CCM_Service_IISConfiguration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_service_iisconfiguration-client-wmi-class.md)  
Supports Internet Information Services (IIS)-related settings used by CCMEXEC for staging and receiving message payloads.  

[CCM_Service_SystemTaskConfiguration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_service_systemtaskconfiguration-client-wmi-class.md)  
Supports system task configuration for the CCMEXEC service.  

[SMS_Authority Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_authority-client-wmi-class.md)  
Represents the client authority that manages the client.  

[SMS_Client Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_client-client-wmi-class.md)  
Represents the client and facilitates manipulation and retrieval of client information.  

[SMS_LocalMP Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_localmp-client-wmi-class.md)  
Represents the local management point.  

[SMS_MPProxyInformation Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_mpproxyinformation-client-wmi-class.md)  
Represents information about a proxy management point.  

[SMS_PendingReRegistrationOnSiteReAssignment Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_pendingreregistrationonsitereassignment-client-wmi-class.md)  
Represents a pending re-registration at the time of site reassignment.  

## Policy Agent Client WMI Classes
The following classes are used to manage policy on client computers and devices.  

[CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md)  
Represents a client policy.  

[CCM_Policy_Action Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_action-client-wmi-class.md)  
Represents settings for a policy action.  

[CCM_Policy_ActionHandlerRegistration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_actionhandlerregistration-client-wmi-class.md)  
Represents an action handler registration for a policy.  

[CCM_Policy_Assignment Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_assignment-client-wmi-class.md)  
Represents a policy assignment.  

[CCM_Policy_Assignment2 Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_assignment2-client-wmi-class.md)  
Represents a policy assignment.  

[CCM_Policy_AuthorityData Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_authoritydata-client-wmi-class.md)  
Stores information about policy from a particular authority.  

[CCM_Policy_Condition Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_condition-client-wmi-class.md)  
Represents a policy condition.  

[CCM_Policy_Config Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_config-client-wmi-class.md)  
Represents a policy configuration used by the Policy Agent that needs to be replicated.  

[CCM_Policy_EmbeddedObject Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_embeddedobject-client-wmi-class.md)  
Represents a policy setting embedded object.  

[CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md)  
Represents a policy expression that evaluates to either `true` or `false`.  

[CCM_Policy_ExpressionHandlerRegistration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expressionhandlerregistration-client-wmi-class.md)  
Describes a registered expression handler for a policy.  

[CCM_Policy_Operator Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_operator-client-wmi-class.md)  
Stores a compound expression that evaluates to either `true` or `false`.  

[CCM_Policy_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_policy-client-wmi-class.md)  
Defines a policy object for a client policy.  

[CCM_Policy_Rule Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_rule-client-wmi-class.md)  
Defines a policy object rule.  

[CCM_PolicyAgent_Configuration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policyagent_configuration-client-wmi-class.md)  
Represents the Policy Agent configuration for a given authority.  

## See Also  
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
