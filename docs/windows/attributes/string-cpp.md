---
title: string (C++ COM 属性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.string
helpviewer_keywords:
- string attribute
ms.assetid: ddde900a-2e99-4fcd-86e8-57e1bdba7c93
ms.openlocfilehash: 119e0aa60d123324c60825a9418e0b8c93696c5f
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88845381"
---
# <a name="string-c"></a>string (C++)

1次元の、 **`char`** **`wchar_t`** 、 `byte` (または同等の) 配列、またはこのような配列へのポインターを文字列として扱う必要があることを示します。

## <a name="syntax"></a>構文

```cpp
[string]
```

## <a name="remarks"></a>解説

**String** C++ 属性には、[文字列](/windows/win32/Midl/string)MIDL 属性と同じ機能があります。

## <a name="example"></a>例

次のコードは、インターフェイスおよび typedef で **文字列** を使用する方法を示しています。

```cpp
// cpp_attr_ref_string.cpp
// compile with: /LD
#include "unknwn.h"
[module(name="ATLFIRELib")];
[export, string] typedef char a[21];
[dispinterface, restricted, uuid("00000000-0000-0000-0000-000000000001")]
__interface IFireTabCtrl
{
   [id(1)] HRESULT Method3([in, string] char *pC);
};
```

## <a name="requirements"></a>必要条件

| 属性コンテキスト | 値 |
|-|-|
|**適用対象**|配列または配列へのポインター、インターフェイスパラメーター、インターフェイスメソッド|
|**Repeatable**|いいえ|
|**必須属性**|なし|
|**無効な属性**|なし|

属性コンテキストの詳細については、「 [属性コンテキスト](cpp-attributes-com-net.md#contexts)」を参照してください。

## <a name="see-also"></a>関連項目

[IDL 属性](idl-attributes.md)<br/>
[配列属性](array-attributes.md)<br/>
[輸出](export.md)
