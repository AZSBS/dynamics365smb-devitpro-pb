---
title: "AdditionalSearchTerms Property"
description: "Describes the AdditionalSearchTerms Property in AL."
author: jswymer
ms.custom: na
ms.date: 01/15/2019
ms.reviewer: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: jswymer
---

# AdditionalSearchTermsML Property

Specifies search terms (words and phrases) for the page or report in different languages. In addition to the caption of the page or report, the terms are used by the search feature (**Tell me**) in the Web client and mobile apps. 

> [!NOTE] 
> The support for using the ML properties is being deprecated, so it is recommended to refactor your extension to use the corresponding [AdditionalSearchTerms property](devenv-additionalsearchterms-property.md), which is being picked up in the .xliff file. For more information, see [Working with Translation Files](../devenv-work-with-translation-files.md).

## Syntax

```
AdditionalSearchTermsML = <language ID> = '<term>[,<term>]'[, <language ID> = '<term>[,<term>]'];
```

## Applies to

- Page objects
- Report objects

## Property Values

|Value           |Description                                  |
|----------------|---------------------------------------------|
|`<language ID>`   |The standard Windows three-letter language ID, such as ENU or DAN. Separate each language by a comma.|
|`<term>`  |The search word or phrase, which can consist of letters, numbers and special characters. Separate each term by a comma.|

## Remarks

For [!INCLUDE[prodshort](../includes/prodshort.md)] on-premises, the [!INCLUDE[webserverinstance](../includes/webserverinstance.md)] configuration file (navsettings.json) includes a setting called `UseAdditionalSearchTerms` that enables or disables the use of additional search terms by the **Tell me**. For more information, see [](../../administration/configure-web-server.md).

## Dependent Properties

The [UsageCategory property](devenv-usagecategory-property.md) must be set to a value other than `None` in order for the page to be searchable by **Tell me**. 

## Example

The following code snippet uses the **AdditionalSearchTermsML** property to add search terms in English and Danish to a list page whose caption is **Items**.

```
page 50101 SearchTestML
{
    PageType = List;
    ApplicationArea = All;
    SourceTable = Item;
    UsageCategory = Lists;
    CaptionMl = ENU = 'Items, DAN ='Varer';
    AdditionalSearchTermsML = ENU = 'product, merchandise', DAN = 'produkter';
    ...
}
```

## See Also

[Adding Pages and Reports to Tell me](../devenv-al-menusuite-functionality.md)  
[Properties](devenv-properties.md)  
[Page Object](../devenv-page-object.md)  
[Report Object](../devenv-report-object.md)  
