---
title: リンカ ツール エラー LNK2019
description: リンカーエラー LNK2019 の Microsoft Visual Studio と、C および C++ コードで診断および修正する方法について説明します。
ms.date: 01/15/2020
f1_keywords:
- LNK2019
helpviewer_keywords:
- nochkclr.obj
- LNK2019
- _check_commonlanguageruntime_version
no-loc:
- ':::no-loc(main):::'
- ':::no-loc(WinMain):::'
- ':::no-loc(wmain):::'
- ':::no-loc(wWinMain):::'
- ':::no-loc(__cdecl):::'
- ':::no-loc(__stdcall):::'
- ':::no-loc(__fastcall):::'
- ':::no-loc(__vectorcall):::'
- ':::no-loc(extern):::'
- ':::no-loc(static):::'
- ':::no-loc(const):::'
- ':::no-loc(ARCH):::'
- ':::no-loc(AVX2):::'
- ':::no-loc(wchar_t):::'
- ':::no-loc(VERBOSE):::'
- ':::no-loc(EXPORTS):::'
- ':::no-loc(SYMBOLS):::'
- ':::no-loc(DUMPBIN):::'
- ':::no-loc(UNDNAME):::'
ms.openlocfilehash: b83ed3663e6b199e0f3384f6d30cb1c87c0e52c4
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87219808"
---
# <a name="linker-tools-error-lnk2019"></a>リンカ ツール エラー LNK2019

> 未解決の :::no-loc(extern)::: al シンボル '*symbol*' が関数 '*function*' で参照されています

コンパイルされた*関数*のコードは、*シンボル*への参照または呼び出しを行いますが、リンカーはリンクするライブラリまたはオブジェクトファイルでシンボル定義を見つけることができません。

このエラーメッセージの後には、致命的なエラー [LNK1120](../../error-messages/tool-errors/linker-tools-error-lnk1120.md)が続きます。 エラー LNK1120 を修正するには、最初にすべての LNK2001 および LNK2019 エラーを修正する必要があります。

## <a name="possible-causes"></a>考えられる原因

このエラーを取得するには、さまざまな方法があります。 これらのすべてには、リンカーが*解決*できなかった関数または変数への参照、またはの定義を見つけることが含まれます。 コンパイラは、シンボルが*宣言*されているかどうかを識別できますが、シンボルが*定義されて*いないことを示すことはできません。 これは、定義が別のソースファイルまたはライブラリに存在する可能性があるためです。 シンボルが参照されているが定義されていない場合、リンカーは未解決の :::no-loc(extern)::: al シンボルエラーを生成します。

LNK2019 エラーが発生する一般的な問題には次のものがあります。

### <a name="the-source-file-that-contains-the-definition-of-the-symbol-isnt-compiled"></a>シンボルの定義を含むソースファイルはコンパイルされません。

Visual Studio で、シンボルを定義するソースファイルがプロジェクトの一部としてコンパイルされていることを確認します。 中間ビルド出力ディレクトリに一致する .obj ファイルがあるかどうかを確認します。 ソースファイルがコンパイルされていない場合はソリューションエクスプローラーでファイルを右クリックし、[**プロパティ**] を選択して、ファイルのプロパティを確認します。 **構成プロパティの**  >  **[全般**] ページには、 **C/c + + コンパイラ**の項目の**種類**が表示されます。 コマンドラインで、定義を含むソースファイルがコンパイルされていることを確認します。

### <a name="the-object-file-or-library-that-contains-the-definition-of-the-symbol-isnt-linked"></a>シンボルの定義を含むオブジェクトファイルまたはライブラリがリンクされていません

Visual Studio で、シンボル定義を含むオブジェクトファイルまたはライブラリがプロジェクトの一部としてリンクされていることを確認します。 コマンドラインで、リンクするファイルの一覧にオブジェクトファイルまたはライブラリが含まれていることを確認します。

### <a name="the-declaration-of-the-symbol-isnt-spelled-the-same-as-the-definition-of-the-symbol"></a>シンボルの宣言のスペルがシンボルの定義と同じではありません

