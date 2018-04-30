---
title: "Define the UI Extension Assembly"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 77311f19-a9dd-4383-8e21-fa460d45b28c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Define the UI Extension Assembly
The custom wizard assembly is responsible for collecting any data passed in from the Configuration Manager console, and passing it on to the wizard.  The assembly should be named, AdminUI.DeploymentType.\< *AssemblySuffix*>.dll.  

### To define the UI extension assembly  

1.  Below is an example of how the UI extension interfaces with the UI. Review the example in the RDP sample project for complete/specific information on defining the UI Extension Assembly.  

    ```  
    //  
    // Applies the AppManWrapper around PropertyManager to simplify interaction with the AppMgmt SDK and its corresponding WMI classes.   
    //  
    private void BindSdk()  
    {  
        //  
        // Checks if AppManWrapper has been applied to the PropertyManager yet.   
        //  
        AppManWrapper appManWrapper = this.PropertyManager as AppManWrapper;   

        if (appManWrapper == null)   
        {  
            //  
            // Applies the AppManWrapper around the PropertyManager.   
            //  
            this.PropertyManager = appManWrapper = AppManWrapper.WrapExisting(this.PropertyManager, new ApplicationFactory()) as AppManWrapper;   
        }  
        //  

        // Retrieves references to the Application and DeploymentType objects.   
        //  
        this.application = appManWrapper.InnerAppManObject as Application;   
        this.deploymentType = appManWrapper.AppData.ContainsKey(AppDataDeploymentType) ? appManWrapper.AppData[AppDataDeploymentType] as DeploymentType : null;   

        return;   
    }   
    //  
    // Loads the values into the UI.   
    //  
    private void LoadIntoUI()  
    {  
        //  
        // Checks if the Deployment Type has not been created yet.   
        //  
        if (this.deploymentType == null)   
        {  
            //  
            // Sets defaults for the user.   
            //  
            this.ApplyDefaults();  
            this.ApplyFormState();  

            return;   
        }  

        RdpInstaller rdpInstaller = this.deploymentType.Installer as RdpInstaller;   

        //  
        // Checks if content is associated with the installer, which means the RDP is being distributed through the content server.   
        //  
        bool installerHasContentFile = (rdpInstaller.Contents.Count > 0 && rdpInstaller.Contents[0].Files.Count > 0);   

        //  
        // Adjusts the radio buttons according to content settings.   
        //  
        this.distributeThroughContentServerRadioButton.Checked = (installerHasContentFile == true);   
        this.constructOnClientRadioButton.Checked = (installerHasContentFile == false);   

        //  
        // Loads each value into the UI.   
        //  
        this.deploymentTypeNameTextBox.Text = this.deploymentType.Title;   
        this.clientRdpFileTextBox.Text = Path.Combine(rdpInstaller.InstallFolder, rdpInstaller.Filename);   
        this.serverRdpFileTextBox.Text = installerHasContentFile ? Path.Combine(rdpInstaller.Contents[0].Location, rdpInstaller.Contents[0].Files[0].Name) : string.Empty;   
        this.remoteMachineTextBox.Text = rdpInstaller.FullAddress;   
        this.userNameTextBox.Text = rdpInstaller.Username;   
        this.displayWidthTextBox.Text = string.Format(CultureInfo.InvariantCulture, "{0}", rdpInstaller.DesktopWidth);   
        this.displayHeightTextBox.Text = string.Format(CultureInfo.InvariantCulture, "{0}", rdpInstaller.DesktopHeight);   
        this.fullScreenCheckBox.Checked = rdpInstaller.FullScreen;   
        this.audioComboBox.SelectedIndex = (int)rdpInstaller.AudioMode;   
        this.keyboardComboBox.SelectedIndex = (int)rdpInstaller.KeyboardMode;   
        this.redirectPrinterCheckBox.Checked = rdpInstaller.RedirectPrinters;   
        this.redirectSmartCardsCheckBox.Checked = rdpInstaller.RedirectSmartCards;   
        this.remoteProgramCheckBox.Checked = string.IsNullOrEmpty(rdpInstaller.RemoteApplication) == false;   
        this.remoteProgramFileTextBox.Text = Path.GetFileName(rdpInstaller.RemoteApplication);   
        this.remoteStartUpPathTextBox.Text = Path.GetDirectoryName(rdpInstaller.RemoteApplication);   

        //  
        // Adjusts the form according to state.   
        //  
        this.ApplyFormState();  

        return;   
    }  

    //  
     // Saves the values from the UI.   
    //  
    private void SaveFromUI()  
    {  
        //  
        //  In the case of the wizard, the new Deployment Type instance will be available in UserData once the user has navigated from the creation page.   
        //  
        if (this.deploymentType == null &&        this.UserData.ContainsKey(UserDataDeploymentType) == true)   
        {  
            this.deploymentType = this.UserData[UserDataDeploymentType] as DeploymentType;   
        }  

        RdpInstaller rdpInstaller = this.deploymentType.Installer as RdpInstaller;   

        //  
        // Checks if content should be associated with the installer (which means the RDP is being distributed through the content server).   
        //  
        if (this.distributeThroughContentServerRadioButton.Checked == true)   
        {  
            if (rdpInstaller.Contents.Count <= 0)   
            {  
                rdpInstaller.Contents.Add(new Content());  
            }  
            if (rdpInstaller.Contents[0].Files.Count <= 0)   
            {  
                rdpInstaller.Contents[0].Files.Add(new ContentFile());  
            }  

            rdpInstaller.Contents[0].Location = Path.GetDirectoryName(this.serverRdpFileTextBox.Text);   
            rdpInstaller.Contents[0].Files[0].Name = Path.GetFileName(this.serverRdpFileTextBox.Text);   
        }  
        else  
        {  
            rdpInstaller.Contents.Clear();  
        }  

        //  
        // Collects the desktop dimensions.   
        //  
        int desktopWidth = RdpInstaller.DefaultDesktopWidth, desktopHeight = RdpInstaller.DefaultDesktopHeight;   
        int.TryParse(this.displayWidthTextBox.Text, out desktopWidth);   
        int.TryParse(this.displayHeightTextBox.Text, out desktopHeight);   

        //  
        // Saves each value from UI.   
        //    this.deploymentType.Title = this.deploymentTypeNameTextBox.Text;   
        rdpInstaller.InstallFolder = Path.GetDirectoryName(this.clientRdpFileTextBox.Text);   
        rdpInstaller.Filename = Path.GetFileName(this.clientRdpFileTextBox.Text);   
        rdpInstaller.ConstructRdpOnClient = this.constructOnClientRadioButton.Checked;   
        rdpInstaller.FullAddress = this.remoteMachineTextBox.Text;    rdpInstaller.Username = this.userNameTextBox.Text;   
        rdpInstaller.DesktopWidth = desktopWidth;   
        rdpInstaller.DesktopHeight = desktopHeight;   
        rdpInstaller.FullScreen = this.fullScreenCheckBox.Checked;   
        rdpInstaller.AudioMode = (RdpAudioMode)this.audioComboBox.SelectedIndex;   
        rdpInstaller.KeyboardMode = (RdpKeyboardMode)this.keyboardComboBox.SelectedIndex;   
        rdpInstaller.RedirectPrinters = this.redirectPrinterCheckBox.Checked;   
        rdpInstaller.RedirectSmartCards = this.redirectSmartCardsCheckBox.Checked;   
        rdpInstaller.RemoteApplication = this.remoteProgramCheckBox.Checked ? Path.Combine(this.remoteStartUpPathTextBox.Text, this.remoteProgramFileTextBox.Text) : string.Empty;   

        this.SplitFullAddressIntoServerNameAndPort(rdpInstaller);   

        return;   
    }  
    ```  

#### Namespaces  
 Microsoft.ConfigurationManagement.AdminConsole  

 Microsoft.ConfigurationManagement.AdminConsole.AppManFoundation  

 Microsoft.ConfigurationManagement.AdminConsole.CreateDT  

 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.ApplicationManagement.Application  

 Microsoft.ConfigurationManagement.ManagementProvider.ConnectionManagerBase  

 System.Collections.Generic  

 System.ComponentModel  

 System.Diagnostics  

 System.Drawing  

 System.Globalization  

 System.IO  

 System.Linq  

 System.Windows.Forms  

#### Assemblies  
 Microsoft.ConfigurationManagement.ApplicationManagement  

 Microsoft.ConfigurationManagement.DialogFramework  

 Microsoft.ConfigurationManagement  

 Microsoft.ConfigurationManagement.ManagementProvider  

 AdminUI.AppManFoundation  

 AdminUI.CreateDT  

## See Also  
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
