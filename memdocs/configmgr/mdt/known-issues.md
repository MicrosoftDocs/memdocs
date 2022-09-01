---
title: MDT known issues
description: Current limitations with the Microsoft Deployment Toolkit (MDT).
ms.date: 03/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-mdt
ms.topic: article
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# Microsoft Deployment Toolkit known issues

This article provides details of any current known issues and limitations with the Microsoft Deployment Toolkit (MDT). It assumes familiarity with MDT version concepts, features, and capabilities.

## HTA applications report Script error after upgrading to ADK for Windows 11, version 22H2
After you updated your MDT boot image to [ADK for Windows 11, version 22H2](/windows-hardware/get-started/adk-install), HTA applications stop working and a message box is displayed: Script Error - An error has occurred in the script on this page.

HTA applications rely on MSHTML and starting with Windows 11, version 22H2, the default legacy scripting engine was changed.

To work around this issue you need to add the following registry value in WinPE: 
 ``` 
 reg.exe add "HKLM\Software\Microsoft\Internet Explorer\Main" /t REG_DWORD /v JscriptReplacement /d 0 /f
 ```
To enable this change in MDT, we recommend that you back up the following file: `C:\Program Files\Microsoft Deployment Toolkit\Templates\Unattend_PE_x64.xml` and to modify it as follows:
 ``` <?xml version="1.0" encoding="utf-8"?>
<unattend xmlns="urn:schemas-microsoft-com:unattend">
    <settings pass="windowsPE">
        <component name="Microsoft-Windows-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="http://schemas.microsoft.com/WMIConfig/2002/State">
            <Display>
                <ColorDepth>32</ColorDepth>
                <HorizontalResolution>1024</HorizontalResolution>
                <RefreshRate>60</RefreshRate>
                <VerticalResolution>768</VerticalResolution>
            </Display>
            <RunSynchronous>
                <RunSynchronousCommand wcm:action="add">
                    <Description>Lite Touch PE</Description>
                    <Order>1</Order>
                    <Path>reg.exe add "HKLM\Software\Microsoft\Internet Explorer\Main" /t REG_DWORD /v JscriptReplacement /d 0 /f</Path>
                </RunSynchronousCommand>
                <RunSynchronousCommand wcm:action="add">
                    <Description>Lite Touch PE</Description>
                    <Order>2</Order>
                    <Path>wscript.exe X:\Deploy\Scripts\LiteTouch.wsf</Path>
                </RunSynchronousCommand>
            </RunSynchronous>
        </component>
    </settings>
</unattend>
  ```
After saving the changes, you will need to completely regenerate the boot images.

## Windows Deployment Services (WDS) multicast stops working after upgrading to ADK for Windows 11

<!-- 12891430 --> 

After you updated your MDT boot image to [ADK for Windows 11](/windows-hardware/get-started/adk-install) you might see popups in Windows PE (WinPE) multicast enabled environments prompting wdscommonlib.dll and imagelib.dll are missing in WinPE.

The right way to add WDS multicast to WinPE is to install WinPE-WDS-Tools OC ([WinPE optional components](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference?#winpe-optional-components--)) into WinPE.

Follow this example to install WinPE-WDS-Tools OC in WinPE (assuming the mount folder E:\mnt exists).

 ```cmd
Dism /mount-wim /WimFile:"E:\DeploymentShare\Boot\LiteTouchPE_multicast_x64.wim" /Index:1 /MountDir:E:\mnt
Dism /Image:"E:\mnt" /Add-Package /PackagePath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-WDS-Tools.cab"
Dism /Image:"E:\mnt" /Add-Package /PackagePath:"C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"
Dism /Unmount-Wim /MountDir:E:\mnt /Commit
 ```

Add or replace the multicast enabled boot image in WDS snap-in for Microsoft Management Console (MMC).


## ZTI extensions with version 2013 or 2107

<!-- 10695200 -->

If you install a new Configuration Manager site with version 2103 or 2107, when you run the MDT **Configure ConfigMgr Integration Wizard**, the MDT extensions aren't added to the site.

To work around this issue, disable the hierarchy setting for approved console extensions. For more information, see [Enable or disable hierarchy approved console extensions](../core/servers/manage/admin-console-extensions.md#enable-hierarchy-approved-console-extensions).

## Windows 10, version 2004

When you use MDT build 8456 with the Windows ADK for Windows 10, version 2004, the BIOS firmware type is incorrectly identified as UEFI. This issue results in failures when refreshing an existing computer with a new version of Windows. To mitigate this issue, install the [MDT hotfix 4564442](https://support.microsoft.com/help/4564442).

## Modern language pack support

Starting with Windows 10 version 1809, language interface packs (LIPs) are delivered as local experience packs (LXPs). LXPs are AppX bundles. When specified in the unattend.xml file, they aren't automatically selected, and the deployment fails. Don't set LXPs as default. Users should select an applied LXP from Windows settings.

## Security risk when run over the network

<!-- 2835722 -->

Binaries or scripts that run over the network aren't verified against a digital signature. This issue increases the risk of an attacker tampering with the binaries and injecting malicious code.

To mitigate this issue, protect the network connection with IPsec or SMB signing.

## Next steps

[Release notes](release-notes.md)

[Frequently asked questions](faq.yml)
