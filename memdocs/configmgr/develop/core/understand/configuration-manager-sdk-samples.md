---
title: SDK samples
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6f43a577-e1dc-46d8-a22a-50fb24199583
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# SDK samples

The Configuration Manager software development kit (SDK) ships with the following sample projects. Each sample has a readme file that explains how the sample works.  

## Console

The following sample is in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Admin UI` folder.  

|Sample|Description|  
|------------|-----------------|  
|Custom Task Sequence Action|Visual C# Project that shows how to define and edit a custom task sequence action.|  
|Dialog Prototype|Contains the sample code for creating a new dialog using the Configuration Manager Console Extensions and the Managed Provider interfaces.|  
|Extensions|Contains the sample extension XML files for adding actions, dialogs, property pages, nodes.|  

## Application approval workflow

The following solution is in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Solutions\Applications Approval Workflow` folder.  

|Solution|Description|  
|--------------|-----------------|  
|Applications Approval Workflow|This solution accelerator takes an application request submitted through the Configuration Manager application catalog and transforms it into a System Center 2012 Service Manager service request, allowing flexible approval lists and activities.<br /><br /> The Application Approval Workflow (AAW) extends your application approval process. End users can easily request applications on-demand directly through the Configuration Manager application catalog or via redirection from the Service Manager Self-Service Portal. Application requests requiring approval are routed to Service Manager where custom approver lists and activities can be configured based on user and application properties.<br /><br /> AAW uses System Center 2012 Orchestrator between Configuration Manager and Service Manager to sync Configuration Manager applications, leverage Service Manager workflows, and post the approval status back to Configuration Manager. Wizards were created in Service Manager to configure custom service request template-matching criteria. User and application properties received in the approval request from Configuration Manager are used to select a service request template containing an approver list and activities that best fit your business process.<br /><br /> Key features:<br /><br /> 1.  Sync Configuration Manager applications data into the Service Manager database.<br />2.  Monitor and transport Configuration Manager application catalog requests requiring approval to Service Manager and open a service request.<br />3.  Return the completed approval workflow status to Configuration Manager for handling.<br />4.  Allow administrators to define and maintain application selection criteria for specific applications or application groups and specific users or user groups.<br />5.  Track service application requests and view application catalog contents in Service Manager.|  

## Application management

The following samples are in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\AppManagement` folder.  

|Sample|Description|  
|------------|-----------------|  
|AppSupersedence|Demonstrates how to create an application-supersedence relationship between two versions of an application. In this sample, Adobe Reader 9 and Adobe Reader X are used as examples. It is assumed that both the Adobe Reader 9 and Adobe Reader X application models have been imported from the Application Model Kit.|  
|DTRequirements|Demonstrates how to create deployment type requirements and add them to a deployment type.|  

## Application management extension

The following sample is in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Rdp Deployment Technology\Code Sample` folder.  

> [!IMPORTANT]
> The sample contains an error in the `RdpTechnology.AdminConsole` project. When creating the resource manager instance, the code incorrectly references `RdpTechnoloy.AdminConsole.Properties.Resources`. This incorrect reference causes an exception when running the Create Deployment Type Wizard. To fix the problem, change the reference to `Microsoft.RdpTechnoloy.AdminConsole.Properties.Resources`.

|Sample|Description|  
|------------|-----------------|  
|AppMan Extension|Provides several projects that implement the major elements of a custom deployment type for Remote Desktop Protocol (\*.rdp) files.<br /><br /> The Code Sample\AppMan directory contains the following sample code:<br /><br /> -   **\Handler directory**<br />     Contains the sample code for creating a client-side handler. The client-side handler implements a public COM interface and methods (InstallApp, UninstallApp and DiscoveryApp). The methods will be called by the Configuration Manager client framework. However, the actual functionality of the methods is defined by the client-side handler developer.  This directory also contains a custom synclet MOF file, which creates instances of the CCM_AppHandlers and CCM_HandlerSynclet classes. Once compiled into WMI on the client, the new CCM_AppHandlers class instance identifies the custom client-side handler, while the new instances of the CCM_HandlerSynclet class store detect, install and uninstall property values.<br />-   **\SDK directory**<br />     Contains sample code for creating a custom SDK assembly. The custom SDK assembly contains an interface implementation of both the Hosting Technology and Installer Technology. This directory also contains the deployment technology, hosting technology and installer technology registration files (\*.XML) for the custom technology.<br />-   **\UX directory**<br />     Contains sample code for creating a UX assembly, custom property sheets and wizards. The custom UX assembly is responsible for collecting any data passed in from the Configuration Manager console and passing it on to the wizard. This directory also contains the necessary console extension files (*.XML) to define the create application wizard, the create deployment type wizard and the create deployment type property page.|  

