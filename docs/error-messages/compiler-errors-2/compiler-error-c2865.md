---
title: コンパイラ エラー C2865
ms.date: 11/04/2016
f1_keywords:
- C2865
helpviewer_keywords:
- C2865
ms.assetid: 973eb6a0-c99a-4d25-b3e5-fe0539794d77
ms.openlocfilehash: dd4374c1a577c4c39c5dec107ed5025d7cdc79c2
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80201697"
---
# <a name="compiler-error-c2865"></a>コンパイラ エラー C2865

' function ': handle_or_pointer の比較が正しくありません

[クラス、構造体](../../extensions/classes-and-structs-cpp-component-extensions.md)、またはマネージ参照型への参照は、等しいかどうかを比較して、同じオブジェクト (= =) を参照しているか、別のオブジェクト (! =) を参照しているかを調べることができます。

.NET ランタイムはマネージオブジェクトをいつでも移動し、テストの結果を変更することがあるため、順序を比較することはできません。
