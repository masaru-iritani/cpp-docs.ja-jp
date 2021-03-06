---
title: 戻り値の型
ms.date: 11/04/2016
helpviewer_keywords:
- function return types
- return values [C++], function procedures
- function return types, syntax
- return values [C++]
- data types [C++], function return types
- return keyword [C++], function return types
- functions [C++], return types
ms.assetid: 3e5b8a97-b341-48c5-8be8-8986980ef586
ms.openlocfilehash: 1d905e02be02784b562b9d1a8f72a9bfa4057b9b
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87226328"
---
# <a name="return-type"></a>戻り値の型

関数の戻り値の型は、関数によって返される値のサイズと型を規定し、次の構文の type-specifier に相当します。

## <a name="syntax"></a>構文

*function-definition*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*declaration-specifiers*<sub>opt</sub> *attribute-seq*<sub>opt</sub> *declarator* *declaration-list*<sub>opt</sub> *compound-statement*

/\* *attribute-seq* は Microsoft 固有の仕様です \*/

*declaration-specifiers*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*storage-class-specifier* *declaration-specifiers*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-specifier* *declaration-specifiers*<sub>opt</sub><br/>
&nbsp;&nbsp;&nbsp;&nbsp;*type-qualifier* *declaration-specifiers*<sub>opt</sub>

*type-specifier*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`void`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`char`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`short`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`int`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`__int8`**  /\* Microsoft 固有の仕様 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`__int16`**  /\* Microsoft 固有の仕様 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`__int32`**  /\* Microsoft 固有の仕様 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`__int64`**  /\* Microsoft 固有の仕様 \*/<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`long`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`float`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`double`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`signed`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **`unsigned`**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*struct-or-union-specifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*enum-specifier*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;*typedef-name*

*type-specifier* には、任意の基本型、構造体型、または共用体型を指定できます。 *type-specifier* が含まれていない場合、戻り値の型は **`int`** と見なされます。

関数定義で指定された戻り値の型は、プログラムの別の場所に出現する関数宣言の戻り値の型と一致する必要があります。 関数からは、式を含む **`return`** ステートメントが実行されると値が返されます。 この式が評価され、必要に応じて戻り値の型に変換されて、関数が呼び出されたポイントに返されます。 関数で宣言されている戻り値の型が **`void`** の場合、式を含む return ステートメントで警告が生成され、式は評価されません。

次の例に、関数の戻り値を示します。

```C
typedef struct
{
    char name[20];
    int id;
    long class;
} STUDENT;

/* Return type is STUDENT: */

STUDENT sortstu( STUDENT a, STUDENT b )
{
    return ( (a.id < b.id) ? a : b );
}
```

この例では、 **`typedef`** 宣言付きで `STUDENT` 型が定義され、関数 `sortstu` の戻り値の型は `STUDENT` と定義されています。 この関数は、2 つの構造体引数の 1 つを選択して返します。 その後の関数呼び出しでは、コンパイラは引数の型が `STUDENT` であることを確認します。

> [!NOTE]
> 構造体全体ではなく構造体へのポインターを渡すことによって効率が向上します。

```C
char *smallstr( char s1[], char s2[] )
{
    int i;

    i = 0;
    while ( s1[i] != '\0' && s2[i] != '\0' )
        i++;
    if ( s1[i] == '\0' )
        return ( s1 );
    else
        return ( s2 );
}
```

この例では、文字の配列へのポインターを返す関数を定義します。 この関数は 2 つの文字配列 (文字列) を引数として受け取り、2 つの文字列の短い方へのポインターを返します。 配列へのポインターは配列要素の先頭を指し、その型を持つため、この関数の戻り値の型は **`char`** 型へのポインターです。

戻り値の型が **`int`** である関数は、呼び出し前に宣言する必要はありませんが、引数と戻り値の正しい型チェックができるように、プロトタイプをお勧めします。

## <a name="see-also"></a>関連項目

[C 関数の定義](../c-language/c-function-definitions.md)
