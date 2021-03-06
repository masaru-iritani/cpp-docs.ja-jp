---
title: /std (言語の標準バージョンの指定)
ms.date: 06/04/2020
f1_keywords:
- /std
- -std
- VC.Project.VCCLCompilerTool.CppLanguageStandard
ms.assetid: 0acb74ba-1aa8-4c05-b96c-682988dc19bd
ms.openlocfilehash: 9755194d70774f27af4c5174151588cc03d5f97a
ms.sourcegitcommit: 65fead53d56d531d71be42216056aca5f44def11
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88610960"
---
# <a name="std-specify-language-standard-version"></a>`/std` (言語の標準バージョンの指定)

指定したバージョンの C++ 言語標準でサポートされる C++ 言語機能を有効にします。

## <a name="syntax"></a>構文

> **`/std:c++14`**\
> **`/std:c++17`**\
> **`/std:c++latest`**

## <a name="remarks"></a>解説

この **`/std`** オプションは、Visual Studio 2017 以降で使用できます。 これは、コードのコンパイル中に有効になっているバージョン固有の ISO C++ プログラミング言語の標準機能を制御するために使用されます。 このオプションを使用すると、言語標準の特定のバージョンに準拠している既存のコードを破壊する可能性のある、新しい言語およびライブラリ機能のサポートを無効にできます。 既定で **`/std:c++14`** は、が指定されています。これにより、C++ 言語標準の以降のバージョンの言語および標準ライブラリ機能が無効になります。 を使用し  **`/std:c++17`** て、c++ 17 の標準固有の機能と動作を有効にします。 現在実装されているコンパイラと、次のドラフト標準に提案されている標準ライブラリ機能を明示的に有効にするには、を使用し **`/std:c++latest`** ます。 C++ 20 のすべての機能にはが必要 **`/std:c++latest`** です。実装が完了すると、新しいオプションが有効になり **`/std:c++20`** ます。

既定のオプションでは、 **`/std:c++14`** MSVC コンパイラによって実装された c++ 14 の機能のセットが有効になります。 このオプションを使用すると、言語標準のより新しいバージョンで変更された機能または新しい機能に対するコンパイラと標準ライブラリのサポートが無効になります。 以前のリリースの MSVC コンパイラで既に実装されている C++ 17 の一部の機能を無効にすることはできません。 Visual Studio 2015 Update 2 で使用可能な機能に対して既に依存関係を取得しているユーザーの重大な変更を回避するために、これらの機能 **`/std:c++14`** はオプションが指定されている場合は有効のままになります。

- [かっこ付きを `auto` 使用したの規則](https://wg21.link/n3922)

- [`typename` テンプレートテンプレートのパラメーター](https://wg21.link/n4051)

- [トライグラフの削除](https://wg21.link/n4086)

- [名前空間と列挙子の属性](https://wg21.link/n4266)

- [u8 文字リテラル](https://wg21.link/n4267)

を指定したときに有効になる C++ 14 と C++ 17 の機能の一覧 **`/std:c++14`** があります。 詳細については、「 [Microsoft C++ 言語準拠テーブル](../../overview/visual-cpp-language-conformance.md)」のメモを参照してください。

オプションを使用すると、 **`/std:c++17`** MSVC コンパイラによって実装された c++ 17 のすべての機能が有効になります。 このオプションを選択すると、C++ 17 以降で追加または変更された機能に対するコンパイラと標準ライブラリのサポートが無効になります。 これには、C++ 標準の作業ドラフトおよび欠陥更新のバージョンでの C + + 17 の変更が含まれます。

オプションを使用すると、 **`/std:c++latest`** コンパイラおよびライブラリで現在実装されている C + + 17 言語およびライブラリの機能が有効になります。 これらの機能には、C++ 20 の作業ドラフトからの変更、C++ 17 に含まれていない欠陥のある更新、およびドラフト標準の試験的な提案が含まれる場合があります。 サポート対象の言語およびライブラリ機能については、[Visual C++ の新機能](../../overview/what-s-new-for-visual-cpp-in-visual-studio.md)に関するページを参照してください。 オプションは、 **`/std:c++latest`** スイッチによって保護されている機能を有効にしません **`/experimental`** が、有効にする必要がある場合があります。

> [!IMPORTANT]
> によって有効になるコンパイラおよびライブラリの機能は、 **`/std:c++latest`** 将来の c++ 標準で表示される可能性がある機能と、承認された c++ 20 の機能を表します。 承認されていない機能では、破壊的変更や通知なしでの削除が起こる可能性があり、これは無保証で提供されています。

**`/std`** C++ のコンパイル中に有効なオプションは、 [ \_ MSVC \_ LANG](../../preprocessor/predefined-macros.md)プリプロセッサマクロを使用して検出できます。 詳細については、[プリプロセッサ マクロ](../../preprocessor/predefined-macros.md)に関するページを参照してください。

**`/std:c++14`** およびオプションは、 **`/std:c++latest`** Visual Studio 2015 Update 3 以降で使用できます。 この **`/std:c++17`** オプションは、Visual Studio 2017 バージョン15.3 以降で使用できます。 前述のように、一部の C++ 17 標準動作はオプションによって有効になってい **`/std:c++14`** ますが、その他の c++ 17 機能はすべてによって有効になってい **`/std:c++17`** ます。 C++ 20 の機能は **`/std:c++latest`** 、実装が完了するまでによって有効になります。

> [!NOTE]
> MSVC コンパイラのバージョンまたは更新レベルによっては、C++ 17 の機能が完全に実装されていないか、オプションを指定したときに完全に準拠していない可能性があり **`/std:c++17`** ます。 リリースバージョン別の Visual C++ における C++ 言語準拠の概要については、「 [Microsoft c++ 言語準拠テーブル](../../overview/visual-cpp-language-conformance.md)」を参照してください。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 開発環境でこのコンパイラ オプションを設定するには

1. プロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。 詳細については、[Visual Studio での C++ コンパイラとビルド プロパティの設定](../working-with-project-properties.md)に関するページを参照してください。

1. **[構成プロパティ]**、**[C/C++]**、**[言語]** の順に選択します。

1. **[C++ 言語標準]** のドロップダウン コントロールからサポートする言語標準を選択し、**[OK]** または **[適用]** を選択して変更を保存します。

## <a name="see-also"></a>関連項目

[MSVC コンパイラ オプション](compiler-options.md)<br/>
[MSVC コンパイラのコマンドライン構文](compiler-command-line-syntax.md)