## Application model

The following sample is in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Application Model` folder.  

|Sample|Description|  
|------------|-----------------|  
|Application Model Kit|A set of exported applications (.ZIP file) that demonstrate the use of various features of the application model based applications.  The corresponding .DOCX file contains an explanation of each application modeled in the kit.|  

## Client messaging SDK

The following sample is in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Client Messaging SDK` folder.  

|Sample|Description|  
|------------|-----------------|  
|Configuration Manager client messaging SDK|This SDK is an object model and transport for communicating with Configuration Manager site server roles such as the management point for client operations such as registering clients, retrieving policy assignments and bodies, sending inventory, and state/status messages.<br /><br /> The Configuration Manager client messaging SDK contains the following:<br /><br /> -   **Microsoft.ConfigurationManager.Messaging.chm**<br />     A CHM file containing the documentation for the client messaging SDK.<br />-   **Sample.cs**<br />     Sample code for using the client messaging SDK.|  

> [!IMPORTANT]
> The `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Redistributables` folder contains the **Microsoft.ConfigurationManager.Messaging.dll**, a .NET assembly encapsulating the client messaging SDK.  

## Compliance settings

The following samples are in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\DesiredConfigurationManagement` folder.  

> [!IMPORTANT]
> These samples require the .NET Framework 3.5.  

|Sample|Description|  
|------------|-----------------|  
|DcmAssignBaseline|Demonstrates how to assign a configuration baseline to a collection by using an assignment object.|  
|DcmImport|Demonstrates how to create an [SMS_ConfigurationItem Server WMI Class](../../reference/compliance/sms_configurationitem-server-wmi-class.md) from an existing XML definition of a configuration item.|  
|Schema|The XML digest schema file and digest authoring document for Compliance Settings.|  

## Header files

The following header files are in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Includes` folder.  

|Header File|Description|  
|-----------------|-----------------|  
|smscstat.h<br /><br /> ssperrcode.h|Contains header information for creating status messages.<br /><br /> Contains error codes and macros that are used to evaluate an error condition that is returned from the SMS Provider.|  

## Management point interface  

The following files are in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Management Point API` folder.  

|Files|Description|  
|-----------|-----------------|  
|smsmsgapi.h<br /><br /> smsmsgapi_i.c|C++ Source files necessary for compiling the management point API into custom applications.|  

> [!IMPORTANT]
> The [client messaging SDK](#client-messaging-sdk) may be a better option for most users.  
>
> For more information, see the following articles:
>
> - [Management point interface](https://go.microsoft.com/fwlink/?LinkId=255152)
> - [About management point interface messages](https://go.microsoft.com/fwlink/?LinkId=255153)

## OS deployment

The following samples are in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\OperatingSystemDeployment` folder.  

|Sample|Description|  
|------------|-----------------|  
|CustomTaskSequenceAction|Shows how to specify a sample custom task sequence action. Adding a custom action requires a MOF file that defines the action WMI object and properties, and an associated set of controls used for the action's property and option pages in the Task Sequence Editor.|  
|TSEditor|Demonstrates how to work with the task sequencing objects in Configuration Manager.|  
|UnknownSystem|Demonstrates how to create a boot media that can create a computer record for a system unknown to Configuration Manager, add it to a collection, and set machine and Task Sequence variables.|  

## Software updates

The following samples are in the `%Program Files%\Microsoft System Center 2012 R2 Configuration Manager SDK\Samples\Software Updates Management` folder.  

|Sample|Description|  
|------------|-----------------|  
|Gadget|Sidebar gadget that tracks the compliance status of all deployed software updates on a specified site.|  
|SUMCreateGroup|An example command-line utility that creates a software update group.|  
|SUMAssignGroup|An example command-line utility that assigns a software update group to a collection.|  
