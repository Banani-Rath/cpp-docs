---
title: "Diagnostic Services"
ms.custom: na
ms.date: "10/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: na
ms.topic: "article"
f1_keywords: 
  - "vc.mfc.macros"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "diagnosis, diagnostic services"
  - "diagnostic macros, list of general MFC"
  - "services, diagnostic"
  - "MFC, diagnostic services"
  - "general diagnostic functions and variables"
  - "diagnostics, diagnostic functions and variables"
  - "diagnostics, list of general MFC"
  - "diagnosis, diagnostic functions and variables"
  - "diagnosis, list of general MFC"
  - "general diagnostic macros in MFC"
  - "diagnostic macros"
  - "diagnostic services"
  - "object diagnostic functions in MFC"
  - "diagnostics, diagnostic services"
  - "diagnostic functions and variables"
ms.assetid: 8d78454f-9fae-49c2-88c9-d3fabd5393e8
caps.latest.revision: 16
ms.author: "mblome"
manager: "ghogen"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Diagnostic Services
The Microsoft Foundation Class Library supplies many diagnostic services that make debugging your programs easier. These diagnostic services include macros and global functions that allow you to track your program's memory allocations, dump the contents of objects during run time, and print debugging messages during run time. The macros and global functions for diagnostic services are grouped into the following categories:  
  
-   General diagnostic macros  
  
-   General diagnostic functions and variables  
  
