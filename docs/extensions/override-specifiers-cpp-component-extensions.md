---
title: オーバーライド指定子 (C++/CLI および C++/CX)
ms.date: 10/12/2018
ms.topic: reference
helpviewer_keywords:
- override specifiers, C++
- override specifiers
ms.assetid: 155bbf6f-4722-4654-afb1-9cb52af799fb
ms.openlocfilehash: 410fe9ecc48b92c68132f7b1b8057c2549c8afcf
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80181903"
---
# <a name="override-specifiers--ccli-and-ccx"></a>オーバーライド指定子 (C++/CLI および C++/CX)

*オーバーライド指定子*は、継承された型および継承された型のメンバーの派生型での動作を変更します。

## <a name="all-runtimes"></a>すべてのランタイム

### <a name="remarks"></a>解説

オーバーライド指定子の詳細については、以下を参照してください。

- [abstract](abstract-cpp-component-extensions.md)

- [new (vtable の新しいスロット)](new-new-slot-in-vtable-cpp-component-extensions.md)

- [override](override-cpp-component-extensions.md)

- [sealed](sealed-cpp-component-extensions.md)

- [オーバーライド指定子とネイティブ コンパイル](../dotnet/how-to-declare-override-specifiers-in-native-compilations-cpp-cli.md)

**abstract** と **sealed** は型宣言でも有効ですが、その場合はオーバーライド指定子として機能しません。

基底クラスの関数を明示的にオーバーライドする方法については、「[Explicit Overrides (明示的なオーバーライド)](explicit-overrides-cpp-component-extensions.md)」を参照してください。

## <a name="windows-runtime"></a>Windows ランタイム

(この言語機能には Windows ランタイムのみに適用される特記事項がありません。)

### <a name="requirements"></a>必要条件

コンパイラ オプション: `/ZW`

## <a name="common-language-runtime"></a>共通言語ランタイム

(この言語機能には共通言語ランタイムのみに適用される特記事項がありません。)

### <a name="requirements"></a>必要条件

コンパイラ オプション: `/clr`

## <a name="see-also"></a>参照

[.NET および UWP でのコンポーネント拡張](component-extensions-for-runtime-platforms.md)
