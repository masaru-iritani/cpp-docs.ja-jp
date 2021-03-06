---
title: コンパイラ エラー C2059
ms.date: 03/26/2019
f1_keywords:
- C2059
helpviewer_keywords:
- C2059
ms.assetid: 2be4eb39-3f37-4b32-8e8d-75835e07c78a
ms.openlocfilehash: 52b389806f5bacac78750bc745cd77699eb59735
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87212879"
---
# <a name="compiler-error-c2059"></a>コンパイラ エラー C2059

構文エラー: ' token '

トークンにより、構文エラーが発生しました。

次の例では、を宣言する行に対してエラーメッセージを生成し `j` ます。

```cpp
// C2059e.cpp
// compile with: /c
// C2143 expected
// Error caused by the incorrect use of '*'.
   int j*; // C2059
```

エラーの原因を特定するには、エラーメッセージに示されている行だけでなく、その上の行も確認します。 行を調べると問題についての手掛かりが得られない場合は、エラーメッセージに示されている行と、その上の数行をコメントアウトしてください。

変数の直後にあるシンボルでエラーメッセージが発生した場合は、 **`typedef`** 変数がソースコードで定義されていることを確認します。

プリプロセッサシンボル名が識別子として再使用されると、C2059 が発生します。 次の例では、コンパイラは数値1として認識します `DIGITS.ONE` が、これは列挙型の要素名としては無効です。

```cpp
#define ONE 1

enum class DIGITS {
    ZERO,
    ONE // error C2059
};
```

シンボルが何も評価されない場合は、 **/d**_シンボル_を使用してコンパイルすると発生する可能性があるため、C2059 が返されることがあり **=** ます。

```cpp
// C2059a.cpp
// compile with: /DTEST=
#include <stdio.h>

int main() {
   #ifdef TEST
      printf_s("\nTEST defined %d", TEST);   // C2059
   #else
      printf_s("\nTEST not defined");
   #endif
}
```

C2059 が発生するもう1つのケースとして、関数の既定の引数に構造体を指定するアプリケーションをコンパイルする場合があります。 引数の既定値は式である必要があります。 たとえば、構造体の初期化に使用された初期化子リストは、式ではありません。  この問題を解決するには、必要な初期化を実行するコンストラクターを定義します。

次の例では、C2059 が生成されます。

```cpp
// C2059b.cpp
// compile with: /c
struct ag_type {
   int a;
   float b;
   // Uncomment the following line to resolve.
   // ag_type(int aa, float bb) : a(aa), b(bb) {}
};

void func(ag_type arg = {5, 7.0});   // C2059
void func(ag_type arg = ag_type(5, 7.0));   // OK
```

不適切な形式のキャストに対して C2059 が発生する可能性があります。

次の例では、C2059 が生成されます。

```cpp
// C2059c.cpp
// compile with: /clr
using namespace System;
ref class From {};
ref class To : public From {};

int main() {
   From^ refbase = gcnew To();
   To^ refTo = safe_cast<To^>(From^);   // C2059
   To^ refTo2 = safe_cast<To^>(refbase);   // OK
}
```

また、期間を含む名前空間の名前を作成しようとすると、C2059 も発生する可能性があります。

次の例では、C2059 が生成されます。

```cpp
// C2059d.cpp
// compile with: /c
namespace A.B {}   // C2059

// OK
namespace A  {
   namespace B {}
}
```

`::` `->` `.` **`template`** 次の例に示すように、名前を修飾できる演算子 (、、および) の後にキーワードを指定する必要がある場合に、C2059 が発生する可能性があります。

```cpp
template <typename T> struct Allocator {
    template <typename U> struct Rebind {
        typedef Allocator<U> Other;
    };
};

template <typename X, typename AY> struct Container {
    typedef typename AY::Rebind<X>::Other AX; // error C2059
};
```

既定では、C++ はがテンプレートではないことを前提としています。したがって、 `AY::Rebind` 次の `<` は小なり記号として解釈されます。  `Rebind`山かっこを正しく解析できるように、コンパイラにテンプレートであることを明示的に通知する必要があります。 このエラーを修正するには、次 **`template`** に示すように、依存する型の名前にキーワードを使用します。

```cpp
template <typename T> struct Allocator {
    template <typename U> struct Rebind {
        typedef Allocator<U> Other;
    };
};

template <typename X, typename AY> struct Container {
    typedef typename AY::template Rebind<X>::Other AX; // correct
};
```
