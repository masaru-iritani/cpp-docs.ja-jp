﻿---
title: コンパイラの警告 (レベル 1) C4216
ms.date: 11/04/2016
f1_keywords:
- C4216
helpviewer_keywords:
- C4216
ms.assetid: 211079dc-59d0-42a7-801c-2ddab21d7232
ms.openlocfilehash: b7fc44fd15f761c19ed28402a41b3bd3619b21a0
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87223266"
---
# <a name="compiler-warning-level-1-c4216"></a>コンパイラの警告 (レベル 1) C4216

非標準の拡張機能が使用されています: float long

既定の Microsoft 拡張機能 (/Ze) では、 **float 型**はとして扱わ **`double`** れます。 ANSI 互換 ([/za](../../build/reference/za-ze-disable-language-extensions.md)) ではありません。 **`double`** 互換性を維持するには、を使用します。 次の例では、C4216 が生成されます。

```cpp
// C4216.cpp
// compile with: /W1
float long a;   // C4216

// use the line below to resolve the warning
// double a;

int main() {
}
```
