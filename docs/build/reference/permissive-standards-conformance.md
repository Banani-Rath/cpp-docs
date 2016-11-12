---
title: "-permissive- (Standards conformance) | Microsoft Docs"
ms.custom: ""
ms.date: "11/11/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/permissive"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "/permissive compiler options [C++]"
  - "-permissive compiler options [C++]"
  - "Standards conformance compiler options"
  - "permissive compiler options [C++]"
ms.assetid: db1cc175-6e93-4a2e-9396-c3725d2d8f71
caps.latest.revision: 15
author: "corob-msft"
ms.author: "corob"
manager: "ghogen"
translation.priority.ht: 
  - "cs-cz"
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pl-pl"
  - "pt-br"
  - "ru-ru"
  - "tr-tr"
  - "zh-cn"
  - "zh-tw"
---
# /permissive- (Standards conformance)
You can use the **/permissive-** compiler option to specify strict standards-conformant compiler behavior. Note that the trailing dash is required. This option disables language extensions, similar to the deprecated [/Za](../../build/reference/za-ze-disable-language-extensions.md) option, and sets the [/Zc](../../build/reference/zc-conformance.md) compiler options for strict conformance. Not all standards-conformant code is supported by the Visual C++ compiler in Visual Studio 2017 RC. However, when this option is set, the compiler generates errors or warnings when non-standard language constructs are detected in your code.  
  
For more information about conformance issues in Visual C++, see [Nonstandard Behavior](../../cpp/nonstandard-behavior.md).  
  
## See Also  
 [Compiler Options](../../build/reference/compiler-options.md)   
 [Setting Compiler Options](../../build/reference/setting-compiler-options.md)