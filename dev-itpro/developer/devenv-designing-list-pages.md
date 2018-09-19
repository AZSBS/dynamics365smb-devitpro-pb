---
title: Designing List Pages for Business Central
description: "Provides and overview of List page design"
author: jswymer
ms.custom: na
ms.date: 01/19/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: jswymer
---

[!INCLUDE[newdev_dev_preview](includes/newdev_dev_preview.md)]

# Designing List Pages for [!INCLUDE[d365fin_web_md](includes/d365fin_web_md.md)]

The *List* page type displays records from an underlying table in rows and columns. 

## About the list page

You design list pages when you want to provide users with a collection of data, enabling them to get an overview of and find entities to work with, such as customer, vendors, or sales orders. Typically, a list page will in-turn link to an associated card page that lets users view or modify specific entities in the list.

There are different ways to incorporate a list page into that application, depending on what you want to achieve: 

- Make the list page available from the navigation of a Role Center page. This gives users quick access to the page. With this implementation, the list page opens in the content area of the Role Center page, where the Role Center's navigation area is still present and accessible at the top of the page. For more information about Role Centers, see [Designing Role Centers](devenv-designing-role-centers.md).
- Make the list available from an action on another page. With this implementation, the list page opens in a separate window in front of the current page.
- Make the list page searchable in **Tell me what you want to do**. With this implementation, the list page also opens in a separate window.

