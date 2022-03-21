---
title: "Compliance Settings Client Interfaces"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5b566a81-4d1b-4d19-94cb-0fb6589cf76c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Compliance Settings (DCM) Client Interfaces
In Configuration Manager, the desired configuration management COM automation classes and related types are used by client applications to manage configuration items on the client computer. They concern client-side behavior only and are called externally by the Desired Configuration Management Agent, which is enabled by default on the client computer. For more information about the agent, see [Enable or disable the compliance settings agent](../../../../compliance/how-to-enable-or-disable-the-compliance-settings--dcm--agent.md).  

 Before the Desired Configuration Management Client Agent can call the desired configuration management client COM automation objects in your application, Configuration Manager must send a policy to the client computers for the site. The policy requests desired configuration management components to be enabled. The Desired Configuration Management Client Agent properties are site-wide client settings.  

 When the policy is received, the Desired Configuration Management Agent can call the COM automation objects in the client application to handle configuration items as needed. For example, the agent calls an [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md) object to access and query baseline configuration items.  

 For more information about developing applications by using the desired configuration management client COM automation classes, see [Configuration Manager Development Environment](../../../../../develop/core/reqs/about-configuration-manager-sdk-requirements.md).  

|Term|Definition|  
|----------|----------------|  
|[ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)|Represents the properties of a baseline configuration item in a Desired Configuration Management Agent job in the client data store.|  
|[IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)|Represents the callback for the Desired Configuration Management Agent.|  
|[IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)|Represents the Desired Configuration Management SDK and defines methods that are used to handle baseline configuration items.|  
|[CIDetectInfo Structure](../../../../../develop/reference/core/clients/client-classes/cidetectinfo-structure.md)|Contains information for baseline configuration item detection.|  
|[CIPackageInfo Structure](../../../../../develop/reference/core/clients/client-classes/cipackageinfo-structure.md)|Contains package information for a configuration item.|  
|[CIEvalState Enumeration](../../../../../develop/reference/core/clients/client-classes/cievalstate-enumeration.md)|Defines configuration item evaluation states.|  
|[CIJobState Enumeration](../../../../../develop/reference/core/clients/client-classes/cijobstate-enumeration.md)|Defines configuration item agent job states.|  
|[CIPresence Enumeration](../../../../../develop/reference/core/clients/client-classes/cipresence-enumeration.md)|Defines configuration item presence types used in the discovery process.|  
