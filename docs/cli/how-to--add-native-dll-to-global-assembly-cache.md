---
title: "How to: Add Native DLL to Global Assembly Cache"
ms.custom: na
ms.date: "10/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: na
ms.topic: "get-started-article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "DLLs [C++], native"
  - "GAC (global assembly cache), loading native DLLs"
  - "native DLLs [C++]"
ms.assetid: 25e8d78a-b197-4269-b4e9-237a544ab3c8
caps.latest.revision: 6
ms.author: "mblome"
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
# How to: Add Native DLL to Global Assembly Cache
You can put a native DLL (not COM) into the Global Assembly Cache.  
  
## Example  
 **/ASSEMBLYLINKRESOURCE** lets you embed a native DLL in an assembly.  
  
 For more information, see [/ASSEMBLYLINKRESOURCE (Link to .NET Framework Resource)](../buildref/-assemblylinkresource--link-to-.net-framework-resource-.md).  
  
```  
/ASSEMBLYLINKRESOURCE:MyComponent.dll  
```  
  
## See Also  
 [Using C++ Interop (Implicit PInvoke)](../cli/using-c---interop--implicit-pinvoke-.md)