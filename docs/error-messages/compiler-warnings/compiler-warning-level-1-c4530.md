---
title: コンパイラの警告 (レベル 1) C4530
description: Microsoft C++ コンパイラの警告 C4530 のリファレンスガイド。
ms.date: 04/02/2020
f1_keywords:
- C4530
helpviewer_keywords:
- C4530
ms.assetid: a04dcdb2-84db-459d-9e5e-4e743887465f
ms.openlocfilehash: fe0a2b4c8eb881327f3e59d66e7e6941f0a2cad8
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87230663"
---
# <a name="compiler-warning-level-1-c4530"></a>コンパイラの警告 (レベル 1) C4530

> C++ 例外ハンドラーが使用されましたが、アンワインドセマンティクスが有効になっていません。 /EHsc を指定する

このコードでは C++ 例外処理を使用しますが、 [/ehsc](../../build/reference/eh-exception-handling-model.md)はコンパイラオプションに含まれていませんでした。

## <a name="remarks"></a>解説

コンパイラでは、 **`/EHsc`** c++ 標準に従って例外処理を行う c++ コードをビルドするオプションが必要です。 標準 C++*アンワインドセマンティクス*は、例外がスローされる場所とキャッチされる場所との間に構築されるオブジェクトとスタックフレームを破棄し、リソースを回復する必要があることを指定します。 このプロセスは *、スタックのアンワインド*と呼ばれます。

オプションは、 **`/EHsc`** 例外がコンテナーのスタックフレームを通過したときに、自動ストレージオブジェクトに対してデストラクターを呼び出すコードを生成するようコンパイラに指示します。 *自動ストレージ*オブジェクトは、ローカル変数など、スタック上に割り当てられたオブジェクトです。 自動ストレージと呼ばれます。これは、関数が呼び出されたときに自動的に割り当てられ、を返したときに自動的に解放されるためです。 *スタックフレーム*は、関数が呼び出されたときにスタックに配置されたデータであり、自動ストレージと共に使用されます。

例外がスローされた場合は、キャッチされる前に、複数のスタックフレームを通過することがあります。 これらのスタックフレームは、逆呼び出し順序で例外が渡されるため、アンワインドする必要があります。 各スタックフレーム内の自動ストレージオブジェクトは、リソースを正常に復旧するために破棄する必要があります。 関数が正常に返されたときに自動的に実行される破棄および回復プロセスと同じです。

このオプションが有効になっていない場合 **`/EHsc`** 、スロー関数と例外がキャッチされる関数の間のスタックフレーム内の自動ストレージオブジェクトは破棄されません。 またはブロック内に作成された自動ストレージオブジェクトのみが破棄され **`try`** **`catch`** ます。これにより、大量のリソースリークやその他の予期しない動作が発生する可能性があります。

実行可能ファイルで例外がスローされない可能性がある場合は、この警告を無視しても問題ありません。 コードによっては、他の例外処理オプションが必要になる場合があります。 詳細については、「 [/EH](../../build/reference/eh-exception-handling-model.md)」を参照してください。

## <a name="example"></a>例

次の例では、C4530 が生成されます。

```cpp
// C4530.cpp
// compile with: /W1
int main() {
   try{} catch(int*) {}   // C4530
}
```

警告を解決するには、を使用してサンプルをコンパイルし **`/EHsc`** ます。
