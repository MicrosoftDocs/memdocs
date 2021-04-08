---
title: Windows Autopilot FAQ
ms.reviewer: This topic provides OEMs, partners, administrators, and end users with answers to some frequently asked questions about deploying Windows 10 with Windows Autopilot. 
manager: laurawi
description: Support information for Windows Autopilot
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 1/28/2020
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Windows Autopilot FAQ

**Applies to: Windows 10**

This article provides OEMs, partners, administrators, and end users with answers to some frequently asked questions about deploying Windows 10 with Windows Autopilot. 

A [glossary](#glossary) of abbreviations used in this article is provided at the end.


## Microsoft Partner Center

| Question | Answer |
| --- | --- |
| In the Partner Center, does the Tenant ID need to be provided with every device file upload? Is it needed to allow the business customer to access their devices in Microsoft Store for Business (MSfB)? | No. Providing the Tenant ID is a one-time entry in the Partner Center that can be reused with future device uploads. |
| How does the customer or tenant know that their devices are ready to be claimed in MSfB? | After the device file upload is completed in the Partner Center, the tenant can see the devices available for Windows Autopilot setup in MSfB. The OEM needs to advise the tenant to access MSfB. Autonotification from MSfB to the tenant is being developed. |
| How does a customer authorize an OEM or Channel Partner to register Autopilot devices on the customer’s behalf? | Before an OEM or Channel Partner can register a device for Autopilot for a customer, the customer must first give them consent. The consent process begins with the OEM or Channel Partner sending a link to the customer that directs the customer to a consent page in MSfB. For more information, see [Registration](registration-auth.md). |
| Are there any restrictions if a business customer has registered devices in MSfB and later wants those devices to be managed by a Cloud Solution Provider (CSP) using the Partner Center? | The business customer must delete the devices in MSfB before the CSP can upload and manage them in the Partner Center. | 
| Does Windows Autopilot support removing the option to enable a local administrator account? | Windows Autopilot doesn’t support removing the local admin account. However, it does support restricting the user performing Azure Active Directory (Azure AD) domain join in OOBE to a standard account (versus an administrator account by default).|
| How can I test the Windows Autopilot CSV file in the Partner Center? | Only CSP Partners have access to the Partner Center portal. If  you're a CSP, you can create a Sales agent user account that has access to devices for testing the file. This test can be done today in the Partner Center. <br><br>For more information, see [Create user accounts and set permissions](https://msdn.microsoft.com/partner-center/create-user-accounts-and-set-permissions). |
| Is it required to become a CSP to participate in Windows Autopilot? | This requirement doesn't apply to top volume OEMs because they can use the OEM Direct API. All others who choose to use MPC to register devices must become CSPs to access MPC. |
| Do the different CSP levels have all the same capabilities when it comes to Windows Autopilot? | For purposes of Windows Autopilot, there are three different types of CSPs, each with different levels of authority and access: <br><br>1. <b>Direct CSP</b>: Gets direct authorization from the customer to register devices. <br><br>2. <b>Indirect CSP Provider</b>: Gets implicit permission to register devices through the relationship their CSP Reseller partner has with the customer. Indirect CSP Providers register devices through Microsoft Partner Center. <br><br>3. <b>Indirect CSP Reseller</b>: Gets direct authorization from the customer to register devices. At the same time, their indirect CSP Provider partner also gets authorization, which means that either the Indirect Provider or the Indirect Reseller can register devices for the customer. However, the Indirect CSP Reseller must register devices through the MPC UI (manually uploading CSV file), but the Indirect CSP Provider can register devices using the MPC APIs. |
| Is there such a thing as a single, worldwide CSP account? | No. The CSP sales regions depend on the location of the Azure AD tenant. A CSP Partner can only sell or manage customers with a tenant located in the same CSP region. A partner's CSP region is based on the location of the tenant the CSP Partner is using to transact. If the customer tenant was created in the US, only a Partner that has a CSP enrollment in the US can establish a reseller relationship with this customer. With regards to Autopilot & Intune, it doesn't matter where the end user or device is located. A device used by an employee located in Germany can enroll using the Autopilot profile created in the US tenant and can be managed by the Intune service instance in US. The user in Germany will also authenticate in the US AzureAD instance. If a partner wants to manage customers globally, they need to have a global presence. They must have multiple CSP enrollments in each of the CSP sales regions where they wish to conduct business. It's also not possible to create user accounts that have access to all CSP tenants. This scenario would translate into 18 user accounts for a CSP Admin Agent that wants to manage all customers around the world. In summary, the location of the user and devices doesn't matter. The location of the customer tenant matters. Cross-border device registration isn't the problem; the problem is cross-border sales via CSP. |

## Manufacturing

| Question | Answer |
| --- | --- |
| What changes need to be made in the factory OS image for customer configuration settings? |No changes are required on the factory floor to enable Windows Autopilot deployment. |
| What version of the OA3 tool meets Windows Autopilot deployment requirements? | Windows Autopilot can work with any version of the OA3 tool. We recommend using a supported version of Windows 10 semi-annual channel to generate the 4K hardware hash. |
| At the time of placing an order, do customers need to be state whether they want it with or without Windows Autopilot options? | Yes, if they want Windows Autopilot, they'll want a supported version of Windows 10 semi-annual channel. Also, they'll want to receive the CSV file or have the file upload (that is, registration) completed on their behalf. |
| Does the OEM need to manage or collect any custom imaging files from customers? Do they need to upload any images to Microsoft? | No change, OEMs just send the CBRs as usual to Microsoft. No images are sent to Microsoft to enable Windows Autopilot. Windows Autopilot only customizes OOBE and allows policy configurations (disables admin account, for example). |
| Are there any customer impacts to upgrading from Windows 8 to Windows 10? | The devices must be running a supported version of Windows 10 semi-annual channel to enroll in Windows Autopilot deployment. Otherwise, there are no impacts. |
| Will there be any change to the existing CBR with 4K hardware hash? | No. |
| What new information needs to be sent from the OEM to Microsoft? | Nothing, unless the OEM opts to register the device on the customer’s behalf. In this case, they must upload the device ID CSV file into Microsoft Partner Center. Or they can use the OEM Direct API. |
| Is there a contract or amendment for an OEM to participate in Windows Autopilot Deployment? | No. |

## CSV schema

| Question | Answer |
| --- | --- |
| Can a comma be used in the CSV file? | No. |
| What error messages can a user expect to see in the Partner Center or MSfB when uploading a file? | See the In Microsoft Store for Business section of this guide. |
| Is there a limit to the number of devices that can be listed in the CSV file? | Yes, the CSV file can only contain 1,000 devices to apply to a single profile. If more than 1,000 devices need to be applied to a profile, the devices need to be uploaded through multiple CSV files. |
| Does Microsoft have any recommendations on how an OEM should provide the CSV file to their customers? | We recommend encrypting the CSV file when sending to the business customer to self-register their Windows Autopilot devices (either through MPC, MSfB, or Intune). |


## Hardware hash

| Question | Answer |
| --- | --- |
| Must every hardware hash submitted by the OEM contain the following data:<br> - SMBIOS UUID (universally unique identifier)<br> - MAC (media access control) address<br> - Unique disk serial number (if using Windows 10 OEM Activation 3.0 tool)? | Yes. Since Windows Autopilot is based on the ability to uniquely identify devices applying for cloud configuration, it's critical to submit hardware hashes that meet the outlined requirement. |
| What is the reason for needing the SMBIOS UUID, MAC Address, and Disk Serial Number in the hardware hash details? | For creating the hardware hash, these fields are needed to identify a device, as parts of the device are added or removed. Since we don’t have a unique identifier for Windows devices, these fields are the best logic to identify a device. |
| What is difference between OA3 hardware hash, 4K hardware hash, and Windows Autopilot hardware hash? | None. They’re different names for the same thing. The OA3 tool output is called the OA3 Hash, which is 4K in size, which is usable for the Windows Autopilot deployment scenario. Note: When using an older, unsupported Windows version OA3Tool, you get a different-sized Hash, which may not be used for Windows Autopilot deployment. |
| What is the thought around parts replacement and repair for the NIC (network interface controller) and Disk? Will the hardware hash become invalid? | Yes. If you replace parts, you need to gather the new hardware hash, though it depends on what is replaced, and the characteristics of the parts. For example, if you replace the TPM or motherboard, it’s a new device and you must have new hardware hash. If you replace one network card, it’s probably not a new device, and the device will function with the old hardware hash. However, as a best practice, you should assume the old hardware hash is invalid and get a new hardware hash after any hardware changes. This process is recommended anytime you replace parts. |

## Motherboard replacement

| Question | Answer |
| --- | --- |
| How does Autopilot handle motherboard replacement scenarios? | Motherboard replacement is out for scope for Autopilot. Any repaired or serviced device that alters the ability to identify the device for Windows Autopilot must go through the normal OOBE process. It must manually select the right settings or apply a custom image. <br><br>To reuse the same device for Windows Autopilot after a motherboard replacement, the device must be: <br> 1. De-registered from Autopilot.<br>2. The motherboard replaced. <br>3. A new 4K HH harvested. <br>4. Re-registered using the new 4K hardware hash (or device ID). <br><br>**Note**: An OEM can't use the OEM Direct API to re-register the device, since the OEM Direct API only accepts a tuple or PKID. In this case, the OEM would either have to send the new 4K hardware hash information using a CSV file to customer, and let customer reregister the device using MSfB or Intune.|

## SMBIOS

| Question | Answer |
| --- | --- |
| Any specific requirement to SMBIOS UUID? | It must be unique as specified in the Windows 10 hardware requirements. |
| What is the requirement on the SMBIOS table to meet the Windows Autopilot hardware hash need? | It must meet all the Windows 10 hardware requirements. Additional details may be found [here](/previous-versions/windows/hardware/cert-program/windows-hardware-certification-requirements-for-client-and-server-systems). |
| If the SMBIOS supports UUID and Serial Number, is it enough for the OA3 tool to generate the hardware hash? | No. At a minimum, the following SMBIOS fields need to be populated with unique values: ProductKeyID SmbiosSystemManufacturer SmbiosSystemProductName SmbiosSystemSerialNumber SmbiosSkuNumber SmbiosSystemFamily MacAddress SmbiosUuid DiskSerialNumber TPM EkPub |

## Technical interface

| Question | Answer |
| --- | --- |
| What is the interface to get the MAC Address and Disk Serial Number? How does the OA tool get MAC and Disk Serial #? | Disk serial number is found from IOCTL_STORAGE_QUERY_PROPERTY with StorageDeviceProperty/PropertyStandardQuery. Network MAC address is IOCTL_NDIS_QUERY_GLOBAL_STATS from OID_802_3_PERMANENT_ADDRESS. However the method for doing this operation varies depending on the scenario. |
| Follow up clarification: If we have 2-3 MACs on the system, how does OA Tool choose which MAC Address and Disk Serial Number are on the system since there are multiple instances of each? If a platform has LAN And WLAN, which MAC is chosen? | In short, all available values are used. In detail, there may be specific usage rules. The system disk serial number is more important than the other disks available. Network interfaces that are removable shouldn't be used if detected as they're removable. LAN vs WLAN shouldn't matter, as both will be used. |

## The end-user experience

|Question|Answer|
|----|-----|
|How do I know that I received Autopilot?|You can tell that you received Windows Autopilot (as in the device received a configuration but hasn't yet applied it) when you skip the selection page (as seen below), and are immediately taken to a generic or customized sign-in page.|
|Windows Autopilot didn’t work, what do I do now?| Questions and actions to assist in troubleshooting: Did a screen not get skipped? Did a user end up as an admin when configured not to? Remember that Azure AD Admins will be local admins even if Windows Autopilot is configured to disable local admin Collection information: run licensingdiag.exe and send the .cab (Cabinet) file that is generated to AutopilotHelp@microsoft.com. If possible, collect an ETL from Windows Performance Recorder (WPR). Often in these cases, users aren't signing into the right Azure AD tenant, or are creating local user accounts. For a complete list of support options, refer to [Windows Autopilot support](autopilot-support.md). |
| If an Administrator makes changes to an existing profile, will the changes take effect on devices that have that profile assigned to them that have already been deployed? |No. Windows Autopilot profiles aren't resident on the device. They're downloaded during OOBE, the settings defined at the time are applied. Then, the profile is discarded on the device. If the device is reimaged or reset, the new profile settings will take effect the next time the device goes through OOBE.|
|What is the experience if a device isn’t registered or if an IT Admin doesn’t configure Windows Autopilot before an end user attempting to self-deploy? |If the device isn’t registered, it won't receive the Windows Autopilot experience and the end user will go through normal OOBE. The Windows Autopilot configurations won't be applied until the user runs through OOBE again, after registration. If a device is started before an MDM profile is created, the device will go through standard OOBE experience. The IT Admin would then have to manually enroll that device into the MDM, after which the next time that device is reset, it will go through the Windows Autopilot OOBE experience.|
|Why didn't I receive a customized sign-in screen during Autopilot? |Tenant branding must be configured in portal.azure.com to receive a customized sign-in experience.|
|What happens if a device is registered with Azure AD but doesn't have a Windows Autopilot profile assigned? |The regular Azure AD OOBE will occur since no Windows Autopilot profile was assigned to the device.|
|How can I collect logs on Autopilot?|The best way to collect logs on Windows Autopilot performance is to collect a WPR trace during OOBE. The XML file (WPRP extension) for this trace may be provided upon request.|

## MDM

| Question | Answer |
| --- | --- |
| Must we use Intune for our MDM? | No, any MDM will work with Autopilot, but others probably won’t have the same full suite of Windows Autopilot features as Intune. You’ll get the best experience from Intune. |
| Can Intune support Win32 app preinstalls? | Yes. Starting with the Windows 10 October Update (version 1809), Intune supports Win32 apps using .msi and .msix wrappers. |
| What is co-management? | Co-management is when you use a combination of a cloud MDM tool (Intune) and an on-premises configuration tool like Microsoft Endpoint Configuration Manager. You only need to use the Configuration Manager if Intune can’t support what you want to do with your profile. If you choose to co-manage using Intune + Configuration Manager, you do it by including a Configuration Manager agent in your Intune profile. When that profile is pushed to the device, the device will see the Configuration Manager agent and go out to the Configuration Manager to pull down any additional profile settings. |
| Must we use Microsoft Endpoint Configuration Manager for Windows Autopilot | No. Co-management (described above) is optional. |


## Features

| Question | Answer |
| --- | --- |
| Self-deploying mode | A new version of Windows Autopilot where the user only turns on the device, and nothing else. It’s useful for scenarios where a standard user account isn’t needed (for example, shared devices, or KIOSK devices). |
| Hybrid Azure Active Directory join | Allows Windows Autopilot devices to connect to an on-premises Active Directory domain controller (in addition to being Azure AD joined). |
| Windows Autopilot reset | Removes user apps and settings from a device, but maintains Azure AD domain join and MDM enrollment. Useful for when transferring a device from one user to another. |
| Personalization | Adds the following to the OOBE experience: A personalized welcome message can be created. A username hint can be added Sign-in page text can be personalized. The company’s logo can be included |
| [Autopilot for existing devices](existing-devices.md) | Offers an upgrade path to Windows Autopilot for all existing Windows 7 and Windows 8 devices. |



## General

|Question|Answer
|------------------|-----------------|
| If I wipe the machine and restart, will I still receive Windows Autopilot?|Yes, if the device is still registered for Windows Autopilot and is running a supported version of Windows 10 semi-annual channel, it will receive the Windows Autopilot experience.|
| Can I harvest the device fingerprint on existing machines?|Yes, if the device is running a supported version of Windows 10 semi-annual channel, you can harvest device fingerprints for registration. There are no plans to backport the functionality to legacy releases and no way to harvest them on devices running unsupported versions of Windows.|
| Is Windows Autopilot supported on other SKUs, for example, Surface Hub, HoloLens, Windows Mobile.|No, Windows Autopilot isn’t supported on other SKUs.|
| Does Windows Autopilot work after MBR or image reinstallation? | Yes. For more information, see [Windows Autopilot motherboard replacement scenario guidance](autopilot-mbr.md). |
| Can devices that have been reimaged a few times go through Autopilot? What does the error message "This user isn't authorized to enroll" mean? Error code 801c0003. |There are limits to the number of devices a particular Azure AD user can enroll in Azure AD, and the number of devices that are supported per user in Intune. These limits are configurable, but not infinite. You’ll run into this error frequently if you reuse the devices, or even if you roll back to previous virtual machine snapshots.|
| What happens if a device is registered to a malicious agent? | By design, Windows Autopilot doesn't apply a profile until the user signs in with the matching tenant for the configured profile using the Azure AD sign-in process. For example, if badguys.com registers a device owned by contoso.com, then at worst, the user will be directed to sign in to badguys.com. When the user enters their email and password, the sign-in information is redirected through Azure AD to the proper Azure AD authentication and the user is prompted to then sign into contoso.com. Since contoso.com doesn't match badguys.com as the tenant, the Windows Autopilot profile won't be applied and the regular Azure AD OOBE will occur.|
| Where is the Windows Autopilot data stored? |Windows Autopilot data is stored in the United States (US), not in a sovereign cloud, even when the Azure AD tenant is registered in a sovereign cloud. This storage applies to all Windows Autopilot data, whatever portal is used to deploy Autopilot.|
| Why is Windows Autopilot data stored in the US and not in a sovereign cloud?| Customer data isn't stored, only business data that enables Microsoft to provide a service. That's why it's appropriate for the data to be stored in the US. Customers can stop subscribing to the service at any time. In that event, the business data is removed by Microsoft. Autopilot isn't currently supported in any sovereign cloud. |
| How many ways are there to register a device for Windows Autopilot|There are six ways to register a device, depending on who is doing the registering: <br><br>1. OEM Direct API (only available to TVOs) <br>2. MPC using the MPC API (must be a CSP) <br>3. MPC using manual upload of CSV file in the UI (must be a CSP) <br>4. MSfB using CSV file upload <br>5. Intune using CSV file upload <br>6. Microsoft 365 Business Premium portal using CSV file upload|
|How many ways are there to create a Windows Autopilot profile?|There are four ways to create and assign a Windows Autopilot profile: <br><br>1. Through MPC (must be a CSP) <br>2. Through MSfB <br>3. Through Intune (or another MDM) <br>4. Microsoft 365 Business Premium portal <br><br>Microsoft recommends creation and assignment of profiles through Intune. |
| What are some common causes of registration failures? |1. Bad or missing hardware hash entries can lead to faulty registration attempts <br>2. Hidden special characters in CSV files. <br><br>To avoid this issue, after creating your CSV file, open it in Notepad to look for hidden characters or trailing spaces or other corruptions.|
| Is Autopilot supported on IoT devices? | Autopilot isn't supported on IoT Core devices, and there are currently no plans to add this support. Autopilot is supported on Windows 10 IoT Enterprise SAC devices. Autopilot is supported on Windows 10 Enterprise LTSC 2019 and above; it isn't supported on earlier versions of LTSC.|
| Is Autopilot supported in all regions/countries? | Autopilot only supports customers using global Azure. Global Azure doesn't include the three entities listed below:<br>- Azure Germany <br>- Azure China 21Vianet<br>- Azure Government<br>So, if a customer is set up in global Azure, there are no region restrictions. For example, if Contoso uses global Azure but has employees working in China, the Contoso employees working in China could use Autopilot to deploy devices. If Contoso uses Azure China 21Vianet, the Contoso employees couldn't use Autopilot.|
| Why does TPM provisioning/attestatstion take longer during the first boot on a device? | TPM provisioning involves generating and processing strong cryptographic keys and depending on characteristics of TPM hardware used on a device, it may take longer than 1 minute on first boot.|


## Glossary

| Term | Meaning |
| --- | --- |
| CSV | Comma-Separated Values (File type similar to Excel spreadsheet) |
| MPC | Microsoft Partner Center |
| MDM | Mobile Device Management |
| OEM | Original Equipment Manufacturer |
| CSP | Cloud Solution Provider |
| MSfB | Microsoft Store for Business |
| Azure AD | Azure Active Directory |
| 4K HH | 4-K hardware hash |
| CBR | Computer Build Report |
| EC | Enterprise Commerce |
| DDS | Device Directory Service |
| OOBE | Out of the Box Experience |
| UUID | Universally Unique Identifier |