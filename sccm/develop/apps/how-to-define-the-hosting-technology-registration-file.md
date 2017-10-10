---
title: "Define the Hosting Technology Registration File"
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
ms.assetid: 47960cf4-e7dd-4e26-92b7-5774cfc44a1csearchScope: - ConfigMgr SDK
caps.latest.revision: 19
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Define the Hosting Technology Registration File
To define a hosting technology registration file, create an XML file based on the `http://schemas.microsoft.com/SystemCenterConfigurationManager/2009/AppMgmtDigest` schema. Used in the installation process, the registration file registers the custom hosting technology with Configuration Manager.  The hosting technology registration file is required for the installation of the custom hosting technology.  See [Installing the Application Management Extension](../../develop/apps/installing-the-application-management-extension.md) for additional details.  

### To define the hosting technology registration file  

1.  Create a hosting technology registration file.  

     The following example from the RPC sample project demonstrates how to define a hosting technology registration file.  

    ```  
    <AppMgmtDigest xmlns="http://schemas.microsoft.com/SystemCenterConfigurationManager/2009/AppMgmtDigest" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
      <HostingTechnology AuthoringScopeId="GLOBAL" LogicalName="RdpHostingTechnology" HostingId="Rdp" AssemblySuffix="Rdp" Version="1">  
        <Requirements>  
          <Rule xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2009/06/14/Rules" id="Rule_63d22cd6-7f11-4769-8900-9c0ff5c177c5" Severity="None">  
            <Annotation>  
              <DisplayName Text="Operating System" />  
              <Description Text="" />  
            </Annotation>  
            <OperatingSystemExpression>  
              <Operator>OneOf</Operator>  
              <Operands>  
                <RuleExpression RuleId="Windows/All_x86_Windows_XP" />  
                <RuleExpression RuleId="Windows/x86_Windows_XP_Professional_Service_Pack_3" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_Server_2003_Non_R2" />  
                <RuleExpression RuleId="Windows/All_x86_Windows_Server_2003_Non_R2" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_Server_2003_R2" />  
                <RuleExpression RuleId="Windows/All_x86_Windows_Server_2003_R2" />  
                <RuleExpression RuleId="Windows/x64_Windows_Server_2003_R2_original_release_SP1" />  
                <RuleExpression RuleId="Windows/x86_Windows_Server_2003_R2_original_release_SP1" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_XP_Professional" />  
                <RuleExpression RuleId="Windows/x64_Windows_Server_2003_SP2" />  
                <RuleExpression RuleId="Windows/x86_Windows_Server_2003_SP2" />  
                <RuleExpression RuleId="Windows/x64_Windows_XP_Professional_SP2" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_Vista" />  
                <RuleExpression RuleId="Windows/All_x86_Windows_Vista" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_Server_2008" />  
                <RuleExpression RuleId="Windows/All_x86_Windows_Server_2008" />  
                <RuleExpression RuleId="Windows/x64_Windows_Vista_SP1" />  
                <RuleExpression RuleId="Windows/x86_Windows_Vista_SP1" />  
                <RuleExpression RuleId="Windows/x64_Windows_Server_2008_original_release" />  
                <RuleExpression RuleId="Windows/x86_Windows_Server_2008_original_release" />  
                <RuleExpression RuleId="Windows/x64_Windows_Server_2008_SP2" />  
                <RuleExpression RuleId="Windows/x86_Windows_Server_2008_SP2" />  
                <RuleExpression RuleId="Windows/x64_Windows_Vista_SP2" />  
                <RuleExpression RuleId="Windows/x86_Windows_Vista_SP2" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_Server_2008_R2" />  
                <RuleExpression RuleId="Windows/All_x64_Windows_7_Client" />  
                <RuleExpression RuleId="Windows/All_x86_Windows_7_Client" />  
                <RuleExpression RuleId="Windows/x64_Windows_7_Client" />  
                <RuleExpression RuleId="Windows/x86_Windows_7_Client" />  
                <RuleExpression RuleId="Windows/x64_Windows_Server_2008_R2" />  
              </Operands>  
            </OperatingSystemExpression>  
          </Rule>  
        </Requirements>  
      </HostingTechnology>  
    </AppMgmtDigest>  
    ```  

|Attributes|Description|  
|----------------|-----------------|  
|AuthoringScopeID|AuthoringScopeId will always be “GLOBAL��?.|  
|LogicalName|LogicalName must match the name of the SDK class created in the SDK assembly for HostingTechnology.|  
|HostingId|HostingId must match the constant declared and used in the SDK assembly for HostingTechnolgy.|  
|AssemblySuffix|AssemblySuffix must match the filename of the SDK assembly (Microsoft.ConfigurationManagement.ApplicationManagement.< `AssemblySuffix`>.dll).|  
|Version|Version is the version number for the release of the deployment type extension. This version number is used for in-place revisions.|  

|Element|Description|  
|-------------|-----------------|  
|Requirements|The requirements section is based on DCM requirement rules.  The supported platforms for the custom technology must be specified here.|  

## See Also  
 [How to Define the Deployment Technology Registration File](../../develop/apps/how-to-define-the-deployment-technology-registration-file.md)   
 [How to Define the Installer Technology Registration File](../../develop/apps/how-to-define-the-installer-technology-registration-file.md)   
 [Installing the Application Management Extension](../../develop/apps/installing-the-application-management-extension.md)   
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
