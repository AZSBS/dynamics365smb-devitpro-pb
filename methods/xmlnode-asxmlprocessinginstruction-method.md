---
title: "AsXmlProcessingInstruction Method"
ms.author: solsen
ms.custom: na
ms.date: 09/30/2018
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
# AsXmlProcessingInstruction Method
Converts the node to an XmlProcessingInstruction node. The operation will fail if the node is not an XmlProcessingInstruction.

## Syntax
```
XmlProcessingInstruction :=   XmlNode.AsXmlProcessingInstruction()
```

## Parameters
*XmlNode*  
&emsp;Type: [XmlNode](xmlnode-data-type.md)  
An instance of the [XmlNode](xmlnode-data-type.md) data type.  

## Return Value
*XmlProcessingInstruction*  
&emsp;Type: [XmlProcessingInstruction](xmlprocessinginstruction-data-type.md)  
An XmlProcessingInstruction value that references the current XmlNode.  


[//]: # (IMPORTANT: END>DO_NOT_EDIT)
## See Also
[XmlNode Data Type](xmlnode-data-type.md)  
[Getting Started with AL](../devenv-get-started.md)  
[Developing Extensions](../devenv-dev-overview.md)