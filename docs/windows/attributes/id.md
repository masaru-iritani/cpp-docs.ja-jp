---
title: id (C++ COM 属性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.id
helpviewer_keywords:
- id attribute
ms.assetid: a48d2c99-c5d2-4f46-bf96-5ac88dcb5d0c
ms.openlocfilehash: f67bf21fbe0040884cba4a54ed8d2a230cb20cd6
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88830554"
---
# <a name="id"></a>id

メンバー関数 (インターフェイスまたはディスパッチインターフェイスのプロパティまたはメソッド) の *dispid* パラメーターを指定します。

## <a name="syntax"></a>構文

```cpp
[ id(dispid) ]
```

### <a name="parameters"></a>パラメーター

*dispid*<br/>
インターフェイスメソッドのディスパッチ ID。

## <a name="remarks"></a>解説

**Id** C++ 属性には、 [id](/windows/win32/Midl/id) MIDL 属性と同じ機能があります。

## <a name="example"></a>例

**Id**の使用方法の例については、[バインド](bindable.md)可能なの例を参照してください。

## <a name="requirements"></a>必要条件

| 属性コンテキスト | 値 |
|-|-|
|**適用対象**|インターフェイス メソッド|
|**Repeatable**|いいえ|
|**必須属性**|なし|
|**無効な属性**|なし|

詳細については、「 [属性コンテキスト](cpp-attributes-com-net.md#contexts)」を参照してください。

## <a name="see-also"></a>関連項目

[IDL 属性](idl-attributes.md)<br/>
[メソッド属性](method-attributes.md)<br/>
[データメンバー属性](data-member-attributes.md)<br/>
[既定](defaultvalue.md)<br/>
[in](in-cpp.md)<br/>
[out](out-cpp.md)
