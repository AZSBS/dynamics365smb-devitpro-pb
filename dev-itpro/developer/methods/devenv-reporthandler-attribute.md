---
title: "ReportHandler Attribute"
ms.custom: na
ms.date: 08/26/2019
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: jswymer
---

# ReportHandler Attribute

Specifies that the method is a ReportHandler method.

## Applies To  
AL methods on test codeunits. A test codeunit is a codeunit that has the [SubType Property](../properties/devenv-subtype-property.md) set to **Test**. 

## Syntax  
  
```  
[ReportHandler]
procedure ReportHandler(var Report: Report);
```    

## Remarks

The **ReportHandler** method is called when a report is invoked in the code.

The **ReportHandler** attribute requires that the method where it is applied has the signature `ReportHandler(var Report: Report)`. The parameter variable, *Report*, is the specific report in this case.

## See Also  
[Method Attributes](devenv-method-attributes.md)  
[Test Codeunits and Test Functions](../devenv-test-codeunits-and-test-methods.md)
