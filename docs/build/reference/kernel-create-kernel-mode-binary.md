---
title: /kernel (カーネル モード バイナリの作成)
ms.date: 11/04/2016
f1_keywords:
- /kernel
- /kernel-
ms.assetid: 6d7fdff0-c3d1-4b78-9367-4da588ce8b05
ms.openlocfilehash: bcef52144e4da932e9e1b6acbcd5f2170c4c7f86
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87211945"
---
# <a name="kernel-create-kernel-mode-binary"></a>/kernel (カーネル モード バイナリの作成)

Windows カーネルで実行できるバイナリを作成します。

## <a name="syntax"></a>構文

```
/kernel[-]
```

## <a name="arguments"></a>引数

**/kernel**<br/>
現在のプロジェクトのコードは、カーネルモードで実行されるコードに固有の C++ 言語規則のセットを使用してコンパイルおよびリンクされます。

**/kernel**<br/>
現在のプロジェクトのコードは、カーネルモードで実行されるコードに固有の C++ 言語規則を使用せずにコンパイルおよびリンクされます。

## <a name="remarks"></a>解説

`#pragma` には、このオプションを制御するための相当するものはありません。

**/Kernel**オプションを指定すると、コンパイラとリンカーは、カーネルモードで許容される言語機能を判別し、カーネルモード C++ に固有のランタイムの不安定性を回避するために十分な表現力があることを確認するように指示します。 これを実現するには、カーネルモードで破壊的な C++ 言語機能の使用を禁止し、中断される可能性があるが、無効にすることができない C++ 言語機能に対する警告を提供します。

**/Kernel**オプションは、ビルドのコンパイラフェーズとリンカーフェーズの両方に適用され、プロジェクトレベルで設定されます。 **/Kernel**スイッチを渡して、リンク後のバイナリを Windows カーネルに読み込む必要があることをコンパイラに示します。 コンパイラは、C++ 言語機能の範囲をカーネルと互換性のあるサブセットに絞り込みます。

**/Kernel**を指定した場合のコンパイラの動作の変更の一覧を次の表に示します。

|動作の種類|**/kernel**挙動|
|-------------------|---------------------------|
|C++ 例外処理|無効。 キーワードとキーワードのすべてのインスタンスは、 **`throw`** **`try`** コンパイラエラーを生成します (例外指定は除き `throw()` ます)。 **/EH-** を除き、 **/kernel**と互換性のある **/EH**オプションはありません。|
|RTTI|無効。 **`dynamic_cast`** が静的に使用されていない限り、キーワードとキーワードのすべてのインスタンスは **`typeid`** コンパイラエラーを生成し **`dynamic_cast`** ます。|
|`new` および `delete`|または演算子を明示的に定義する必要があります `new()` `delete()` 。コンパイラとランタイムのどちらも既定の定義を提供しません。|

**/Kernel**オプションを使用する場合、カスタム呼び出し規則、 [/gs](gs-buffer-security-check.md)ビルドオプション、およびすべての最適化が許可されます。 インライン展開は、コンパイラによって実現されるのと同じセマンティクスを使用して、主に **/kernel**による影響を受けません。 インライン展開の修飾子が確実に有効になるようにするには **`__forceinline`** 、特定の関数がインライン化されていないことを確認できるように、警告[C4714](../../error-messages/compiler-warnings/compiler-warning-level-4-c4714.md)が有効になっていることを確認する必要があり **`__forceinline`** ます。

コンパイラに **/kernel**スイッチが渡されると、事前という名前のプリプロセッサマクロが生成され、 `_KERNEL_MODE` 値が**1**になります。 これを使用すると、実行環境がユーザーモードとカーネルモードのどちらであるかに基づいて、条件付きでコードをコンパイルできます。 たとえば、次のコードでは、カーネルモードの実行用にコンパイルされるときに、クラスを非ページングメモリセグメントに配置するように指定しています。

```cpp
#ifdef _KERNEL_MODE
#define NONPAGESECTION __declspec(code_seg("$kerneltext$"))
#else
#define NONPAGESECTION
#endif

class NONPAGESECTION MyNonPagedClass
{
   // ...
};
```

次のターゲットアーキテクチャと **/arch**オプションの組み合わせでは、 **/kernel**で使用するとエラーが発生します。

- **/arch: {SSE&#124;SSE2&#124;AVX}** は、x86 ではサポートされていません。 **/Arch: IA32** **のみが x86 でサポート**されています。

- **/arch: AVX**は、x64 では **/kernel**でサポートされていません。

**/Kernel**でビルドすると、リンカーにも **/kernel**が渡されます。 これがリンカーの動作に与える影響は次のとおりです。

- インクリメンタルリンクは無効です。 コマンドラインに **/incremental**を追加すると、リンカーは次のような致命的なエラーを出力します。

   **リンク: 致命的なエラー LNK1295: '/INCREMENTAL ' は '/KERNEL ' 仕様と互換性がありません。'/INCREMENTAL ' のないリンク**

- リンカーは、各オブジェクトファイル (またはスタティックライブラリの含まれている archive メンバー) を検査し、 **/kernel**オプションを使用してコンパイルされた可能性があるかどうかを調べます。 次の表に示すように、いずれかのインスタンスがこの条件を満たしている場合でも、リンカーは正常にリンクされますが、警告が発行される可能性があります。

   ||**/kernel** obj|**/カーネル**OBJ、MASM obj、または cvtresed|**/Kernel** **と obj**の組み合わせ|
   |-|----------------------|-----------------------------------------------|-------------------------------------------------|
   |**/kernel のリンク**|はい|はい|はい (警告 LNK4257 あり)|
   |**リンク**|はい|はい|はい|

   **LNK4257 リンクオブジェクトが/KERNEL でコンパイルされていません。イメージは実行されない可能性があります**

**/Kernel**オプションと **/driver**オプションは独立して動作し、もう一方には影響しません。

### <a name="to-set-the-kernel-compiler-option-in-visual-studio"></a>/Kernel コンパイラオプションを Visual Studio で設定するには

1. プロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。 詳しくは、「[Visual Studio で C++ コンパイラとビルド プロパティを設定する](../working-with-project-properties.md)」をご覧ください。

1. [ **C/c + +** ] フォルダーを選択します。

1. [**コマンドライン**] プロパティページを選択します。

1. [**追加オプション**] ボックスで、 `/kernel` またはを追加し `/kernel-` ます。

## <a name="see-also"></a>関連項目

[MSVC コンパイラ オプション](compiler-options.md)<br/>
[MSVC コンパイラのコマンドライン構文](compiler-command-line-syntax.md)
