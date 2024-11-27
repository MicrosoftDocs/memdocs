---

# required metadata

title: Microsoft Intune App SDK for iOS developer guide - Web-view features
description: The Microsoft Intune App SDK for iOS lets you incorporate Intune app protection policies (also known as APP or MAM policies) into your native iOS app. Web-view features
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/31/2024
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

# Intune App SDK for iOS - Web-view features

## Displaying web content within an application

In iOS, web views can be used to surface a wide variety of web content without having to leave the context of the app. Some applications might also use web views as a way of sharing features and UI across multiple platforms.

Because web views exist within the app, they expose it to potential data leaks. If a user is able to navigate to arbitrary external web pages within an app (either through intentional app design or by clever maneuvering through exposed links in the rendered web page's html content), then the user may be able to leak managed data from the app. 

The Intune MAM SDK provides several APIs for handling different scenarios where both managed and unmanaged content are surfaced through web views within an app. **These APIs only need to be called if there is a managed user signed into the app.** Please see the table below as a quick guide on which API applies to which scenario. 

| Scenario | APIs |
| - | - |
| Only user and organizational content with no risk of arbitrary web pages | No APIs needed |
| Only non-user and non-organizational content | Set `TreatAllWebViewsAsUnmanaged` in the `Info.plist` |
| A mix of user/organizational and non-user/non-organizational content (majority non-user/non-organizational) | Set `TreatAllWebViewsAsUnmanaged` in the `Info.plist` and use `setWebViewPolicy:forWebViewer:` with `IntuneMAMWebViewPolicyCurrentIdentity` on web views that contain user or organizational data |
| A mix of user/organizational and non-user/non-organizational content (majority user/organizational) | Only use `setWebViewPolicy:forWebViewer:` with `IntuneMAMWebViewPolicyUnmanaged` on web views that don't contain user or organizational data |
| User or organizational content but with a risk of arbitrary web pages | Following suitable usage of `TreatAllWebViewsAsUnmanaged` and `setWebViewPolicy:forWebViewer:`, also implement the `IntuneMAMWebViewPolicyDelegate` for web views that might navigate to arbitrary web pages |

### Web View Scenario 1: Only web pages that display user or organizational content
If an app only uses web views as a way of rendering user or organizational content and there's no risk of the web view navigating to arbitrary external web pages, then there's no need to use any of the APIs or settings. By default, the SDK will treat any web view surfaced within the app as content belonging to the current UI policy identity.

If a managed user opens a web view within an app, any cut/copy data from the web view will be treated as managed content. Pasting into the web view will be treated according to the managed account's policies.

If an unmanaged user opens a web view within an app, any cut/copy data from the web view will be treated as unmanaged content. Pasting into the web view will be treated as if done by the unmanaged account and no additional restrictions will be imposed.

### Web View Scenario 2: Only web pages that don't display user or organizational content

If an app knows that it will never display user or organizational content within a web view, then it can set `TreatAllWebViewsAsUnmanaged` to `YES` in the app's `Info.plist`. This will treat all cut, copy, and paste actions done by any user within a web view as unmanaged. Regardless of the management status of the account used to perform the actions, the action will be treated as if performed by an unmanaged user.

Doing so will ensure that managed app content isn't leaked outside the app through the web view. Setting this flag would be a good idea if an app only uses web views to display privacy notices, EULAs, or other static page content that doesn't require a user to view it.

When `TreatAllWebViewsAsUnmanaged` is set, all content displayed within the web views **can** be copied and pasted to other unmanaged apps since the web views themselves are considered unmanaged.

### Web View Scenario 3: A mix of user/organizational and non-user/non-organizational content

More complex apps might use a combination of user/organizational and non-user/non-organizational web views. An app might use web views to display privacy notices but also use web views to surface user content. In this case, the `IntuneMAMPolicyManager`'s `setWebViewPolicy:forWebViewer:` API can be used. This API allows an app to mark individual web views as unmanaged or undo the effect of `TreatAllWebViewsAsUnmanaged` for individual web views.

The API takes two arguments. The first is an enum value of `IntuneMAMWebViewPolicy` type. The second can be either a UIView or UIViewController that may contain a WKWebView in its child view hierarchy. A WKWebView itself can also be passed in directly as the second argument. 

If the WKWebView is a child of the UIView or UIViewController passed in as the second argument, it does not have to exist within the view hierarchy at the time this API is called. Any child WKWebViews of the passed in UIView or UIViewController will have the proper policy applied when they are added.

- `IntuneMAMWebViewPolicyUnset` - This is the default policy for all WKWebViews. Web views will be treated according to only the `TreatAllWebViewsAsUnmanaged` flag.
- `IntuneMAMWebViewPolicyUnmanaged` - Any cut/copy/paste actions performed by a user on a web view tagged with this policy will be treated as if performed by an unmanaged identity. This policy will overwrite the `TreatAllWebViewsAsUnmanaged` flag.
- `IntuneMAMWebViewPolicyCurrentIdentity` - Any cut/copy/paste actions performed by a user on a web view tagged with this policy will be treated as if performed by the current UI policy identity. This policy will overwrite the `TreatAllWebViewsAsUnmanaged` flag.

#### Majority non-user and non-organizational data

If a majority of the web views within an app display unmanaged content, then `TreatAllWebViewsAsUnmanaged` can be set in the app's `Info.plist` and `setWebViewPolicy:forWebViewer:` with `IntuneMAMWebViewPolicyCurrentIdentity` can be called on the user or organizational content web views.

#### Majority user and organizational data

If a majority of the web views within an app display user or organizational content, then only `setWebViewPolicy:forWebViewer:` with `IntuneMAMWebViewPolicyUnmanaged` needs to be called on the unmanaged web views since all web views are treated as managed by default.

### Web View Scenario 4: User or organizational content but with a risk of arbitrary web pages

If a web view is used to display user or organizational content but has a risk of navigating to arbitrary external URLs, then an additional API can be used in combination with `TreatAllWebViewsAsUnmanaged` and `setWebViewPolicy:forWebViewer:`. Examples of this are Suggest a Feature or Feedback webpages that have either direct or indirect links to a search engine.

`IntuneMAMWebViewPolicyDelegate` can be implemented and set to a web view using `IntuneMAMPolicyManager`'s `setWebViewPolicyDelegate:forWebViewer:`. The `IntuneMAMWebViewPolicyDelegate` has one required method, `isExternalURL:`.

The `setWebViewPolicyDelegate:forWebViewer:` method must be called directly on a WKWebView or SFSafariViewController.

Each time the web view navigates to a new page, the `isExternalURL:` delegate method will be called. Applications should determine if the URL passed to the delegate method represents an internal website where user or organizational data can be pasted in or an external website that could leak organizational data. Returning `NO` will tell the SDK that the website being loaded is an organizational location where user or organizational data can be shared. Returning `YES` will cause the SDK to open the URL in a managed browser rather than the WKWebView or SFSafariViewController if current policy settings require it. This will ensure that no user or organizational data from within the app can be leaked to the external website.


### Web View APIs Example

An app is built with five web views (A, B, C, D, and E). Web views A, B, and C don't display user or organizational data. Web view D displays an organization page available to all users of the company. Web view E renders the user's documents which may contain links.

Since the majority of web views are unmanaged (A, B, and C), we can set `TreatAllWebViewsAsUnmanaged` to reduce the number of times we need to call `setWebViewPolicy:forWebViewer:`.

Since web views D and E display user content and all web views are unmanaged by default now, we need to tag them with `setWebViewPolicy:forWebViewer:` using `IntuneMAMWebViewPolicyCurrentIdentity`.

Because web view E contains links that the user might click on and could use to navigate to arbitrary URLs, we also need to implement the `IntuneMAMWebViewPolicyDelegate` and set it to web view E using `setWebViewPolicyDelegate:forWebViewer:`. In our `isExternalURL:` implementation, we could check incoming URLs and see if they are the same as the URL for the document. If they don't match, then we know it's an external URL and can return `YES`. If they do match, then we know it's an internal URL and can return `NO`.

Implementing and calling these APIs means that managed user or organizational content can't leak to web views A, B, and C. It also means that managed content can't leak to any external URLs that the user might navigate to in E by clicking on links within documents. Managed content will also be protected by preventing the data from web views D and E from leaking outside the app.

## SwiftUI Support

A newly created SwiftUI app supports UIScenes but doesn't have a UISceneDelegate implemented by default. If your app intends to support UIScenes and use the Intune App SDK, then it's required to implement a UISceneDelegate. If it doesn't intend to support UIScenes, the `UIApplicationSceneManifest` (also named "Application Scene Manifest") setting in the app's Info.plist must be removed.