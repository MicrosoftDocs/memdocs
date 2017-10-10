---
title: "How to Create an Application with the Script Deployment Type"
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
ms.assetid: 11ec1d68-c5ee-4822-a519-b92011909d1dsearchScope: - ConfigMgr SDK
caps.latest.revision: 16
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create an Application with the Script Deployment Type
Applications are new to System Center Configuration Manager.  Prior to System Center Configuration Manager, a package was the basic object that was used to install software.  Now, a more flexible and complete model exists for applications in Configuration Manager.  Software based on this new model are referred to as Applications.  Packages still exist in System Center Configuration Manager, but they are defined and behave in much the same manner as packages did in Configuration Manager.  

 The application model defines a standard set of properties and metadata that is used by the system to manage the lifecycle of the application. As applications are modeled, the application itself can be a building block used to help define other applications in the system. For example, .NET Framework can be defined as an application, and then it can be referenced by a parent application as a dependency that must be present or installed before the parent application is installed.  

## To Create an Application with the Script Deployment Type  
 In order to get started with creating an application, the following section defines a simple application and its basic properties.  Assuming that all applications you create are new from the Configuration Manager perspective, then adding a new application into Configuration Manager is relatively straightforward. When applications may already exist, and may have relationships to other applications, either through dependencies or supersedence is more complicated and not covered in the example below.  

 A simple command line program that demonstrates the how to create the model and persist to the database through the SMS Provider is shown below. As a sample, it contains strings that are hard-coded, and should not be considered a real world application for automating application creation. Additionally, there is minimal error handling. However, this example should be enough to get you started.  

### Additional References  
 You can refer to the following posts for additional details about creating applications:  

