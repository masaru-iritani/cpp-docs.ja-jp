---
title: CComCurrency クラス
ms.date: 11/04/2016
f1_keywords:
- CComCurrency
- ATLCUR/ATL::CComCurrency
- ATLCUR/ATL::CComCurrency::CComCurrency
- ATLCUR/ATL::CComCurrency::GetCurrencyPtr
- ATLCUR/ATL::CComCurrency::GetFraction
- ATLCUR/ATL::CComCurrency::GetInteger
- ATLCUR/ATL::CComCurrency::Round
- ATLCUR/ATL::CComCurrency::SetFraction
- ATLCUR/ATL::CComCurrency::SetInteger
- ATLCUR/ATL::CComCurrency::m_currency
helpviewer_keywords:
- CComCurrency class
ms.assetid: a1c3d10a-bba6-40cc-8bcf-aed9023c8a9e
ms.openlocfilehash: 2b3c260f250fdb198c8317355628fa2fe62c44eb
ms.sourcegitcommit: 13f42c339fb7af935e3a93ac80e350d5e784c9f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87470785"
---
# <a name="ccomcurrency-class"></a>CComCurrency クラス

`CComCurrency` には、CURRENCY オブジェクトを作成および管理するためのメソッドと演算子があります。

## <a name="syntax"></a>構文

```
class CComCurrency
```

## <a name="members"></a>メンバー

### <a name="public-constructors"></a>パブリック コンストラクター

