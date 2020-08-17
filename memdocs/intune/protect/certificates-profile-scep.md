---
title: Use SCEP certificate profiles with Microsoft Intune - Azure | Microsoft Docs
description: Create and assign Simple Certificate Enrollment Protocol (SCEP) certificate profiles with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create and assign SCEP certificate profiles in Intune

After you [configure your infrastructure](certificates-scep-configure.md) to support Simple Certificate Enrollment Protocol (SCEP) certificates, you can create and then assign SCEP certificate profiles to users and devices in Intune.

> [!IMPORTANT]
> For devices to use a SCEP certificate profile, they must trust your Trusted Root Certification Authority (CA). Trust of the root CA is best established by deploying a [trusted certificate profile](../protect/certificates-configure.md#create-trusted-certificate-profiles) to the same group that receives the SCEP certificate profile. Trusted certificate profiles provision the Trusted Root CA certificate.

## Create a SCEP certificate profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select  and go to **Devices** > **Configuration profiles** > **Create profile**.

3. Enter the following properties:
   - **Platform**: Choose the platform of your devices.
   - **Profile**: Select **SCEP certificate**

     For the **Android Enterprise** platform, *Profile type* is divided into two categories, *Fully Managed, Dedicated, and Corporate-Owned Work Profile* and *Work Profile Only*. Be sure to select the correct SCEP certificate profile for the devices you manage.  

     SCEP certificate profiles for the *Fully Managed, Dedicated, and Corporate-Owned Work Profile* profile have the following limitations:

      1. Under Monitoring, certificate reporting isn't available for Device Owner SCEP certificate profiles.

      2. You can't use Intune to revoke certificates that were provisioned by SCEP certificate profiles for Device Owners. You can manage revocation through an external process or directly with the certification authority.

      3. For Android Enterprise dedicated devices, SCEP certificate profiles are supported for Wi-Fi network configuration, VPN, and authentication. SCEP certificate profiles on Android Enterprise dedicated devices are not supported for app authentication.

4. Select **Create**.

5. In **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is *SCEP profile for entire company*.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, complete the following configurations:

   - **Certificate type**:

     *(Applies to:  Android, Android Enterprise, iOS/iPadOS, macOS, Windows 8.1 and later, and Windows 10 and later.)*

     Select a type depending on how you'll use the certificate profile:

     - **User**: *User* certificates can contain both user and device attributes in the subject and SAN of the certificate.  
     - **Device**:  *Device* certificates can only contain device attributes in the subject and SAN of the certificate.

       Use **Device** for scenarios such as user-less devices, like kiosks, or for Windows devices. On Windows devices, the certificate is placed in the Local Computer certificate store.

     > [!NOTE]
     > On macOS, certificates you provision with SCEP are always placed in the system keychain (System store) of the device.
 
   - **Subject name format**:

     Select how Intune automatically creates the subject name in the certificate request. Options for the subject name format depend on the Certificate type you select, either **User** or **Device**.

     > [!NOTE]
     > There is a [known issue](#avoid-certificate-signing-requests-with-escaped-special-characters) for using SCEP to get certificates when the subject name in the resulting Certificate Signing Request (CSR) includes one of the following characters as an escaped character (proceeded by a backslash \\):
     > - \+
     > - ;
     > - ,
     > - =

     - **User certificate type**

       Format options for the *Subject name format* include:

       - **Not configured**
       - **Common name**
       - **Common name including email**
       - **Common name as email**
       - **IMEI (International Mobile Equipment Identity)**
       - **Serial number**
       - **Custom**: When you select this option, a **Custom** text box is also shown. Use this field to enter a custom subject name format, including variables. Custom format supports two variables: **Common Name (CN)** and **Email (E)**. **Common Name (CN)** can be set to any of the following variables:

         - **CN={{UserName}}**: The user name of the user, such as janedoe.
         - **CN={{UserPrincipalName}}**: The user principal name of the user, such as janedoe@contoso.com.\*
         - **CN={{AAD_Device_ID}}**: An ID assigned when you register a device in Azure Active Directory (AD). This ID is typically used to authenticate with Azure AD.
         - **CN={{SERIALNUMBER}}**: The unique serial number (SN) typically used by the manufacturer to identify a device.
         - **CN={{IMEINumber}}**: The International Mobile Equipment Identity (IMEI) unique number used to identify a mobile phone.
         - **CN={{OnPrem_Distinguished_Name}}**: A sequence of relative distinguished names separated by comma, such as *CN=Jane Doe,OU=UserAccounts,DC=corp,DC=contoso,DC=com*.

           To use the *{{OnPrem_Distinguished_Name}}* variable, be sure to sync the *onpremisesdistinguishedname* user attribute using [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) to your Azure AD.

         - **CN={{onPremisesSamAccountName}}**: Admins can sync the samAccountName attribute from Active Directory to Azure AD using Azure AD connect into an attribute called *onPremisesSamAccountName*. Intune can substitute that variable as part of a certificate issuance request in the subject of a certificate. The samAccountName attribute is the user sign-in name used to support clients and servers from a previous version of Windows (pre-Windows 2000). The user sign in name format is: *DomainName\testUser*, or only *testUser*.

            To use the *{{onPremisesSamAccountName}}* variable, be sure to sync the *onPremisesSamAccountName* user attribute using [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) to your Azure AD.

         By using a combination of one or many of these variables and static strings, you can create a custom subject name format, such as:  
         - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**

         That example includes a subject name format that uses the CN and E variables, and strings for Organizational Unit, Organization, Location, State, and Country values. [CertStrToName function](https://msdn.microsoft.com/library/windows/desktop/aa377160.aspx) describes this function, and its supported strings.
         
         \* For Android Fully Managed, Dedicated, and Corporate-Owned Work Profile profiles, the **CN={{UserPrincipalName}}** setting will not work. Android Fully Managed, Dedicated, and Corporate-Owned Work Profile profiles can be used for devices without User so this profile will not be able to get the user principal name of the user. If you really need this option for devices with users, you can use a workaround like this: **CN={{UserName}}\@contoso.com** It will provide the User Name and the domain you added manually, such as janedoe@contoso.com

      - **Device certificate type**

        Format options for the Subject name format include the following variables:

        - **{{AAD_Device_ID}}** or **{{AzureADDeviceId​}}** - Either variable can be used to identify a device by its Azure AD ID.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}** *(Only applicable for Windows and domain-joined devices)*
        - **{{MEID}}**

        You can specify these variables, followed by the text for the variable, in the textbox. For example, the common name for a device named *Device1* can be added as **CN={{DeviceName}}Device1**.

        > [!IMPORTANT]
        > - When you specify a variable, enclose the variable name in curly brackets { } as seen in the example, to avoid an error.  
        > - Device properties used in the *subject* or *SAN* of a device certificate, like **IMEI**, **SerialNumber**, and **FullyQualifiedDomainName**, are properties that could be spoofed by a person with access to the device.
        > - A device must support all variables specified in a certificate profile for that profile to install on that device.  For example, if **{{IMEI}}** is used in the subject name of a SCEP profile and is assigned to a device that doesn't have an IMEI number, the profile fails to install.

   - **Subject alternative name**:
     Select how Intune automatically creates the subject alternative name (SAN) in the certificate request. Options for the SAN depend on the Certificate type you selected; either **User** or **Device**.

      - **User certificate type**

        Select from the available attributes:

        - **Email address**
        - **User principal name (UPN)**

        For example, user certificate types can include the user principal name (UPN) in the subject alternative name. If a client certificate is used to authenticate to a Network Policy Server, set the subject alternative name to the UPN.

      - **Device certificate type**

        Use the **Attribute** dropdown and select an attribute, assign a **Value**, and **Add** that to the certificate profile. You can add multiple values by selecting additional attributes.

        Available attributes include:

        - **Email address**
        - **User principal name (UPN)**
        - **DNS**

        With the *Device* certificate type, you can use the following device certificate variables for the value:

        - **{{AAD_Device_ID}}** or **{{AzureADDeviceId​}}** - Either variable can be used to identify a device by its Azure AD ID.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}**
        - **{{MEID}}**

        To specify a value for an attribute, include the variable name with curly brackets, followed by the text for that variable. For example, a value for the DNS attribute can be added **{{AzureADDeviceId}}.domain.com** where *.domain.com* is the text. For a user named *User1* an Email address might appear as {{FullyQualifiedDomainName}}User1@Contoso.com.

        > [!IMPORTANT]
        > - When using a device certificate variable, enclose the variable name in curly brackets { }.
        > - Don't use curly brackets **{ }**, pipe symbols **|**, and semicolons **;**, in the text that follows the variable.
        > - Device properties used in the *subject* or *SAN* of a device certificate, like **IMEI**, **SerialNumber**, and **FullyQualifiedDomainName**, are properties that could be spoofed by a person with access to the device.
        > - A device must support all variables specified in a certificate profile for that profile to install on that device.  For example, if **{{IMEI}}** is used in the SAN of a SCEP profile and is assigned to a device that doesn't have an IMEI number, the profile fails to install.

   - **Certificate validity period**:

     You can enter a value that is lower than the validity period in the certificate template, but not higher. If you configured the certificate template to [support a custom value that can be set from within the Intune console](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template), use this setting to specify the amount of remaining time before the certificate expires.

     For example, if the certificate validity period in the certificate template is two years, you can enter a value of one year, but not a value of five years. The value must also be lower than the remaining validity period of the issuing CA's certificate.

   - **Key storage provider (KSP)**:

     *(Applies to:  Windows 8.1 and later, and Windows 10 and later)*

     Specify where the key to the certificate is stored. Choose from the following values:

     - **Enroll to Trusted Platform Module (TPM) KSP if present, otherwise Software KSP**
     - **Enroll to Trusted Platform Module (TPM) KSP, otherwise fail**
     - **Enroll to Passport, otherwise fail (Windows 10 and later)**
     - **Enroll to Software KSP**

   - **Key usage**:

     Select key usage options for the certificate:

     - **Digital signature**: Allow key exchange only when a digital signature helps protect the key.
     - **Key encipherment**: Allow key exchange only when the key is encrypted.

   - **Key size (bits)**:

     Select the number of bits contained in the key.

   - **Hash algorithm**:

     *(Applies to Android, Android enterprise, Windows 8.1 and later, and Windows 10 and later)*

     Select one of the available hash algorithm types to use with this certificate. Select the strongest level of security that the connecting devices support.

   - **Root Certificate**:

     Select the *trusted certificate profile* you previously configured and assigned to applicable users and devices for this SCEP certificate profile. The trusted certificate profile is used to provision users and devices with the Trusted Root CA certificate. For information about the trusted certificate profile, see [Export your trusted root CA certificate](certificates-configure.md#export-the-trusted-root-ca-certificate) and [Create trusted certificate profiles](certificates-configure.md#create-trusted-certificate-profiles) in *Use certificates for authentication in Intune*. If you have a root Certification Authority and an issuing Certification Authority, select the Trusted Root certificate profile that validates the Issuing Certification Authority.

   - **Extended key usage**:

     Add values for the certificate's intended purpose. In most cases, the certificate requires *client authentication* so that the user or device can authenticate to a server. You can add additional key usages as required.

   - **Renewal threshold (%)**:

     Enter the percentage of the certificate lifetime that remains before the device requests renewal of the certificate. For example, if you enter 20, the renewal of the certificate will be attempted when the certificate is 80% expired. Renewal attempts continue until renewal is successful. Renewal generates a new certificate, which results in a new public/private key pair.

   - **SCEP Server URLs**:

     Enter one or more URLs for the NDES Servers that issue certificates via SCEP. For example, enter something like `https://ndes.contoso.com/certsrv/mscep/mscep.dll`.

     You can add additional SCEP URLs for load balancing as needed. Devices make three separate calls to the NDES server; to get the servers capabilities, to get a public key, and then to submit a signing request. When you use multiple URLs its possible that load balancing might result in a different URL being used for subsequent calls to an NDES Server. If a different server is contacted for a subsequent call during the same request, the request will fail.

     The behavior for managing the NDES server URL is specific to each device platform:

     - **Android**: The device randomizes the list of URLs received in the SCEP policy, and then works through the list until an accessible NDES server is found. The device then continues to use that same URL and server through the entire process. If the device can’t access any of the NDES servers, the process fails.
     - **iOS/iPadOS**: Intune randomizes the URLs and provides a single URL to a device. If the device can’t access the NDES server, the SCEP request fails.
     - **Windows**: The list of NDES URLs is randomized and then passed to the Windows device, which then tries them in the order received, until one that's available is found. If the device can’t access any of the NDES servers, the process fails.

     If a device fails to reach the same NDES server successfully during any of the three calls to the NDES server, the SCEP request fails. For example, this might happen when a load balancing solution provides a different URL for the second or third call to the NDES server, or provides a different actual NDES server based on a virtualized URL for NDES. After a failed request, a device tries the process again on its next policy cycle, starting with the randomized list of NDES URLs (or a single URL for iOS/iPadOS).  

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

   Select **Next**.

10. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

    Select **Next**.

11. (*Applies to Windows 10 only*) In **Applicability Rules**, specify applicability rules to refine the assignment of this profile. You can choose to assign or not assign the profile based on the OS edition or version of a device.

   For more information, see [Applicability rules](../configuration/device-profile-create.md#applicability-rules) in *Create a device profile in Microsoft Intune*.

12. In **Review + create**, review your settings. When you select Create, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

### Avoid certificate signing requests with escaped special characters

There's a known issue for SCEP and PKCS certificate requests that include a Subject Name (CN) with one or more of the following special characters as an escaped character. Subject names that include one of the special characters as an escaped character result in a CSR with an incorrect subject name. An incorrect subject name results in the Intune SCEP challenge validation failing and no certificate issued.

The special characters are:
- \+
- ,
- ;
- =

When your subject name includes one of the special characters, use one of the following options to work around this limitation:

- Encapsulate the CN value that contains the special character with quotes.  
- Remove the special character from the CN value.

**For example**, you have a Subject Name that appears as *Test user (TestCompany, LLC)*.  A CSR that includes a CN that has the comma between *TestCompany* and *LLC* presents a problem.  The problem can be avoided by placing quotes around the entire CN, or by removing of the comma from between *TestCompany* and *LLC*:

- **Add quotes**: *CN="Test User (TestCompany, LLC)",OU=UserAccounts,DC=corp,DC=contoso,DC=com*
- **Remove the comma**: *CN=Test User (TestCompany LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

 However, attempts to escape the comma by using a backslash character will fail with an error in the CRP logs:
 
- **Escaped comma**: *CN=Test User (TestCompany\\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

The error is similar to the following error:

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## Assign the certificate profile

Assign SCEP certificate profiles the same way you [deploy device profiles](../configuration/device-profile-assign.md) for other purposes.

To use a SCEP certificate profile, a device must have also received the trusted certificate profile that provisions it with your Trusted Root CA certificate. We recommend you deploy both the trusted root certificate profile and SCEP certificate profile to the same groups.

Consider the following before you continue:

- When you assign SCEP certificate profiles to groups, the Trusted Root CA certificate file (as specified in the *trusted certificate profile*) is installed on the device. The device uses the SCEP certificate profile to create a certificate request for that Trusted Root CA certificate.

- The SCEP certificate profile installs only on devices that run the platform you specified when you created the certificate profile.

- You can assign certificate profiles to user collections or to device collections.

- To publish a certificate to a device quickly after the device enrolls, assign the certificate profile to a user group rather than to a device group. If you assign to a device group, a full device registration is required before the device receives policies.

- If you use co-management for Intune and Configuration Manager, in Configuration Manager [set the workload slider](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) for Resource Access Policies to **Intune** or **Pilot Intune**. This setting allows Windows 10 clients to start the process of requesting the certificate.

> [!NOTE]
> - On iOS/iPadOS devices, when a SCEP certificate profile or a PKCS certificate profile is associated with an additional profile, like a Wi-Fi or VPN profile, the device receives a certificate for each of those additional profiles. This results in the iOS/iPadOS device having multiple certificates delivered by the SCEP or PKCS certificate request. 
> 
>   Certificates delivered by SCEP are each unique. Certificates delivered by PKCS are the same certificate, but appear different as each profile instance is represented by a separate line in the management profile.
> - On iOS 13 and macOS 10.15, there are some [additional security requirements that are documented by Apple](https://support.apple.com/HT210176) to take into consideration.  


## Next steps

[Assign profiles](../configuration/device-profile-assign.md)

[Troubleshoot deployment of SCEP certificate profiles](../protect/troubleshoot-scep-certificate-profiles.md)
