---
title: 例外処理 (C++/CLI および C++/CX)
ms.date: 10/12/2018
ms.topic: reference
helpviewer_keywords:
- structured exception handling [C++], managed exceptions
- Exception class, managed applications
- exception handling
- C++ exception handling
- exception handling, types of
- System::Exception class in managed applications
ms.assetid: ccb11fe8-6938-41ac-b477-a183e85865b9
ms.openlocfilehash: 23d65bb8056672d12e3d40f9fcab1e58bab65a3d
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87219704"
---
# <a name="exception-handling--ccli-and-ccx"></a>例外処理 (C++/CLI および C++/CX)

`/ZW` コンパイラ オプションまたは `/clr` コンパイラ オプションを指定してコンパイルされたアプリケーションでは、プログラムの実行中に発生した予期しないエラーを "*例外*" を使用して処理します。 次のトピックでは、C++/CX アプリケーションまたは C++/CLI アプリケーションでの例外処理について説明します。

## <a name="in-this-section"></a>このセクションの内容

[マネージ例外の使用に関する基本的な概念](../dotnet/basic-concepts-in-using-managed-exceptions.md)<br/>
例外のスローとブロックの使用について説明し **`try`** / **`catch`** ます。

[/Clr での例外処理動作の相違点](../dotnet/differences-in-exception-handling-behavior-under-clr.md)<br/>
C++ での例外処理の標準的な動作との相違点について説明します。

[finally](../dotnet/finally.md)<br/>
finally キーワードの使用方法について説明します。

[方法: グローバル例外ハンドラーを定義およびインストールする](../dotnet/how-to-define-and-install-a-global-exception-handler.md)<br/>
未処理の例外をキャプチャする方法を示します。

[方法: MSIL からスローされるネイティブコードの例外をキャッチする](../dotnet/how-to-catch-exceptions-in-native-code-thrown-from-msil.md)<br/>
ネイティブ コードで CLR と C++ の例外をキャッチする方法について説明します。

[方法: グローバル例外ハンドラーを定義およびインストールする](../dotnet/how-to-define-and-install-a-global-exception-handler.md)<br/>
すべての未処理の例外をキャッチする方法を示します。

## <a name="related-sections"></a>関連項目

[例外処理](../cpp/exception-handling-in-visual-cpp.md)<br/>
標準 C++ での例外処理について説明します。

## <a name="see-also"></a>関連項目

[.NET および UWP 用のコンポーネントの拡張機能](component-extensions-for-runtime-platforms.md)
