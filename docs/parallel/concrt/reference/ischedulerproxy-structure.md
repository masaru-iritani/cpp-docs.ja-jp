---
title: ISchedulerProxy 構造体
ms.date: 11/04/2016
f1_keywords:
- ISchedulerProxy
- CONCRTRM/concurrency::ISchedulerProxy
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::BindContext
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::CreateOversubscriber
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::RequestInitialVirtualProcessors
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::Shutdown
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::SubscribeCurrentThread
- CONCRTRM/concurrency::ISchedulerProxy::ISchedulerProxy::UnbindContext
helpviewer_keywords:
- ISchedulerProxy structure
ms.assetid: af416973-7a1c-4c30-aa3b-4161c2aaea54
ms.openlocfilehash: dcb6d175fa84e33f6a5af974eb76f1e1246bdc35
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87226699"
---
# <a name="ischedulerproxy-structure"></a>ISchedulerProxy 構造体

スケジューラは、このインターフェイスを使用してコンカレンシー ランタイムのリソース マネージャーと通信して、リソース割り当てをネゴシエートします。

## <a name="syntax"></a>構文

```cpp
struct ISchedulerProxy;
```

## <a name="members"></a>メンバー

### <a name="public-methods"></a>パブリック メソッド

|名前|[説明]|
|----------|-----------------|
|[ISchedulerProxy:: BindContext](#bindcontext)|まだ関連付けられていない場合は、実行コンテキストをスレッドプロキシに関連付けます。|
|[ISchedulerProxy:: CreateOversubscriber](#createoversubscriber)|既存の実行リソースに関連付けられているハードウェアスレッドに新しい仮想プロセッサルートを作成します。|
|[ISchedulerProxy:: RequestInitialVirtualProcessors](#requestinitialvirtualprocessors)|仮想プロセッサルートの初期割り当てを要求します。 すべての仮想プロセッサルートは、スケジューラに対して処理を実行できる1つのスレッドを実行する機能を表します。|
|[ISchedulerProxy:: Shutdown](#shutdown)|スケジューラがシャットダウン中であることをリソースマネージャーに通知します。 これにより、リソースマネージャーは、スケジューラに付与されているすべてのリソースを直ちに回収します。|
|[ISchedulerProxy:: SubscribeCurrentThread](#subscribecurrentthread)|現在のスレッドをリソースマネージャーに登録し、このスケジューラに関連付けます。|
|[ISchedulerProxy:: UnbindContext](#unbindcontext)|パラメーターによって指定された実行コンテキストからスレッドプロキシの関連付けを解除 `pContext` し、スレッドプロキシファクトリの解放プールに返します。 このメソッドは、 [ISchedulerProxy:: BindContext](#bindcontext)メソッドを使用してバインドされた実行コンテキストでのみ呼び出すことができます。また、 `pContext` [Ithreadproxy:: SwitchTo](ithreadproxy-structure.md#switchto)メソッド呼び出しのパラメーターではなく、まだ開始されていません。|

## <a name="remarks"></a>解説

リソースマネージャーは、 `ISchedulerProxy` [iresourcemanager:: registerscheduler](iresourcemanager-structure.md#registerscheduler)メソッドを使用して、それに登録するすべてのスケジューラにインターフェイスを渡します。

## <a name="inheritance-hierarchy"></a>継承階層

`ISchedulerProxy`

## <a name="requirements"></a>必要条件

**ヘッダー:** concrtrm. h

**名前空間:** concurrency

## <a name="ischedulerproxybindcontext-method"></a><a name="bindcontext"></a>ISchedulerProxy:: BindContext メソッド

まだ関連付けられていない場合は、実行コンテキストをスレッドプロキシに関連付けます。

```cpp
virtual void BindContext(_Inout_ IExecutionContext* pContext) = 0;
```

### <a name="parameters"></a>パラメーター

*pContext*<br/>
スレッドプロキシに関連付ける実行コンテキストへのインターフェイス。

### <a name="remarks"></a>解説

通常、 [Ithreadproxy:: SwitchTo](ithreadproxy-structure.md#switchto)メソッドは、必要に応じてスレッドプロキシを実行コンテキストにバインドします。 ただし、メソッドが既にバインドされているコンテキストに切り替わっていることを確認するために、事前にコンテキストをバインドする必要がある状況もあり `SwitchTo` ます。 これは、メモリを割り当てるメソッドを呼び出すことができず、スレッドプロキシファクトリの空きプールでスレッドプロキシを使用できない場合に、スレッドプロキシのバインドにメモリの割り当てが含まれている可能性があるため、UMS スケジューリングコンテキストの場合です。

`invalid_argument`パラメーターの値がの場合は、がスローされ `pContext` `NULL` ます。

## <a name="ischedulerproxycreateoversubscriber-method"></a><a name="createoversubscriber"></a>ISchedulerProxy:: CreateOversubscriber メソッド

既存の実行リソースに関連付けられているハードウェアスレッドに新しい仮想プロセッサルートを作成します。

```cpp
virtual IVirtualProcessorRoot* CreateOversubscriber(_Inout_ IExecutionResource* pExecutionResource) = 0;
```

### <a name="parameters"></a>パラメーター

*pExecutionResource*<br/>
`IExecutionResource`オーバーサブスクライブするハードウェアスレッドを表すインターフェイス。

### <a name="return-value"></a>戻り値

`IVirtualProcessorRoot` インターフェイスです。

### <a name="remarks"></a>解説

スケジューラが特定のハードウェアスレッドを制限時間内にオーバーサブスクライブする場合は、このメソッドを使用します。 仮想プロセッサルートが完成したら、インターフェイスの[Remove](iexecutionresource-structure.md#remove)メソッドを呼び出して、それをリソースマネージャーに返す必要があり `IVirtualProcessorRoot` ます。

インターフェイスはインターフェイスから継承するため、既存の仮想プロセッサルートをオーバーサブスクライブすることもでき `IVirtualProcessorRoot` `IExecutionResource` ます。

## <a name="ischedulerproxyrequestinitialvirtualprocessors-method"></a><a name="requestinitialvirtualprocessors"></a>ISchedulerProxy:: RequestInitialVirtualProcessors メソッド

仮想プロセッサルートの初期割り当てを要求します。 すべての仮想プロセッサルートは、スケジューラに対して処理を実行できる1つのスレッドを実行する機能を表します。

```cpp
virtual IExecutionResource* RequestInitialVirtualProcessors(bool doSubscribeCurrentThread) = 0;
```

### <a name="parameters"></a>パラメーター

*doSubscribeCurrentThread*<br/>
リソース割り当て中に、現在のスレッドとアカウントをサブスクライブするかどうかを指定します。

### <a name="return-value"></a>戻り値

`IExecutionResource`パラメーターに値がある場合は、現在のスレッドのインターフェイス `doSubscribeCurrentThread` **`true`** 。 値がの場合 **`false`** 、メソッドは NULL を返します。

### <a name="remarks"></a>解説

スケジューラは、すべての作業を実行する前に、この方法を使用してリソースマネージャーの仮想プロセッサルートを要求します。 リソースマネージャーは、 [IScheduler:: GetPolicy](ischeduler-structure.md#getpolicy)を使用してスケジューラのポリシーにアクセスし、ポリシーキーの値を使用して、 `MinConcurrency` `MaxConcurrency` `TargetOversubscriptionFactor` スケジューラに割り当てるハードウェアスレッドの数と、各ハードウェアスレッドに対して作成する仮想プロセッサルートの数を決定します。 スケジューラポリシーを使用してスケジューラの初期割り当てを決定する方法の詳細については、「 [Policyelementkey](concurrency-namespace-enums.md)」を参照してください。

リソースマネージャーは、仮想プロセッサルートのリストを使用して[IScheduler:: AddVirtualProcessors](ischeduler-structure.md#addvirtualprocessors)メソッドを呼び出すことにより、リソースをスケジューラに付与します。 メソッドは、このメソッドが返される前に、スケジューラにコールバックとして呼び出されます。

スケジューラがパラメーターをに設定して現在のスレッドのサブスクリプションを要求した場合 `doSubscribeCurrentThread` **`true`** 、メソッドはインターフェイスを返し `IExecutionResource` ます。 サブスクリプションは、 [Iexecutionresource:: Remove](iexecutionresource-structure.md#remove)メソッドを使用して、後で終了する必要があります。

選択されているハードウェアスレッドを特定するときに、リソースマネージャーはプロセッサノードアフィニティの最適化を試行します。 現在のスレッドに対してサブスクリプションが要求された場合、現在のスレッドがこのスケジューラに割り当てられた作業に参加することを示します。 このような場合、割り当てられた仮想プロセッサのルートは、可能であれば、現在のスレッドが実行されているプロセッサノードに配置されます。

スレッドをサブスクライブすることにより、基になるハードウェアスレッドのサブスクリプションレベルが1ずつ増加します。 サブスクリプションを終了すると、サブスクリプションレベルは1つ減少します。 サブスクリプションレベルの詳細については、「 [Iexecutionresource:: CurrentSubscriptionLevel](iexecutionresource-structure.md#currentsubscriptionlevel)」を参照してください。

## <a name="ischedulerproxyshutdown-method"></a><a name="shutdown"></a>ISchedulerProxy:: Shutdown メソッド

スケジューラがシャットダウン中であることをリソースマネージャーに通知します。 これにより、リソースマネージャーは、スケジューラに付与されているすべてのリソースを直ちに回収します。

```cpp
virtual void Shutdown() = 0;
```

### <a name="remarks"></a>解説

`IExecutionContext`メソッドを使用して外部スレッドをサブスクライブした結果としてスケジューラが受信したすべてのインターフェイス、 `ISchedulerProxy::RequestInitialVirtualProcessors` またはスケジューラがシャットダウンする `ISchedulerProxy::SubscribeCurrentThread` 前にを使用してリソースマネージャーに返す必要があるすべてのインターフェイス `IExecutionResource::Remove` 。

スケジューラに非アクティブ化された仮想プロセッサルートがある場合は、 [Ivirtualprocessorroot:: activate](ivirtualprocessorroot-structure.md#activate)を使用してアクティブ化する必要があります。また、スケジューラプロキシでを呼び出す前に、これらのスレッドプロキシを実行しているスレッドプロキシが、 `Dispatch` ディスパッチされる実行コンテキストのメソッドをそのまま残し `Shutdown` ます。

スケジューラは、 `Remove` すべての仮想プロセッサルートがシャットダウン時にリソースマネージャーに返されるため、リソースマネージャーがメソッドへの呼び出しによって付与されたすべての仮想プロセッサルートを個別に返す必要はありません。

## <a name="ischedulerproxysubscribecurrentthread-method"></a><a name="subscribecurrentthread"></a>ISchedulerProxy:: SubscribeCurrentThread メソッド

現在のスレッドをリソースマネージャーに登録し、このスケジューラに関連付けます。

```cpp
virtual IExecutionResource* SubscribeCurrentThread() = 0;
```

### <a name="return-value"></a>戻り値

`IExecutionResource`ランタイムの現在のスレッドを表すインターフェイス。

### <a name="remarks"></a>解説

リソースマネージャーが、スケジューラや他のスケジューラにリソースを割り当てるときに現在のスレッドを考慮する必要がある場合は、この方法を使用します。 これは特に、スケジューラにキューに置かれている作業にスレッドが参加する予定の場合に、スケジューラがリソースマネージャーから受け取る仮想プロセッサルートと共に役立ちます。 リソースマネージャーは情報を使用して、システム上のハードウェアスレッドの不要なオーバーサブスクリプションを防止します。

このメソッドを使用して受信した実行リソースは、 [Iexecutionresource:: Remove](iexecutionresource-structure.md#remove)メソッドを使用してリソースマネージャーに返される必要があります。 メソッドを呼び出すスレッドは、 `Remove` 以前にメソッドを呼び出したスレッドと同じである必要があり `SubscribeCurrentThread` ます。

スレッドをサブスクライブすることにより、基になるハードウェアスレッドのサブスクリプションレベルが1ずつ増加します。 サブスクリプションを終了すると、サブスクリプションレベルは1つ減少します。 サブスクリプションレベルの詳細については、「 [Iexecutionresource:: CurrentSubscriptionLevel](iexecutionresource-structure.md#currentsubscriptionlevel)」を参照してください。

## <a name="ischedulerproxyunbindcontext-method"></a><a name="unbindcontext"></a>ISchedulerProxy:: UnbindContext メソッド

パラメーターによって指定された実行コンテキストからスレッドプロキシの関連付けを解除 `pContext` し、スレッドプロキシファクトリの解放プールに返します。 このメソッドは、 [ISchedulerProxy:: BindContext](#bindcontext)メソッドを使用してバインドされた実行コンテキストでのみ呼び出すことができます。また、 `pContext` [Ithreadproxy:: SwitchTo](ithreadproxy-structure.md#switchto)メソッド呼び出しのパラメーターではなく、まだ開始されていません。

```cpp
virtual void UnbindContext(_Inout_ IExecutionContext* pContext) = 0;
```

### <a name="parameters"></a>パラメーター

*pContext*<br/>
スレッドプロキシから関連付けを解除する実行コンテキスト。

## <a name="see-also"></a>関連項目

[concurrency 名前空間](concurrency-namespace.md)<br/>
[IScheduler 構造体](ischeduler-structure.md)<br/>
[IThreadProxy 構造体](ithreadproxy-structure.md)<br/>
[IVirtualProcessorRoot 構造体](ivirtualprocessorroot-structure.md)<br/>
[IResourceManager 構造体](iresourcemanager-structure.md)
