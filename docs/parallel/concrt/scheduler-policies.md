---
title: スケジューラ ポリシー
ms.date: 11/04/2016
helpviewer_keywords:
- scheduler policies
ms.assetid: 58fb68bd-4a57-40a8-807b-6edb6f083cd9
ms.openlocfilehash: d074646a333090138c916bc4d3b7a2e072731b3d
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87228415"
---
# <a name="scheduler-policies"></a>スケジューラ ポリシー

このドキュメントでは、同時実行ランタイムにおける scheduler ポリシーの役割について説明します。 *スケジューラポリシー*では、タスクを管理するときにスケジューラが使用する戦略を制御します。 たとえば、で実行するタスクと、で実行するタスクを必要とするアプリケーションを考えてみ `THREAD_PRIORITY_NORMAL` `THREAD_PRIORITY_HIGHEST` ます。  2つの scheduler インスタンスを作成できます。1つはポリシーを指定し、もう1つは `ContextPriority` `THREAD_PRIORITY_NORMAL` 同じポリシーを指定するもの `THREAD_PRIORITY_HIGHEST` です。

Scheduler ポリシーを使用すると、使用可能な処理リソースを分割し、各スケジューラに固定されたリソースのセットを割り当てることができます。 たとえば、4つのプロセッサを超えて拡張されない並列アルゴリズムについて考えてみます。 同時に4つ以下のプロセッサを使用するようにタスクを制限するスケジューラポリシーを作成できます。

> [!TIP]
> 同時実行ランタイムには、既定のスケジューラが用意されています。 そのため、アプリケーションで作成する必要はありません。 タスクスケジューラはアプリケーションのパフォーマンスを微調整するのに役立ちます。そのため、同時実行ランタイムを初めて使用する場合は、[並列パターンライブラリ (PPL)](../../parallel/concrt/parallel-patterns-library-ppl.md)または[非同期エージェントライブラリ](../../parallel/concrt/asynchronous-agents-library.md)から始めることをお勧めします。

