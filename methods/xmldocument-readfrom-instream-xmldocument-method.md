---
title: "ReadFrom Method"
ms.author: solsen
ms.custom: na
ms.date: 07/30/2018
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
# ReadFrom Method
Read and parse the XML document from the given data source.

## Syntax
```
[Ok := ]  XmlDocument.ReadFrom(InStream: InStream, var Result: XmlDocument)
```
## Parameters
*InStream*  
&emsp;Type: [InStream](instream-data-type.md)  
A stream containing an XML document.  
*Result*  
&emsp;Type: [XmlDocument](xmldocument-data-type.md)  
The XmlDocument parsed from the given data source.  


## Return Value
*Ok*  
&emsp;Type: [Boolean](boolean-data-type.md)  
**True** if the operation was successful; otherwise, **false**.  
  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)
## See Also
[XmlDocument Data Type](xmldocument-data-type.md)  
[Getting Started with AL](../devenv-get-started.md)  
[Developing Extensions](../devenv-dev-overview.md)