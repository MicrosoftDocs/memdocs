---
title: "How to Define the Client-side Handler"
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
ms.assetid: 259af33a-af65-4f80-b458-0414bba6f164searchScope: - ConfigMgr SDK
caps.latest.revision: 24
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Define the Client-side Handler
The custom client-side handler needs to implement a public COM interface and methods. The below methods will be called by the Configuration Manager client framework.  

 The client extension maps closely to the Installer object, defined as part of the DeploymentType. Property values are stored in WMI and the public COM methods in the client-side handler map to detection, installation and uninstallation.  

> [!IMPORTANT]
>  The COM object’s globally unique identifier needs to be registered in WMI; see the topic [How to Define the AppSynclet MOF File](../../develop/apps/how-to-define-the-appsynclet-mof-file.md).  

 A complete example of implementing the public COM interface and methods is provided for reference. Below are examples of key methods.  

1.  InstallApp Method  

2.  UninstallApp Method  

3.  DiscoverApp Method  

### To define a custom client-side handler  

1.  In the client-side handler, create an instance of the InstallApp method class. This method will be called by client framework.  

     The following example from the RDP sample project demonstrates how to define an InstallApp method.  

    ```  
    //***********************************************************************  
    HRESULT CRdpHandler::InstallApp  
    (  
        __in  HANDLE                hUserToken,   
        __in  IWbemClassObject  *   pHandlerSynclet,   
        __in  LPCWSTR               szLocalContentPath  
    )   
    {  
        CComPtr<IWbemClassObject>         spHandlerSynclet;   
        RdpInstallationParam rdpInstallationParam;   
        wstring sContentPath;   
        wstring sSourceFileName;   
        wstring sDestFileName;   
        wstring sInstallFolder;   
        HRESULT hrResult = S_OK;   
        assert(pHandlerSynclet!=NULL);   
        sContentPath=szLocalContentPath;   
        spHandlerSynclet=pHandlerSynclet;   

        //Read synclet  
        hrResult = GetInstallationParamFromSynclet(spHandlerSynclet,rdpInstallationParam);   
        if(FAILED(hrResult)) {return hrResult;}   

        hrResult = ExpandSystemEnvironmentStrings(hUserToken,rdpInstallationParam.InstallFolder.c_str(),sInstallFolder);   
        if(FAILED(hrResult)) {return hrResult;}   

        if (!IsDirectoryExists(sInstallFolder.c_str()))  
        {  
            hrResult = RecursiveCreatePath(sInstallFolder.c_str(),NULL);   
            if(FAILED(hrResult)) {return hrResult;}   
        }  
        sDestFileName = sInstallFolder + L"\\" + rdpInstallationParam.Filename;   
        if (rdpInstallationParam.ConstructRdpOnClient)   
        {  
            hrResult = ConstructRdpFile(sDestFileName,rdpInstallationParam);   
        }  
        else  
        {  
            sSourceFileName = sContentPath + L"\\" + rdpInstallationParam.ContentFilename;   

            //Check if the specific RDP file exists in file system  
            if(!IsFileExist( sSourceFileName.c_str()))  
            {  
                return HRESULT_FROM_WIN32( ERROR_FILE_NOT_FOUND);   
            }  
            if(CopyFile(sSourceFileName.c_str(),sDestFileName.c_str(),false)==0)   
            {  
                hrResult = HRESULT_FROM_WIN32(GetLastError());  
            }  
        }  
            return hrResult;   
    }  
    ```  

