---
# required metadata

title: Create WiFi profile with preshared key in Microsoft Intune
description: Use a custom profile to create a Wi-Fi profile with a preshared key, and get sample XML code for Android, Android Enterprise, Windows, and EAP-based Wi-Fi profiles in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/16/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: c6fd72a6-7dc8-48fc-9df1-db5627a51597

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection:
- tier2
- M365-identity-device-management
---

# Use a custom device profile to create a WiFi profile with a preshared key in Intune

Pre-shared keys (PSK) are typically used to authenticate users in WiFi networks, or wireless LANs. With Intune, you can create a WiFi profile using a preshared key. To create the profile, use the **Custom device profiles** feature within Intune. This article also includes some examples of how to create an EAP-based Wi-Fi profile.

This feature applies to:

- Android device administrator
- Android Enterprise personally owned devices with a work profile
- Windows
- EAP-based Wi-Fi

> [!IMPORTANT]
>
> - Using a pre-shared key with Windows 10/11 causes a remediation error to show in Intune. When this happens, the Wi-Fi profile is properly assigned to the device, and the profile does work as expected.
> - If you export a Wi-Fi profile that includes a pre-shared key, be sure the file is protected. The key is in plain text. It's your responsibility to protect the key.

## Before you begin

- It may be easier to copy the code from a computer that connects to that network, as described in [Create the XML file from an existing Wi-Fi connection](#create-the-xml-file-from-an-existing-wi-fi-connection) (in this article).
- You can add multiple networks and keys by adding more OMA-URI settings.
- For iOS/iPadOS, use Apple Configurator on a Mac station to set up the profile.
- PSK requires a string of 64 hexadecimal digits, or a passphrase of 8 to 63 printable ASCII characters. Some characters, such as asterisk ( * ), aren't supported.

## Create a custom profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose your platform.
    - **Profile**: Select **Custom**. Or, select **Templates** > **Custom**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Custom OMA-URI Wi-Fi profile for Android DA**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Add**. Enter a new OMA-URI setting with the following properties:

    1. **Name**: Enter a name for the OMA-URI setting.
    2. **Description**: Enter a description for the OMA-URI setting. This setting is optional, but recommended.
    3. **OMA-URI**: Enter one of the following options:

        - **For Android**: `./Vendor/MSFT/WiFi/Profile/SSID/Settings`
        - **For Windows**: `./Vendor/MSFT/WiFi/Profile/SSID/WlanXml`

        > [!NOTE]
        > 
        > - Be sure to include the dot character at the beginning.
        > - If the SSID has a space, then add an escape space `%20`.

        SSID is the SSID for which you're creating the policy. For example, if the Wi-Fi is named `Hotspot-1`, enter `./Vendor/MSFT/WiFi/Profile/Hotspot-1/Settings`. If the Wi-Fi is named `Contoso WiFi`, enter `./Vendor/MSFT/WiFi/Profile/Contoso%20WiFi/Settings` (with the `%20` escape space).

    4. **Data Type**: Select **String**.

    5. **Value**: Paste your XML code. See the [examples](#android-or-windows-wi-fi-profile-example) in this article. Update each value to match your network settings. The comments section of the code includes some pointers.
    6. Select **Add** to save your changes.

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    > [!NOTE]
    > This policy can only be assigned to user groups.

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied, and a Wi-Fi profile is created on the device. The device can then connect to the network automatically.

## Android or Windows Wi-Fi profile example

The following example includes the XML code for an Android or Windows Wi-Fi profile. The example is provided to show proper format and provide more details. It's only an example, and isn't intended as a recommended configuration for your environment.

### What you need to know

- `<protected>false</protected>` must be set to **false**. When **true**, it could cause the device to expect an encrypted password, and then try to decrypt it; which may result in a failed connection.

- `<hex>53534944</hex>` should be set to the hexadecimal value of `<name><SSID of wifi profile></name>`. Windows 10/11 devices may return a false `x87D1FDE8 Remediation failed` error, but the device still contains the profile.

- XML has special characters, such as the `&` (ampersand). Using special characters may prevent the XML from working as expected. 

### Example

``` xml
<!--
<hex>53534944</hex> = The hexadecimal value of <name><SSID of wifi profile></name>
<Name of wifi profile> = Name of profile shown to users. For example, enter <name>ContosoWiFi</name>.
<SSID of wifi profile> = Plain text of SSID. Does not need to be escaped. It could be <name>Your Company's Network</name>.
<nonBroadcast><true/false></nonBroadcast>
<Type of authentication> = Type of authentication used by the network, such as WPA2PSK.
<Type of encryption> = Type of encryption used by the network, such as AES.
<protected>false</protected> do not change this value, as true could cause device to expect an encrypted password and then try to decrypt it, which may result in a failed connection.
<password> = Plain text of the password to connect to the network
-->

<WLANProfile xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
  <name><Name of wifi profile></name>
  <SSIDConfig>
    <SSID>
      <hex>53534944</hex>
 <name><SSID of wifi profile></name>
    </SSID>
    <nonBroadcast>false</nonBroadcast>
  </SSIDConfig>
  <connectionType>ESS</connectionType>
  <connectionMode>auto</connectionMode>
  <autoSwitch>false</autoSwitch>
  <MSM>
    <security>
      <authEncryption>
        <authentication><Type of authentication></authentication>
        <encryption><Type of encryption></encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>false</protected>
        <keyMaterial>password</keyMaterial>
      </sharedKey>
      <keyIndex>0</keyIndex>
    </security>
  </MSM>
</WLANProfile>
```

### EAP-based Wi-Fi profile example

The following example includes the XML code for an EAP-based Wi-Fi profile: The example is provided to show proper format and provide more details. It's only an example, and isn't intended as a recommended configuration for your environment.

```xml
    <WLANProfile xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
      <name>testcert</name>
      <SSIDConfig>
        <SSID>
          <hex>7465737463657274</hex>
          <name>testcert</name>
        </SSID>
        <nonBroadcast>true</nonBroadcast>
      </SSIDConfig>
      <connectionType>ESS</connectionType>
      <connectionMode>auto</connectionMode>
      <autoSwitch>false</autoSwitch>
      <MSM>
        <security>
          <authEncryption>
            <authentication>WPA2</authentication>
            <encryption>AES</encryption>
            <useOneX>true</useOneX>
            <FIPSMode     xmlns="http://www.microsoft.com/networking/WLAN/profile/v2">false</FIPSMode>
          </authEncryption>
          <PMKCacheMode>disabled</PMKCacheMode>
          <OneX xmlns="http://www.microsoft.com/networking/OneX/v1">
            <cacheUserData>false</cacheUserData>
            <authMode>user</authMode>
            <EAPConfig>
              <EapHostConfig     xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
                <EapMethod>
                  <Type xmlns="http://www.microsoft.com/provisioning/EapCommon">13</Type>
                  <VendorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorId>
                  <VendorType xmlns="http://www.microsoft.com/provisioning/EapCommon">0</VendorType>
                  <AuthorId xmlns="http://www.microsoft.com/provisioning/EapCommon">0</AuthorId>
                </EapMethod>
                <Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
                  <Eap xmlns="http://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1">
                    <Type>13</Type>
                    <EapType xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1">
                      <CredentialsSource>
                        <CertificateStore>
                          <SimpleCertSelection>true</SimpleCertSelection>
                        </CertificateStore>
                      </CredentialsSource>
                      <ServerValidation>
                        <DisableUserPromptForServerValidation>false</DisableUserPromptForServerValidation>
                        <ServerNames></ServerNames>
                      </ServerValidation>
                      <DifferentUsername>false</DifferentUsername>
                      <PerformServerValidation xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</PerformServerValidation>
                      <AcceptServerName xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName>
                      <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">
                        <FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3">
                          <AllPurposeEnabled>true</AllPurposeEnabled>
                          <CAHashList Enabled="true">
                            <IssuerHash>75 f5 06 9c a4 12 0e 9b db bc a1 d9 9d d0 f0 75 fa 3b b8 78 </IssuerHash>
                          </CAHashList>
                          <EKUMapping>
                            <EKUMap>
                              <EKUName>Client Authentication</EKUName>
                              <EKUOID>1.3.6.1.5.5.7.3.2</EKUOID>
                            </EKUMap>
                          </EKUMapping>
                          <ClientAuthEKUList Enabled="true"/>
                          <AnyPurposeEKUList Enabled="false">
                            <EKUMapInList>
                              <EKUName>Client Authentication</EKUName>
                            </EKUMapInList>
                          </AnyPurposeEKUList>
                        </FilteringInfo>
                      </TLSExtensions>
                    </EapType>
                  </Eap>
                </Config>
              </EapHostConfig>
            </EAPConfig>
          </OneX>
        </security>
      </MSM>
    </WLANProfile>
```

## Create the XML file from an existing Wi-Fi connection

You can also create an XML file from an existing Wi-Fi connection. On a Windows computer, use the following steps:

1. Create a local folder for the exported W-Fi- profiles, such as c:\WiFi.
2. Open up a command prompt as an administrator (right-click `cmd` > **Run as administrator**).
3. Run `netsh wlan show profiles`. The names of all the profiles are listed.
4. Run `netsh wlan export profile name="YourProfileName" folder=c:\Wifi`. This command creates a file named `Wi-Fi-YourProfileName.xml` in c:\Wifi.

    - If you're exporting a Wi-Fi profile that includes a preshared key, add `key=clear` to the command:
  
        `netsh wlan export profile name="YourProfileName" key=clear folder=c:\Wifi`

        `key=clear` exports the key in plain text, which is required to successfully use the profile.

    - If the exported Wi-Fi profile `<name></name>` element includes a space, then it might return a `ERROR CODE 0x87d101f4 ERROR DETAILS Syncml(500)` error when assigned. When this issue happens, the profile is listed in `\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces`, and shows as a known network. But, it doesn't successfully display as managed policy in the "Areas managed by..." URI.

      To resolve this issue, remove the space.

After you have the XML file, copy and paste the XML syntax into OMA-URI settings > **Data type**. [Create a custom profile](#create-a-custom-profile) (in this article) lists the steps.

> [!TIP]
> `\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces\{guid}` also includes all the profiles in XML format.

## Best practices

- Before you deploy a Wi-Fi profile with PSK, confirm that the device can connect to the endpoint directly.

- When rotating keys (passwords or passphrases), expect downtime and plan your deployments. Consider pushing new Wi-Fi profiles during non-working hours. Also, warn users that connectivity may be affected.

- For a smooth transition, be sure the end user's device has an alternate connection to the Internet. For example, the end user can switch back to Guest WiFi (or some other WiFi network) or have cellular connectivity to communicate with Intune. The extra connection allows the user to receive policy updates when the corporate WiFi Profile is updated on the device.

## Next steps

Be sure to [assign the profile](device-profile-assign.md), and [monitor](device-profile-monitor.md) its status.
