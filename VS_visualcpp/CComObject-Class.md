---
title: "CComObject Class"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e2b6433b-6349-4749-b4bc-acbd7a22c8b0
caps.latest.revision: 13
manager: ghogen
translation.priority.ht: 
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
# CComObject Class
This class implements **IUnknown** for a nonaggregated object.  
  
## Syntax  
  
```  
template<  
    class Base>  
    class CComObject :  
    public Base  
```  
  
#### Parameters  
 `Base`  
 Your class, derived from [CComObjectRoot](../VS_visualcpp/CComObjectRoot-Class.md) or [CComObjectRootEx](../VS_visualcpp/CComObjectRootEx-Class.md), as well as from any other interfaces you want to support on the object.  
  
## Members  
  
### Public Constructors  
  
|Name|Description|  
|----------|-----------------|  
|[CComObject::CComObject](../Topic/CComObject::CComObject.md)|The constructor.|  
|[CComObject::~CComObject](../Topic/CComObject::~CComObject.md)|The destructor.|  
  
### Public Methods  
  
|Name|Description|  
|----------|-----------------|  
|[CComObject::AddRef](../Topic/CComObject::AddRef.md)|Increments the reference count on the object.|  
|[CComObject::CreateInstance](../Topic/CComObject::CreateInstance.md)|(Static) Creates a new `CComObject` object.|  
|[CComObject::QueryInterface](../Topic/CComObject::QueryInterface.md)|Retrieves a pointer to the requested interface.|  
|[CComObject::Release](../Topic/CComObject::Release.md)|Decrements the reference count on the object.|  
  
## Remarks  
 `CComObject` implements [IUnknown](http://msdn.microsoft.com/library/windows/desktop/ms680509) for a nonaggregated object. However, calls to `QueryInterface`, `AddRef`, and **Release** are delegated to `CComObjectRootEx`.  
  
 For more information about using `CComObject`, see the article [Fundamentals of ATL COM Objects](../VS_visualcpp/Fundamentals-of-ATL-COM-Objects.md).  
  
## Inheritance Hierarchy  
 `Base`  
  
 `CComObject`  
  
## Requirements  
 **Header:** atlcom.h  
  
##  <a name="ccomobject__addref"></a>  CComObject::AddRef  
 Increments the reference count on the object.  
  
```  
STDMETHOD_(ULONG, AddRef)();  
```  
  
### Return Value  
 This function returns the new incremented reference count on the object. This value may be useful for diagnostics or testing.  
  
##  <a name="ccomobject__ccomobject"></a>  CComObject::CComObject  
 The constructor increments the module lock count.  
  
```  
CComObject(  
    void* = NULL   
   );  
```  
  
### Parameters  
 **void\***  
 [in] This unnamed parameter is not used. It exists for symmetry with other **CCom***XXX*`Object`*XXX* constructors.  
  
### Remarks  
 The destructor decrements it.  
  
 If a `CComObject`-derived object is successfully constructed using the **new** operator, the initial reference count is 0. To set the reference count to the proper value (1), make a call to the [AddRef](../Topic/CComObject::AddRef.md) function.  
  
##  <a name="ccomobject___dtorccomobject"></a>  CComObject::~CComObject  
 The destructor.  
  
```  
CComObject();  
```  
  
### Remarks  
 Frees all allocated resources, calls [FinalRelease](../Topic/CComObjectRootEx::FinalRelease.md), and decrements the module lock count.  
  
##  <a name="ccomobject__createinstance"></a>  CComObject::CreateInstance  
 This static function allows you to create a new **CComObject<**`Base`**>** object, without the overhead of [CoCreateInstance](http://msdn.microsoft.com/library/windows/desktop/ms686615).  
  
```  
static HRESULT WINAPI CreateInstance(  
    CComObject< Base  
    >** pp );  
```  
  
### Parameters  
 `pp`  
 [out] A pointer to a **CComObject<**`Base`**>** pointer. If `CreateInstance` is unsuccessful, `pp` is set to **NULL**.  
  
### Return Value  
 A standard `HRESULT` value.  
  
### Remarks  
 The object returned has a reference count of zero, so call `AddRef` immediately, then use **Release** to free the reference on the object pointer when you're done.  
  
 If you do not need direct access to the object, but still want to create a new object without the overhead of `CoCreateInstance`, use [CComCoClass::CreateInstance](../Topic/CComCoClass::CreateInstance.md) instead.  
  
### Example  
 [!CODE [NVC_ATL_COM#38](../CodeSnippet/VS_Snippets_Cpp/NVC_ATL_COM#38)]  
  
 [!CODE [NVC_ATL_COM#39](../CodeSnippet/VS_Snippets_Cpp/NVC_ATL_COM#39)]  
  
##  <a name="ccomobject__queryinterface"></a>  CComObject::QueryInterface  
 Retrieves a pointer to the requested interface.  
  
```  
STDMETHOD(QueryInterface)(  
    REFIID iid,  
    void** ppvObject );  
  
    template <class Q>  
    HRESULT STDMETHODCALLTYPE QueryInterface(  
    Q** pp );  
```  
  
### Parameters  
 `iid`  
 [in] The identifier of the interface being requested.  
  
 `ppvObject`  
 [out] A pointer to the interface pointer identified by `iid`. If the object does not support this interface, `ppvObject` is set to **NULL**.  
  
 `pp`  
 [out] A pointer to the interface pointer identified by type `Q`. If the object does not support this interface, `pp` is set to **NULL**.  
  
### Return Value  
 A standard `HRESULT` value.  
  
##  <a name="ccomobject__release"></a>  CComObject::Release  
 Decrements the reference count on the object.  
  
```  
STDMETHOD_(ULONG, Release)();  
```  
  
### Return Value  
 This function returns the new decremented reference count on the object. In debug builds, the return value may be useful for diagnostics or testing. In non-debug builds,                         **Release** always returns 0.  
  
## See Also  
 [CComAggObject Class](../VS_visualcpp/CComAggObject-Class.md)   
 [CComPolyObject Class](../VS_visualcpp/CComPolyObject-Class.md)   
 [DECLARE_AGGREGATABLE](../Topic/DECLARE_AGGREGATABLE.md)   
 [DECLARE_NOT_AGGREGATABLE](../Topic/DECLARE_NOT_AGGREGATABLE.md)   
 [Class Overview](../VS_visualcpp/ATL-Class-Overview.md)