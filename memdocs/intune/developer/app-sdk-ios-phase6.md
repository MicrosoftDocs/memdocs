---
# required metadata

title: Microsoft Intune App SDK for iOS developer guide - App Protection CA support (optional)
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. App Protection CA support (optional)
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/18/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.assetid: 8e280d23-2a25-4a84-9bcb-210b30c63c0b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: has-adal-ref
ms.collection:
- tier2
- M365-identity-device-management
- iOS/iPadOS
---

# Intune App SDK for iOS - App Protection CA support (optional)

App Protection Conditional Access blocks access to server tokens until Intune has confirmed app protection policy has been applied. This feature requires changes to your add user flows. Once a customer enables App Protection CA, applications in that customer's tenant that access protected resources won't be able to acquire an access token unless they support this feature.

> [!NOTE]
> This guide is divided into several distinct stages. Start by reviewing [Stage 1: Plan the Integration].

## Stage 6: App Protection CA support

## Stage Goals

- Learn about different APIs that can be used to support App Protection Conditional Access within iOS app
- Integrate App Protection Conditional Access to your app and users.
- Test the above integration with your app and users.

### Dependencies
In addition to the Intune SDK, you need these two components to enable App Protection CA in your app.

1. iOS Authenticator app
2. MSAL authentication library 1.0 or greater

### MAM-CA remediation flow

:::image type="content" alt-text="Diagram of MAM-CA remediation flow." source="./media/app-sdk-ios/app-ca-flow.png" lightbox="./media/app-sdk-ios/app-ca-flow.png":::

### New APIs
Most of the new APIs can be found in the IntuneMAMComplianceManager.h. The app needs to be aware of three differences in behavior explained below.

New behavior	| Description	|
--	| --	|
App → ADAL/MSAL: Acquire token	| When an application tries to acquire a token, it should be prepared to receive a ERROR_SERVER_PROTECTION_POLICY_REQUIRED. The app can receive this error during their initial account add flow or when accessing a token later in the application lifecycle. When the app receives this error, it won't be granted an access token and needs to be remediated to retrieve any server data.	|
App → Intune SDK: Call remediateComplianceForIdentity	| When an app receives a ERROR_SERVER_PROTECTION_POLICY_REQUIRED from ADAL, or MSALErrorServerProtectionPoliciesRequired from MSAL it should call [[IntuneMAMComplianceManager instance] remediateComplianceForIdentity] to let Intune enroll the app and apply policy. The app may be restarted during this call. If the app needs to save state before restarting, it can do so in restartApplication delegate method in IntuneMAMPolicyDelegate. <br><br>remediateComplianceForIdentity provides all the functionality of registerAndEnrollAccount and loginAndEnrollAccount. Therefore, the app doesn't need to use either of these older APIs.	|
Intune → App: Delegate remediation notification	|After Intune has retrieved and applied policies, it notifies the app of the result using the IntuneMAMComplianceDelegate protocol. Refer to IntuneMAMComplianceStatus in IntuneComplianceManager.h for information on how the app should handle each error. In all cases except IntuneMAMComplianceCompliant, the user won't have a valid access token. <br><br>If the app already has managed content and isn't able to enter a compliant status, the application should call selective wipe to remove any corporate content. <br><br>If we can't reach a compliant state, the app should display localized the error message and title string supplied by withErrorMessage and andErrorTitle.	|

Example for hasComplianceStatus method of IntuneMAMComplianceDelegate

```objc
(void) accountId:(NSString*_Nonnull) accountId hasComplianceStatus:(IntuneMAMComplianceStatus) status withErrorMessage:(NSString*_Nonnull) errMsg andErrorTitle:(NSString*_Nonnull) errTitle
{
    switch(status)
    {
        case IntuneMAMComplianceCompliant:
        {
            /*
            Handle successful compliance
            */
            break;
        }
        case IntuneMAMComplianceNotCompliant:
        case IntuneMAMComplianceNetworkFailure:
        case IntuneMAMComplianceUserCancelled:
        case IntuneMAMComplianceServiceFailure:
        {
            UIAlertController* alert = [UIAlertController alertControllerWithTitle:errTitle
            message:errMsg
            preferredStyle:UIAlertControllerStyleAlert];
            UIAlertAction* defaultAction = [UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleDefault
            handler:^(UIAlertAction * action) {exit(0);}];
            [alert addAction:defaultAction];
            dispatch_async(dispatch_get_main_queue(), ^{
            [self presentViewController:alert animated:YES completion:nil];
            });
            break;
        }
        case IntuneMAMComplianceInteractionRequired:
        {
            [[IntuneMAMComplianceManager instance] remediateComplianceForAccountId:accountId silent:NO];
            break;
        }
    }
}
```

```swift
func accountId(_ accountId: String, hasComplianceStatus status: IntuneMAMComplianceStatus, withErrorMessage errMsg: String, andErrorTitle errTitle: String) {
        switch status {
        case .compliant:
           //Handle successful compliance
        case .notCompliant, .networkFailure,.serviceFailure,.userCancelled:
            DispatchQueue.main.async {
              let alert = UIAlertController(title: errTitle, message: errMsg, preferredStyle: .alert)
                alert.addAction(UIAlertAction(title: "OK", style: .default, handler: { action in
                    exit(0)
                })) 
                self.present(alert, animated: true, completion: nil) 
            }
        case .interactionRequired:
            IntuneMAMComplianceManager.instance().remediateCompliance(forAccountId: accountId, silent: false)
   }
```

