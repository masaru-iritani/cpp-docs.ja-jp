---
title: コンパイラの警告 (レベル 1) C4091
ms.date: 11/04/2016
f1_keywords:
- C4091
helpviewer_keywords:
- C4091
ms.assetid: 3a404967-ab42-49b0-b324-fd7ba1859d78
ms.openlocfilehash: 333f76c2f570832c9d08a7ad666f2540cca37f05
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87233341"
---
# <a name="compiler-warning-level-1-c4091"></a>コンパイラの警告 (レベル 1) C4091

' keyword ': 変数が宣言されていない場合、' type ' の左側では無視されます

コンパイラは、ユーザーが宣言される変数を想定していたのに、コンパイラが変数を宣言できなかった状況を検出しました。

## <a name="example"></a>例

**`__declspec`** ユーザー定義型の宣言の先頭にある属性は、その型の変数に適用されます。 C4091 は、変数が宣言されていないことを示します。 次の例では、C4091 が生成されます。

```cpp
// C4091.cpp
// compile with: /W1 /c
__declspec(dllimport) class X {}; // C4091

// __declspec attribute applies to varX
__declspec(dllimport) class X2 {} varX;

// __declspec attribute after the class or struct keyword
// applies to user defined type
class __declspec(dllimport) X3 {};
```

## <a name="example"></a>例

識別子が typedef の場合は、変数名にすることもできません。 次の例では、C4091 が生成されます。

```cpp
// C4091_b.cpp
// compile with: /c /W1 /WX
#define LIST 4
typedef struct _LIST {} LIST;   // C4091
```