-   **Saving the World One Line of Code at a Time**  

     [How to Create a Basic App using the Configuration Manager 2012 Beta 2 SDK](http://blogs.msdn.com/b/one_line_of_code_at_a_time/archive/2011/06/14/how-to-create-a-basic-app-using-the-configuration-manager-2012-beta-2-sdk.aspx)  

-   **Adam Meltzer's Configuration Manager Blog**  

     [SDK: How to create a basic application and add a deployment type](http://blogs.msdn.com/b/ameltzer/archive/2012/04/25/sdk-how-to-create-a-basic-application-and-add-a-deployment-type.aspx)  

-   **SDK Sample: AppSupersedence**  

     Demonstrates how to create an application-supersedence relationship between two versions of an application.  

     See [Configuration Manager SDK Samples](../../develop/core/understand/configuration-manager-sdk-samples.md) for more information.  

-   **SDK Sample: DTRequirements**  

     Demonstrates how to create deployment type requirements and add them to a deployment type.  

     See [Configuration Manager SDK Samples](../../develop/core/understand/configuration-manager-sdk-samples.md) for more information.  

##### To Create an Application with the Script Deployment Type  

1.  Initialize the provider connection and ApplicationFactory. (The application factory is a wrapper that makes creating the provider classes a little easier.)  

2.  Create the application and the deployment type.  

3.  Persist the application to the provider.  

 To use this sample, create a new command line C# application and copy and replace the code shown. You’ll need to add references to the 5 assemblies below are all found in the adminconsole\bin directory:  

-   AdminUI.AppManFoundation.dll  

     A wrapper encapsulating Configuration Manager provider functionality for creating applications.  

-   AdminUI.WqlQueryEngine.dll  

     The WqlConnectionManager.  

-   Microsoft.ConfigurationManagement.ApplicationManagement.dll  

     The core application model, used to serialize/deserialize applications.  

-   Microsoft.ConfigurationManagement.ApplicationManagement.MsiInstaller.dll  

     An implementation of the Windows Installer and Script Deployment Types.  

-   Microsoft.ConfigurationManagement.ManagementProvider.dll  

     The Configuration Manager managed WMI interface.  

 After compiling and running the application, the output for the application will show this when it is successful.  

```  
C:\sms\AdminConsole\bin>ApplicationCreator.exe  

Connecting to the SMS Provider on computer [machinename].  
Initializing the ApplicationFactory.Creating application [app].  
Creating Script DeploymentType.  
Initializing the SMS_Application object with the model.  
Saving application, Title: [app], Scope: [ScopeId_D5230FF0-B439-44D9-906E-00A330F2AE06].  
Successfully saved application.  
```  

## Example  
 The following example method shows …  

```c#  
// Sample program for creating an Application with the Script Deployment Type and persisting into the   
// Configuration Manager database.  
//   
// This is example code and does not contain error handling for all cases, nor demonstrate relationships  
// such as dependencies and supersedence, and also does not demonstrate creating requirement rules for a   
// Deployment Type.  

namespace ApplicationCreator  
{  
    using System;  
    using System.IO;  
    using Microsoft.ConfigurationManagement.AdminConsole.AppManFoundation;  
    using Microsoft.ConfigurationManagement.ApplicationManagement;  
    using Microsoft.ConfigurationManagement.ManagementProvider;  
    using Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine;  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Initialize(Environment.MachineName);  
            Application application = CreateApplication("app", "description", System.Globalization.CultureInfo.CurrentCulture.TwoLetterISOLanguageName);  
            application.DeploymentTypes.Add(CreateScriptDt(application.Title, application.Description, "notepad.exe", "return 0;", null));  
            Store(application);  
        }  

        private static AppManWrapper wrapper;  
        private static ApplicationFactory factory;  

        // Initializes the default authoring scope and establishes connection to the SMS Provider.  
        // <param name="siteServerName">A string containing the name of the Configuration Manager site.</param>  

        public static void Initialize(string siteServerName)  
        {  
            Validator.CheckForNull(siteServerName, "siteServerName");  
            Log("Connecting to the SMS Provider on computer [{0}].", siteServerName);  
            // Creates a connection to the SMS Provider.  
            WqlConnectionManager connectionManager = new WqlConnectionManager();  
            connectionManager.Connect(siteServerName);  
            Log("Initializing the ApplicationFactory.");  
            // Initialize application wrapper and factory for creating the SMS Provider application object.  
            factory = new ApplicationFactory();  
            wrapper = AppManWrapper.Create(connectionManager, factory) as AppManWrapper;  
        }  

        // Inserts the provided application to the provided connected Configuration Manager site.  
        // <param name="application">An application object that will be inserted into the Configuration Manager site.</param>  

        public static void Store(Application application)  
        {  
            Validator.CheckForNull(application, "application");  
            Validator.CheckForNull(wrapper, "wrapper");  
            Exception ex = null;  
            try  
            {  
                // Set the application into the provider object.  
                wrapper.InnerAppManObject = application;  
                Log("Initializing the SMS_Application object with the model.");  
                factory.PrepareResultObject(wrapper);  
                Log("Saving application, Title: [{0}], Scope: [{1}].", application.Title, application.Scope);  
                // Save to the database.  
                wrapper.InnerResultObject.Put();  
            }  
            catch (SmsException exception)  
            {  
                ex = exception;  
            }  
            catch (Exception exception)  
            {  
                ex = exception;  
            }  
            if (ex != null)  
            {  
                Log("ERROR saving application [{0}].", ex.Message);  
                Log(ex);  
            }  
            else  
            {  
                Log("Successfully saved application.");  
            }  
        }  

        // Creates an Application object.  
        // <param name="title">The title of the application that will be visible in the admin console and in the Software Center and Portal.</param>  
        // <param name="description">The description for the application.</param>  
        // <param name="language">The language of the resources supplied.</param>  

        public static Application CreateApplication(string title, string description, string language)  
        {  
            Validator.CheckForNull(title, "title");  
            Validator.CheckForNull(language, "language");  
            Log("Creating application [{0}].", title);  
            Application app = new Application { Title = title };  
            app.DisplayInfo.DefaultLanguage = language;  
             app.DisplayInfo.Add(new AppDisplayInfo { Title = title, Description = description, Language = language });  
            return app;  
        }  

        // Creates a Deployment Type with a Script Installer.  
        // <param name="title">A string containing the title for the Deployment Type (required).</param>  
        // <param name="description"> A string containing the description for the Deployment Type (optional).</param>  
        // <param name="installCommandLine">A string containing the installation command line for the installer (required).</param>  
        // <param name="detectionScript">A string containing the script for detection, this would most likely be separated out.  
        // to a different method to support creating different detection method types such as Windows Installer, EHD, and script. Additionally, in the case  
        // of script, the more likely scenario would be to load the script from a file, read the file, and then set the value.</param>  
        // <param name="contentFolder">The folder that will contain the set of files that will represent the content for this Deployment Type. Validation  
        // should verify that this is a UNC path, otherwise the Configuration Manager system will fail to create the content package correctly.</param>  
        // <returns>A deployment type object.</returns>  

        public static DeploymentType CreateScriptDt(string title, string description, string installCommandLine, string detectionScript, string contentFolder)  
        {  
            Validator.CheckForNull(installCommandLine, "installCommandLine");  
            Validator.CheckForNull(title, "title");  
            Validator.CheckForNull(detectionScript, "detectionScript");  
            Log("Creating Script DeploymentType.");  
            ScriptInstaller installer = new ScriptInstaller();  
            installer.InstallCommandLine = installCommandLine;  
            installer.DetectionScript = new Script { Text = detectionScript, Language = ScriptLanguage.JavaScript.ToString() };  
            // Only add content if specified and exists.  
            if (Directory.Exists(contentFolder) == true)  
            {  
                Content content = ContentImporter.CreateContentFromFolder(contentFolder);  
                if (content != null)  
                {  
                    installer.Contents.Add(content);  
                }  
            }  
            DeploymentType dt = new DeploymentType(installer, ScriptInstaller.TechnologyId, NativeHostingTechnology.TechnologyId);  
            dt.Title = title;  
            return dt;  
        }  

        public static void Log(Exception exception)  
        {  
            Log("ERROR: [{0}] ", exception.Message);  
            Log("Stack: [{0}]", exception.StackTrace);  
            if (exception.InnerException != null)  
            {  
                Log(exception.InnerException);  
            }  
        }  

        public static void Log(string message, params object[] args)  
        {  
            Console.WriteLine(message, args);  
        }  
    }  
}  

```  

### Namespaces  
 System  

 System.IO  

 Microsoft.ConfigurationManagement.AdminConsole.AppManFoundation  

 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 AdminUI.AppManFoundation.dll  

 AdminUI.WqlQueryEngine.dll  

 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

 Microsoft.ConfigurationManagement.ApplicationManagement.MsiInstaller.dll  

 Microsoft.ConfigurationManagementProvider.dll  

 AdminUI.DcmObjectWrapper.dll  

 DcmObjectModel.dll  

 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Configuration Manager Application Management](../../develop/apps/application-management.md)   
 [SMS_Collection Server WMI Class](../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)
