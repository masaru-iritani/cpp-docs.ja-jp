---
title: _STATIC_ASSERT マクロ
ms.date: 11/04/2016
api_location:
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
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _STATIC_ASSERT
helpviewer_keywords:
- _STATIC_ASSERT macro
ms.assetid: 89b0350c-2c2f-4be6-9786-8b1f0780a5da
ms.openlocfilehash: 78544424b727797158109fa3000ee2ebf8066cf7
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87229325"
---
# <a name="_static_assert-macro"></a>_STATIC_ASSERT マクロ

コンパイル時に式を評価し、結果が**FALSE**の場合にエラーを生成します。

## <a name="syntax"></a>構文

```C
_STATIC_ASSERT(
    booleanExpression
);
```

### <a name="parameters"></a>パラメーター

*booleanExpression*<br/>
0以外 (**TRUE**) または 0 (**FALSE**) に評価される式 (ポインターを含む)。

## <a name="remarks"></a>解説

このマクロは[_ASSERT と _ASSERTE マクロ](assert-asserte-assert-expr-macros.md)に似ていますが、 *booleanExpression*は実行時ではなくコンパイル時に評価される点が異なります。 *BooleanExpression*が**FALSE** (0) に評価される場合、[コンパイラエラー C2466](../../error-messages/compiler-errors-1/compiler-error-c2466.md)が生成されます。

## <a name="example"></a>例

この例では、 [sizeof](../../c-language/sizeof-operator-c.md) **`int`** a が2バイト以上であり、 [sizeof](../../c-language/sizeof-operator-c.md) a が1バイトであるかどうかを確認し **`long`** ます。 が1バイトを超えるため、プログラムはコンパイルされず、[コンパイラエラー C2466](../../error-messages/compiler-errors-1/compiler-error-c2466.md)が生成され **`long`** ます。

```C
// crt__static_assert.c

#include <crtdbg.h>
#include <stdio.h>

_STATIC_ASSERT(sizeof(int) >= 2);
_STATIC_ASSERT(sizeof(long) == 1);  // C2466

int main()
{
    printf("I am sure that sizeof(int) will be >= 2: %d\n",
        sizeof(int));
    printf("I am not so sure that sizeof(long) == 1: %d\n",
        sizeof(long));
}
```

## <a name="requirements"></a>必要条件

|マクロ|必須ヘッダー|
|-----------|---------------------|
|**_STATIC_ASSERT**|\<crtdbg.h>|

## <a name="see-also"></a>関連項目

[アルファベット順の関数リファレンス](crt-alphabetical-function-reference.md)<br/>
[_ASSERT、_ASSERTE、_ASSERT_EXPR マクロ](assert-asserte-assert-expr-macros.md)<br/>
