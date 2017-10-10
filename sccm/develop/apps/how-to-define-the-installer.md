---
title: "How to Define the Installer"
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
ms.assetid: f18ca88b-a1e2-46d0-8740-00d36dc09e0esearchScope: - ConfigMgr SDK
caps.latest.revision: 24
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Define the Installer
To define the application management deployment technology installer, use an instance of the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer` class. The new class instance will define the properties and methods used on the client to actually install the application.  

 The Installer class has three abstract methods (CreateDetectionAction, CreateInstallAction, CreateUninstallAction) allowing the Installer to specify the Action objects that will be used on the client for detection, installation and uninstall.  

 Corresponding client-side implementation is required for the end to end Installer to work correctly.  The client-side implementation is covered in [How to Define the Client-side Handler](../../develop/apps/how-to-define-the-client-side-handler.md).  

 In the Remote Desktop Protocol (RDP) sample project, a new installer is required for Remote Desktop Protocol (RDP).  Installation support for RDP is not built-in to Configuration Manager, so a custom installer is required.  

 Basic Overview of Defining a Custom Installer  

1.  Create a custom instance of the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer` class.  

2.  Override the Technology property and return the TechnologyId string specific to the technology.  

3.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.CreateDetectAction` method and create a custom detection method specific to the technology.  

4.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.CreateInstallAction` method and create a custom installation method specific to the technology.  

5.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.CreateUninstallAction` method and create a custom uninstallation method specific to the technology.  

6.  Create the general properties required to install the custom technology on the client.  

### To define a custom installer  

1.  Create an instance of the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer` class using the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer` constructor.  

     The following example from the RDP sample project demonstrates how to create the custom class.  

    ```  
    //   Installer class for a specific technology. The Installer class defines properties and methods used on the client to actually install the application.   
    public class RdpInstaller : Installer  
    ```  

2.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.Technology` property to return the correct value for the custom installer technology.  

     The following example from the RDP sample project demonstrates how to override the Technology property.  

    ```  
    // RDP Installer Technology string  
    public override string Technology  
    {  
        get  
        {  
           return Common.TechnologyId;   
        }  
    }  
    ```  

     In the RDP sample project, the string parameter for InstallerTechnologyId is defined as a constant in the Common class of the project.  

    ```  
    //   Internal ID of the technology.   
          public const string TechnologyId = "Rdp";  
    ```  

3.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.CreateDetectAction` method and create a custom action specific to the custom technology.  

     The following example from the RDP sample project demonstrates how to override the CreateDetectAction method.  

    ```  
    //   Creates an Action used for detection. On the client, this sequence is used to validate if the application is installed.   
    public override Action CreateDetectAction()  
    {  
        Action detectionAction = new Action { Provider = Common.TechnologyId };  

        detectionAction.Arguments.Add(new Argument("Filename", typeof(string), this.Filename));   
        detectionAction.Arguments.Add(new Argument("InstallFolder", typeof(string), this.InstallFolder));   
        detectionAction.Arguments.Add(new Argument("FullAddress", typeof(string), this.FullAddress));   
        detectionAction.Arguments.Add(new Argument("RemoteApplication", typeof(string), this.RemoteApplication));   
        detectionAction.Arguments.Add(new Argument("RemoteApplicationMode", typeof(bool), false));   

        return detectionAction;   
    }  
    ```  

4.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.CreateInstallAction` method and create a custom action specific to the custom technology.  

     The following example from the RDP sample project demonstrates how to override the CreateInstallAction method.  

    ```  
    //   Creates an Action used for installation. On the client, this sequence defines the properties needed to install the application.   
    public override Action CreateInstallAction()  
    {  
        Action installationAction = new Action { Provider = Common.TechnologyId };  
        installationAction.Arguments.Add(new Argument("Filename", typeof(string), this.Filename));   
        installationAction.Arguments.Add(new Argument("InstallFolder", typeof(string), this.InstallFolder));   
        installationAction.Arguments.Add(new Argument("FullScreen", typeof(int), (true == this.fullScreen) ? 1 : 0));   
        installationAction.Arguments.Add(new Argument("DesktopWidth", typeof(int), this.desktopWidth));   
        installationAction.Arguments.Add(new Argument("DesktopHeight", typeof(int), this.desktopHeight));   
        installationAction.Arguments.Add(new Argument("AudioMode", typeof(int), (int)this.AudioMode));   
        installationAction.Arguments.Add(new Argument("FullAddress", typeof(string), this.FullAddress));   
        installationAction.Arguments.Add(new Argument("RemoteServerName", typeof(string), this.RemoteServerName));   
        installationAction.Arguments.Add(new Argument("RemoteServerPort", typeof(int), this.RemoteServerPort));   
        installationAction.Arguments.Add(new Argument("RemoteApplication", typeof(string), this.RemoteApplication));   
        installationAction.Arguments.Add(new Argument("RemoteApplicationMode", typeof(bool), false));   
        installationAction.Arguments.Add(new Argument("ConstructRdpOnClient", typeof(bool), this.ConstructRdpOnClient));   
        installationAction.Arguments.Add(new Argument("KeyboardMode", typeof(int), (int)this.KeyboardMode));   
        installationAction.Arguments.Add(new Argument("RedirectPrinters", typeof(int), (true == this.RedirectPrinters) ? 1 : 0));   
        installationAction.Arguments.Add(new Argument("RedirectSmartCards", typeof(int), (true == this.RedirectSmartCards) ? 1 : 0));   
        installationAction.Arguments.Add(new Argument("Username", typeof(string), this.Username));   
        //  Adds any references to content to the action.   
        if (this.ConstructRdpOnClient == false && this.Contents.Count > 0)   
        {  
            foreach (Content content in this.Contents)   
            {  
                 installationAction.Contents.Add(new ContentRef(content));   
            }  
        }  
        return installationAction;   
    }  
    ```  

