---
title: "_CrtMemDifference"
ms.custom: na
ms.date: 10/06/2016
ms.devlang: 
  - C++
  - C
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: article
apiname: 
  - _CrtMemDifference
apilocation: 
  - msvcrt.dll
  - msvcr80.dll
  - msvcr90.dll
  - msvcr100.dll
  - msvcr100_clr0400.dll
  - msvcr110.dll
  - msvcr110_clr0400.dll
  - msvcr120.dll
  - msvcr120_clr0400.dll
  - ucrtbase.dll
apitype: DLLExport
ms.assetid: 0f327278-b551-482f-958b-76941f796ba4
caps.latest.revision: 16
manager: ghogen
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# _CrtMemDifference
Compares two memory states and returns their differences (debug version only).  
  
## Syntax  
  
```  
int _CrtMemDifference(   
   _CrtMemState *stateDiff,  
   const _CrtMemState *oldState,  
   const _CrtMemState *newState   
);  
```  
  
#### Parameters  
 `stateDiff`  
 Pointer to a `_CrtMemState` structure that is used to store the differences between the two memory states (returned).  
  
 `oldState`  
 Pointer to an earlier memory state (`_CrtMemState` structure).  
  
 `newState`  
 Pointer to a later memory state (`_CrtMemState` structure).  
  
## Return Value  
 If the memory states are significantly different, `_CrtMemDifference` returns TRUE. Otherwise, the function returns FALSE.  
  
## Remarks  
 The `_CrtMemDifference` function compares `oldState` and `newState` and stores their differences in `stateDiff`, which can then be used by the application to detect memory leaks and other memory problems. When [_DEBUG](../VS_visualcpp/_DEBUG.md) is not defined, calls to `_CrtMemDifference` are removed during preprocessing.  
  
 `newState` and `oldState` must each be a valid pointer to a `_CrtMemState` structure, defined in Crtdbg.h, that has been filled in by [_CrtMemCheckpoint](../VS_visualcpp/_CrtMemCheckpoint.md) before calling `_CrtMemDifference`. `stateDiff` must be a pointer to a previously allocated instance of the `_CrtMemState` structure. If `stateDiff`, `newState`, or `oldState` is `NULL`, the invalid parameter handler is invoked, as described in [Parameter Validation](../VS_visualcpp/Parameter-Validation.md). If execution is allowed to continue, [errno, _doserrno, _sys_errlist, and _sys_nerr](../VS_visualcpp/errno--_doserrno--_sys_errlist--and-_sys_nerr.md) is set to `EINVAL` and the function returns FALSE.  
  
 `_CrtMemDifference` compares the `_CrtMemState` field values of the blocks in `oldState` to those in `newState` and stores the result in `stateDiff`. When the number of allocated block types or total number of allocated blocks for each type differs between the two memory states, the states are said to be significantly different. The difference between the largest amount ever allocated at once for the two states and the difference between total allocations for the two states are also stored in `stateDiff`.  
  
 By default, internal C run-time blocks (`_CRT_BLOCK`) are not included in memory state operations. The [_CrtSetDbgFlag](../VS_visualcpp/_CrtSetDbgFlag.md) function can be used to turn on the `_CRTDBG_CHECK_CRT_DF` bit of `_crtDbgFlag` to include these blocks in leak detection and other memory state operations. Freed memory blocks (`_FREE_BLOCK`) do not cause `_CrtMemDifference` to return TRUE.  
  
 For more information about heap state functions and the `_CrtMemState` structure, see [Heap State Reporting Functions](../Topic/CRT%20Debug%20Heap%20Details.md#BKMK_Heap_State_Reporting_Functions). For information about how memory blocks are allocated, initialized, and managed in the debug version of the base heap, see [CRT Debug Heap Details](../Topic/CRT%20Debug%20Heap%20Details.md).  
  
## Requirements  
  
|Routine|Required header|Optional header|  
|-------------|---------------------|---------------------|  
|`_CrtMemDifference`|<crtdbg.h>|<errno.h>|  
  
 For more compatibility information, see [Compatibility](../VS_visualcpp/Compatibility.md) in the Introduction.  
  
 **Libraries:** Debug versions of [CRT Library Features](../VS_visualcpp/CRT-Library-Features.md) only.  
  
## .NET Framework Equivalent  
 Not applicable. To call the standard C function, use `PInvoke`. For more information, see [Platform Invoke Examples](../Topic/Platform%20Invoke%20Examples.md).  
  
## See Also  
 [Debug Routines](../VS_visualcpp/Debug-Routines.md)   
 [_crtDbgFlag](../VS_visualcpp/_crtDbgFlag.md)