-   Object diagnostic functions  
  
 These macros and functions are available for all classes derived from             `CObject` in the Debug and Release versions of MFC. However, all except             `DEBUG_NEW` and             **VERIFY** do nothing in the Release version.  
  
 In the Debug library, all allocated memory blocks are bracketed with a series of "guard bytes." If these bytes are disturbed by an errant memory write, then the diagnostic routines can report a problem. If you include the line:  
  
 [!code[NVC_MFCCObjectSample#14](../mfc/codesnippet/CPP/diagnostic-services_1.cpp)]  
  
 in your implementation file, all calls to             **new** will store the filename and line number where the memory allocation took place. The function             [CMemoryState::DumpAllObjectsSince](../Topic/CMemoryState::DumpAllObjectsSince.md) will display this extra information, allowing you to identify memory leaks. Refer also to the class             [CDumpContext](../mfcref/cdumpcontext-class.md) for additional information on diagnostic output.  
  
 In addition, the C run-time library also supports a set of diagnostic functions you can use to debug your applications. For more information, see             [Debug Routines](../crt/debug-routines.md) in the Run-Time Library Reference.  
  
### MFC General Diagnostic Macros  
  
|||  
|-|-|  
|[ASSERT](../Topic/ASSERT%20\(MFC\).md)|Prints a message and then aborts the program if the specified expression evaluates to                             **FALSE** in the Debug version of the library.|  
|[ASSERT_KINDOF](../Topic/ASSERT_KINDOF.md)|Tests that an object is an object of the specified class or of a class derived from the specified class.|  
|[ASSERT_VALID](../Topic/ASSERT_VALID.md)|Tests the internal validity of an object by calling its                             `AssertValid` member function; typically overridden from                             `CObject`.|  
|[DEBUG_NEW](../Topic/DEBUG_NEW.md)|Supplies a filename and line number for all object allocations in Debug mode to help find memory leaks.|  
|[DEBUG_ONLY](../Topic/DEBUG_ONLY.md)|Similar to                             **ASSERT** but does not test the value of the expression; useful for code that should execute only in Debug mode.|  
|[TRACE](../Topic/TRACE.md)|Provides                             `printf`-like capability in the Debug version of the library.|  
|[VERIFY](../Topic/VERIFY.md)|Similar to                             **ASSERT** but evaluates the expression in the Release version of the library as well as in the Debug version.|  
  
### MFC General Diagnostic Variables and Functions  
  
|||  
|-|-|  
|[afxDump](../Topic/afxDump%20\(CDumpContext%20in%20MFC\).md)|Global variable that sends                             [CDumpContext](../mfcref/cdumpcontext-class.md) information to the debugger output window or to the debug terminal.|  
|[afxMemDF](../Topic/afxMemDF.md)|Global variable that controls the behavior of the debugging memory allocator.|  
|[AfxCheckError](../Topic/AfxCheckError.md)|Global variable used to test the passed                             **SCODE** to see if it is an error and, if so, throws the appropriate error.|  
|[AfxCheckMemory](../Topic/AfxCheckMemory.md)|Checks the integrity of all currently allocated memory.|  
|[AfxDump](../Topic/AfxDump%20\(MFC\).md)|If called while in the debugger, dumps the state of an object while debugging.|  
|[AfxDumpStack](../Topic/AfxDumpStack.md)|Generate an image of the current stack. This function is always linked statically.|  
|[AfxEnableMemoryLeakDump](../Topic/AfxEnableMemoryLeakDump.md)|Enables the memory leak dump.|  
|[AfxEnableMemoryTracking](../Topic/AfxEnableMemoryTracking.md)|Turns memory tracking on and off.|  
|[AfxIsMemoryBlock](../Topic/AfxIsMemoryBlock.md)|Verifies that a memory block has been properly allocated.|  
|[AfxIsValidAddress](../Topic/AfxIsValidAddress.md)|Verifies that a memory address range is within the program's bounds.|  
|[AfxIsValidString](../Topic/AfxIsValidString.md)|Determines whether a pointer to a string is valid.|  
|[AfxSetAllocHook](../Topic/AfxSetAllocHook.md)|Enables the calling of a function on each memory allocation.|  
  
### MFC Object Diagnostic Functions  
  
|||  
|-|-|  
|[AfxDoForAllClasses](../Topic/AfxDoForAllClasses.md)|Performs a specified function on all                             `CObject`-derived classes that support run-time type checking.|  
|[AfxDoForAllObjects](../Topic/AfxDoForAllObjects.md)|Performs a specified function on all                             `CObject`-derived objects that were allocated with                             **new**.|  
  
##  <a name="assert__mfc_"></a>  ASSERT (MFC)  
 Evaluates its argument.  
  
```  
  
ASSERT(  
booleanExpression  
)  
  
```  
  
### Parameters  
 `booleanExpression`  
 Specifies an expression (including pointer values) that evaluates to nonzero or 0.  
  
### Remarks  
 If the result is 0, the macro prints a diagnostic message and aborts the program. If the condition is nonzero, it does nothing.  
  
 The diagnostic message has the form  
  
 `assertion failed in file <name> in line <num>`  
  
 where                         *name* is the name of the source file, and                         *num* is the line number of the assertion that failed in the source file.  
  
 In the Release version of MFC,                         **ASSERT** does not evaluate the expression and thus will not interrupt the program. If the expression must be evaluated regardless of environment, use the                         **VERIFY** macro in place of                         **ASSERT**.  
  
> [!NOTE]
>  This function is available only in the Debug version of MFC.  
  
### Example  
 [!code[NVC_MFC_Utilities#44](../mfc/codesnippet/CPP/diagnostic-services_2.cpp)]  
  
##  <a name="assert_kindof"></a>  ASSERT_KINDOF  
 This macro asserts that the object pointed to is an object of the specified class, or is an object of a class derived from the specified class.  
  
```  
  
ASSERT_KINDOF(  
classname  
,   
pobject  
)  
  
```  
  
### Parameters  
 *classname*  
 The name of a                                 `CObject`-derived class.  
  
 *pobject*  
 A pointer to a class object.  
  
### Remarks  
 The                         *pobject* parameter should be a pointer to an object and can be                         **const**. The object pointed to and the class must support                         `CObject` run-time class information. As an example, to ensure that                         `pDocument` is a pointer to an object of the                         `CMyDoc` class, or any of its derivatives, you could code:  
  
 [!code[NVC_MFCDocView#194](../mfc/codesnippet/CPP/diagnostic-services_3.cpp)]  
  
 Using the                         `ASSERT_KINDOF` macro is exactly the same as coding:  
  
 [!code[NVC_MFCDocView#195](../mfc/codesnippet/CPP/diagnostic-services_4.cpp)]  
  
 This function works only for classes declared with the                         [DECLARE_DYNAMIC](../Topic/DECLARE_DYNAMIC.md) or                         [DECLARE_SERIAL](../Topic/DECLARE_SERIAL.md) macro.  
  
> [!NOTE]
>  This function is available only in the Debug version of MFC.  
  
##  <a name="assert_valid"></a>  ASSERT_VALID  
 Use to test your assumptions about the validity of an object's internal state.  
  
```  
  
ASSERT_VALID(  
pObject  
)  
  
```  
  
### Parameters  
 `pObject`  
 Specifies an object of a class derived from                                 `CObject` that has an overriding version of the                                 `AssertValid` member function.  
  
### Remarks  
 `ASSERT_VALID` calls the                         `AssertValid` member function of the object passed as its argument.  
  
 In the Release version of MFC,                         `ASSERT_VALID` does nothing. In the Debug version, it validates the pointer, checks against                         **NULL**, and calls the object's own                         `AssertValid` member functions. If any of these tests fails, an alert message is displayed in the same manner as                         [ASSERT](../Topic/ASSERT%20\(MFC\).md).  
  
> [!NOTE]
>  This function is available only in the Debug version of MFC.  
  
 For more information and examples, see                         [Debugging MFC Applications](../Topic/MFC%20Debugging%20Techniques.md).  
  
### Example  
 [!code[NVC_MFCCObjectSample#19](../mfc/codesnippet/CPP/diagnostic-services_5.cpp)]  
  
##  <a name="debug_new"></a>  DEBUG_NEW  
 Assists in finding memory leaks.  
  
```  
  
#define  
new  
DEBUG_NEW  
  
```  
  
### Remarks  
 You can use                         `DEBUG_NEW` everywhere in your program that you would ordinarily use the                         **new** operator to allocate heap storage.  
  
 In debug mode (when the                         **_DEBUG** symbol is defined),                         `DEBUG_NEW` keeps track of the filename and line number for each object that it allocates. Then, when you use the                         [CMemoryState::DumpAllObjectsSince](../Topic/CMemoryState::DumpAllObjectsSince.md) member function, each object allocated with                         `DEBUG_NEW` is shown with the filename and line number where it was allocated.  
  
 To use                         `DEBUG_NEW`, insert the following directive into your source files:  
  
 [!code[NVC_MFCCObjectSample#14](../mfc/codesnippet/CPP/diagnostic-services_1.cpp)]  
  
 Once you insert this directive, the preprocessor will insert                         `DEBUG_NEW` wherever you use                         **new**, and MFC does the rest. When you compile a release version of your program,                         `DEBUG_NEW` resolves to a simple                         **new** operation, and the filename and line number information are not generated.  
  
> [!NOTE]
>  In previous versions of MFC (4.1 and earlier) you needed to put the                             `#define` statement after all statements that called the                             `IMPLEMENT_DYNCREATE` or                             `IMPLEMENT_SERIAL` macros. This is no longer necessary.  
  
##  <a name="debug_only"></a>  DEBUG_ONLY  
 In debug mode (when the                 **_DEBUG** symbol is defined),                 `DEBUG_ONLY` evaluates its argument.  
  
```  
  
DEBUG_ONLY(  
expression  
 )  
  
```  
  
### Remarks  
 In a release build,                         **DEBUG_ONLY** does not evaluate its argument. This is useful when you have code that should be executed only in debug builds.  
  
 The                         `DEBUG_ONLY` macro is equivalent to surrounding                         *expression* with                         **#ifdef _DEBUG** and                         `#endif`.  
  
### Example  
 [!code[NVC_MFC_Utilities#32](../mfc/codesnippet/CPP/diagnostic-services_6.cpp)]  
  
##  <a name="trace"></a>  TRACE  
 Sends the specified string to the debugger of the current application.  
  
```  
  
TRACE(  
exp  
 )  
TRACE(DWORD   
category  
, UINT   
level  
, LPCSTR   
lpszFormat  
, ... )  
  
```  
  
### Remarks  
 See                         [ATLTRACE2](../Topic/ATLTRACE2.md) for a description of                         **TRACE**.                          **TRACE** and                         `ATLTRACE2` have the same behavior.  
  
 In the debug version of MFC, this macro sends the specified string to the debugger of the current application. In a release build, this macro compiles to nothing (no code is generated at all).  
  
 For more information, see                         [Debugging MFC Applications](../Topic/MFC%20Debugging%20Techniques.md).  
  
##  <a name="verify"></a>  VERIFY  
 In the Debug version of MFC, evaluates its argument.  
  
```  
  
VERIFY(  
booleanExpression  
)  
  
```  
  
### Parameters  
 `booleanExpression`  
 Specifies an expression (including pointer values) that evaluates to nonzero or 0.  
  
### Remarks  
 If the result is 0, the macro prints a diagnostic message and halts the program. If the condition is nonzero, it does nothing.  
  
 The diagnostic message has the form  
  
 `assertion failed in file <name> in line <num>`  
  
 where                         *name* is the name of the source file and                         *num* is the line number of the assertion that failed in the source file.  
  
 In the Release version of MFC,                         **VERIFY** evaluates the expression but does not print or interrupt the program. For example, if the expression is a function call, the call will be made.  
  
### Example  
 [!code[NVC_MFCDocView#198](../mfc/codesnippet/CPP/diagnostic-services_7.cpp)]  
  
##  <a name="afxdump__cdumpcontext_in_mfc_"></a>  afxDump (CDumpContext in MFC)  
 Provides basic object-dumping capability in your application.  
  
```  
  
CDumpContext  
afxDump;  
  
```  
  
### Remarks  
 `afxDump` is a predefined                         [CDumpContext](../mfcref/cdumpcontext-class.md) object that allows you to send                         `CDumpContext` information to the debugger output window or to a debug terminal. Typically, you supply                         `afxDump` as a parameter to                         `CObject::Dump`.  
  
 Under Windows NT and all versions of Windows,                         `afxDump` output is sent to the Output-Debug window of Visual C++ when you debug your application.  
  
 This variable is defined only in the Debug version of MFC. For more information on                         `afxDump`, see                         [Debugging MFC Applications](../Topic/MFC%20Debugging%20Techniques.md).  
  
### Example  
 [!code[NVC_MFC_Utilities#23](../mfc/codesnippet/CPP/diagnostic-services_8.cpp)]  
  
##  <a name="afxmemdf"></a>  afxMemDF  
 This variable is accessible from a debugger or your program and allows you to tune allocation diagnostics.  
  
```  
  
int  
afxMemDF;  
  
```  
  
### Remarks  
 `afxMemDF` can have the following values as specified by the enumeration                         `afxMemDF`:  
  
-   **allocMemDF** Turns on debugging allocator (default setting in Debug library).  
  
-   **delayFreeMemDF** Delays freeing memory. While your program frees a memory block, the allocator does not return that memory to the underlying operating system. This will place maximum memory stress on your program.  
  
-   **checkAlwaysMemDF** Calls                                 `AfxCheckMemory` every time memory is allocated or freed. This will significantly slow memory allocations and deallocations.  
  
### Example  
 [!code[NVC_MFC_Utilities#30](../mfc/codesnippet/CPP/diagnostic-services_9.cpp)]  
  
##  <a name="afxcheckerror"></a>  AfxCheckError  
 This function tests the passed                 **SCODE** to see if it is an error.  
  
```  
  
void AFXAPI AfxCheckError(  
   SCODE   
sc  
);  
throw CMemoryException*  
throw COleException*  
  
```  
  
### Remarks  
 If it is an error, the function throws an exception. If the passed                         `SCODE` is                         **E_OUTOFMEMORY**, the function throws a                         [CMemoryException](../mfcref/cmemoryexception-class.md) by calling                         [AfxThrowMemoryException](../Topic/AfxThrowMemoryException.md). Otherwise, the function throws a                         [COleException](../mfcref/coleexception-class.md) by calling                         [AfxThrowOleException](../Topic/AfxThrowOleException.md).  
  
 This function can be used to check the return values of calls to OLE functions in your application. By testing the return value with this function in your application, you can properly react to error conditions with a minimal amount of code.  
  
> [!NOTE]
>  This function has the same effect in debug and non-debug builds.  
  
### Example  
 [!code[NVC_MFCOleContainer#33](../mfc/codesnippet/CPP/diagnostic-services_10.cpp)]  
  
##  <a name="afxcheckmemory"></a>  AfxCheckMemory  
 This function validates the free memory pool and prints error messages as required.  
  
```  
  
BOOL  
AfxCheckMemory(  
);  
  
```  
  
### Return Value  
 Nonzero if no memory errors; otherwise 0.  
  
### Remarks  
 If the function detects no memory corruption, it prints nothing.  
  
 All memory blocks currently allocated on the heap are checked, including those allocated by                         **new** but not those allocated by direct calls to underlying memory allocators, such as the                         `malloc` function or the                         **GlobalAlloc** Windows function. If any block is found to be corrupted, a message is printed to the debugger output.  
  
 If you include the line  
  
 [!code[NVC_MFCCObjectSample#14](../mfc/codesnippet/CPP/diagnostic-services_1.cpp)]  
  
 in a program module, then subsequent calls to                         `AfxCheckMemory` show the filename and line number where the memory was allocated.  
  
> [!NOTE]
>  If your module contains one or more implementations of serializable classes, then you must put the                             `#define` line after the last                             `IMPLEMENT_SERIAL` macro call.  
  
 This function works only in the Debug version of MFC.  
  
### Example  
 [!code[NVC_MFCCObjectSample#26](../mfc/codesnippet/CPP/diagnostic-services_11.cpp)]  
  
##  <a name="afxdump__mfc_"></a>  AfxDump (MFC)  
 Call this function while in the debugger to dump the state of an object while debugging.  
  
```  
  
void  
AfxDump(  
   const  
CObject*  
pOb  
);  
  
```  
  
### Parameters  
 `pOb`  
 A pointer to an object of a class derived from                                 `CObject`.  
  
### Remarks  
 **AfxDump** calls an object's                         `Dump` member function and sends the information to the location specified by the                         `afxDump` variable.                         **AfxDump** is available only in the Debug version of MFC.  
  
 Your program code should not call                         **AfxDump**, but should instead call the                         `Dump` member function of the appropriate object.  
  
##  <a name="afxdumpstack"></a>  AfxDumpStack  
 This global function can be used to generate an image of the current stack.  
  
```  
  
void AFXAPI AfxDumpStack(  
   DWORD   
dwTarget  
 = AFX_STACK_DUMP_TARGET_DEFAULT  
);  
  
```  
  
### Parameters  
 *dwTarget*  
 Indicates the target of the dump output. Possible values, which can be combined using the bitwise-OR (                                **&#124;**) operator, are as follows:  
  
-   **AFX_STACK_DUMP_TARGET_TRACE** Sends output by means of the                                         [TRACE](../Topic/TRACE.md) macro. The                                         **TRACE** macro generates output in debug builds only; it generates no output in release builds. Also,                                         **TRACE** can be redirected to other targets besides the debugger.  
  
-   **AFX_STACK_DUMP_TARGET_DEFAULT** Sends dump output to the default target. For a debug build, output goes to the                                         **TRACE** macro. In a release build, output goes to the Clipboard.  
  
-   **AFX_STACK_DUMP_TARGET_CLIPBOARD** Sends output to the Clipboard only. The data is placed on the Clipboard as plain text using the                                         **CF_TEXT** Clipboard format.  
  
-   **AFX_STACK_DUMP_TARGET_BOTH** Sends output to the Clipboard and to the                                         **TRACE** macro, simultaneously.  
  
-   **AFX_STACK_DUMP_TARGET_ODS** Sends output directly to the debugger by means of the Win32 function                                         **OutputDebugString()**. This option will generate debugger output in both debug and release builds when a debugger is attached to the process.                                         **AFX_STACK_DUMP_TARGET_ODS** always reaches the debugger (if it is attached) and cannot be redirected.  
  
### Remarks  
 The example below reflects a single line of the output generated from calling                         `AfxDumpStack` from a button handler in an MFC dialog application:  
  
 `=== begin AfxDumpStack output ===`  
  
 `00427D55: DUMP2\DEBUG\DUMP2.EXE! void AfxDumpStack(unsigned long) + 181 bytes`  
  
 `0040160B: DUMP2\DEBUG\DUMP2.EXE! void CDump2Dlg::OnClipboard(void) + 14 bytes`  
  
 `0044F884: DUMP2\DEBUG\DUMP2.EXE! int _AfxDispatchCmdMsg(class CCmdTarget *,`  
  
 `unsigned int,int,void ( CCmdTarget::*)(void),void *,unsigned int,struct AFX_CMDHANDLE`  
  
 `0044FF7B: DUMP2\DEBUG\DUMP2.EXE! virtual int CCmdTarget::OnCmdMsg(unsigned`  
  
 `int,int,void *,struct AFX_CMDHANDLERINFO *) + 626 bytes`  
  
 `00450C71: DUMP2\DEBUG\DUMP2.EXE! virtual int CDialog::OnCmdMsg(unsigned`  
  
 `int,int,void *,struct AFX_CMDHANDLERINFO *) + 36 bytes`  
  
 `00455B27: DUMP2\DEBUG\DUMP2.EXE! virtual int CWnd::OnCommand(unsigned`  
  
 `int,long) + 312 bytes`  
  
 `00454D3D: DUMP2\DEBUG\DUMP2.EXE! virtual int CWnd::OnWndMsg(unsigned`  
  
 `int,unsigned int,long,long *) + 83 bytes`  
  
 `00454CC0: DUMP2\DEBUG\DUMP2.EXE! virtual long CWnd::WindowProc(unsigned`  
  
 `int,unsigned int,long) + 46 bytes`  
  
 `004528D9: DUMP2\DEBUG\DUMP2.EXE! long AfxCallWndProc(class CWnd *,struct`  
  
 `HWND__ *,unsigned int,unsigned int,long) + 237 bytes`  
  
 `00452D34: DUMP2\DEBUG\DUMP2.EXE! long AfxWndProc(struct HWND__ *,unsigned`  
  
 `int,unsigned int,long) + 129 bytes`  
  
 `BFF73663: WINDOWS\SYSTEM\KERNEL32.DLL! ThunkConnect32 + 2148 bytes`  
  
 `BFF928E0: WINDOWS\SYSTEM\KERNEL32.DLL! UTUnRegister + 2492 bytes`  
  
 `=== end AfxDumpStack() output ===`  
  
 Each line in the output above indicates the address of the last function call, the full path name of the module that contains the function call, and the function prototype called. If the function call on the stack does not happen at the exact address of the function, an offset of bytes is shown.  
  
 For example, the following table describes the first line of the above output:  
  
|Output|Description|  
|------------|-----------------|  
|`00427D55:`|The return address of the last function call.|  
|`DUMP2\DEBUG\DUMP2.EXE!`|The full path name of the module that contains the function call.|  
|`void AfxDumpStack(unsigned long)`|The function prototype called.|  
|`+ 181 bytes`|The offset in bytes from the address of the function prototype (in this case,                                         `void AfxDumpStack(unsigned long)`) to the return address (in this case,                                         `00427D55`).|  
  
 `AfxDumpStack` is available in debug and nondebug versions of the MFC libraries; however, the function is always linked statically, even when your executable file uses MFC in a shared DLL. In shared-library implementations, the function is found in the MFCS42.LIB library (and its variants).  
  
 To use this function successfully:  
  
-   The file IMAGEHLP.DLL must be on your path. If you do not have this DLL, the function will display an error message. See                                 [Image Help Library](http://msdn.microsoft.com/library/windows/desktop/ms680321) for information on the function set provided by IMAGEHLP.  
  
-   The modules that have frames on the stack must include debugging information. If they do not contain debugging information, the function will still generate a stack trace, but the trace will be less detailed.  
  
##  <a name="afxenablememoryleakdump"></a>  AfxEnableMemoryLeakDump  
 Enables and disables the memory leak dump in the                 `AFX_DEBUG_STATE` destructor.  
  
```  
BOOL AFXAPI AfxEnableMemoryLeakDump(  
   BOOL                 bDump  
);  
```  
  
### Parameters  
 [in]                             `bDump`  
 `TRUE` indicates the memory leak dump is enabled;                                 `FALSE` indicates the memory leak dump is disabled.  
  
### Return Value  
 The previous value for this flag.  
  
### Remarks  
 When an application unloads the MFC library, the MFC library checks for memory leaks. At this point, any memory leaks are reported to the user through the                         **Debug** window of                         [!INCLUDE[vsprvs](../build/includes/vsprvs_md.md)].  
  
 If your application loads another library before the MFC library, some memory allocations in that library will be incorrectly reported as memory leaks. False memory leaks can cause your application to close slowly as the MFC library reports them. In this case, use                         `AfxEnableMemoryLeakDump` to disable the memory leak dump.  
  
> [!NOTE]
>  If you use this method to turn off the memory leak dump, you will not receive reports of valid memory leaks in your application. You should only use this method if you are confident that the memory leak report contains false memory leaks.  
  
##  <a name="afxenablememorytracking"></a>  AfxEnableMemoryTracking  
 Diagnostic memory tracking is normally enabled in the Debug version of MFC.  
  
```  
  
BOOL  
AfxEnableMemoryTracking(  
   BOOL  
bTrack  
);  
  
```  
  
### Parameters  
 *bTrack*  
 Setting this value to                                 **TRUE** turns on memory tracking;                                 **FALSE** turns it off.  
  
### Return Value  
 The previous setting of the tracking-enable flag.  
  
### Remarks  
 Use this function to disable tracking on sections of your code that you know are allocating blocks correctly.  
  
 For more information on                         `AfxEnableMemoryTracking`, see                         [Debugging MFC Applications](../Topic/MFC%20Debugging%20Techniques.md).  
  
> [!NOTE]
>  This function works only in the Debug version of MFC.  
  
### Example  
 [!code[NVC_MFC_Utilities#24](../mfc/codesnippet/CPP/diagnostic-services_12.cpp)]  
  
##  <a name="afxismemoryblock"></a>  AfxIsMemoryBlock  
 Tests a memory address to make sure it represents a currently active memory block that was allocated by the diagnostic version of                 **new**.  
  
```  
  
BOOL  
AfxIsMemoryBlock(  
   const  
void*  
p  
,  
   UINT  
nBytes  
,  
   LONG*  
plRequestNumber  
=  
NULL  
);  
  
```  
  
### Parameters  
 `p`  
 Points to the block of memory to be tested.  
  
 `nBytes`  
 Contains the length of the memory block in bytes.  
  
 `plRequestNumber`  
 Points to a                                 **long** integer that will be filled in with the memory block's allocation sequence number, or zero if it does not represent a currently active memory block.  
  
### Return Value  
 Nonzero if the memory block is currently allocated and the length is correct; otherwise 0.  
  
### Remarks  
 It also checks the specified size against the original allocated size. If the function returns nonzero, the allocation sequence number is returned in                         `plRequestNumber`. This number represents the order in which the block was allocated relative to all other                         **new** allocations.  
  
### Example  
 [!code[NVC_MFC_Utilities#27](../mfc/codesnippet/CPP/diagnostic-services_13.cpp)]  
  
##  <a name="afxisvalidaddress"></a>  AfxIsValidAddress  
 Tests any memory address to ensure that it is contained entirely within the program's memory space.  
  
```  
  
BOOL  
AfxIsValidAddress(  
   const  
void*  
lp  
,  
   UINT  
nBytes  
,  
   BOOL  
bReadWrite  
=  
TRUE  
);  
  
```  
  
### Parameters  
 `lp`  
 Points to the memory address to be tested.  
  
 `nBytes`  
 Contains the number of bytes of memory to be tested.  
  
 *bReadWrite*  
 Specifies whether the memory is both for reading and writing (                                **TRUE**) or just reading (                                **FALSE**).  
  
### Return Value  
 In debug builds, nonzero if the specified memory block is contained entirely within the program's memory space; otherwise 0.  
  
 In non-debug builds, nonzero if                         `lp` is not NULL; otherwise 0.  
  
### Remarks  
 The address is not restricted to blocks allocated by                         **new**.  
  
### Example  
 [!code[NVC_MFC_Utilities#28](../mfc/codesnippet/CPP/diagnostic-services_14.cpp)]  
  
##  <a name="afxisvalidstring"></a>  AfxIsValidString  
 Use this function to determine whether a pointer to a string is valid.  
  
```  
  
BOOL  
AfxIsValidString(  
   LPCSTR  
lpsz  
,  
   int  
nLength  
=  
-1  
);  
  
```  
  
### Parameters  
 `lpsz`  
 The pointer to test.  
  
 `nLength`  
 Specifies the length of the string to be tested, in bytes. A value of –1 indicates that the string will be null-terminated.  
  
### Return Value  
 In debug builds, nonzero if the specified pointer points to a string of the specified size; otherwise 0.  
  
 In non-debug builds, nonzero if                         `lpsz` is not NULL; otherwise 0.  
  
### Example  
 [!code[NVC_MFC_Utilities#29](../mfc/codesnippet/CPP/diagnostic-services_15.cpp)]  
  
##  <a name="afxsetallochook"></a>  AfxSetAllocHook  
 Sets a hook that enables calling of the specified function before each memory block is allocated.  
  
```  
  
AFX_ALLOC_HOOK  
AfxSetAllocHook(  
   AFX_ALLOC_HOOK  
pfnAllocHook  
);  
  
```  
  
### Parameters  
 *pfnAllocHook*  
 Specifies the name of the function to call. See the Remarks for the prototype of an allocation function.  
  
### Return Value  
 Nonzero if you want to permit the allocation; otherwise 0.  
  
### Remarks  
 The Microsoft Foundation Class Library debug-memory allocator can call a user-defined hook function to allow the user to monitor a memory allocation and to control whether the allocation is permitted. Allocation hook functions are prototyped as follows:  
  
 **BOOL AFXAPI AllocHook( size_t** `nSize`**, BOOL** `bObject`**, LONG** `lRequestNumber` **);**  
  
 `nSize`  
 The size of the proposed memory allocation.  
  
 `bObject`  
 **TRUE** if the allocation is for a                                 `CObject`-derived object; otherwise                                 **FALSE**.  
  
 `lRequestNumber`  
 The memory allocation's sequence number.  
  
 Note that the                         **AFXAPI** calling convention implies that the callee must remove the parameters from the stack.  
  
##  <a name="afxdoforallclasses"></a>  AfxDoForAllClasses  
 Calls the specified iteration function for all serializable                 `CObject`-derived classes in the application's memory space.  
  
```  
  
void  
AFXAPI  
AfxDoForAllClasses(  
   void  
(*  
pfn  
)(const  
CRuntimeClass*  
pClass  
,  
   void*  
pContext  
),  
   void*  
pContext  
);  
  
```  
  
### Parameters  
 `pfn`  
 Points to an iteration function to be called for each class. The function arguments are a pointer to a                                 `CRuntimeClass` object and a void pointer to extra data that the caller supplies to the function.  
  
 `pContext`  
 Points to optional data that the caller can supply to the iteration function. This pointer can be                                 **NULL**.  
  
### Remarks  
 Serializable                         `CObject`-derived classes are classes derived using the                         `DECLARE_SERIAL` macro. The pointer that is passed to                         `AfxDoForAllClasses` in                         `pContext` is passed to the specified iteration function each time it is called.  
  
> [!NOTE]
>  This function works only in the Debug version of MFC.  
  
### Example  
 [!code[NVC_MFCCollections#113](../mfc/codesnippet/CPP/diagnostic-services_16.cpp)]  
  
 [!code[NVC_MFCCollections#114](../mfc/codesnippet/CPP/diagnostic-services_17.cpp)]  
  
##  <a name="afxdoforallobjects"></a>  AfxDoForAllObjects  
 Executes the specified iteration function for all objects derived from                 `CObject` that have been allocated with                 **new**.  
  
```  
  
void  
AfxDoForAllObjects(  
   void  
(*  
pfn  
)(CObject*  
pObject  
,  
   void*  
pContext  
),  
   void*  
pContext  
);  
  
```  
  
### Parameters  
 `pfn`  
 Points to an iteration function to execute for each object. The function arguments are a pointer to a                                 `CObject` and a void pointer to extra data that the caller supplies to the function.  
  
 `pContext`  
 Points to optional data that the caller can supply to the iteration function. This pointer can be                                 **NULL**.  
  
### Remarks  
 Stack, global, or embedded objects are not enumerated. The pointer passed to                         `AfxDoForAllObjects` in                         `pContext` is passed to the specified iteration function each time it is called.  
  
> [!NOTE]
>  This function works only in the Debug version of MFC.  
  
### Example  
 [!code[NVC_MFCCollections#115](../mfc/codesnippet/CPP/diagnostic-services_18.cpp)]  
  
 [!code[NVC_MFCCollections#116](../mfc/codesnippet/CPP/diagnostic-services_19.cpp)]  
  
## See Also  
 [Macros and Globals](../mfcref/mfc-macros-and-globals.md)