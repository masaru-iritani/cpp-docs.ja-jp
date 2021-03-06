---
title: コンパイラの警告 (レベル 1) C4346
ms.date: 11/04/2016
f1_keywords:
- C4346
helpviewer_keywords:
- C4346
ms.assetid: 68ee562d-cca9-4a2a-9a1b-14ad1a1e7396
ms.openlocfilehash: f1f731eed2dae2721b13bb2e526992849e217f7f
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87223201"
---
# <a name="compiler-warning-level-1-c4346"></a>コンパイラの警告 (レベル 1) C4346

' name ': 依存名は型ではありません

依存名を型として扱う場合は、 [typename](../../cpp/typename.md)キーワードを指定する必要があります。 Visual C++ のすべてのバージョンで同じように動作するコードの場合は、を **`typename`** 宣言に追加します。

次の例では、C4346 が生成されます。

```cpp
// C4346.cpp
// compile with: /WX /LD
template<class T>
struct C {
   T::X* x;   // C4346
   // try the following line instead
   // typename T::X* x;
};
```

次のサンプルは、キーワードが必要なその他の例を示して **`typename`** います。

```cpp
// C4346b.cpp
// compile with: /LD /W1
template<class T>
const typename T::X& f(typename T::Z* p);   // Required in both places

template<class T, int N>
struct L{};

template<class T>
struct M : public L<typename T::Type, T::Value>
{   // required on type argument, not on non-type argument
   typedef typename T::X   Type;
   Type f();   // OK: "Type" is a type-specifer
   typename T::X g();   // typename required
   operator typename T::Z();   // typename required
};
```

でこれを

```cpp
// C4346c.cpp
// compile with: /LD /WX
struct Y {
   typedef int Y_t;
};

template<class T>
struct A {
   typedef Y A_t;
};

template<class T>
struct B {
   typedef /*typename*/ A<T>::A_t B_t;   // C4346 typename needed here
   typedef /*typename*/ B_t::Y_t  B_t2;   // typename also needed here
};
```
