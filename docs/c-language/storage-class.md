---
title: ストレージ クラス
ms.date: 11/04/2016
helpviewer_keywords:
- linkage [C++], external
- function storage class
- function specifiers, storage class
- storage classes
- Microsoft-specific storage classes
- external linkage, storage-class specifiers
- static storage class specifiers
ms.assetid: 39a79ba6-edf5-42b6-8e45-f94227603dd6
ms.openlocfilehash: 872a014dfc7c21b46f9af810f1cb3463016c7e09
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87211685"
---
# <a name="storage-class"></a>ストレージ クラス

関数定義では、ストレージクラス指定子により、関数に **`extern`** または **`static`** のストレージクラスが指定されます。

## <a name="syntax"></a>構文

*function-definition*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*declaration-specifiers*<sub>opt</sub> *attribute-seq*<sub>opt</sub> *declarator* *declaration-list*<sub>opt</sub> *compound-statement*

/\* *attribute-seq* は Microsoft 固有の仕様です \*/

*declaration-specifiers*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*storage-class-specifier* *declaration-specifiers*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-specifier* *declaration-specifiers*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier* *declaration-specifiers*<sub>opt</sub>

*storage-class-specifier*: /\* 関数定義用 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`extern`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`static`**

関数定義に *storage-class-specifier* が含まれていない場合、ストレージクラスは既定で **`extern`** になります。 関数を **`extern`** として明示的に宣言することもできますが、必須ではありません。

関数の宣言に *storage-class-specifier* **`extern`** が含まれる場合、その識別子は、ファイル スコープで宣言されたあらゆる可視の該当識別子と同じリンケージを持ちます。 ファイル スコープで可視の宣言がない場合、その識別子は外部リンケージを持ちます。 識別子がファイル スコープで、*ストレージ クラス指定子*がない場合、その識別子は外部リンケージを持ちます。 外部リンケージは、その識別子の各インスタンスが同じオブジェクトまたは関数を表すことを意味します。 リンケージとファイル スコープの詳細については、「[有効期間、スコープ、可視性、およびリンケージ](../c-language/lifetime-scope-visibility-and-linkage.md)」を参照してください。

**`extern`** 以外のストレージクラス指定子を持つブロック スコープの関数を宣言すると、エラーが発生します。

**`static`** ストレージ クラスとして宣言された関数は、定義されているソース ファイル内でのみ可視になります。 それ以外のすべての関数は、 **`extern`** ストレージ クラスの指定が明示的か暗黙的かに関係なく、プログラムのすべてのソース ファイルで可視になります。 **`static`** ストレージ クラスを指定する必要がある場合は、その関数の宣言が最初に発生する場所 (存在する場合) の関数定義で宣言する必要があります。

**Microsoft 固有の仕様**

Microsoft 拡張機能が有効な場合、最初にストレージ クラスを指定せずに (または **`extern`** ストレージ クラスで) 宣言された関数が **`static`** ストレージ クラスとなるのは、最初と同じソース ファイルに含まれる関数定義で、 **`static`** ストレージ クラスが明示的に指定された場合です。

/Ze コンパイラ オプションを使用してコンパイルすると、 **`extern`** キーワードを使用してブロック内で宣言された関数はグローバルで可視になります。 /Za でコンパイルした場合は、これに該当しません。 ソース コードの移植性を考慮している場合は、この機能に依存しないでください。

**Microsoft 固有の仕様はここまで**

## <a name="see-also"></a>関連項目

[C 関数の定義](../c-language/c-function-definitions.md)
