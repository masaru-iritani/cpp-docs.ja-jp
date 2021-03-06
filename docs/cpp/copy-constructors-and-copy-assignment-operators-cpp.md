---
title: コピー コンストラクターとコピー代入演算子 (C++)
ms.date: 11/04/2016
helpviewer_keywords:
- = operator [C++], copying objects
- assignment statements [C++], copying objects
- assignment operators [C++], for copying objects
- objects [C++], copying
- initializing objects, by copying objects
- copying objects
- assigning values to copy objects
ms.assetid: a94fe1f9-0289-4fb9-8633-77c654002c0d
ms.openlocfilehash: faf1a94e27f5a0a435d0a906661444f67709628e
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87221797"
---
# <a name="copy-constructors-and-copy-assignment-operators-c"></a>コピー コンストラクターとコピー代入演算子 (C++)

> [!NOTE]
> C++ 11 以降では、*コピー代入*と*移動代入*の2種類の代入がサポートされています。 この記事では、特に明示的に記載しない限り、"代入" はコピーの代入を意味します。 移動代入の詳細については、「[移動コンストラクターと移動代入演算子 (C++)](move-constructors-and-move-assignment-operators-cpp.md)」を参照してください。
>
> 代入演算と初期化操作では、いずれもオブジェクトがコピーされます。

- **割り当て**: あるオブジェクトの値が別のオブジェクトに割り当てられると、最初のオブジェクトが2番目のオブジェクトにコピーされます。 したがって、次のようになります。

    ```cpp
    Point a, b;
    ...
    a = b;
    ```

   の場合、`b` の値が `a` にコピーされます。

- **初期化**: 初期化は、新しいオブジェクトが宣言されたとき、引数が値によって関数に渡されたとき、または値によって関数から値が返されたときに発生します。

クラス型のオブジェクトに「コピー」の意味を定義できます。 たとえば、次のコードを検討してみましょう。

```cpp
TextFile a, b;
a.Open( "FILE1.DAT" );
b.Open( "FILE2.DAT" );
b = a;
```

前のコードは、「FILE1.DAT から FILE2.DAT に内容をコピーする」を意味する場合もありますが、「FILE2.DAT を無視して `b` を FILE1.DAT への 2 番目のハンドルにする」という意味もあります。 各クラスには、次のように適切なコピーのセマンティクスを割り当てる必要があります。

- 戻り値の型としてのクラス型への参照、および参照によって渡されるパラメーター (など) と共に代入演算子**演算子 =** を使用する **`const`** `ClassName& operator=(const ClassName& x);` 。

- コピー コンストラクターを使用する。

コピー コンストラクターを宣言していない場合、コンパイラはメンバーごとのコピー コンストラクターを生成します。  コピー代入演算子を宣言していない場合、コンパイラはメンバーごとのコピー代入演算子を生成します。 コピー コンストラクターを宣言しても、コンパイラで生成されるコピー代入演算子は抑制されません。また、その逆も同様です。 いずれか 1 つを実装する場合、コードの意味を明確にするために、もう 1 つも実装することをお勧めします。

コピーコンストラクターは、<em>クラス名</em>型の引数を受け取り <strong>&</strong> ます。ここで、*クラス*名は、コンストラクターが定義されているクラスの名前です。 次に例を示します。

```cpp
// spec1_copying_class_objects.cpp
class Window
{
public:
    Window( const Window& ); // Declare copy constructor.
    // ...
};

int main()
{
}
```

> [!NOTE]
> 可能な限り、コピーコンストラクターの引数クラス名の型を作成し **`const`** <em>class-name</em> <strong>&</strong> ます。 これによって、コピー コンストラクターが誤ってコピー元のオブジェクトを変更しないようにすることができます。 また、オブジェクトからコピーすることもでき **`const`** ます。

## <a name="compiler-generated-copy-constructors"></a>コンパイラによって生成されたコピー コンストラクター

コンパイラによって生成されるコピーコンストラクターは、ユーザー定義のコピーコンストラクターと同様に、"*クラス名*への参照" 型の引数を1つ持ちます。 例外は、すべての基底クラスとメンバークラスに、 **`const`** <em>クラス名</em>の単一の引数を取得するためにコピーコンストラクターが宣言されている場合です <strong>&</strong> 。 このような場合、コンパイラによって生成されるコピーコンストラクターの引数も **`const`** です。

コピーコンストラクターへの引数の型がでない場合 **`const`** 、オブジェクトをコピーして初期化すると、 **`const`** エラーが発生します。 逆は true ではありません。引数がの場合は **`const`** 、ではないオブジェクトをコピーすることによって初期化でき **`const`** ます。

コンパイラによって生成された代入演算子は、const に関して同じパターンに従い**ます。** <em>class-name</em> <strong>&</strong> すべての基本クラスとメンバークラスの代入演算子がクラス名型の引数を受け取る場合を除き、型クラス名の引数を1つ受け取り **`const`** <em>class-name</em> <strong>&</strong> ます。 この場合、クラスで生成された代入演算子は **`const`** 引数を受け取ります。

> [!NOTE]
> コピー コンストラクターによって初期化されるか、コンパイラによって生成されるか、またはユーザーによって定義される場合、仮想基底クラスは構築される時点で 1 回だけ初期化されます。

影響はコピー コンストラクターの影響と似ています。 引数の型がでない場合 **`const`** 、オブジェクトからの割り当てに **`const`** よってエラーが発生します。 逆は true ではありません。 **`const`** 値が値に割り当てられていない場合 **`const`** 、代入は成功します。

オーバーロードされた代入演算子の詳細については、「[代入](../cpp/assignment.md)」を参照してください。
