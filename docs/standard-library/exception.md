---
title: '&lt;exception&gt;'
ms.date: 11/04/2016
f1_keywords:
- <exception>
helpviewer_keywords:
- exception header
ms.assetid: 28900768-5dd7-4834-b907-5e37ab3407db
ms.openlocfilehash: 1533e8238b40f6ca5dc6faaef35a65db9020defd
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88835970"
---
# <a name="ltexceptiongt"></a>&lt;exception&gt;

例外の処理に関連する型と関数を定義します。 例外処理は、システムがエラーから回復できる場合に使用されます。 例外処理では、関数からプログラムへ制御を返すための方法を利用できます。 例外処理を組み込む目的は、規則的な手順でエラーから回復する方法を実施して、プログラムの信頼性を向上させることです。

## <a name="requirements"></a>必要条件

**ヘッダー:**\<exception>

**名前空間:** std

## <a name="members"></a>メンバー

### <a name="typedefs"></a>Typedefs

|名前|説明|
|-|-|
|[exception_ptr](../standard-library/exception-typedefs.md#exception_ptr)|例外へのポインターを表す型。|
|[terminate_handler](../standard-library/exception-typedefs.md#terminate_handler)|`terminate_handler` として使用するのに適した関数へのポインターを表す型。|
|[unexpected_handler](../standard-library/exception-typedefs.md#unexpected_handler)|`unexpected_handler` として使用するのに適した関数へのポインターを表す型。|

### <a name="functions"></a>Functions

|名前|説明|
|-|-|
|[current_exception](../standard-library/exception-functions.md#current_exception)|現在の例外へのポインターを取得します。|
|[get_terminate](../standard-library/exception-functions.md#get_terminate)|現在の `terminate_handler` 関数を取得します。|
|[get_unexpected](../standard-library/exception-functions.md#get_unexpected)|現在の `unexpected_handler` 関数を取得します。|
|[make_exception_ptr](../standard-library/exception-functions.md#make_exception_ptr)|例外のコピーを保持する `exception_ptr` オブジェクトを作成します。|
|[rethrow_exception](../standard-library/exception-functions.md#rethrow_exception)|パラメーターとして渡された例外をスローします。|
|[rethrow_if_nested](../standard-library/exception-functions.md#rethrow_if_nested)|入れ子になっている場合は、をキャストし、例外をスローします。|
|[set_terminate](../standard-library/exception-functions.md#set_terminate)|プログラムの終了時に呼び出される新しい `terminate_handler` を設定します。|
|[set_unexpected](../standard-library/exception-functions.md#set_unexpected)|予期しない例外が発生したときに新しい `unexpected_handler` が存在するように設定します。|
|[解約](../standard-library/exception-functions.md#terminate)|終了ハンドラーを呼び出します。|
|[throw_with_nested](../standard-library/exception-functions.md#throw_with_nested)|入れ子になっている場合は例外をスローします。|
|[uncaught_exception](../standard-library/exception-functions.md#uncaught_exception)|**`true`** スローされた例外が現在処理されている場合にのみ、を返します。|
|[不適切](../standard-library/exception-functions.md#unexpected)|予期しないハンドラーを呼び出します。|

### <a name="classes"></a>クラス

|名前|説明|
|-|-|
|[bad_exception クラス](../standard-library/bad-exception-class.md)|このクラスは、`unexpected_handler` からスローされる例外を記述します。|
|[exception クラス](../standard-library/exception-class.md)|このクラスは、特定の式と C++ 標準ライブラリによってスローされたすべての例外の基底クラスとして機能します。|
|[nested_exception クラス](../standard-library/nested-exception-class.md)|クラスは、後で使用するためにキャプチャして格納できる例外を記述します。|

## <a name="see-also"></a>関連項目

[ヘッダーファイルのリファレンス](../standard-library/cpp-standard-library-header-files.md)\
[C++ 標準ライブラリのスレッドセーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)
