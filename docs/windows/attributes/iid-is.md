---
title: iid_is (C++ COM 属性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.iid_is
helpviewer_keywords:
- iid_is attribute
ms.assetid: 2f9b42a9-7130-4b08-9b1e-0d5d360e10ff
ms.openlocfilehash: 6a8fe8c7481cd251baff65293607733573f46ea6
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88832218"
---
# <a name="iid_is"></a>iid_is

インターフェイスポインターが指す COM インターフェイスの IID を指定します。

## <a name="syntax"></a>構文

```cpp
[ iid_is("expression") ]
```

### <a name="parameters"></a>パラメーター

*式 (expression)*<br/>
インターフェイスポインターが指す COM インターフェイスの IID を指定する C 言語式。

## <a name="remarks"></a>解説

**Iid_is** C++ 属性には、 [iid_is](/windows/win32/Midl/iid-is) MIDL 属性と同じ機能があります。

## <a name="example"></a>例

次のコードは、 **iid_is**の使用方法を示しています。

```cpp
// cpp_attr_ref_iid_is.cpp
// compile with: /LD
#include "wtypes.h"
#include "unknwn.h"
[dispinterface, uuid("00000000-0000-0000-0000-000000000001")]
__interface IFireTabCtrl : IDispatch
{
   [id(1)] HRESULT CreateInstance([in] REFIID riid,[out, iid_is("riid")]
   IUnknown ** ppvObject);
};

[module(name="ATLFIRELib")];
```

## <a name="requirements"></a>必要条件

| 属性コンテキスト | 値 |
|-|-|
|**適用対象**|インターフェイスパラメーター、データメンバー|
|**Repeatable**|いいえ|
|**必須属性**|なし|
|**無効な属性**|なし|

詳細については、「 [属性コンテキスト](cpp-attributes-com-net.md#contexts)」を参照してください。

## <a name="see-also"></a>関連項目

[IDL 属性](idl-attributes.md)<br/>
[パラメーター属性](parameter-attributes.md)
