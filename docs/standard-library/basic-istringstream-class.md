---
title: basic_istringstream クラス
ms.date: 11/04/2016
f1_keywords:
- sstream/std::basic_istringstream
- sstream/std::basic_istringstream::allocator_type
- sstream/std::basic_istringstream::rdbuf
- sstream/std::basic_istringstream::str
- sstream/std::basic_istringstream::swap
helpviewer_keywords:
- std::basic_istringstream [C++]
- std::basic_istringstream [C++], allocator_type
- std::basic_istringstream [C++], rdbuf
- std::basic_istringstream [C++], str
- std::basic_istringstream [C++], swap
ms.assetid: 1d5bb4b5-793d-4833-98e5-14676c451915
ms.openlocfilehash: fd2ab79466c01343cbdadbcb649e3b05eee3c2a0
ms.sourcegitcommit: 1839405b97036891b6e4d37c99def044d6f37eff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88561779"
---
# <a name="basic_istringstream-class"></a>basic_istringstream クラス

[basic_stringbuf](../standard-library/basic-stringbuf-class.md) <  **Elem**、 **Tr**、> クラス basic_stringbuf のストリームバッファーからの要素とエンコードされたオブジェクトの抽出を制御するオブジェクトを記述し `Alloc` ます。

## <a name="syntax"></a>構文

```cpp
template <class Elem, class Tr = char_traits<Elem>, class Alloc = allocator<Elem>>
class basic_istringstream : public basic_istream<Elem, Tr>
```

### <a name="parameters"></a>パラメーター

*割り当て*\
アロケーター クラス。

*Elem*\
文字列の基本要素の型。

*Tr*\
文字列の基本要素に特化した文字の特徴。

## <a name="remarks"></a>解説

クラステンプレートは、elem、Tr、> の各[basic_stringbuf](../standard-library/basic-stringbuf-class.md)クラスのストリームバッファーから、要素とエンコードされたオブジェクトの抽出を制御するオブジェクトを記述し <  **Elem** **Tr** `Alloc` ます。 *elem*型の要素は、文字の特徴が*tr*クラスによって決定され、その要素が*Alloc*クラスのアロケーターによって割り当てられている要素を持ちます。 このオブジェクトは、クラス basic_stringbuf< **Elem**, **Tr**, `Alloc`> のオブジェクトを格納します。

### <a name="constructors"></a>コンストラクター