2.  In the client-side handler, create an instance of the UninstallApp method class. This method will be called by the client framework.  

     The following example from the RDP sample project demonstrates how to define an UninstallApp method.  

    ```  
    //***********************************************************************  
    //  
    //  CRdpHandler::UninstallApp  
    //  
    //  Purpose: Delete an Rdp file per the uninstalation synclet.   
    //  
    //  Parameters:   
    //  
    //  Return values:   
    //      S_OK - Success: Success  
    //      All other return values indicate failure.   
    //  
    //**********************************************************************  
    HRESULT CRdpHandler::UninstallApp  
    (  
        __in  HANDLE                hUserToken,   
        __in  IWbemClassObject  *   pHandlerSynclet  
    )   
    {  
        CComPtr<IWbemClassObject>         spHandlerSynclet;   
        RdpUninstallationParam rdpUninstallationParam;   
        wstring  sRdpFileFullPath;   
        HRESULT hrResult = S_OK;   

        assert(pHandlerSynclet!=NULL);   

        spHandlerSynclet = pHandlerSynclet;   
        hrResult = GetUninstallationParamFromSynclet(spHandlerSynclet,rdpUninstallationParam);   
        if(FAILED(hrResult)) {return hrResult;}   

        wstring sInstallFolder = rdpUninstallationParam.InstallFolder;   

        hrResult = ExpandSystemEnvironmentStrings(hUserToken,rdpUninstallationParam.InstallFolder.c_str(),sInstallFolder);    if(FAILED(hrResult)) {return hrResult; }   

        sRdpFileFullPath = sInstallFolder + L"\\" + rdpUninstallationParam.Filename;   

        if(IsFileExist(sRdpFileFullPath.c_str()))  
        {  
            if(DeleteFile(sRdpFileFullPath.c_str())==0)   
            {  
                return HRESULT_FROM_WIN32(GetLastError());  
            }  
        }  
        return hrResult;   
    }  
    ```  

3.  In the client-side handler, create an instance of the DiscoverApp method class. This method will be called by client framework.  

     The following example from the RDP sample project demonstrates how to define a DiscoverApp method.  

    ```  
    //***********************************************************************  
    //  
    //  CRdpHandler::DiscoverApp  
    //  
    //  Purpose: check if an Rdp file is installed per detect synclet  
    //  
    //  Parameters:   
    //      __in HANDLE hUserToken: the user token. If it is null, the action is for computer. If it is not NULL, the action is for the user  
    //      __in  LPCWSTR                   szDeploymentTypeId: the id of the deployment type.   
    //      __in  DWORD                     dwDeploymentTypeRevision: The revision of the deployment type  
    //      __out AppDeploymentTypeData *   pDetectResult: The detection result  
    //  
    //  Return values:   
    //      S_OK - Success:   
    //      All other return values indicate failure.   
    //  
    //**********************************************************************  
    STDMETHODIMP CRdpHandler::DiscoverApp  
    (  
        __in  HANDLE                    hUserToken,   
        __in  LPCWSTR                   szDeploymentTypeId,   
        __in  DWORD                     dwDeploymentTypeRevision,   
        __out AppDeploymentTypeData *   pDetectResult  
    )   
    {  
        CComPtr<IWbemClassObject>         spHandlerSynclet;   
        CString              sTargetedSyncletPath;   
        RdpDiscoverParam    rdpDiscoverParam;   
        AppDetectState      eDetectState;   
        HRESULT hrResult = S_OK;   

        assert(pDetectResult!=NULL);   

        // Initial return  
        ZeroMemory(pDetectResult, sizeof(AppDeploymentTypeData));   

        // Load the synclet  
        sTargetedSyncletPath.Format(L"Rdp_Detect_Synclet.ActionType=\"Detect\",AppDeliveryTypeId=\"%s\",Revision=%d", szDeploymentTypeId, dwDeploymentTypeRevision);   
        BSTR bsTargetedSyncletPath = sTargetedSyncletPath.AllocSysString();  
        hrResult = m_pSvc->GetObject(bsTargetedSyncletPath,0, NULL,&spHandlerSynclet,NULL);   
        ::SysFreeString(bsTargetedSyncletPath);   

        if(FAILED(hrResult)) {return hrResult;}   

        // Populate information from synclet to discovery param.   
        hrResult = GetDiscoverParamFromSynclet(spHandlerSynclet,rdpDiscoverParam);   

        if(FAILED(hrResult)) {return hrResult;}   

        // Discover it  
        hrResult = DiscoverIndividualApp(  
                    hUserToken,   
                    rdpDiscoverParam,   
                    eDetectState);   

        if(FAILED(hrResult)) {return hrResult;}   

        // Return result  
        if (appDetectInstalled == eDetectState)   
        {  
            hrResult = AllocInitDetectData(pDetectResult, 1);   
            if(FAILED(hrResult)) {return hrResult;}   

            hrResult = MarkDetectItem(  
                        pDetectResult->pData,   
                        rdpDiscoverParam.AppDeliveryTypeId,   
                        dwDeploymentTypeRevision,   
                        S_OK);   
            if(FAILED(hrResult)) {return hrResult;}   
        }  
        return hrResult;   
    }  
    ```  

## See Also  
 [Scenario: Extending Application Management](../../develop/apps/scenario--extending-application-management.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
