---
title: process
ms.date: 11/04/2016
f1_keywords:
- process_cpp
helpviewer_keywords:
- __declspec keyword [C++], process
- process __declspec keyword
ms.assetid: 60eecc2f-4eef-4567-b9db-aaed34733023
ms.openlocfilehash: f684c9c2ddfcb0aa166e1240c5f928ee52218f45
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87227206"
---
# `process`

マネージド アプリケーション プロセスが、プロセス内のすべてのアプリケーション ドメイン間で共有される特定のグローバル変数、静的メンバー変数、または静的ローカル変数のコピーを 1 つ持つことを指定します。 これは主に **`/clr:pure`** 、Visual studio 2015 で非推奨とされ、Visual studio 2017 ではサポートされていない、でコンパイルするときに使用することを目的としていました。 を使用してコンパイルする場合 **`/clr`** 、グローバル変数と静的変数は既定でプロセスごとに使用されるため、を使用する必要はありません **`__declspec(process)`** 。

でマークできるのは、グローバル変数、静的メンバー変数、またはネイティブ型の静的ローカル変数だけ **`__declspec(process)`** です。

**`process`** は、を使用してコンパイルする場合にのみ有効です [`/clr`](../build/reference/clr-common-language-runtime-compilation.md) 。

各アプリケーションドメインがグローバル変数の独自のコピーを持つようにするには、 [appdomain](../cpp/appdomain.md)を使用します。

詳細については[、「アプリケーションドメインと Visual C++](../dotnet/application-domains-and-visual-cpp.md) 」を参照してください。

## <a name="see-also"></a>関連項目

[`__declspec`](../cpp/declspec.md)<br/>
[キーワード](../cpp/keywords-cpp.md)