宣言と定義の両方で正しいスペルと大文字小文字が使用されていること、およびシンボルが使用または呼び出された場所であることを確認します。

### <a name="a-function-is-used-but-the-type-or-number-of-the-parameters-dont-match-the-function-definition"></a>関数が使用されていますが、パラメーターの型または数が関数の定義と一致しません

関数の宣言は、定義と一致している必要があります。 関数呼び出しが宣言と一致し、宣言が定義と一致していることを確認します。 また、テンプレート関数を呼び出すコードでも、テンプレート関数の宣言を一致させ、定義と同じテンプレート パラメーターを組み込む必要があります。 テンプレート宣言の不一致の例については、「例」の「sample LNK2019e」を参照してください。

### <a name="a-function-or-variable-is-declared-but-not-defined"></a>関数または変数が宣言されていますが、定義されていません。

LNK2019 は、ヘッダーファイルに宣言が存在するが、一致する定義が実装されていない場合に発生する可能性があります。 メンバー関数または :::no-loc(static)::: データメンバーの場合、実装にはクラススコープセレクターを含める必要があります。 例については、「 [Missing Function Body or Variable](../../error-messages/tool-errors/missing-function-body-or-variable.md)」を参照してください。

### <a name="the-calling-convention-is-different-between-the-function-declaration-and-the-function-definition"></a>呼び出し規則が関数宣言と関数定義で異なっています。

呼び出し規則 ( [:::no-loc(__cdecl):::](../../cpp/cdecl.md) 、 [:::no-loc(__stdcall):::](../../cpp/stdcall.md) 、 [:::no-loc(__fastcall):::](../../cpp/fastcall.md) 、または [:::no-loc(__vectorcall):::](../../cpp/vectorcall.md) ) は、装飾名の一部としてエンコードされます。 呼び出し規則が同じであることを確認します。

### <a name="a-symbol-is-defined-in-a-c-file-but-declared-without-using-no-locextern-c-in-a-c-file"></a>シンボルは C ファイルで定義されていますが、 :::no-loc(extern)::: C++ ファイルで "C" を使用せずに宣言されています。

C としてコンパイルされたファイルで定義されたシンボルは、 [ :::no-loc(extern)::: "C"](../../cpp/using-:::no-loc(extern):::-to-specify-linkage.md)修飾子を使用しない限り、C++ ファイルで宣言されているシンボルとは異なる装飾名を持ちます。 宣言がシンボルごとにコンパイルリンケージと一致していることを確認します。 同様に、C++ ファイルで定義されているシンボルを C プログラムで使用する場合にも、定義の中で `:::no-loc(extern)::: "C"` を使用します。

### <a name="a-symbol-is-defined-as-no-locstatic-and-then-later-referenced-outside-the-file"></a>シンボルはとして定義され、 :::no-loc(static)::: 後でファイルの外部で参照されます。

C++ では、C とは異なり、[グローバル :::no-loc(const)::: に](../../error-messages/tool-errors/global-:::no-loc(const):::ants-in-cpp.md)はリンケージがあり **`:::no-loc(static):::`** ます。 この制限を回避するには、初期化を **`:::no-loc(const):::`** ヘッダーファイルに含め、そのヘッダーを .cpp ファイルにインクルードします。または、変数を非 :::no-loc(const)::: ant にして、ant 参照を使用してアクセスすることもできます :::no-loc(const)::: 。

### <a name="a-no-locstatic-member-of-a-class-isnt-defined"></a>:::no-loc(static):::クラスのメンバーが定義されていません

:::no-loc(static):::クラスメンバーには一意の定義が必要です。または、1つの定義規則に違反します。 :::no-loc(static):::インラインで定義できないクラスメンバーは、完全修飾名を使用して1つのソースファイルで定義する必要があります。 まったく定義されていない場合、リンカーは LNK2019 を生成します。

### <a name="a-build-dependency-is-only-defined-as-a-project-dependency-in-the-solution"></a>ビルドの依存関係は、ソリューション内のプロジェクトの依存関係としてのみ定義されます

