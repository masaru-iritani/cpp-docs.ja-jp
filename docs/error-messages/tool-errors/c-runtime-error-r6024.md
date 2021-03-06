---
title: C ランタイム エラー R6024
ms.date: 11/04/2016
f1_keywords:
- R6024
helpviewer_keywords:
- R6024
ms.assetid: 0fb11c0f-9b81-4cab-81bd-4785742946a5
ms.openlocfilehash: de89d2e9e2b34f40b906a5dacca4179eade23f7e
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80197198"
---
# <a name="c-runtime-error-r6024"></a>C ランタイム エラー R6024

_onexit/atexit テーブルに十分な領域がありません

> [!NOTE]
> アプリの実行中にこのエラーメッセージが表示された場合、アプリは内部メモリの問題があるため、シャットダウンされました。 このエラーが発生するのは、通常、プログラムのバグや、使用しているビジュアルC++ライブラリが破損していることが原因で、メモリが極端に不足しているか、めったに発生しない場合です。
>
> このエラーを解決するには、次の手順を試してみます。
>
> - 実行中の他のアプリケーションを閉じるか、コンピューターを再起動してメモリを解放します。
> - **コントロールパネル**の **[アプリと機能]** ページまたは **[プログラムと機能]** ページを使用して、プログラムを修復または再インストールします。
> - **コントロールパネル**の **[アプリと機能]** ページまたは **[プログラムと機能]** ページを使用して、Microsoft Visual C++再頒布可能パッケージのすべてのコピーを修復または再インストールします。
> - ソフトウェアの更新については、**コントロールパネル**の**Windows Update**を確認してください。
> - アプリの更新バージョンを確認します。 問題が解決しない場合は、アプリの製造元にお問い合わせください。

**プログラマ向けの情報**

このエラーは、`_onexit` または `atexit` 関数に使用できるメモリがなかったことが原因で発生します。 このエラーは、メモリ不足の状態が原因で発生します。 アプリの起動時にバッファーを事前に割り当てることを検討して、ユーザーデータを保存し、メモリ不足状態でアプリのクリーン終了を実行することをお勧めします。
