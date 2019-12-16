---
title: "RecallNotificationHandler Attribute"
ms.custom: na
ms.date: 08/26/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: jswymer
---

# RecallNotificationHandler Attribute

Specifies that the method is a RecallNotificationHandler method.

## Applies To  
AL methods on test codeunits. A test codeunit is a codeunit that has the [SubType Property](../properties/devenv-subtype-property.md) set to **Test**. 

## Syntax  
  
```  
[RecallNotificationHandler]
procedure RecallNotificationHandler(var Notification: Notification): Boolean;
```    

## Remarks

The **RecallNotificationHandler** method is called when a notification is recalled from the code.

The **RecallNotificationHandler** attribute requires that the method where it is applied has the signature `RecallNotificationHandler(var Notification: Notification): Boolean`. The parameter variable, *Notification*, holds the actual notification.

## See Also  
[Method Attributes](devenv-method-attributes.md)  
[Test Codeunits and Test Functions](../devenv-test-codeunits-and-test-methods.md)