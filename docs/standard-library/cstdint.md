---
title: '&lt;cstdint&gt;'
ms.date: 11/04/2016
f1_keywords:
- <cstdint>
ms.assetid: 87afafb2-c630-4383-a2fc-a6b47c639e21
ms.openlocfilehash: 142ea2b341dad307dea98d1406803a1e7eca5e78
ms.sourcegitcommit: 8e285a766523e653aeeb34d412dc6f615ef7b17b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80076642"
---
# <a name="ltcstdintgt"></a>&lt;cstdint&gt;

標準 C ライブラリ ヘッダー \<stdint.h> をインクルードし、関連する名前を `std` 名前空間に追加します。 このヘッダーをインクルードすると、標準 C ライブラリ ヘッダーの外部リンケージで宣言された名前が、`std` 名前空間でも宣言されます。

## <a name="syntax"></a>構文

```cpp
#include <cstdint>
```

## <a name="types"></a>型

```cpp
namespace std {
    using int8_t = signed integer type; // optional
    using int16_t = signed integer type; // optional
    using int32_t = signed integer type; // optional
    using int64_t = signed integer type; // optional
    using int_fast8_t = signed integer type;
    using int_fast16_t = signed integer type;
    using int_fast32_t = signed integer type;
    using int_fast64_t = signed integer type;
    using int_least8_t = signed integer type;
    using int_least16_t = signed integer type;
    using int_least32_t = signed integer type;
    using int_least64_t = signed integer type;
    using intmax_t = signed integer type;
    using intptr_t = signed integer type; // optional
    using uint8_t = unsigned integer type; // optional
    using uint16_t = unsigned integer type; // optional
    using uint32_t = unsigned integer type; // optional
    using uint64_t = unsigned integer type; // optional
    using uint_fast8_t = unsigned integer type;
    using uint_fast16_t = unsigned integer type;
    using uint_fast32_t = unsigned integer type;
    using uint_fast64_t = unsigned integer type;
    using uint_least8_t = unsigned integer type;
    using uint_least16_t = unsigned integer type;
    using uint_least32_t = unsigned integer type;
    using uint_least64_t = unsigned integer type;
    using uintmax_t = unsigned integer type;
    using uintptr_t = unsigned integer type; // optional
}
```

## <a name="macros"></a>マクロ

```cpp
INT_[FAST LEAST]{8 16 32 64}_MIN
[U]INT_[FAST LEAST]{8 16 32 64}_MAX
INT{MAX PTR}_MIN
[U]INT{MAX PTR}_MAX
{PTRDIFF SIG_ATOMIC WCHAR WINT}{_MAX _MIN}
SIZE_MAX

[U]INT{8 16 32 64 MAX}_C
```

## <a name="see-also"></a>参照

[ヘッダー ファイル リファレンス](../standard-library/cpp-standard-library-header-files.md)\
[C++ 標準ライブラリの概要](../standard-library/cpp-standard-library-overview.md)
