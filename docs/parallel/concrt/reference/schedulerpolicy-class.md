---
title: SchedulerPolicy クラス
ms.date: 11/04/2016
f1_keywords:
- SchedulerPolicy
- concrt/concurrency::SchedulerPolicy
- concrt/concurrency::SchedulerPolicy::SchedulerPolicy
- concrt/concurrency::SchedulerPolicy::GetPolicyValue
- concrt/concurrency::SchedulerPolicy::SetConcurrencyLimits
- concrt/concurrency::SchedulerPolicy::SetPolicyValue
helpviewer_keywords:
- SchedulerPolicy class
ms.assetid: bcebf51a-65f8-45a3-809b-d1ff93527dc4
ms.openlocfilehash: b7b99dae2ffb58123c05a65872e4c71e149ac12c
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87219574"
---
# <a name="schedulerpolicy-class"></a>SchedulerPolicy クラス

`SchedulerPolicy` クラスには、ポリシー要素ごとに 1 つずつ、スケジューラ インスタンスの動作を制御するキーと値のペアのセットが含まれています。

## <a name="syntax"></a>構文

```cpp
class SchedulerPolicy;
```

## <a name="members"></a>メンバー

### <a name="public-constructors"></a>パブリック コンストラクター

|名前|説明|
|----------|-----------------|
|[SchedulerPolicy](#ctor)|オーバーロードされます。 新しいスケジューラポリシーを構築し、同時実行ランタイムスケジューラおよびリソースマネージャーによってサポートされる[ポリシーキー](concurrency-namespace-enums.md)の値を設定します。|
|[~ スケジューラポリシーのデストラクター](#dtor)|スケジューラ ポリシーを破棄します。|

### <a name="public-methods"></a>パブリック メソッド

|名前|説明|
|----------|-----------------|
|[GetPolicyValue](#getpolicyvalue)|`key` パラメーターとして指定されるポリシー キーの値を取得します。|
|[SetConcurrencyLimits](#setconcurrencylimits)|`MinConcurrency` オブジェクトに対して、`MaxConcurrency` ポリシーおよび `SchedulerPolicy` ポリシーを同時に設定します。|
|[SetPolicyValue](#setpolicyvalue)|`key` パラメーターとして指定されるポリシー キーの値を設定し、古い値を返します。|

### <a name="public-operators"></a>パブリック演算子

|名前|説明|
|----------|-----------------|
|[operator =](#operator_eq)|別のスケジューラ ポリシーからスケジューラ ポリシーを割り当てます。|

## <a name="remarks"></a>解説

クラスを使用して制御できるポリシーの詳細については `SchedulerPolicy` 、「 [Policyelementkey](concurrency-namespace-enums.md)」を参照してください。

## <a name="inheritance-hierarchy"></a>継承階層

`SchedulerPolicy`

## <a name="requirements"></a>必要条件

**ヘッダー:** concrt、concrtrm .h

**名前空間:** concurrency

## <a name="getpolicyvalue"></a><a name="getpolicyvalue"></a>GetPolicyValue

`key` パラメーターとして指定されるポリシー キーの値を取得します。

```cpp
unsigned int GetPolicyValue(PolicyElementKey key) const;
```

### <a name="parameters"></a>パラメーター

*key*<br/>
値を取得する対象のポリシーキー。

### <a name="return-value"></a>戻り値

パラメーターで指定したキーがサポートされている場合は、 `key` にキャストするキーのポリシー値 **`unsigned int`** 。

### <a name="remarks"></a>解説

メソッドは、無効なポリシーキーの[invalid_scheduler_policy_key](invalid-scheduler-policy-key-class.md)をスローします。

## <a name="operator"></a><a name="operator_eq"></a>operator =

別のスケジューラ ポリシーからスケジューラ ポリシーを割り当てます。

```cpp
SchedulerPolicy& operator= (const SchedulerPolicy& _RhsPolicy);
```

### <a name="parameters"></a>パラメーター

*_RhsPolicy*<br/>
このポリシーに割り当てるポリシー。

### <a name="return-value"></a>戻り値

スケジューラポリシーへの参照。

### <a name="remarks"></a>解説

通常、新しいスケジューラ ポリシーを定義する最も簡単な方法は、既存のポリシーをコピーし、それを `SetPolicyValue` メソッドまたは `SetConcurrencyLimits` メソッドを使用して変更することです。

## <a name="schedulerpolicy"></a><a name="ctor"></a>SchedulerPolicy

新しいスケジューラポリシーを構築し、同時実行ランタイムスケジューラおよびリソースマネージャーによってサポートされる[ポリシーキー](concurrency-namespace-enums.md)の値を設定します。

```cpp
SchedulerPolicy();

SchedulerPolicy(
    size_t _PolicyKeyCount,
...);

SchedulerPolicy(
    const SchedulerPolicy& _SrcPolicy);
```

### <a name="parameters"></a>パラメーター

*_PolicyKeyCount*<br/>
`_PolicyKeyCount` パラメーターの後に続くキーと値のペアの数。

*_SrcPolicy*<br/>
コピー元のポリシー。

### <a name="remarks"></a>解説

最初のコンストラクターでは、すべてのポリシーが既定値に初期化される新しいスケジューラ ポリシーを作成します。

2 番目のコンストラクターでは、名前付きパラメーター スタイルの初期化を使用する新しいスケジューラ ポリシーを作成します。 `_PolicyKeyCount` パラメーターの後の値は、キーと値のペアとして渡されます。 このコンストラクターで指定されていないポリシー キーには既定値が設定されます。 このコンストラクターは、 [invalid_scheduler_policy_key](invalid-scheduler-policy-key-class.md)、 [invalid_scheduler_policy_value](invalid-scheduler-policy-value-class.md)または[invalid_scheduler_policy_thread_specification](invalid-scheduler-policy-thread-specification-class.md)の例外をスローする可能性があります。

3 番目のコンストラクターはコピー コンストラクターです。 通常、新しいスケジューラ ポリシーを定義する最も簡単な方法は、既存のポリシーをコピーし、それを `SetPolicyValue` メソッドまたは `SetConcurrencyLimits` メソッドを使用して変更することです。

## <a name="schedulerpolicy"></a><a name="dtor"></a>~ スケジューラポリシー

スケジューラ ポリシーを破棄します。

```cpp
~SchedulerPolicy();
```

## <a name="setconcurrencylimits"></a><a name="setconcurrencylimits"></a>SetConcurrencyLimits

`MinConcurrency` オブジェクトに対して、`MaxConcurrency` ポリシーおよび `SchedulerPolicy` ポリシーを同時に設定します。

```cpp
void SetConcurrencyLimits(
    unsigned int _MinConcurrency,
    unsigned int _MaxConcurrency = MaxExecutionResources);
```

### <a name="parameters"></a>パラメーター

*_MinConcurrency*<br/>
ポリシーキーの値 `MinConcurrency` 。

*_MaxConcurrency*<br/>
ポリシーキーの値 `MaxConcurrency` 。

### <a name="remarks"></a>解説

ポリシーに指定された値がポリシーに指定された値よりも大きい場合、メソッドは[invalid_scheduler_policy_thread_specification](invalid-scheduler-policy-thread-specification-class.md)をスローし `MinConcurrency` `MaxConcurrency` ます。

メソッドは、他の無効な値の[invalid_scheduler_policy_value](invalid-scheduler-policy-value-class.md)をスローすることもできます。

## <a name="setpolicyvalue"></a><a name="setpolicyvalue"></a>SetPolicyValue

`key` パラメーターとして指定されるポリシー キーの値を設定し、古い値を返します。

```cpp
unsigned int SetPolicyValue(
    PolicyElementKey key,
    unsigned int value);
```

### <a name="parameters"></a>パラメーター

*key*<br/>
値を設定するポリシーキー。

*value*<br/>
ポリシーキーを設定する値。

### <a name="return-value"></a>戻り値

パラメーターで指定されたキーがサポートされている場合は、にキャストされた `key` キーの古いポリシー値 **`unsigned int`** 。

### <a name="remarks"></a>解説

メソッドは、無効なポリシーキーまたはメソッドによって値を設定できないポリシーキーの[invalid_scheduler_policy_key](invalid-scheduler-policy-key-class.md)をスローし `SetPolicyValue` ます。

メソッドは、パラメーターで指定されたキーに対してサポートされていない値の[invalid_scheduler_policy_value](invalid-scheduler-policy-value-class.md)をスローし `key` ます。

このメソッドでは、ポリシーまたはポリシーの設定は許可されていないことに注意 `MinConcurrency` `MaxConcurrency` してください。 これらの値を設定するには、 [SetConcurrencyLimits](#setconcurrencylimits)メソッドを使用します。

## <a name="see-also"></a>関連項目

[concurrency 名前空間](concurrency-namespace.md)<br/>
[PolicyElementKey](concurrency-namespace-enums.md)<br/>
[CurrentScheduler クラス](currentscheduler-class.md)<br/>
[Scheduler クラス](scheduler-class.md)<br/>
[タスク スケジューラ](../../../parallel/concrt/task-scheduler-concurrency-runtime.md)