5.  Override the `Microsoft.ConfigurationManagement.ApplicationManagement.Installer.CreateUninstallAction` method and create a custom action specific to the custom technology.  

     The following example from the RDP sample project demonstrates how to override the CreateUninstallAction method.  

    ```  
    public override Action CreateUninstallAction()  
    {  
        Action uninstallAction = new Action { Provider = Common.TechnologyId };  
        uninstallAction.Arguments.Add(new Argument("Filename", typeof(string), this.Filename));   
        uninstallAction.Arguments.Add(new Argument("InstallFolder", typeof(string), this.InstallFolder));   
        return uninstallAction;   
    }  
    ```  

6.  Create addition properties and methods used on the client to install the custom technology.  

     The following example from the RDP sample project demonstrates the creation of properties and methods used on the client to install the RDP application.  

    ```  
    // Default height for the RDP window.  
    public const int DefaultDesktopHeight = 768;   
    // Default width for the RDP window  
    public const int DefaultDesktopWidth = 1024;   
    // Default storage location for RDP files created using this Installer  
    public const string DefaultInstallFolder = @"%USERPROFILE%\Desktop\Remote Desktop Connections";  
    private RdpAudioMode audioMode;   
    private bool constructRdpOnClient;private int desktopHeight;   
    private int desktopWidth;   
    private bool fullScreen;   
    private string installFolder;   
    private RdpKeyboardMode keyboardMode;   
    private string filename;   
    private bool redirectPrinters;   
    private bool redirectSmartCards;   
    private string remoteApplication;   
    private string fullAddress;   
    private string remoteServerName;   
    private ushort remoteServerPort;   
    private string username;   
    // Audio mode for the RDP connection. The default is BringToComputer.   
    public RdpAudioMode AudioMode  
    {  
        get  
        {  
            return audioMode;   
        }  
        set   
        {  
            SetProp("AudioMode", ref audioMode, value);   
        }  
    }  
    // If true, the RDP file will be constructed locally on the client. If false, the RDP file will live on the server and will be downloaded as content.   
    [Mandatory]   
    public bool ConstructRdpOnClient  
    {  
        get  
        {  
            return constructRdpOnClient;   
        }  
        set  
        {  
            SetProp("ConstructRdpOnClient", ref constructRdpOnClient, value);   
        }  
    }  
    // Height of the remote desktop window. This setting is ignored if FullScreen = true.   
    [Default(DefaultDesktopHeight)]   
    public int DesktopHeight  
    {  
        get  
        {  
            return desktopHeight;   
        }  
        set  
        {  
            SetProp("DesktopHeight", ref desktopHeight, value);   
        }  
    }   
    // Width of the remote desktop window. This setting is ignored if FullScreen = true.   
    [Default(DefaultDesktopWidth)]   
    public int DesktopWidth  
    {  
        get  
        {  
            return desktopWidth;   
        }  
        set  
        {  
            SetProp("DesktopWidth", ref desktopWidth, value);   
        }  
    }  
    // If true, full screen window will be used.   
    public bool FullScreen  
    {  
        get  
        {  
            return fullScreen;   
        }  
        set  
        {  
            SetProp("FullScreen", ref fullScreen, value);   
        }  
    }  
    // Directory on the client where the RDP file will be stored. This is part of Detection.   
    [Mandatory][Default(DefaultInstallFolder)]   
    public string InstallFolder  
    {  
        get  
        {  
            return installFolder;   
        }  
        set  
        {  
            SetProp("InstallFolder", ref installFolder, value);   
        }  
    }  
    // Keyboard mode to use for the RDP session. Default is <see cref = "RdpKeyboardMode.FullScreenOnly" />  
    [Default(RdpKeyboardMode.FullScreenOnly)]   
    public RdpKeyboardMode KeyboardMode  
    {  
        get  
        {  
            return keyboardMode;   
        }  
        set  
        {  
            SetProp("KeyboardMode", ref keyboardMode, value);   
        }  
    }  
    // Name of the RDP profile. This is part of Detection.   
    [Mandatory]public string Filename  
    {  
        get  
        {  
            return filename;   
        }  
        set  
        {  
            SetProp("Filename", ref filename, value);   
        }  
    }  
    // If true, local printers will be redirected to the remote computer. Default is true.   
    [Default(true)]public bool RedirectPrinters  
    {  
        get  
        {  
            return redirectPrinters;   
        }  
        set  
        {  
            SetProp("RedirectPrinters", ref redirectPrinters, value);   
        }  
    }  
    // If true, local smart cards will be redirected to the remote computer. Default is true.   
    [Default(true)]   
    public bool RedirectSmartCards  
    {  
        get  
        {  
            return redirectSmartCards;   
        }  
        set  
        {  
            SetProp("RedirectSmartCards", ref redirectSmartCards, value);   
        }  
    }  
    // Remote application to run. Setting to %WINDIR%\system32\notepad.exe for example will remote only the notepad.exe application. If unspecified, remote shell will be used. Default is unspecified.   
    public string RemoteApplication  
    {  
        get  
        {  
            return remoteApplication;   
        }  
        set  
        {  
            SetProp("RemoteApplication", ref remoteApplication, value);   
        }  
    }  
    // Remote server name for the RDP connection.   
    [MaxLength(254)]   
    public string RemoteServerName  
    {  
        get  
        {  
            return remoteServerName;   
        }  
        set  
        {  
            SetProp("RemoteServerName", ref remoteServerName, value);   
        }  
    }  
    // Remote server port for the RDP connection. Default is 3389.   
    public string FullAddress  
    {  
        get  
        {  
            return fullAddress;   
        }  
        set  
        {  
            SetProp("FullAddress", ref fullAddress, value);   
        }  
    }  
    //   Remote server port for the RDP connection. Default is 3389.   
    [Default((ushort)3389)][Range(Min = (ushort)1, Max = (ushort)65534)]   
    public ushort RemoteServerPort  
    {  
        get  
        {  
            return remoteServerPort;   
        }  
        set  
        {  
            SetProp("RemoteServerPort", ref remoteServerPort, value);   
        }  
    }  
    // RDP Installer Technology string  
    public override string Technology  
    {  
        get  
        {  
            return Common.TechnologyId;   
        }  
    }  
    //   Username to use for the remote desktop connection.   
    public string Username  
    {  
        get  
        {  
            return username;   
        }  
        set  
        {   
            SetProp("Username", ref username, value);   
        }  
    }  
    ```  

#### Namespaces  
 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement.Serialization  

#### Assemblies  
 Microsoft.ConfigurationManagement.ApplicationManagement.dll  

## See Also  
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