### Customizing a list pages from the client
In the client, users can personalize list pages by rearranging or hiding records or FactBoxes as they like. For more information, see [Personalizing Your Workspace](https://docs.microsoft.com/en-us/dynamics365/business-central/ui-personalization-user). 

As a developer or administrator, you can use Designer to customize list page the same way that individual users personalize their own workspaces. The difference is that changes you make are applied to all users assigned to the same profile. For more information, see [Using Designer](devenv-inclient-designer.md). 

## List page definition and structure

### General definition
A list page is defined by page that has the [PageType property](properties/devenv-pagetype-property.md) set to `List`, and [SourceTable property](properties/devenv-sourcetable-property.md) set to the table object that contains the records that you want to display.

A list page will typically be associated with a card page, which  enables users to view and modify records in the list or create a new record. You make this association by setting the [CardPageId](properties/devenv-cardpageid-property.md) property of the list page.

For a simple code example of a list page, see [Simple List Page Example](devenv-simple-list-page-example.md) 
 
### Structure

The following figure illustrates the general layout and elements of a list page.

![List page overview](media/list-page-overview-v2.png "List page overview")

The following table describes the elements of a typical list page.


|    |Area|Description|Usage Guidelines|
|----|-------|-----------|----------------|
|1|List|Displays records of the source table as rows and columns, where each row is a record and the columns are the fields. You define the list by adding a `repeater` control in the page code, and then in the `repeater` control, you add `field` control for field that you wan tot display.||
|2|Tile view|The tile view renders records in a list as tiles (or bricks). All lists can be displayed as tiles, however, if you want to give users the option of displaying a list as tiles, you must specify the table fields that you want to include in the tiles. You do this by adding a `fieldgroup(Brick; <Field>` keyword in the code of the source table.<br /><br /> For more information, see [Field Groups](devenv-field-groups.md).|The tile view is particularly beneficial for lists with records that include media or images, such a customers, contacts, and items lists. For more information about adding media to records, see [Working With Media on Records](devenv-working-with-media-on-records.md).|
|3|Action bar|The action bar provides links to other pages, reports, and codeunits. The action bar is defined by an `actions` control in the page code, and individual actions are defined by an `action` control.<br /><br /> Actions can be displayed on three standard menus in the action bar, **Actions**, **Navigate**, and **Report**, or in promoted action menus, which are custom menus that you define. The action can be displayed in the root-level of each menu or grouped in a submenu.<br /><br /> The objects targeted by these links will open in a separate window.<br /><br />For more information, see [Adding Actions to a Page](devenv-adding-actions-to-a-page.md).|The action bar is designed for running the most important or most often used tasks and operations required by users. Actions will typically target card type pages that enable users to create new entities, such as customers, invoices, and sales orders, or run reports. Place the most important action at the root-level, and group closely related actions in a sub-menu.|
|4|Promoted action menus|Promoted actions are actions that are set up on the **Actions**, **Navigate**, or **Report** menus in the action bar, but are also configured to display on a higher level, in a specific category (menu) that you define. You promote actions by setting various properties on `action` controls.<br /><br /> For more information, see [Promoted Actions](devenv-promoted-actions.md). |Use promoted actions provide quick access to the most common tasks that would be performed by the user. Give categories a name that provides a good description of the included actions.|
|5|FactBox|A FactBox is located on the right-most side of a page and it is divided into one or more parts that are arranged vertically. You use this area to display content including other pages, charts, and system parts such as Microsoft Outlook, Notes, and Record Links.<br /><br />  For more information, see [Adding a FactBox to a Page](devenv-adding-a-factbox-to-page.md).|Typically, you can use a FactBox to display information that is related to an item on the main content page. For example, on a page that shows a sales order list, you can use a FactBox to show sell-to customer sales history for a selected sales order in the list.|



<!--
|||`area(creation)` - Actions in this control will appear first in the action area, and will display with a plus (+) icon. |Use this control to target pages that enable the user to create new entities.|
|||`area(processing)` - Actions in this control will appear after the `area(creation)` items. You can group actions in submenus by using a `group` control.|Use this control to target pages that are associated with the work flow for processing documents, such as payments or sales orders. Use the `group` control to organize similar actions under a common parent.|
|||`area(reporting)` - Actions in this control will appear last in the action area. They display with a default report icon. |Use this control to target report objects.|
|2|List|Displays records of source table as rows and columns, where each column is a field from the table. The list is defined by using a  `repeater()` control in the `area(content)` control. Columns are defined by the `field(Name; Field)` keyword that specifies the caption and the field from the underlying table.||-..nl

For more information about navigation, see [Adding to Navigation](devenv-adding-menus-to-navigation-pane.md). -->


## Behavioral points of interest
- List pages that are accessed from the Role Center page are open embedded within the Role Center framework. The pages are always opened in the read-only mode, regardless of the [Editable](properties/devenv-editable-property.md) property.
- There are a few system actions that are automatically added to the actions bar, such as **See Attached** and **Open in Excel**.
- The dynamic caption is automatically displayed  
- Media and image fields only display in tile view.  

## Development tips for page design

From the user’s perspective, the following are qualities of a well-designed list page does the following:

-  Displays a single collection of entities or entries that the user needs for their work. 
-  Includes page title that clearly identifies the collection and any specific view that is in effect.
-  Places the most important columns first, and enable a freeze column, so scrolling is not typically necessary. 
-  The page is accessible from relevant actions on the Role Center page.
-  Includes one or two FactBoxes to give necessary statistics and quick access to related documents.
- The most typical actions for users of the page are promoted.

## Design for all display targets

-   Mobile devices will display the same content as the [!INCLUDE[d365fin_web_md](includes/d365fin_web_md.md)], but it is presented in different way to suit how users hold and interact with their mobile device.
-   You can preview how your Role Center will look on mobile devices directly in Designer.
-  Some limitations on mobile devices include the following:


## See Also
[AL Development Environment](devenv-reference-overview.md)  
[Page Extension Object](devenv-page-ext-object.md)  
[Actions Overview](devenv-actions-overview.md)  
[Adding Pages and Reports to Search](devenv-al-menusuite-functionality.md)  
[Personalizing Your Workspace](https://docs.microsoft.com/en-us/dynamics365/business-central/ui-personalization-user)  
[Using Designer](devenv-inclient-designer.md)  