|コンストラクター|説明|
|-|-|
|[basic_istringstream](#basic_istringstream)|`basic_istringstream` 型のオブジェクトを構築します。|

### <a name="typedefs"></a>Typedefs

|型名|説明|
|-|-|
|[allocator_type](#allocator_type)|この型は、テンプレート パラメーター `Alloc` のシノニムです。|

### <a name="member-functions"></a>メンバー関数

|メンバー関数|説明|
|-|-|
|[rdbuf](#rdbuf)|型の格納されているストリームバッファーのアドレスを `pointer` [basic_stringbuf](../standard-library/basic-stringbuf-class.md) <  `Elem` 、 `Tr` 、> に返し `Alloc` ます。|
|[引数](#str)|文字列バッファー内のテキストを設定または取得します。書き込み位置は変更しません。|
|[スワップ](#swap)|この `basic_istringstream` オブジェクト内の値を、提供されるオブジェクトの値と交換します。|

### <a name="operators"></a>オペレーター

|演算子|説明|
|-|-|
|[operator =](#op_eq)|オブジェクト パラメーターの値をこの `basic_istringstream` オブジェクトに代入します。|

## <a name="requirements"></a>必要条件

**ヘッダー:**\<sstream>

**名前空間:** std

## <a name="basic_istringstreamallocator_type"></a><a name="allocator_type"></a> basic_istringstream:: allocator_type

この型は、テンプレート パラメーター `Alloc` のシノニムです。

```cpp
typedef Alloc allocator_type;
```

## <a name="basic_istringstreambasic_istringstream"></a><a name="basic_istringstream"></a> basic_istringstream:: basic_istringstream

`basic_istringstream` 型のオブジェクトを構築します。

```cpp
explicit basic_istringstream(
    ios_base::openmode _Mode = ios_base::in);

explicit basic_istringstream(
    const basic_string<Elem, Tr, Alloc>& str,
    ios_base::openmode _Mode = ios_base::in);

basic_istringstream(
    basic_istringstream&& right);
```

### <a name="parameters"></a>パラメーター

*_Mode*\
[ios_base::openmode](../standard-library/ios-base-class.md#openmode) の列挙値のうちの 1 つ。

*引数*\
`basic_string` 型のオブジェクト。

*そうです*\
`basic_istringstream` オブジェクトの右辺値参照。

### <a name="remarks"></a>解説

最初のコンストラクターは[basic_istream](../standard-library/basic-istream-class.md)() を呼び出すことによって基底クラスを初期化し `sb` ます。ここで、 `sb` は、クラス[basic_stringbuf](../standard-library/basic-stringbuf-class.md) <  `Elem` 、 `Tr` 、 `Alloc`> の格納されているオブジェクトです。 また、`basic_stringbuf`< `Elem`, `Tr`, `Alloc`>( `_Mode` &#124; `ios_base::in`) を呼び出すことで `sb` の初期化もします。

2 番目のコンストラクターが `basic_istream(sb)` を呼び出して基底クラスを初期化します。 また、`basic_stringbuf`< `Elem`, `Tr`, `Alloc`>( `str`, `_Mode` &#124; `ios_base::in`) を呼び出すことで `sb` の初期化もします。

3番目のコンストラクターは、右辺値参照として扱われる *right*の内容を使用してオブジェクトを初期化します。

## <a name="basic_istringstreamoperator"></a><a name="op_eq"></a> basic_istringstream:: operator =

オブジェクト パラメーターの値をこの `basic_istringstream` オブジェクトに代入します。

```cpp
basic_istringstream& operator=(basic_istringstream&& right);
```

### <a name="parameters"></a>パラメーター

*そうです*\
`basic_istringstream` オブジェクトへの右辺値参照。

### <a name="remarks"></a>解説

メンバー演算子は、右辺値参照の移動代入として扱われる、オブジェクトの内容を *右*の内容に置き換えます。

## <a name="basic_istringstreamrdbuf"></a><a name="rdbuf"></a> basic_istringstream:: rdbuf

型の格納されたストリームバッファーのアドレス `pointer` を[basic_stringbuf](../standard-library/basic-stringbuf-class.md) <  **Elem**、 **Tr**、 `Alloc`> に返します。

```cpp
basic_stringbuf<Elem, Tr, Alloc> *rdbuf() const;
```

### <a name="return-value"></a>戻り値

`pointer` **Elem**、 **Tr**、>< basic_stringbuf する型の格納されたストリームバッファーのアドレス `Alloc` 。

### <a name="example"></a>例

`rdbuf` の使用例については、「[basic_filebuf::close](../standard-library/basic-filebuf-class.md#close)」を参照してください。

## <a name="basic_istringstreamstr"></a><a name="str"></a> basic_istringstream:: str

文字列バッファー内のテキストを設定または取得します。書き込み位置は変更しません。

```cpp
basic_string<Elem, Tr, Alloc> str() const;

void str(
    const basic_string<Elem, Tr, Alloc>& _Newstr);
```

### <a name="parameters"></a>パラメーター

*_Newstr*\
新しい文字列。

### <a name="return-value"></a>戻り値

[basic_string](../standard-library/basic-string-class.md) <  **Elem** **Tr** `Alloc` 制御されたシーケンスが** \* this**によって制御されるシーケンスのコピーである Elem、Tr、> basic_string クラスのオブジェクトを返します。

### <a name="remarks"></a>解説

1つ目のメンバー関数は、 [rdbuf](#rdbuf)  ->  [str](../standard-library/basic-stringbuf-class.md#str)を返します。 2番目のメンバー関数は `rdbuf`  ->  **str**() を呼び出し `_Newstr` ます。

### <a name="example"></a>例

の使用例については、「 [basic_stringbuf:: str](../standard-library/basic-stringbuf-class.md#str) 」を参照してください `str` 。

## <a name="basic_istringstreamswap"></a><a name="swap"></a> basic_istringstream:: swap

2 つの `basic_istringstream` オブジェクトの値を交換します。

```cpp
void swap(basic_istringstream& right);
```

### <a name="parameters"></a>パラメーター

*そうです*\
`basic_istringstream` オブジェクトへの左辺値参照。

### <a name="remarks"></a>解説

このメンバー関数は、このオブジェクトの値と *right*の値を交換します。

## <a name="see-also"></a>関連項目

[C++ 標準ライブラリのスレッドセーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[iostream プログラミング](../standard-library/iostream-programming.md)\
[iostreams の規則](../standard-library/iostreams-conventions.md)
