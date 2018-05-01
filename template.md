---
title: [ARTICLE TITLE in 35 chars or less]
titleSuffix: Configuration Manager
description: 
ms.date: mm/dd/yyyy
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.assetid: [GET ONE FROM guidgenerator.com]
author: [GITHUB USERNAME]
ms.author: [ALIAS]
manager: [ALIAS]
---

# Metadata and Markdown Template

This docs.ms template contains examples of markdown syntax, as well as guidance on setting the metadata. It is available in the root directory of each EM Pilot repository (e.g. ~/Azure-RMSDocs-pr
/template.md) and is meant to be read as a markdown file, although you can refer to [the published version](https://stage.docs.microsoft.com/en-us/rights-management/template) to see how the markdown examples rendeer.

When creating a markdown file you should copy the template to a new file, fill out the metadata as specified below, set the H1 heading above to the title of the article, and delete the content.


## Metadata

The full metadata block is above, divided into required fields and optional fields; see the [OPS metadata cheatsheet](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) for more details. Some key notes:

- You **must** have a space between the colon (:) and the value for a metadata element.
- If an optional metadata element does not have a value, comment out the element with a # (do not leave it blank or use "na"); if you are adding a value to an element that was commented out, be sure to remove the #.
- Colons in a value (e.g., a title) break the metadata parser. In their place, use the HTML encoding of &#58; (e.g., "title: Azure Rights Management&#58; the basics | Azure RMS").
- **title**: This title will appear in search engine results. The title should end with a pipe (|) followed by the name of the service (e.g. see above). The title need not (and probably should not) be identical to the title in your H1 heading. It should be roughly 65 characters (including | SERVICE NAME)
- **author**, **manager**, **reviewer**: The author field should contain the **Github username** of the author, not their alias.  The "manager" and "reviewer" fields, on the other hand, should contain aliases. ms.reviewer specifies the name of the PM associated with the article or service.
- **ms.assetid**: This is the GUID of the article from CAPS. When creating a new markdown file, get a GUID from [https://www.guidgenerator.com](https://www.guidgenerator.com).
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: Possible values for these elements can be found [here](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## Basic Markdown and GFM

All basic and Github-flavored markdown is supported. For more information on these, see:

- [Baseline markdown syntax](https://daringfireball.net/projects/markdown/syntax)
- [Github-flavored markdown (GFM) documentation](https://guides.github.com/features/mastering-markdown)

## Headings

Examples of first- and second-level headings are above.

There **must** be only one first-level heading in your topic, which will be displayed as the on-page title.  

Second-level headings will generate the on-page TOC that appears in the "In this article" section underneath the on-page title.

### Third-level heading
#### Fourth-level heading
##### Fifth level heading
###### Sixth-level heading

## Text styling

*Italics*

**Bold**

~~Strikethrough~~



## Links

To link to a markdown file in the same repo, use [relative links](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Example: [What is Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

To link to a header in the same markdown file, view the source of the published article, find the id of the head (e.g. `id="blockquote"`, and link using # + id (e.g. `#blockquote`).

- Example: [Blockquotes](#blockquote)

To link to a header in a markdown file in the same repo, use relative linking + hashtag linking.

- Example: [technical overiew of the sign-up process](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

To link to an external file, use the full URL as the link.

- Example: [Github](http://www.github.com)

If a URL appears in a markdown file, it will be transformed into a clickable link.

- Example: http://www.github.com

## Lists

### Ordered lists

1. This
1. Is
1. An
1. Ordered
1. List  


#### Ordered list with an embedded list

1. Here
1. comes
1. an
1. embedded
    1. Miss Scarlett
    1. Professor Plum
1. ordered
1. list


### Unordered Lists

- This
- is
- a
- bulleted
- list


##### Unordered list with an embedded lists

- This
- bulleted
- list
    - Mrs. Peacock
    - Mr. Green
- contains  
- other
    1. Colonel Mustard
    1. Mrs. White
- lists


## Horizontal rule

---

## Tables

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| col 1 is default | left-aligned     |    $1 |


## Code

### Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### In-line code

This is an example of `in-line code`.

## Blockquotes

> The drought had lasted now for ten million years, and the reign of the terrible lizards had long since ended. Here on the Equator, in the continent which would one day be known as Africa, the battle for existence had reached a new climax of ferocity, and the victor was not yet in sight. In this barren and desiccated land, only the small or the swift or the fierce could flourish, or even hope to survive.

## Images

### Static Image

![this is the alt text](./media/AzRMS_elements.png)

### Linked Image

[![alt text for linked image](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### Animated gif

![animated gif](./media/hololens.gif)

## Alerts

### Note

> [!NOTE]
> This is NOTE

### Warning

> [!WARNING]
> This is WARNING

### Tip

> [!TIP]
> This is TIP

### Important

> [!IMPORTANT]
> This is IMPORTANT

## Videos

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## docs.ms extentions

### Button

> [!div class="button"]
[button links](/rights-management)

### Selector

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### Step-By-Step

>[!div class="step-by-step"]
[Pre](https://www.example.com)
[Next](https://www.example.com)