|名前|説明|
|----------|-----------------|
|[CComCurrency::CComCurrency](#ccomcurrency)|`CComCurrency` オブジェクトのコンストラクター。|

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[CComCurrency::GetCurrencyPtr](#getcurrencyptr)|`m_currency` データ メンバーのアドレスを返します。|
|[CComCurrency::GetFraction](#getfraction)|`CComCurrency` オブジェクトの小数部を返すには、このメソッドを呼び出します。|
|[CComCurrency::GetInteger](#getinteger)|`CComCurrency` オブジェクトの整数部を返すには、このメソッドを呼び出します。|
|[CComCurrency::Round](#round)|`CComCurrency` オブジェクトを最も近い整数値に四捨五入するには、このメソッドを呼び出します。|
|[CComCurrency::SetFraction](#setfraction)|`CComCurrency` オブジェクトの小数部を設定するには、このメソッドを呼び出します。|
|[CComCurrency::SetInteger](#setinteger)|`CComCurrency` オブジェクトの整数部を設定するには、このメソッドを呼び出します。|

### <a name="public-operators"></a>パブリック演算子

|名前|説明|
|----------|-----------------|
|[CComCurrency:: operator-](#operator_-)|この演算子は、`CComCurrency` オブジェクトで減算を実行するために使用します。|
|[CComCurrency:: operator! =](#operator_neq)|2 つの `CComCurrency` オブジェクトが等しくないかどうかを比較します。|
|[CComCurrency:: operator *](#operator_star)|この演算子は、`CComCurrency` オブジェクトで乗算を実行するために使用します。|
|[CComCurrency:: operator * =](#operator_star_eq)|この演算子は、`CComCurrency` オブジェクトで乗算を実行し、オブジェクトに結果を代入するために使用します。|
|[CComCurrency:: operator/](#operator_div)|この演算子は、`CComCurrency` オブジェクトで除算を実行するために使用します。|
|[CComCurrency::operator /=](#operator_div_eq)|この演算子は、`CComCurrency` オブジェクトで除算を実行し、オブジェクトに結果を代入するために使用します。|
|[CComCurrency:: operator +](#operator_add)|この演算子は、`CComCurrency` オブジェクトで加算を実行するために使用します。|
|[CComCurrency:: operator + =](#operator_add_eq)|この演算子は、`CComCurrency` オブジェクトで加算を実行し、結果を現在のオブジェクトに代入するために使用します。|
|[CComCurrency:: operator <](#operator_lt)|この演算子は、2 つの `CComCurrency` オブジェクトを比較して、小さい方を決定します。|
|[CComCurrency:: operator <=](#operator_lt_eq)|この演算子では、2 つの `CComCurrency` オブジェクトを比較して、等しいかどうか、または小さい方を決定します。|
|[CComCurrency:: operator =](#operator_eq)|この演算子は、`CComCurrency` オブジェクトに新しい値を割り当てます。|
|[CComCurrency:: operator-=](#operator_-_eq)|この演算子は、`CComCurrency` オブジェクトで減算を実行し、オブジェクトに結果を代入するために使用します。|
|[CComCurrency:: operator = =](#operator_eq_eq)|この演算子は、2 つの `CComCurrency` オブジェクトが等しいかどうかを比較します。|
|[CComCurrency:: operator >](#operator_gt)|この演算子は、2 つの `CComCurrency` オブジェクトを比較して、大きい方を決定します。|
|[CComCurrency:: operator >=](#operator_gt_eq)|この演算子は、2 つの `CComCurrency` オブジェクトを比較して、等しいかどうか、または大きい方を決定します。|
|[CComCurrency:: operator CURRENCY](#operator_currency)|CURRENCY オブジェクトをキャストします。|

### <a name="public-data-members"></a>パブリック データ メンバー

|名前|説明|
|----------|-----------------|
|[CComCurrency::m_currency](#m_currency)|クラスインスタンスによって作成される通貨変数。|

## <a name="remarks"></a>Remarks

`CComCurrency` は、CURRENCY データ型のラッパーです。 CURRENCY は、10,000 倍した値を 8 バイトの 2 の補数で表現した整数値として実装されます。 これは、15 桁の整数部と 4 桁の小数部を持つ固定小数点数として表現されます。 CURRENCY データ型は、通貨に関連する計算、または精度が重要となる固定小数点数の計算に非常に役立ちます。

ラッパーは、 `CComCurrency` この固定小数点型の算術演算、代入演算、および比較演算を実装します。 固定小数点数の計算中に発生する可能性のある丸め誤差を制御するために、サポートするアプリケーションが選択されています。

`CComCurrency` オブジェクトは、小数点の左側に値を格納する整数部と小数点の右側に値を格納する小数部という 2 つの構成要素を使用した形で、小数点の左側と右側の数値にアクセスできます。 小数部は、-9999 (CY_MIN_FRACTION) から +9999 (CY_MAX_FRACTION) までの整数値として内部に格納されます。 [CComCurrency:: GetFraction](#getfraction)メソッドは、係数 1万 (CY_SCALE) でスケーリングされた値を返します。

オブジェクトの整数部分と小数部を指定する場合は、 `CComCurrency` 小数部分が 0 ~ 9999 の範囲の数値であることに注意してください。 これは、小数点の後の有効桁数に 2 桁のみを使用して金額を表す米ドルなどの通貨を扱う場合に重要です。 最後の 2 桁が表示されていない場合でも考慮する必要があります。

|値|考えられる CComCurrency の割り当て|
|-----------|---------------------------------------|
|$10.50|CComCurrency (10, 5000)*または*CComCurrency (10.50)|
|$10.05|CComCurrency (10500)*または*CComCurrency (10.05)|

値  CY_MIN_FRACTION、CY_MAX_FRACTION、および  CY_SCALE は、atlcur.h で定義されています。

## <a name="requirements"></a>必要条件

**ヘッダー:** atlcur .h です。

## <a name="ccomcurrencyccomcurrency"></a><a name="ccomcurrency"></a>CComCurrency:: CComCurrency

コンストラクターです。

```
CComCurrency() throw();
CComCurrency(const CComCurrency& curSrc) throw();
CComCurrency(CURRENCY cySrc) throw();
CComCurrency(DECIMAL dSrc);
CComCurrency(ULONG ulSrc);
CComCurrency(USHORT usSrc);
CComCurrency(CHAR cSrc);
CComCurrency(DOUBLE dSrc);
CComCurrency(FLOAT fSrc);
CComCurrency(LONG lSrc);
CComCurrency(SHORT sSrc);
CComCurrency(BYTE bSrc);
CComCurrency(LONGLONG nInteger, SHORT nFraction);
explicit CComCurrency(LPDISPATCH pDispSrc);
explicit CComCurrency(const VARIANT& varSrc);
explicit CComCurrency(LPCWSTR szSrc);
explicit CComCurrency(LPCSTR szSrc);
```

### <a name="parameters"></a>パラメーター

*curSrc*<br/>
既存の `CComCurrency` オブジェクトです。

*cySrc*<br/>
CURRENCY 型の変数。

*Bsrc*、 *dsrc*、 *fsrc*、 *Lsrc*、 *sSrc*、 *ulsrc、ussrc*<br/>
メンバー変数に与えられた初期値 `m_currency` 。

*cSrc*<br/>
メンバー変数に与えられた初期値を格納している文字 `m_currency` 。

*Ninteger*、 *ninteger*<br/>
初期通貨値の整数部と小数部の要素。 詳細については、「 [CComCurrency](../../atl/reference/ccomcurrency-class.md)の概要」を参照してください。

*pDispSrc*<br/>
`IDispatch`ポインター。

*varSrc*<br/>
VARIANT 型の変数。 変換を実行するために、現在のスレッドのロケールが使用されます。

*szSrc*<br/>
初期値を格納している Unicode または ANSI 文字列。 変換を実行するために、現在のスレッドのロケールが使用されます。

### <a name="remarks"></a>Remarks

コンストラクターは[CComCurrency:: m_currency](#m_currency)の初期値を設定し、整数、文字列、浮動小数点数、通貨変数、その他のオブジェクトなど、さまざまなデータ型を受け入れ `CComCurrency` ます。 値が指定されていない場合、 `m_currency` は0に設定されます。

オーバーフローなどのエラーが発生した場合、コンストラクターには、エラーを説明する HRESULT を使用して、空の例外指定 (**throw ()**) 呼び出しが不足して `AtlThrow` います。

浮動小数点値または double 値を使用して値を代入する場合、はと等価であり、ではないことに注意して `CComCurrency(10.50)` `CComCurrency(10,5000)` `CComCurrency(10,50)` ください。

## <a name="ccomcurrencygetcurrencyptr"></a><a name="getcurrencyptr"></a>CComCurrency:: GetCurrencyPtr

`m_currency` データ メンバーのアドレスを返します。

```
CURRENCY* GetCurrencyPtr() throw();
```

### <a name="return-value"></a>戻り値

データメンバーのアドレスを返します。 `m_currency`

## <a name="ccomcurrencygetfraction"></a><a name="getfraction"></a>CComCurrency:: GetFraction

オブジェクトの小数部分を返すには、このメソッドを呼び出し `CComCurrency` ます。

```
SHORT GetFraction() const;
```

### <a name="return-value"></a>戻り値

データメンバーの小数部分を返し `m_currency` ます。

### <a name="remarks"></a>Remarks

小数部分は、-9999 (CY_MIN_FRACTION) ~ + 9999 (CY_MAX_FRACTION) の4桁の整数値です。 `GetFraction`1万 (CY_SCALE) でスケーリングされたこの値を返します。 CY_MIN_FRACTION、CY_MAX_FRACTION、および CY_SCALE の値は、atlcur .h で定義されています。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#50](../../atl/codesnippet/cpp/ccomcurrency-class_1.cpp)]

## <a name="ccomcurrencygetinteger"></a><a name="getinteger"></a>CComCurrency:: GetInteger

オブジェクトの整数部分を取得するには、このメソッドを呼び出し `CComCurrency` ます。

```
LONGLONG GetInteger() const;
```

### <a name="return-value"></a>戻り値

データメンバーの整数部分を返し `m_currency` ます。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#51](../../atl/codesnippet/cpp/ccomcurrency-class_2.cpp)]

## <a name="ccomcurrencym_currency"></a><a name="m_currency"></a>CComCurrency:: m_currency

通貨データメンバー。

```
CURRENCY m_currency;
```

### <a name="remarks"></a>Remarks

このメンバーは、このクラスのメソッドによってアクセスおよび操作される通貨を保持します。

## <a name="ccomcurrencyoperator--"></a><a name="operator_-"></a>CComCurrency:: operator-

この演算子は、`CComCurrency` オブジェクトで減算を実行するために使用します。

```
CComCurrency operator-() const;
CComCurrency operator-(const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

`CComCurrency`減算の結果を表すオブジェクトを返します。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#55](../../atl/codesnippet/cpp/ccomcurrency-class_3.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_neq"></a>CComCurrency:: operator! =

この演算子は、2つのオブジェクトが等しくないかどうかを比較します。

```
bool operator!= (const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
比較される `CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

比較対象の項目がオブジェクトと等しくない場合は TRUE `CComCurrency` 、それ以外の場合は FALSE を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#56](../../atl/codesnippet/cpp/ccomcurrency-class_4.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_star"></a>CComCurrency:: operator *

この演算子は、`CComCurrency` オブジェクトで乗算を実行するために使用します。

```
CComCurrency operator*(long nOperand) const;
CComCurrency operator*(const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*nOperand*<br/>
乗数。

*cur*<br/>
`CComCurrency`乗数として使用されるオブジェクト。

### <a name="return-value"></a>戻り値

`CComCurrency`乗算の結果を表すオブジェクトを返します。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#57](../../atl/codesnippet/cpp/ccomcurrency-class_5.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_star_eq"></a>CComCurrency:: operator\*=

この演算子は、`CComCurrency` オブジェクトで乗算を実行し、オブジェクトに結果を代入するために使用します。

```
const CComCurrency& operator*= (long nOperand);
const CComCurrency& operator*= (const CComCurrency& cur);
```

### <a name="parameters"></a>パラメーター

*nOperand*<br/>
乗数。

*cur*<br/>
`CComCurrency`乗数として使用されるオブジェクト。

### <a name="return-value"></a>戻り値

更新されたオブジェクトを返し `CComCurrency` ます。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#58](../../atl/codesnippet/cpp/ccomcurrency-class_6.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_div"></a>CComCurrency:: operator/

この演算子は、`CComCurrency` オブジェクトで除算を実行するために使用します。

```
CComCurrency operator/(long nOperand) const;
```

### <a name="parameters"></a>パラメーター

*nOperand*<br/>
除数。

### <a name="return-value"></a>戻り値

`CComCurrency`除算の結果を表すオブジェクトを返します。 除数が0の場合、アサートエラーが発生します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#59](../../atl/codesnippet/cpp/ccomcurrency-class_7.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_div_eq"></a>CComCurrency:: operator/=

この演算子は、`CComCurrency` オブジェクトで除算を実行し、オブジェクトに結果を代入するために使用します。

```
const CComCurrency& operator/= (long nOperand);
```

### <a name="parameters"></a>パラメーター

*nOperand*<br/>
除数。

### <a name="return-value"></a>戻り値

更新されたオブジェクトを返し `CComCurrency` ます。 除数が0の場合、アサートエラーが発生します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#60](../../atl/codesnippet/cpp/ccomcurrency-class_8.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_add"></a>CComCurrency:: operator +

この演算子は、`CComCurrency` オブジェクトで加算を実行するために使用します。

```
CComCurrency operator+(const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency`元のオブジェクトに追加するオブジェクト。

### <a name="return-value"></a>戻り値

`CComCurrency`加算の結果を表すオブジェクトを返します。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#61](../../atl/codesnippet/cpp/ccomcurrency-class_9.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_add_eq"></a>CComCurrency:: operator + =

この演算子は、`CComCurrency` オブジェクトで加算を実行し、結果を現在のオブジェクトに代入するために使用します。

```
const CComCurrency& operator+= (const CComCurrency& cur);
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

更新されたオブジェクトを返し `CComCurrency` ます。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#62](../../atl/codesnippet/cpp/ccomcurrency-class_10.cpp)]

## <a name="ccomcurrencyoperator-lt"></a><a name="operator_lt"></a>CComCurrency:: operator&lt;

この演算子は、2 つの `CComCurrency` オブジェクトを比較して、小さい方を決定します。

```
bool operator<(const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

最初のオブジェクトが2番目のオブジェクトより小さい場合は TRUE、それ以外の場合は FALSE を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#63](../../atl/codesnippet/cpp/ccomcurrency-class_11.cpp)]

## <a name="ccomcurrencyoperator-lt"></a><a name="operator_lt_eq"></a>CComCurrency:: operator&lt;=

この演算子では、2 つの `CComCurrency` オブジェクトを比較して、等しいかどうか、または小さい方を決定します。

```
bool operator<= (const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

最初のオブジェクトが2番目のオブジェクト以下の場合は TRUE、それ以外の場合は FALSE を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#64](../../atl/codesnippet/cpp/ccomcurrency-class_12.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_eq"></a>CComCurrency:: operator =

この演算子は、`CComCurrency` オブジェクトに新しい値を割り当てます。

```
const CComCurrency& operator= (const CComCurrency& curSrc) throw();
const CComCurrency& operator= (CURRENCY cySrc) throw();
const CComCurrency& operator= (FLOAT fSrc);
const CComCurrency& operator= (SHORT sSrc);
const CComCurrency& operator= (LONG lSrc);
const CComCurrency& operator= (BYTE bSrc);
const CComCurrency& operator= (USHORT usSrc);
const CComCurrency& operator= (DOUBLE dSrc);
const CComCurrency& operator= (CHAR cSrc);
const CComCurrency& operator= (ULONG ulSrc);
const CComCurrency& operator= (DECIMAL dSrc);
```

### <a name="parameters"></a>パラメーター

*curSrc*<br/>
`CComCurrency` オブジェクト。

*cySrc*<br/>
CURRENCY 型の変数。

*sSrc*、 *fsrc*、 *lsrc*、 *bsrc*、 *ussrc*、 *dsrc*、 *csrc*、 *ulsrc*、 *dsrc*<br/>
オブジェクトに代入する数値 `CComCurrency` 。

### <a name="return-value"></a>戻り値

更新されたオブジェクトを返し `CComCurrency` ます。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#65](../../atl/codesnippet/cpp/ccomcurrency-class_13.cpp)]

## <a name="ccomcurrencyoperator--"></a><a name="operator_-_eq"></a>CComCurrency:: operator-=

この演算子は、`CComCurrency` オブジェクトで減算を実行し、オブジェクトに結果を代入するために使用します。

```
const CComCurrency& operator-= (const CComCurrency& cur);
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

更新されたオブジェクトを返し `CComCurrency` ます。 オーバーフローなどのエラーが発生した場合、この演算子は、 `AtlThrow` エラーを説明する HRESULT を使用してを呼び出します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#66](../../atl/codesnippet/cpp/ccomcurrency-class_14.cpp)]

## <a name="ccomcurrencyoperator-"></a><a name="operator_eq_eq"></a>CComCurrency:: operator = =

この演算子は、2 つの `CComCurrency` オブジェクトが等しいかどうかを比較します。

```
bool operator== (const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
比較対象の `CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

オブジェクトが等しい場合 ( `m_currency` 両方のオブジェクトの整数と小数の両方に同じ値が設定されている場合) は TRUE、それ以外の場合は FALSE を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#67](../../atl/codesnippet/cpp/ccomcurrency-class_15.cpp)]

## <a name="ccomcurrencyoperator-gt"></a><a name="operator_gt"></a>CComCurrency:: operator&gt;

この演算子は、2 つの `CComCurrency` オブジェクトを比較して、大きい方を決定します。

```
bool operator>(const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

最初のオブジェクトが2番目のオブジェクトより大きい場合は TRUE、それ以外の場合は FALSE を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#68](../../atl/codesnippet/cpp/ccomcurrency-class_16.cpp)]

## <a name="ccomcurrencyoperator-gt"></a><a name="operator_gt_eq"></a>CComCurrency:: operator&gt;=

この演算子は、2 つの `CComCurrency` オブジェクトを比較して、等しいかどうか、または大きい方を決定します。

```
bool operator>= (const CComCurrency& cur) const;
```

### <a name="parameters"></a>パラメーター

*cur*<br/>
`CComCurrency` オブジェクト。

### <a name="return-value"></a>戻り値

最初のオブジェクトが2番目のオブジェクト以上の場合は TRUE、それ以外の場合は FALSE を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#69](../../atl/codesnippet/cpp/ccomcurrency-class_17.cpp)]

## <a name="ccomcurrencyoperator-currency"></a><a name="operator_currency"></a>CComCurrency:: operator CURRENCY

これらの演算子は、オブジェクトを `CComCurrency` CURRENCY データ型にキャストするために使用されます。

```
operator CURRENCY&() throw();
operator const CURRENCY&() const throw();
```

### <a name="return-value"></a>戻り値

CURRENCY オブジェクトへの参照を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#70](../../atl/codesnippet/cpp/ccomcurrency-class_18.cpp)]

## <a name="ccomcurrencyround"></a><a name="round"></a>CComCurrency:: Round

このメソッドを呼び出して、指定した小数点以下の桁数に通貨を丸めます。

```
HRESULT Roundint nDecimals);
```

### <a name="parameters"></a>パラメーター

*nDecimals*<br/>
が丸められる桁数 `m_currency` 。 0 ~ 4 の範囲で丸められます。

### <a name="return-value"></a>戻り値

成功した場合は S_OK を返し、失敗した場合はエラー HRESULT を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#52](../../atl/codesnippet/cpp/ccomcurrency-class_19.cpp)]

## <a name="ccomcurrencysetfraction"></a><a name="setfraction"></a>CComCurrency:: SetFraction

`CComCurrency` オブジェクトの小数部を設定するには、このメソッドを呼び出します。

```
HRESULT SetFraction(SHORT nFraction);
```

### <a name="parameters"></a>パラメーター

*nFraction*<br/>
データメンバーの小数部分に代入される値 `m_currency` 。 小数部分の符号は整数部分と同じである必要があり、値は 9999 (CY_MIN_FRACTION) ~ + 9999 (CY_MAX_FRACTION) の範囲内である必要があります。

### <a name="return-value"></a>戻り値

成功した場合は S_OK を返し、失敗した場合はエラー HRESULT を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#53](../../atl/codesnippet/cpp/ccomcurrency-class_20.cpp)]

## <a name="ccomcurrencysetinteger"></a><a name="setinteger"></a>CComCurrency:: SetInteger

`CComCurrency` オブジェクトの整数部を設定するには、このメソッドを呼び出します。

```
HRESULT SetInteger(LONGLONG nInteger);
```

### <a name="parameters"></a>パラメーター

*n 整数*<br/>
データメンバーの整数部分に代入される値 `m_currency` 。 整数部分の符号は、既存の小数部分の符号と一致している必要があります。

*Ninteger*は CY_MAX_INTEGER を含む CY_MIN_INTEGER の範囲内である必要があります。 これらの値は、atlcur. h で定義されています。

### <a name="return-value"></a>戻り値

成功した場合は S_OK を返し、失敗した場合はエラー HRESULT を返します。

### <a name="example"></a>例

[!code-cpp[NVC_ATL_Utilities#54](../../atl/codesnippet/cpp/ccomcurrency-class_21.cpp)]

## <a name="see-also"></a>関連項目

[COleCurrency クラス](../../mfc/reference/colecurrency-class.md)<br/>
[貨](/windows/win32/api/wtypes/ns-wtypes-cy-r1)<br/>
[クラスの概要](../../atl/atl-class-overview.md)
