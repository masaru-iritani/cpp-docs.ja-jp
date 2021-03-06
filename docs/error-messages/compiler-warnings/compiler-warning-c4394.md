---
title: コンパイラの警告 C4394
ms.date: 11/04/2016
f1_keywords:
- C4394
helpviewer_keywords:
- C4394
ms.assetid: 5de94de0-17e3-4e7c-92f4-5c3c1b825120
ms.openlocfilehash: ad6b9624a1bf510465843167d104d1bec189bc70
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87197359"
---
# <a name="compiler-warning-c4394"></a>コンパイラの警告 C4394

'関数' : appdomain ごとのシンボルは __declspec(dllexport) と共に設定することはできません

[Appdomain](../../cpp/appdomain.md)修飾子でマークされた関数 **`__declspec`** は MSIL にコンパイルされ (ネイティブではなく)、エクスポートテーブル ([export](../../windows/export.md) **`__declspec`** 修飾子) はマネージ関数ではサポートされていません。

public アクセシビリティを持つようにマネージド関数を宣言できます。 詳細については、「[型の可視性](../../dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli.md#BKMK_Type_visibility)と[メンバーの可視性](../../dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli.md#BKMK_Member_visibility)」を参照してください。

C4394 は、常にエラーとして表示されます。  この警告は、または/wd で無効にできます `#pragma warning` 。詳細については、「 [warning](../../preprocessor/warning.md)または **/wd** [/W、/W0、/W1、/W2、/W3、/W4、/W1、/W2、/W3、/W4、/Wall、/wd、/WE、/Wo、/Wv、/wx (警告レベル)](../../build/reference/compiler-option-warning-level.md) 」を参照してください。

## <a name="example"></a>例

次の例では、C4394 が生成されます。

```cpp
// C4394.cpp
// compile with: /clr /c
__declspec(dllexport) __declspec(appdomain) int g1 = 0;   // C4394
__declspec(dllexport) int g2 = 0;   // OK
```