[Concurrency:: CurrentScheduler:: create](reference/currentscheduler-class.md#create)、concurrency:: scheduler [:](reference/scheduler-class.md#create): [setdefaultscheduler policy](reference/scheduler-class.md#setdefaultschedulerpolicy)メソッドを使用して scheduler インスタンスを作成する場合は、scheduler の動作を指定するキーと値のペアのコレクションを含む[concurrency:: scheduler policy](../../parallel/concrt/reference/schedulerpolicy-class.md)オブジェクトを指定します。 コンストラクターは、 `SchedulerPolicy` 可変個の引数を受け取ります。 最初の引数は、指定しようとしているポリシー要素の数です。 残りの引数は、各ポリシー要素のキーと値のペアです。 次の例では、 `SchedulerPolicy` 3 つのポリシー要素を指定するオブジェクトを作成します。 ランタイムは、指定されていないポリシーキーの既定値を使用します。

[!code-cpp[concrt-scheduler-policy#2](../../parallel/concrt/codesnippet/cpp/scheduler-policies_1.cpp)]

[Concurrency::P olicyElementKey](reference/concurrency-namespace-enums.md#policyelementkey)列挙体は、タスクスケジューラに関連付けられているポリシーキーを定義します。 次の表では、ポリシーキーと、ランタイムがそれぞれに使用する既定値について説明します。

|ポリシーキー|説明|Default value|
|----------------|-----------------|-------------------|
|`SchedulerKind`|タスクのスケジュール設定に使用するスレッドの種類を指定する[concurrency:: スケジューラの型](reference/concurrency-namespace-enums.md#schedulertype)の値。|`ThreadScheduler`(通常のスレッドを使用します)。 これは、このキーの唯一の有効な値です。|
|`MaxConcurrency`|**`unsigned int`** スケジューラが使用する同時実行リソースの最大数を指定する値。|[concurrency:: MaxExecutionResources](reference/concurrency-namespace-constants1.md#maxexecutionresources)|
|`MinConcurrency`|**`unsigned int`** スケジューラが使用する同時実行リソースの最小数を指定する値。|`1`|
|`TargetOversubscriptionFactor`|**`unsigned int`** 各処理リソースに割り当てるスレッドの数を指定する値。|`1`|
|`LocalContextCacheSize`|**`unsigned int`** 各仮想プロセッサのローカルキューにキャッシュできるコンテキストの最大数を指定する値。|`8`|
|`ContextStackSize`|**`unsigned int`** 各コンテキストに予約するスタックのサイズ (kb 単位) を指定する値。|`0`(既定のスタックサイズを使用)|
|`ContextPriority`|**`int`** 各コンテキストのスレッドの優先度を示す値です。 これには、 [Setthreadpriority](/windows/win32/api/processthreadsapi/nf-processthreadsapi-setthreadpriority)またはに渡すことができる任意の値を指定でき `INHERIT_THREAD_PRIORITY` ます。|`THREAD_PRIORITY_NORMAL`|

|`SchedulingProtocol`|使用するスケジューリングアルゴリズムを指定する[concurrency:: SchedulingProtocolType](reference/concurrency-namespace-enums.md#schedulingprotocoltype)値。 | `EnhanceScheduleGroupLocality` ||`DynamicProgressFeedback`|統計に基づく進捗情報に従ってリソースを再調整するかどうかを指定する[concurrency::D ynamicprogressfeedbacktype](reference/concurrency-namespace-enums.md#dynamicprogressfeedbacktype)値。<br /><br /> **メモ**このポリシー `ProgressFeedbackDisabled` は、ランタイムで使用するために予約されているため、に設定しないでください |。`ProgressFeedbackEnabled`|

各スケジューラは、タスクをスケジュールするときに独自のポリシーを使用します。 1つのスケジューラに関連付けられているポリシーは、他のスケジューラの動作には影響しません。 また、オブジェクトを作成した後で、scheduler ポリシーを変更することはできません `Scheduler` 。

> [!IMPORTANT]
> スケジューラポリシーのみを使用して、ランタイムによって作成されるスレッドの属性を制御します。 ランタイムによって作成されたスレッドのスレッドアフィニティや優先順位は、未定義の動作が発生する可能性があるため、変更しないでください。

明示的に作成しない場合、ランタイムは既定のスケジューラを作成します。 アプリケーションで既定のスケジューラを使用するが、そのスケジューラに使用するポリシーを指定する場合は、並列処理をスケジュールする前に、 [concurrency:: scheduler:: Setdefaultscheduler policy](reference/scheduler-class.md#setdefaultschedulerpolicy)メソッドを呼び出します。 メソッドを呼び出さない場合、 `Scheduler::SetDefaultSchedulerPolicy` ランタイムはテーブルの既定のポリシー値を使用します。

Scheduler ポリシーのコピーを取得するには、 [concurrency:: CurrentScheduler:: getpolicy](reference/currentscheduler-class.md#getpolicy)メソッドと[Concurrency:: Scheduler:: getpolicy](reference/scheduler-class.md#getpolicy)メソッドを使用します。 これらのメソッドから受け取ったポリシー値は、スケジューラの作成時に指定したポリシー値とは異なる場合があります。

## <a name="example"></a>例

特定のスケジューラポリシーを使用してスケジューラの動作を制御する例を確認するには、「[方法: 特定](../../parallel/concrt/how-to-specify-specific-scheduler-policies.md)のスケジューラポリシーを指定する」および「[方法: 特定のスケジューラポリシーを使用するエージェントを作成](../../parallel/concrt/how-to-create-agents-that-use-specific-scheduler-policies.md)する」を参照してください。

## <a name="see-also"></a>関連項目

[タスク スケジューラ](../../parallel/concrt/task-scheduler-concurrency-runtime.md)<br/>
[方法: 特定のスケジューラポリシーを指定する](../../parallel/concrt/how-to-specify-specific-scheduler-policies.md)<br/>
[方法: 特定のスケジューラポリシーを使用するエージェントを作成する](../../parallel/concrt/how-to-create-agents-that-use-specific-scheduler-policies.md)
