---
title: "FindNextField Method"
ms.author: solsen
ms.custom: na
ms.date: 09/28/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: solsen
---
[//]: # (START>DO_NOT_EDIT)
[//]: # (IMPORTANT:Do not edit any of the content between here and the END>DO_NOT_EDIT.)
[//]: # (Any modifications should be made in the .resx files in the ModernDev repo.)
# FindNextField Method
Finds the next field in the data set that is displayed on a test page.

## Syntax
```
[Ok := ]  TestPart.FindNextField(Field: TestField, Value: Any)
```
## Parameters
*TestPart*  
&emsp;Type: [TestPart](testpart-data-type.md)  
An instance of the [TestPart](testpart-data-type.md) data type.  

*Field*  
&emsp;Type: [TestField](testfield-data-type.md)  
The field to find.  
*Value*  
&emsp;Type: [Any](any-data-type.md)  
The value of the field.  


## Return Value
*Ok*  
&emsp;Type: [Boolean](boolean-data-type.md)  
**True** if the operation was successful; otherwise, **false**.  
  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)
## See Also
[TestPart Data Type](testpart-data-type.md)  
[Getting Started with AL](../devenv-get-started.md)  
[Developing Extensions](../devenv-dev-overview.md)