以前のバージョンの Visual Studio では、このレベルの依存関係で十分でした。 ただし、visual Studio 2010 以降では、Visual Studio でプロジェクト[間参照](/visualstudio/ide/managing-references-in-a-project)が必要になります。 プロジェクトがプロジェクト間参照を持っていない場合は、このリンカーエラーが発生することがあります。 この問題を修正するには、プロジェクト間参照を追加します。

### <a name="an-entry-point-isnt-defined"></a>エントリポイントが定義されていません

アプリケーションコードでは、適切なエントリポイント ( `:::no-loc(main):::` `:::no-loc(wmain):::` コンソールアプリケーションの場合) また `:::no-loc(WinMain):::` は ( `:::no-loc(wWinMain):::` Windows アプリケーションの場合) を定義する必要があります。 詳細については、「 [ :::no-loc(main)::: 関数とコマンドライン引数](../../cpp/:::no-loc(main):::-function-command-line-args.md)または[ :::no-loc(WinMain)::: 関数](/windows/win32/api/winbase/nf-winbase-win:::no-loc(main):::)」を参照してください。 カスタムエントリポイントを使用するには、 [/entry (エントリポイントシンボル)](../../build/reference/entry-entry-point-symbol.md)リンカーオプションを指定します。

### <a name="you-build-a-console-application-by-using-settings-for-a-windows-application"></a>Windows アプリケーションの設定を使用してコンソールアプリケーションを作成する

エラーメッセージが、関数*function_name* ** :::no-loc(extern)::: :::no-loc(WinMain)::: で参照**されている未解決の al シンボルと類似している場合は、 **/SUBSYSTEM: WINDOWS**ではなく **/SUBSYSTEM: CONSOLE**を使用してリンクします。 この設定の詳細と、Visual Studio でこのプロパティを設定する手順の詳細については、「 [/SUBSYSTEM (Specify Subsystem)](../../build/reference/subsystem-specify-subsystem.md)」を参照してください。

### <a name="you-attempt-to-link-64-bit-libraries-to-32-bit-code-or-32-bit-libraries-to-64-bit-code"></a>64ビットライブラリを32ビットコードに、または32ビットライブラリを64ビットコードにリンクしようとしています

コードにリンクされているライブラリとオブジェクトファイルは、コードと同じアーキテクチャ用にコンパイルする必要があります。 プロジェクトが参照するライブラリが、プロジェクトと同じアーキテクチャ用にコンパイルされていることを確認します。 [/Libpath](../../build/reference/libpath-additional-libpath.md)または追加の**ライブラリディレクトリ**のプロパティが、正しいアーキテクチャ用に構築されたライブラリを参照していることを確認します。

### <a name="you-use-different-compiler-options-for-function-inlining-in-different-source-files"></a>異なるソースファイルでの関数のインライン展開に異なるコンパイラオプションを使用しています

.cpp ファイルで定義されている関数のインライン展開を使用している場合に、異なるソース ファイルで関数のインライン展開のコンパイラ オプションが混在していると、LNK2019 が発生することがあります。 詳細については、「 [Function Inlining Problems](../../error-messages/tool-errors/function-inlining-problems.md)」を参照してください。

### <a name="you-use-automatic-variables-outside-their-scope"></a>スコープ外で自動変数を使用する

自動変数 (関数スコープ) は、その関数のスコープ内でのみ使用できます。 これらの変数は **`:::no-loc(extern):::`** 、他のソースファイルで宣言して使用することはできません。 例については、「 [Automatic (Function Scope) Variables](../../error-messages/tool-errors/automatic-function-scope-variables.md)」を参照してください。

### <a name="you-call-intrinsic-functions-or-pass-argument-types-to-intrinsic-functions-that-arent-supported-on-your-target-architecture"></a>組み込み関数を呼び出したり、ターゲットアーキテクチャでサポートされていない組み込み関数に引数の型を渡したりします。

