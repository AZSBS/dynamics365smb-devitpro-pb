---
title: "Name Method"
ms.author: solsen
ms.custom: na
ms.date: 10/01/2018
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
# Name Method
Gets the name of a table filter control that is included on a filter page based on an index number that is assigned to the filter control.

## Syntax
```
Name :=   FilterPageBuilder.Name(Index: Integer)
```
## Parameters
*FilterPageBuilder*  
&emsp;Type: [FilterPageBuilder](filterpagebuilder-data-type.md)  
An instance of the [FilterPageBuilder](filterpagebuilder-data-type.md) data type.  

*Index*  
&emsp;Type: [Integer](integer-data-type.md)  
The index of a filter control. The value must be in the range 1 to N, where N is the number of filter controls on the filter page.  


## Return Value
*Name*  
&emsp;Type: [String](string-data-type.md)  
The name of the filter control.  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)

## Example  
 The following example initializes a filter page object that includes two filter controls for the **Date** system table. The NAME method returns the names of filter control in a message dialog box.  
  
 This example requires that you create the following global variables.  
  
|Variable name|DataType|SubType|  
|-------------------|--------------|-------------|  
|varDateItem|Text||  
|varCount|Integer|Date|  
|varIndex|Integer||  
|varFilterPageBuilder|FilterPageBuilder||  
  
```  
varDateVariable := 'Date record';  
varFilterPageBuilder.ADDTABLE(varDateVariable + ‘ 1’,DATABASE::Date);  
varFilterPageBuilder.ADDTABLE(varDateVariable + ‘ 2’,DATABASE::Date);  
varCount := varFilterPageBuilder.COUNT;  
IF varCount <> 2 THEN   
  error(‘There should be two controls in FilterPageBuilder’);  
FOR varIndex := 1 to varCount do  
  MESSAGE(‘Control item %1 is named %2’, varIndex, varFilterPageBuilder.Name(varIndex));  
  
```  
  

## See Also
[FilterPageBuilder Data Type](filterpagebuilder-data-type.md)  
[Getting Started with AL](../devenv-get-started.md)  
[Developing Extensions](../devenv-dev-overview.md)