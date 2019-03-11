---
title: "Code Actions"
description: "Code Actions"

author: SusanneWindfeldPedersen
ms.custom: na
ms.date: 02/25/2019
ms.topic: article
ms.service: "dynamics365-business-central"
ms.author: solsen
---

# Code Actions
The [!INCLUDE[d365al_ext_md](../includes/d365al_ext_md.md)] offers users the option to help fix issues in code. Code Actions is a Visual Studio Code feature providing the user with possible corrective actions right next to an error or warning. If actions are available, a light bulb appears next to the error or warning. When the user clicks the light bulb (or presses Ctrl+.), a list of available Code Actions is presented. 

In [!INCLUDE[d365al_ext_md](../includes/d365al_ext_md.md)] two code actions are available in the current version:

- Multiple IF to CASE converting code action.
- Spell check code action.

## To enable Code Actions
1. Open the Command Palette **Ctrl+Shift+P** and choose either **User Settings** or **Workspace Settings** depending on which scope you want the code actions to apply to.
2. Enter the setting `al.enableCodeActions` to the settings file and set it to `true`: `"al.enableCodeActions": true`
3. Save the settings file. You have now enabled code actions on your project.

## See Also
[AL Development Environment](devenv-reference-overview.md)  
[AL Outline View](devenv-al-outline-view.md)