たとえば、組み込みのを使用し、 :::no-loc(AVX2)::: [ / :::no-loc(ARCH)::: :::no-loc(AVX2)::: :](../../build/reference/arch-x86.md)コンパイラオプションを指定しない場合、コンパイラは組み込みが al 関数であると見なし :::no-loc(extern)::: ます。 コンパイラは、インライン命令を生成するのではなく、 :::no-loc(extern)::: 組み込みと同じ名前を持つ al シンボルへの呼び出しを生成します。 リンカーは、欠落しているこの関数の定義を検索しようとして、LNK2019 を生成します。 ターゲットアーキテクチャでサポートされている組み込みと型のみを使用するようにしてください。

### <a name="you-mix-code-that-uses-native-no-locwchar_t-with-code-that-doesnt"></a>ネイティブを使用するコード :::no-loc(wchar_t)::: と、

Visual Studio 2005 で行われた C++ 言語準拠作業では **`:::no-loc(wchar_t):::`** 、既定でネイティブ型が作成されています。 すべてのファイルが同じ **/zc: :::no-loc(wchar_t)::: **設定を使用してコンパイルされていない場合、型参照は互換性のある型に解決されない可能性があります。 **`:::no-loc(wchar_t):::`** すべてのライブラリファイルとオブジェクトファイルの型に互換性があることを確認します。 をコンパイルするときに、typedef から更新するか **`:::no-loc(wchar_t):::`** 、一貫性のある **/zc: :::no-loc(wchar_t)::: ** settings を使用します。

## <a name="third-party-library-issues-and-vcpkg"></a>サードパーティライブラリの問題と vcpkg