### MSAL/ADAL
Apps need to indicate support for App Protection CA by adding client capabilities variable to their MSAL/ADAL configuration.
The following values are required:   claims = {"access_token":{"xms_cc":{"values":["protapp"]}}} 

[MSALPublicClientApplicationConfig Class Reference (azuread.github.io)](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fazuread.github.io%2Fmicrosoft-authentication-library-for-objc%2FClasses%2FMSALPublicClientApplicationConfig.html%23%2Fc%3Aobjc(cs)MSALPublicClientApplicationConfig(py)clientApplicationCapabilities&data=04%7C01%7CJamie.Silvestri%40microsoft.com%7C9b7fffa9a0e14b82cf1a08d8bcc1f11e%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637466888444795023%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=NNYF4cvojrG67BGNMPZdY2dGyATZHkVsYa5vzENWwHk%3D&reserved=0)

```objc
    MSALAADAuthority *authority = [[MSALAADAuthority alloc] initWithURL:[[NSURL alloc] initWithString:IntuneMAMSettings.aadAuthorityUriOverride] error:&msalError];
    MSALPublicClientApplicationConfig *config = [[MSALPublicClientApplicationConfig alloc]
                                                 initWithClientId:IntuneMAMSettings.aadClientIdOverride
                                                 redirectUri:IntuneMAMSettings.aadRedirectUriOverride
                                                 authority:authority];

    /*
     IF YOU'RE IMPLEMENTING CA IN YOUR APP, PLEASE PAY ATTENTION TO THE FOLLOWING...
    */
    // This is needed for CA!
    // This line adds an option to the MSAL token request so that MSAL knows that CA may be active
    // Without this, MSAL won't know that CA could be activated
    // In the event that CA is activated and this line isn't in place, the auth flow will fail

    config.clientApplicationCapabilities = @[@"protapp"];
```

```swift
guard let authorityURL = URL(string: kAuthority) else {
            print("Unable to create authority URL")
            return
        }
         let authority = try MSALAADAuthority(url: authorityURL)
         let msalConfiguration = MSALPublicClientApplicationConfig(clientId: kClientID,redirectUri: kRedirectUri,
                                                                  authority: authority)
        msalConfiguration.clientApplicationCapabilities = ["ProtApp"]
        self.applicationContext = try MSALPublicClientApplication(configuration: msalConfiguration)

```
To fetch the Microsoft Entra object ID for the accountId parameter of the MAM SDK compliance remediation APIs, you need to do the following steps:
- First get the homeAccountId from userInfo[MSALHomeAccountIdKey] within MSALError object sent back by MSAL when it reports ERROR_SERVER_PROTECTION_POLICY_REQUIRED to the app.
- This homeAccountId is in the format ObjectId.TenantId. Extract the ObjectId value by splitting the string on the '.' and then use that value for the accountId parameter in remediation API remediateComplianceForAccountId.

### Exit criteria

#### Configuring a test user for App Protection CA

1. Sign in with your administrator credentials to https://portal.azure.com.
2. Select **Microsoft Entra ID** > **Security** > **Conditional Access** > **New policy**. Create a new conditional access policy.
3. Configure conditional access policy by setting the following items:
    - Filling in the **Name** field.
    - Enabling the policy.
    - Assigning the policy to a user or group.
4. Assign cloud apps. Select **Include** > **All cloud apps**. As the warning notes, be careful not to misconfigure this setting. For example, if you excluded all cloud apps, you would lock yourself out of the console.
5. Grant access controls by selecting **Access Controls** > **Grant Access** > **Require app protection policy**. 
6. When you're finished configuring the policy, select **Create** to save the policy and apply it.
7. Enable the policy.
8. You also need to make sure that the users are targeted for MAM policies.

#### Test cases
Test Case	| How to test	|	Expected Outcome	|
--	| --	| --	|
MAM-CA always applied		| Ensure the user is targeted for both App Protection CA and MAM policy before enrolling in your app.|  Verify that your app handles the remediation cases described above and the app can get an access token.	|
MAM-CA applied after user enrolled	| The user should be logged into the app already, but not targeted for App Protection CA.	| Target the user for App Protection CA in the console and verify that you correctly handle MAM remediation	|
MAM-CA noncompliance	| Set up an App Protection CA policy, but don't assign a MAM policy.	| The user shouldn't be able to acquire an access token. This is useful for testing how your app handles IntuneMAMComplianceStatus error cases.	|

## Next Steps

After you've completed all the [Exit Criteria] above, your app is now successfully integrated with App Protection CA support. The subsequent section, [Stage 7: Web-view features], may or may not be required, depending on your app's desired app protection policy support.

<!-- Stage 6 links -->
[Exit Criteria]:#exit-criteria
[Stage 1: Plan the Integration]:app-sdk-ios-phase1.md
[Stage 7: Web-view features]:app-sdk-ios-phase7.md
