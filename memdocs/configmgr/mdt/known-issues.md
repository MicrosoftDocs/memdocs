---
title: MDT known issues
description: Current limitations with the Microsoft Deployment Toolkit (MDT).
ms.date: 03/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-mdt
ms.topic: article
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Microsoft Deployment Toolkit known issues

This article provides details of any current known issues and limitations with the Microsoft Deployment Toolkit (MDT). It assumes familiarity with MDT version concepts, features, and capabilities.

> [!IMPORTANT]
> MDT is not supported with Windows 11.  Any listed known issues for Windows 11 or the ADK for Windows 11 is for informational purposes only and does not imply support. For additional information, please see [Supported platforms](release-notes.md#supported-platforms)

## The Create Boot Image using MDT wizard fails when creating a boot image in Microsoft Configuration Manager after upgrading to ADK for Windows 11, version 22H2

After upgrading to the ADK for Windows 11, version 22H2, the **Create Boot Image using MDT** wizard fails when trying to create a boot image with the following error:

**Could not find a part of the path 'C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Windows Preinstallation Environment\x86\WinPE_OCs'.**

This error occurs regardless if the boot image being created is x64.

This error is an expected error since starting with the ADK for Windows 11, version 22H2, the 32-bit versions of Windows PE are no longer included. Additionally, MDT isn't supported with Windows 11 or the ADK for Windows 11. For more information, see [Download and install the Windows ADK](/windows-hardware/get-started/adk-install).

The **Create Boot Image using MDT** wizard was created when Configuration Manager had no out of box functionality to create boot images using the currently installed ADK directly in the console. Integrating MDT with Configuration Manager added the functionality to create boot images using the currently installed ADK in the console. However, Configuration Manager has since added the ability to create boot images in console out of the box without the need for MDT integration.

Additionally, boot images created using the **Create Boot Image using MDT** wizard aren't required for task sequences created using the **Create MDT Task Sequence** wizard. These boot images and task sequences are commonly called "MDT" boot images and "MDT" task sequences. However, there's nothing special about an "MDT" boot image and they're binary equivalent to a Configuration Manager boot image. "MDT" task sequences are also not special. They're just Configuration Manager task sequences that happen to run MDT scripts. In other words, "MDT" boot images are not required for "MDT" task sequences to work. There are no additional binaries in an "MDT" boot image that are required by "MDT" task sequences. Configuration Manager boot images will work without issue with "MDT" task sequences.

Instead of using the **Create Boot Image using MDT** wizard to create boot images in Configuration Manager, use the out of box functionality in Configuration Manager to create boot images. For more information, see [Managing boot images with Configuration Manager: Update distribution points with the boot image](/mem/configmgr/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

To create a new boot image using the out of box Configuration Manager functionality:

1. Navigate to the path that hosts the default x64 boot image on the Configuration Manager site server. This path would normally be `<Configuration_Manager_install_directory>\OSD\boot\x64`.

2. In the `\OSD\boot\x64` directory, make a copy of `boot.wim` and rename it to the name of your choice.

3. In the Configuration Manager console, go to the **Software Library** node and then navigate to **Overview** > **Operating Systems** > **Boot Images**.

4. Right click on **Boot Images** and select **Add Boot Image**.

5. Follow the **Add Boot Image Wizard** to import the copy of `boot.wim` created in Step 2 as a new boot image. For more information on adding a boot image using the **Add Boot Image Wizard**, see [Manage boot images with Configuration Manager: Add a boot image](/mem/configmgr/osd/get-started/manage-boot-images#add-a-boot-image).

6. Once the **Add Boot Image Wizard** completes and the new boot image has been added, right click on the newly created boot image and select **Update Distribution Points**.

    > [!NOTE]
    > Don't first distribute the newly created boot image to distribution points before selecting **Update Distribution Points**. The next steps will finish updating the newly created boot image so that it is the same version as the currently installed ADK and Windows PE. This can be accomplished without first distributing the newly created boot image to the distribution points. It is better to finish properly creating the boot image before distributing the boot image to distribution points to avoid unnecessary updates to the distribution points. Distributing the boot image first before finishing updating the boot image will result in unneeded updates to the distribution points.

7. In the **Update Distribution Points Wizard**, select the option **Reload this boot image with the current Windows PE version from the Windows ADK**, select **Next >**, and then **Next >** again.

8. Allow the **Update Distribution Points Wizard** to complete.

Once the **Update Distribution Points Wizard** completes, the newly created boot image will be at the same version as the currently installed ADK and Windows PE.

If additional components need to be added to the boot image:

1. Right click on the newly created boot image and select **Properties**.

2. In the boot image properties window, select the **Optional Components** tab

3. Add in the desired optional components. For more information, see [Manage boot images with Configuration Manager: Optional components](/mem/configmgr/osd/get-started/manage-boot-images#optional-components).

Make any additional desired changes to the newly created boot image, such as adding drivers, and then distribute the boot image to distribution points.

> [!NOTE]
> The above guide only shows x64 boot images since only x64 boot images are supported with the ADK for Windows 11, version 22H2 or newer.

## HTA applications report Script error after upgrading to ADK for Windows 11, version 22H2

After you updated your MDT boot image to [ADK for Windows 11, version 22H2](/windows-hardware/get-started/adk-install), HTA applications stop working and a message box is displayed: Script Error - An error has occurred in the script on this page.

HTA applications rely on MSHTML and starting with Windows 11, version 22H2, the default legacy scripting engine was changed.

To work around this issue, you need to add the following registry value in WinPE:

```cmd
 reg.exe add "HKLM\Software\Microsoft\Internet Explorer\Main" /t REG_DWORD /v JscriptReplacement /d 0 /f
```

To enable this change in MDT, we recommend that you back up the following file: `C:\Program Files\Microsoft Deployment Toolkit\Templates\Unattend_PE_x64.xml` and to modify it as follows:

```xml
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

After saving the changes, you'll need to completely regenerate the boot images.

## Windows Deployment Services (WDS) multicast stops working after upgrading to ADK for Windows 11

<!-- 12891430 -->

After you updated your MDT boot image to [ADK for Windows 11](/windows-hardware/get-started/adk-install), you might see popups in Windows PE (WinPE) multicast enabled environments prompting wdscommonlib.dll and imagelib.dll are missing in WinPE.

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