ビルドの一部としてサードパーティのライブラリを構成しようとしているときにこのエラーが表示される場合は、C++ パッケージマネージャーである[vcpkg](../../vcpkg.md)を使用してライブラリをインストールし、ビルドすることを検討してください。 vcpkg では、[サードパーティ製ライブラリの](https://github.com/Microsoft/vcpkg/tree/master/ports)大規模で拡大しているリストがサポートされています。 これは、プロジェクトの一部として成功したビルドに必要なすべての構成プロパティと依存関係を設定します。

## <a name="diagnosis-tools"></a>診断ツール

場合によっては、リンカーが特定のシンボル定義を見つけられない理由を判断することが困難な場合があります。 多くの場合、問題は、ビルドに定義を含むコードを含めていないことです。 または、ビルドオプションによって、al シンボルに対して異なる装飾名が作成されました :::no-loc(extern)::: 。 LNK2019 エラーを診断するのに役立つツールとオプションがいくつかあります。

- [/:::no-loc(VERBOSE):::](../../build/reference/verbose-print-progress-messages.md)リンカーオプションは、リンカーが参照するファイルを特定するのに役立ちます。 このオプションは、シンボルの定義が含まれているファイルがビルドに含まれているかどうかを確認するのに役立ちます。

- [/:::no-loc(EXPORTS):::](../../build/reference/dash-exports.md) [/:::no-loc(SYMBOLS):::](../../build/reference/symbols.md) ユーティリティのオプションとオプションを使用すると、 **:::no-loc(DUMPBIN):::** .dll ファイルとオブジェクトファイルまたはライブラリファイルで定義されているシンボルを見つけることができます。 エクスポートされた装飾名が、リンカーが検索する装飾名と一致していることを確認します。

- このユーティリティでは、 **:::no-loc(UNDNAME):::** 装飾名に対応する装飾されていない al シンボルを表示でき :::no-loc(extern)::: ます。

## <a name="examples"></a>例

ここでは、LNK2019 エラーが発生するコードの例を、そのエラーを修正する方法に関する情報と一緒に紹介します。

### <a name="a-symbol-is-declared-but-not-defined"></a>シンボルが宣言されているが、定義されていない

この例では、 :::no-loc(extern)::: al 変数が宣言されていますが、定義されていません。

```cpp
// LNK2019.cpp
// Compile by using: cl /EHsc /W4 LNK2019.cpp
// LNK2019 expected
:::no-loc(extern)::: char B[100];   // B isn't available to the linker
int :::no-loc(main):::() {
   B[0] = ' ';   // LNK2019
}
```

変数と関数がとして宣言されていますが、定義が指定されていない別の例を次に示し **`:::no-loc(extern):::`** ます。

```cpp
// LNK2019c.cpp
// Compile by using: cl /EHsc LNK2019c.cpp
// LNK2019 expected
:::no-loc(extern)::: int i;
:::no-loc(extern)::: void g();
void f() {
   i++;
   g();
}
int :::no-loc(main):::() {}
```

`i`と `g` がビルドに含まれているいずれかのファイルで定義されていない場合、リンカーは LNK2019 を生成します。 このエラーを修正するには、定義を含むソース コード ファイルをコンパイルの一部に組み込みます。 または、定義を含む .obj ファイルまたは .lib ファイルをリンカーに渡すこともできます。

### <a name="a-no-locstatic-data-member-is-declared-but-not-defined"></a>:::no-loc(static):::データメンバーが宣言されていますが定義されていません

LNK2019 は、 :::no-loc(static)::: データメンバーが宣言されているが定義されていない場合にも発生する可能性があります。 次の例は LNK2019 を生成します。その修正方法も示しています。

```cpp
// LNK2019b.cpp
// Compile by using: cl /EHsc LNK2019b.cpp
// LNK2019 expected
struct C {
   :::no-loc(static)::: int s;
};

// Uncomment the following line to fix the error.
// int C::s;

int :::no-loc(main):::() {
   C c;
   C::s = 1;
}
```

### <a name="declaration-parameters-dont-match-the-definition"></a>宣言パラメーターが定義と一致しません

テンプレート関数を呼び出すコードには、対応するテンプレート関数宣言が必要です。 宣言には、定義と同じテンプレート パラメーターを含める必要があります。 次の例では、ユーザー定義の演算子で LNK2019 が発生します。その修正方法も示しています。

```cpp
// LNK2019e.cpp
// compile by using: cl /EHsc LNK2019e.cpp
// LNK2019 expected
#include <iostream>
using namespace std;

template<class T> class
Test {
   // The operator<< declaration doesn't match the definition below:
   friend ostream& operator<<(ostream&, Test&);
   // To fix, replace the line above with the following:
   // template<typename T> friend ostream& operator<<(ostream&, Test<T>&);
};

template<typename T>
ostream& operator<<(ostream& os, Test<T>& tt) {
   return os;
}

int :::no-loc(main):::() {
   Test<int> t;
   cout << "Test: " << t << endl;   // LNK2019 unresolved :::no-loc(extern):::al
}
```

### <a name="inconsistent-no-locwchar_t-type-definitions"></a>一貫性のない :::no-loc(wchar_t)::: 型定義

このサンプルでは、を使用するエクスポートを含む DLL を作成し `WCHAR` ます。これは、に解決さ **`:::no-loc(wchar_t):::`** れます。

```cpp
// LNK2019g.cpp
// compile with: cl /EHsc /LD LNK2019g.cpp
#include "windows.h"
// WCHAR resolves to :::no-loc(wchar_t):::
__declspec(dllexport) void func(WCHAR*) {}
```

次のサンプルでは、前のサンプルの DLL を使用して、LNK2019 を生成します。これは、と型が同じではないため `unsigned short*` `WCHAR*` です。

```cpp
// LNK2019h.cpp
// compile by using: cl /EHsc LNK2019h LNK2019g.lib
// LNK2019 expected
__declspec(dllimport) void func(unsigned short*);

int :::no-loc(main):::() {
   func(0);
}
```

このエラーを修正するに **`unsigned short`** は、をまたはに変更する **`:::no-loc(wchar_t):::`** `WCHAR` か、 **/zc: :::no-loc(wchar_t)::: - **を使用して lnk2019g.cpp をコンパイルします。

## <a name="additional-resources"></a>その他の技術情報

LNK2001 の考えられる原因と解決方法の詳細については、「Stack Overflow の質問」を参照してください。[未定義の参照/未解決の :::no-loc(extern)::: al シンボルエラーとその解決方法](https://stackoverflow.com/q/12573816/2002113)について説明します。
