---
title: コンパイラの警告 C4484
ms.date: 11/04/2016
f1_keywords:
- C4484
helpviewer_keywords:
- C4484
ms.assetid: 3d30e5b3-2297-45b7-a37a-1360056fdd0e
ms.openlocfilehash: c168c91f8259b744ed10dd72701d34fd60b98681
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80165159"
---
# <a name="compiler-warning-c4484"></a>コンパイラの警告 C4484

' override_function ': 基本 ref クラスメソッド ' base_class_function ' と一致しますが、' virtual '、' new '、' override ' に設定されていません。' new ' (' virtual ' ではなく) が想定されています

**/Clr**を指定してコンパイルする場合、コンパイラは基底クラスの関数を暗黙的にオーバーライドしません。これは、関数が vtable 内の新しいスロットを取得することを意味します。 解決するには、関数がオーバーライドであるかどうかを明示的に指定します。

詳細については、次を参照してください。

- [/clr (共通言語ランタイムのコンパイル)](../../build/reference/clr-common-language-runtime-compilation.md)

- [override](../../extensions/override-cpp-component-extensions.md)

- [new (vtable の新しいスロット)](../../extensions/new-new-slot-in-vtable-cpp-component-extensions.md)

C4484 は常にエラーとして発行されます。 C4484 を抑制するには、 [warning](../../preprocessor/warning.md)プラグマを使用します。

## <a name="example"></a>例

次の例では、C4484 が生成されます。

```cpp
// C4484.cpp
// compile with: /clr
ref struct A {
   virtual void Test() {}
};

ref struct B : A {
   void Test() {}   // C4484
};

// OK
ref struct C {
   virtual void Test() {}
   virtual void Test2() {}
};

ref struct D : C {
   virtual void Test() new {}
   virtual void Test2() override {}
};
```
