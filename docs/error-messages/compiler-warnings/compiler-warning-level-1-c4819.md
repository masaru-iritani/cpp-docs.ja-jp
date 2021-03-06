---
title: コンパイラの警告 (レベル 1) C4819
ms.date: 04/08/2019
f1_keywords:
- C4819
helpviewer_keywords:
- C4819
ms.assetid: c0316e85-249c-414d-9df0-622d077c6bc2
ms.openlocfilehash: c9bf60e8eec0ee6416bda3323583f3e056fce1a8
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80174883"
---
# <a name="compiler-warning-level-1-c4819"></a>コンパイラの警告 (レベル 1) C4819

> このファイルには、現在のコードページ (*number*) では表現できない文字が含まれています。 データの損失を防ぐために、ファイルを Unicode 形式で保存してください。

C4819 は、ファイル内のすべての文字を表すことができないコードページを使用して、システムで ANSI ソースファイルをコンパイルするときに発生します。

C4819 を解決するには、いくつかの方法があります。 簡単な方法の1つは、問題のある文字を削除することです。たとえば、コメントに含まれている場合など、不要な文字を削除します。 コントロールパネルのシステムコードページを、ソースコードで使用される文字セットをサポートしているものに設定できます。 Unicode[エスケープシーケンス](/cpp/c-language/escape-sequences)を使用して、ソースコード内で基本的な ANSI 文字セットのみを使用する文字または文字列を作成できます。 最後に、バイト順マーク (BOM) とも呼ばれる、署名付きの Unicode 形式でファイルを保存できます。

Unicode 形式でファイルを保存するには、Visual Studio で **[ファイル]**  > 名前を付け **[て保存]** を選択します。 **[名前を付けてファイルを保存]** ダイアログボックスで、 **[保存]** ボタンのドロップダウンを選択し、 **[エンコード付きで保存]** を選択します。 同じファイル名に保存する場合は、ファイルを置換することを確認する必要があります。 **[保存オプションの詳細設定**] ダイアログボックスで、ファイル内のすべての文字を表すことができるエンコードを選択します。たとえば、 **Unicode (utf-8 とシグネチャ)-コードページ 65001**) を選択し、[ **OK]** をクリックします。
