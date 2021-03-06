---
title: 手動アクセサーの使用
ms.date: 10/24/2018
helpviewer_keywords:
- command handling, OLE DB Templates
- manual accessors
- accessors [C++], manual
ms.assetid: 29f00a89-0240-482b-8413-4120b9644672
ms.openlocfilehash: b76c6a2d0af404bc526fee8f511320a58ffd86ec
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87218287"
---
# <a name="using-manual-accessors"></a>手動アクセサーの使用

不明なコマンドを処理する場合は、次の4つの操作を実行します。

- パラメーターを決定する

- コマンドを実行します。

- 出力列を決定する

- 複数のリターン行セットがあるかどうかを確認する

OLE DB コンシューマーテンプレートでこれらの操作を行うには、 `CManualAccessor` クラスを使用して次の手順を実行します。

1. `CCommand`で `CManualAccessor` テンプレートパラメーターとしてオブジェクトを開きます。

    ```cpp
    CCommand<CManualAccessor, CRowset, CMultipleResults> rs;
    ```

1. インターフェイスのセッションに対してクエリ `IDBSchemaRowset` を実行し、プロシージャパラメーターの行セットを使用します。 インターフェイスが使用できない場合は、 `IDBSchemaRowset` インターフェイスを照会し `ICommandWithParameters` ます。 `GetParameterInfo`情報を参照してください。 どちらのインターフェイスも使用できない場合は、パラメーターがないと見なすことができます。

1. 各パラメーターに対してを呼び出し、 `AddParameterEntry` パラメーターを追加して設定します。

1. 行セットを開き、bind パラメーターをに設定 **`false`** します。

1. `GetColumnInfo`を呼び出して、出力列を取得します。 を使用して、 `AddBindEntry` 出力列をバインドに追加します。

1. を呼び出して、 `GetNextResult` 使用可能な行セットがあるかどうかを確認します。 手順 2. ~ 5. を繰り返します。

手動アクセサーの例については、 `CDBListView::CallProcedure` [DBVIEWER](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/ATL/OLEDB/Consumer)サンプルの「」を参照してください。

## <a name="see-also"></a>関連項目

[アクセサーの使用](../../data/oledb/using-accessors.md)
