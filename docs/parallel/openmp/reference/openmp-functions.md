---
title: OpenMP の関数
ms.date: 03/20/2019
f1_keywords:
- OpenMP functions
- omp_destroy_lock
- omp_destroy_nest_lock
- omp_get_dynamic
- omp_get_max_threads
- omp_get_nested
- omp_get_num_procs
- omp_get_num_threads
- omp_get_thread_num
- omp_get_wtick
- omp_get_wtime
- omp_in_parallel
- omp_init_lock
- omp_init_nest_lock
- omp_set_dynamic
- omp_set_lock
- omp_set_nest_lock
- omp_set_nested
- omp_set_num_threads
- omp_test_lock
- omp_test_nest_lock
- omp_unset_lock
- omp_unset_nest_lock
helpviewer_keywords:
- OpenMP functions
- omp_destroy_lock OpenMP function
- omp_destroy_nest_lock OpenMP function
- omp_get_dynamic OpenMP function
- omp_get_max_threads OpenMP function
- omp_get_nested OpenMP function
- omp_get_num_procs OpenMP function
- omp_get_num_threads OpenMP function
- omp_get_thread_num OpenMP function
- omp_get_wtick OpenMP function
- omp_get_wtime OpenMP function
- omp_in_parallel OpenMP function
- omp_init_lock OpenMP function
- omp_init_nest_lock OpenMP function
- omp_set_dynamic OpenMP function
- omp_set_lock OpenMP function
- omp_set_nest_lock OpenMP function
- omp_set_nested OpenMP function
- omp_set_num_threads OpenMP function
- omp_test_lock OpenMP function
- omp_test_nest_lock OpenMP function
- omp_unset_lock OpenMP function
- omp_unset_nest_lock OpenMP function
ms.assetid: a55a2e5c-a260-44ee-bbd6-de7e2351b384
ms.openlocfilehash: 0475a83ba259ed00bbcb9ddaba99a1556b35f613
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81317134"
---
# <a name="openmp-functions"></a>OpenMP の関数

OpenMP API で使用される関数へのリンクを示します。

OpenMP 標準の Visual C++ 実装には、次の関数とデータ型が含まれています。

環境の実行:

|機能|説明|
|--------|-----------|
|[omp_set_num_threads](#omp-set-num-threads)|[num_threads](openmp-clauses.md#num-threads)節でオーバーライドされない限り、今後の並列領域内のスレッド数を設定します。|
|[omp_get_num_threads](#omp-get-num-threads)|並列領域のスレッド数を返します。|
|[omp_get_max_threads](#omp-get-max-threads)|コードのその時点で[、num_threads](openmp-clauses.md#num-threads)のない並列領域が定義されている場合に使用できるスレッド数以上の整数を返します。|
|[omp_get_thread_num](#omp-get-thread-num)|スレッド チーム内で実行されているスレッドのスレッド番号を返します。|
|[omp_get_num_procs](#omp-get-num-procs)|関数が呼び出されたときに使用可能なプロセッサの数を返します。|
|[omp_in_parallel](#omp-in-parallel)|並列領域内から呼び出された場合は、0 以外を返します。|
|[omp_set_dynamic](#omp-set-dynamic)|今後の並列領域で使用可能なスレッド数を実行時に調整できることを示します。|
|[omp_get_dynamic](#omp-get-dynamic)|今後の並列領域で使用可能なスレッド数を実行時に調整できるかどうかを示す値を返します。|
|[omp_set_nested](#omp-set-nested)|ネストされた並列処理を有効にします。|
|[omp_get_nested](#omp-get-nested)|入れ子になった並列処理が有効かどうかを示す値を返します。|

ロックの場合:

|機能|説明|
|--------|-----------|
|[omp_init_lock](#omp-init-lock)|単純なロックを初期化します。|
|[omp_init_nest_lock](#omp-init-nest-lock)|ロックを初期化します。|
|[omp_destroy_lock](#omp-destroy-lock)|ロックを初期化解除します。|
|[omp_destroy_nest_lock](#omp-destroy-nest-lock)|入れ子にできるロックを初期化解除します。|
|[omp_set_lock](#omp-set-lock)|ロックが使用可能になるまでスレッドの実行をブロックします。|
|[omp_set_nest_lock](#omp-set-nest-lock)|ロックが使用可能になるまでスレッドの実行をブロックします。|
|[omp_unset_lock](#omp-unset-lock)|ロックを解除します。|
|[omp_unset_nest_lock](#omp-unset-nest-lock)|ネスト可能ロックを解放します。|
|[omp_test_lock](#omp-test-lock)|ロックを設定しようとしますが、スレッドの実行をブロックしません。|
|[omp_test_nest_lock](#omp-test-nest-lock)|入れ子にできるロックを設定しようとしますが、スレッドの実行をブロックしません。|

|データ型|説明|
|---------|-----------|
|`omp_lock_t`|ロックの状態を保持する型。ロックが使用可能かどうか、またはスレッドがロックを所有しているかどうか。|
|`omp_nest_lock_t`|ロックに関する情報の 1 つを保持する型: ロックが使用可能かどうか、およびロックを所有するスレッドの ID と入れ子のカウント。|

タイミング ルーチンの場合:

|機能|説明|
|--------|-----------|
|[omp_get_wtime](#omp-get-wtime)|ある時点から経過した時間の秒数を返します。|
|[omp_get_wtick](#omp-get-wtick)|プロセッサクロック刻み間隔の秒数を返します。|

## <a name="omp_destroy_lock"></a><a name="omp-destroy-lock"></a>omp_destroy_lock

ロックを初期化解除します。

```cpp
void omp_destroy_lock(
   omp_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_lock で初期化`omp_lock_t`された型の変数[omp_init_lock](#omp-init-lock)。

### <a name="remarks"></a>解説

詳細については[、「3.2.2 omp_destroy_lockとomp_destroy_nest_lock関数](../../../parallel/openmp/3-2-2-omp-destroy-lock-and-omp-destroy-nest-lock-functions.md)」を参照してください。

### <a name="example"></a>例

の使用例については[、「omp_init_lock」](#omp-init-lock)を`omp_destroy_lock`参照してください。

## <a name="omp_destroy_nest_lock"></a><a name="omp-destroy-nest-lock"></a>omp_destroy_nest_lock

入れ子にできるロックを初期化解除します。

```cpp
void omp_destroy_nest_lock(
   omp_nest_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_nest_lock で初期化`omp_nest_lock_t`された型の変数[omp_init_nest_lock](#omp-init-nest-lock)。

### <a name="remarks"></a>解説

詳細については[、「3.2.2 omp_destroy_lockとomp_destroy_nest_lock関数](../../../parallel/openmp/3-2-2-omp-destroy-lock-and-omp-destroy-nest-lock-functions.md)」を参照してください。

### <a name="example"></a>例

の使用例`omp_destroy_nest_lock`については[、「omp_init_nest_lock」](#omp-init-nest-lock)を参照してください。

## <a name="omp_get_dynamic"></a><a name="omp-get-dynamic"></a>omp_get_dynamic

今後の並列領域で使用可能なスレッド数を実行時に調整できるかどうかを示す値を返します。

```cpp
int omp_get_dynamic();
```

### <a name="return-value"></a>戻り値

ゼロ以外の値は、スレッドが動的に調整されることを意味します。

### <a name="remarks"></a>解説

スレッドの動的調整は、 [omp_set_dynamic](#omp-set-dynamic)と[OMP_DYNAMIC](openmp-environment-variables.md#omp-dynamic)で指定します。

詳細については[、3.1.7 omp_set_dynamic機能](../../../parallel/openmp/3-1-7-omp-set-dynamic-function.md)を参照してください。

### <a name="example"></a>例

の使用例については[、「omp_set_dynamic」](#omp-set-dynamic)を`omp_get_dynamic`参照してください。

## <a name="omp_get_max_threads"></a><a name="omp-get-max-threads"></a>omp_get_max_threads

コードのその時点で[、num_threads](openmp-clauses.md#num-threads)のない並列領域が定義されている場合に使用できるスレッド数以上の整数を返します。

```cpp
int omp_get_max_threads( )
```

### <a name="remarks"></a>解説

詳細については[、3.1.3 omp_get_max_threads機能](../../../parallel/openmp/3-1-3-omp-get-max-threads-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_get_max_threads.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

int main( )
{
    omp_set_num_threads(8);
    printf_s("%d\n", omp_get_max_threads( ));
    #pragma omp parallel
        #pragma omp master
        {
            printf_s("%d\n", omp_get_max_threads( ));
        }

    printf_s("%d\n", omp_get_max_threads( ));

    #pragma omp parallel num_threads(3)
        #pragma omp master
        {
            printf_s("%d\n", omp_get_max_threads( ));
        }

    printf_s("%d\n", omp_get_max_threads( ));
}
```

```Output
8
8
8
8
8
```

## <a name="omp_get_nested"></a><a name="omp-get-nested"></a>omp_get_nested

入れ子になった並列処理が有効かどうかを示す値を返します。

```cpp
int omp_get_nested( );
```

### <a name="return-value"></a>戻り値

ゼロ以外の値は、ネストされた並列処理が有効であることを意味します。

### <a name="remarks"></a>解説

ネストされた並列処理は、 [omp_set_nested](#omp-set-nested)と[OMP_NESTED](openmp-environment-variables.md#omp-nested)で指定します。

詳細については[、「3.1.10 omp_get_nested関数](../../../parallel/openmp/3-1-10-omp-get-nested-function.md)」を参照してください。

### <a name="example"></a>例

の使用例については[、「omp_set_nested」](#omp-set-nested)を`omp_get_nested`参照してください。

## <a name="omp_get_num_procs"></a><a name="omp-get-num-procs"></a>omp_get_num_procs

関数が呼び出されたときに使用可能なプロセッサの数を返します。

```cpp
int omp_get_num_procs();
```

### <a name="remarks"></a>解説

詳細については[、3.1.5 omp_get_num_procs関数](../../../parallel/openmp/3-1-5-omp-get-num-procs-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_get_num_procs.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

int main( )
{
    printf_s("%d\n", omp_get_num_procs( ));
    #pragma omp parallel
        #pragma omp master
        {
            printf_s("%d\n", omp_get_num_procs( ));
        }
}
```

```Output
// Expect the following output when the example is run on a two-processor machine:
2
2
```

## <a name="omp_get_num_threads"></a><a name="omp-get-num-threads"></a>omp_get_num_threads

並列領域のスレッド数を返します。

```cpp
int omp_get_num_threads( );
```

### <a name="remarks"></a>解説

詳細については[、3.1.2 omp_get_num_threads機能](../../../parallel/openmp/3-1-2-omp-get-num-threads-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_get_num_threads.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

int main()
{
    omp_set_num_threads(4);
    printf_s("%d\n", omp_get_num_threads( ));
    #pragma omp parallel
        #pragma omp master
        {
            printf_s("%d\n", omp_get_num_threads( ));
        }

    printf_s("%d\n", omp_get_num_threads( ));

    #pragma omp parallel num_threads(3)
        #pragma omp master
        {
            printf_s("%d\n", omp_get_num_threads( ));
        }

    printf_s("%d\n", omp_get_num_threads( ));
}
```

```Output
1
4
1
3
1
```

## <a name="omp_get_thread_num"></a><a name="omp-get-thread-num"></a>omp_get_thread_num

スレッド チーム内で実行されているスレッドのスレッド番号を返します。

```cpp
int omp_get_thread_num( );
```

### <a name="remarks"></a>解説

詳細については[、3.1.4 omp_get_thread_num機能](../../../parallel/openmp/3-1-4-omp-get-thread-num-function.md)を参照してください。

### <a name="example"></a>例

の使用例については、[パラレル](openmp-directives.md#parallel)を`omp_get_thread_num`参照してください。

## <a name="omp_get_wtick"></a><a name="omp-get-wtick"></a>omp_get_wtick

プロセッサクロック刻み間隔の秒数を返します。

```cpp
double omp_get_wtick( );
```

### <a name="remarks"></a>解説

詳細については[、3.3.2 omp_get_wtick機能](../../../parallel/openmp/3-3-2-omp-get-wtick-function.md)を参照してください。

### <a name="example"></a>例

の使用例`omp_get_wtick`については[、omp_get_wtime](#omp-get-wtime)を参照してください。

## <a name="omp_get_wtime"></a><a name="omp-get-wtime"></a>omp_get_wtime

ある時点から経過した時間の秒数を返します。

```cpp
double omp_get_wtime( );
```

### <a name="return-value"></a>戻り値

任意の一貫性のあるポイントから経過した時間の秒数を返します。

### <a name="remarks"></a>解説

その点はプログラムの実行中も一貫して維持され、今後の比較が可能になります。

詳細については[、3.3.1 omp_get_wtime関数](../../../parallel/openmp/3-3-1-omp-get-wtime-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_get_wtime.cpp
// compile with: /openmp
#include "omp.h"
#include <stdio.h>
#include <windows.h>

int main() {
    double start = omp_get_wtime( );
    Sleep(1000);
    double end = omp_get_wtime( );
    double wtick = omp_get_wtick( );

    printf_s("start = %.16g\nend = %.16g\ndiff = %.16g\n",
             start, end, end - start);

    printf_s("wtick = %.16g\n1/wtick = %.16g\n",
             wtick, 1.0 / wtick);
}
```

```Output
start = 594255.3671159324
end = 594256.3664474116
diff = 0.9993314791936427
wtick = 2.793651148400146e-007
1/wtick = 3579545
```

## <a name="omp_in_parallel"></a><a name="omp-in-parallel"></a>omp_in_parallel

並列領域内から呼び出された場合は、0 以外を返します。

```cpp
int omp_in_parallel( );
```

### <a name="remarks"></a>解説

詳細については[、3.1.6 omp_in_parallel機能](../../../parallel/openmp/3-1-6-omp-in-parallel-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_in_parallel.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

int main( )
{
    omp_set_num_threads(4);
    printf_s("%d\n", omp_in_parallel( ));

    #pragma omp parallel
        #pragma omp master
        {
            printf_s("%d\n", omp_in_parallel( ));
        }
}
```

```Output
0
1
```

## <a name="omp_init_lock"></a><a name="omp-init-lock"></a>omp_init_lock

単純なロックを初期化します。

```cpp
void omp_init_lock(
   omp_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
`omp_lock_t` 型の変数。

### <a name="remarks"></a>解説

詳細については[、「3.2.1 omp_init_lock関数とomp_init_nest_lock関数](../../../parallel/openmp/3-2-1-omp-init-lock-and-omp-init-nest-lock-functions.md)」を参照してください。

### <a name="example"></a>例

```cpp
// omp_init_lock.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

omp_lock_t my_lock;

int main() {
   omp_init_lock(&my_lock);

   #pragma omp parallel num_threads(4)
   {
      int tid = omp_get_thread_num( );
      int i, j;

      for (i = 0; i < 5; ++i) {
         omp_set_lock(&my_lock);
         printf_s("Thread %d - starting locked region\n", tid);
         printf_s("Thread %d - ending locked region\n", tid);
         omp_unset_lock(&my_lock);
      }
   }

   omp_destroy_lock(&my_lock);
}
```

```Output
Thread 0 - starting locked region
Thread 0 - ending locked region
Thread 0 - starting locked region
Thread 0 - ending locked region
Thread 0 - starting locked region
Thread 0 - ending locked region
Thread 0 - starting locked region
Thread 0 - ending locked region
Thread 0 - starting locked region
Thread 0 - ending locked region
Thread 1 - starting locked region
Thread 1 - ending locked region
Thread 1 - starting locked region
Thread 1 - ending locked region
Thread 1 - starting locked region
Thread 1 - ending locked region
Thread 1 - starting locked region
Thread 1 - ending locked region
Thread 1 - starting locked region
Thread 1 - ending locked region
Thread 2 - starting locked region
Thread 2 - ending locked region
Thread 2 - starting locked region
Thread 2 - ending locked region
Thread 2 - starting locked region
Thread 2 - ending locked region
Thread 2 - starting locked region
Thread 2 - ending locked region
Thread 2 - starting locked region
Thread 2 - ending locked region
Thread 3 - starting locked region
Thread 3 - ending locked region
Thread 3 - starting locked region
Thread 3 - ending locked region
Thread 3 - starting locked region
Thread 3 - ending locked region
Thread 3 - starting locked region
Thread 3 - ending locked region
Thread 3 - starting locked region
Thread 3 - ending locked region
```

## <a name="omp_init_nest_lock"></a><a name="omp-init-nest-lock"></a>omp_init_nest_lock

ロックを初期化します。

```cpp
void omp_init_nest_lock(
   omp_nest_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
`omp_nest_lock_t` 型の変数。

### <a name="remarks"></a>解説

初期ネスト数はゼロです。

詳細については[、「3.2.1 omp_init_lock関数とomp_init_nest_lock関数](../../../parallel/openmp/3-2-1-omp-init-lock-and-omp-init-nest-lock-functions.md)」を参照してください。

### <a name="example"></a>例

```cpp
// omp_init_nest_lock.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

omp_nest_lock_t my_lock;

void Test() {
   int tid = omp_get_thread_num( );
   omp_set_nest_lock(&my_lock);
   printf_s("Thread %d - starting nested locked region\n", tid);
   printf_s("Thread %d - ending nested locked region\n", tid);
   omp_unset_nest_lock(&my_lock);
}

int main() {
   omp_init_nest_lock(&my_lock);

   #pragma omp parallel num_threads(4)
   {
      int i, j;

      for (i = 0; i < 5; ++i) {
         omp_set_nest_lock(&my_lock);
            if (i % 3)
               Test();
            omp_unset_nest_lock(&my_lock);
        }
    }

    omp_destroy_nest_lock(&my_lock);
}
```

```Output
Thread 0 - starting nested locked region
Thread 0 - ending nested locked region
Thread 0 - starting nested locked region
Thread 0 - ending nested locked region
Thread 3 - starting nested locked region
Thread 3 - ending nested locked region
Thread 3 - starting nested locked region
Thread 3 - ending nested locked region
Thread 3 - starting nested locked region
Thread 3 - ending nested locked region
Thread 2 - starting nested locked region
Thread 2 - ending nested locked region
Thread 2 - starting nested locked region
Thread 2 - ending nested locked region
Thread 2 - starting nested locked region
Thread 2 - ending nested locked region
Thread 1 - starting nested locked region
Thread 1 - ending nested locked region
Thread 1 - starting nested locked region
Thread 1 - ending nested locked region
Thread 1 - starting nested locked region
Thread 1 - ending nested locked region
Thread 0 - starting nested locked region
Thread 0 - ending nested locked region
```

## <a name="omp_set_dynamic"></a><a name="omp-set-dynamic"></a>omp_set_dynamic

今後の並列領域で使用可能なスレッド数を実行時に調整できることを示します。

```cpp
void omp_set_dynamic(
   int val
);
```

### <a name="parameters"></a>パラメーター

*ヴァル*<br/>
今後の並列領域で使用可能なスレッド数をランタイムで調整できるかどうかを示す値。 0 以外の場合、ランタイムはスレッド数を調整できます (0 の場合、ランタイムはスレッド数を動的に調整しません)。

### <a name="remarks"></a>解説

スレッドの数が[、omp_set_num_threads](#omp-set-num-threads)または[OMP_NUM_THREADS](openmp-environment-variables.md#omp-num-threads)によって設定された値を超えることはありません。

[omp_get_dynamic](#omp-get-dynamic)を使用して、 の現在`omp_set_dynamic`の設定を表示します。

の設定`omp_set_dynamic`は[、OMP_DYNAMIC](openmp-environment-variables.md#omp-dynamic)環境変数の設定をオーバーライドします。

詳細については[、3.1.7 omp_set_dynamic機能](../../../parallel/openmp/3-1-7-omp-set-dynamic-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_set_dynamic.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

int main()
{
    omp_set_dynamic(9);
    omp_set_num_threads(4);
    printf_s("%d\n", omp_get_dynamic( ));
    #pragma omp parallel
        #pragma omp master
        {
            printf_s("%d\n", omp_get_dynamic( ));
        }
}
```

```Output
1
1
```

## <a name="omp_set_lock"></a><a name="omp-set-lock"></a>omp_set_lock

ロックが使用可能になるまでスレッドの実行をブロックします。

```cpp
void omp_set_lock(
   omp_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_lock で初期化`omp_lock_t`された型の変数[omp_init_lock](#omp-init-lock)。

### <a name="remarks"></a>解説

詳細については[、「3.2.3 omp_set_lockとomp_set_nest_lock関数](../../../parallel/openmp/3-2-3-omp-set-lock-and-omp-set-nest-lock-functions.md)」を参照してください。

### <a name="examples"></a>例

の使用例については[、「omp_init_lock」](#omp-init-lock)を`omp_set_lock`参照してください。

## <a name="omp_set_nest_lock"></a><a name="omp-set-nest-lock"></a>omp_set_nest_lock

ロックが使用可能になるまでスレッドの実行をブロックします。

```cpp
void omp_set_nest_lock(
   omp_nest_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_nest_lock で初期化`omp_nest_lock_t`された型の変数[omp_init_nest_lock](#omp-init-nest-lock)。

### <a name="remarks"></a>解説

詳細については[、「3.2.3 omp_set_lockとomp_set_nest_lock関数](../../../parallel/openmp/3-2-3-omp-set-lock-and-omp-set-nest-lock-functions.md)」を参照してください。

### <a name="examples"></a>例

の使用例`omp_set_nest_lock`については[、「omp_init_nest_lock」](#omp-init-nest-lock)を参照してください。

## <a name="omp_set_nested"></a><a name="omp-set-nested"></a>omp_set_nested

ネストされた並列処理を有効にします。

```cpp
void omp_set_nested(
   int val
);
```

### <a name="parameters"></a>パラメーター

*ヴァル*<br/>
ゼロ以外の値はネストされた並列処理を可能にし、ゼロはネストされた並列処理を無効にします。

### <a name="remarks"></a>解説

OMP ネストされた並列処理は、 を`omp_set_nested`使用してオンにするか[、OMP_NESTED](openmp-environment-variables.md#omp-nested)環境変数を設定することによって有効にすることができます。

の設定`omp_set_nested`は環境変数の設定を`OMP_NESTED`オーバーライドします。

並列領域を入れ子にするときにスレッドの数が指数関数的に増加するため、環境変数を有効にすると、それ以外の操作プログラムが中断される可能性があります。 たとえば、OMP スレッドの数を 4 に設定して 6 回再帰する関数には、4,096 (6 の累乗の 4) スレッドが必要です。 I/O バインド アプリケーションを除き、プロセッサよりもスレッド数が多い場合、アプリケーションのパフォーマンスは一般的に低下します。

[omp_get_nested](#omp-get-nested)を使用して、 の現在`omp_set_nested`の設定を表示します。

詳細については[、3.1.9 omp_set_nested関数](../../../parallel/openmp/3-1-9-omp-set-nested-function.md)を参照してください。

### <a name="example"></a>例

```cpp
// omp_set_nested.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

int main( )
{
    omp_set_nested(1);
    omp_set_num_threads(4);
    printf_s("%d\n", omp_get_nested( ));
    #pragma omp parallel
        #pragma omp master
        {
            printf_s("%d\n", omp_get_nested( ));
        }
}
```

```Output
1
1
```

## <a name="omp_set_num_threads"></a><a name="omp-set-num-threads"></a>omp_set_num_threads

[num_threads](openmp-clauses.md#num-threads)節でオーバーライドされない限り、今後の並列領域内のスレッド数を設定します。

```cpp
void omp_set_num_threads(
   int num_threads
);
```

### <a name="parameters"></a>パラメーター

*num_threads*<br/>
並列領域内のスレッドの数。

### <a name="remarks"></a>解説

詳細については[、3.1.1 omp_set_num_threads関数](../../../parallel/openmp/3-1-1-omp-set-num-threads-function.md)を参照してください。

### <a name="example"></a>例

の[omp_get_num_threads](#omp-get-num-threads)使用例`omp_set_num_threads`についてはomp_get_num_threadsを参照してください。

## <a name="omp_test_lock"></a><a name="omp-test-lock"></a>omp_test_lock

ロックを設定しようとしますが、スレッドの実行をブロックしません。

```cpp
int omp_test_lock(
   omp_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_lock で初期化`omp_lock_t`された型の変数[omp_init_lock](#omp-init-lock)。

### <a name="remarks"></a>解説

詳細については[、「3.2.5 omp_test_lockとomp_test_nest_lock関数](../../../parallel/openmp/3-2-5-omp-test-lock-and-omp-test-nest-lock-functions.md)」を参照してください。

### <a name="example"></a>例

```cpp
// omp_test_lock.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

omp_lock_t simple_lock;

int main() {
    omp_init_lock(&simple_lock);

    #pragma omp parallel num_threads(4)
    {
        int tid = omp_get_thread_num();

        while (!omp_test_lock(&simple_lock))
            printf_s("Thread %d - failed to acquire simple_lock\n",
                     tid);

        printf_s("Thread %d - acquired simple_lock\n", tid);

        printf_s("Thread %d - released simple_lock\n", tid);
        omp_unset_lock(&simple_lock);
    }

    omp_destroy_lock(&simple_lock);
}
```

```Output
Thread 1 - acquired simple_lock
Thread 1 - released simple_lock
Thread 0 - failed to acquire simple_lock
Thread 3 - failed to acquire simple_lock
Thread 0 - failed to acquire simple_lock
Thread 3 - failed to acquire simple_lock
Thread 2 - acquired simple_lock
Thread 0 - failed to acquire simple_lock
Thread 3 - failed to acquire simple_lock
Thread 0 - failed to acquire simple_lock
Thread 3 - failed to acquire simple_lock
Thread 2 - released simple_lock
Thread 0 - failed to acquire simple_lock
Thread 3 - failed to acquire simple_lock
Thread 0 - acquired simple_lock
Thread 3 - failed to acquire simple_lock
Thread 0 - released simple_lock
Thread 3 - failed to acquire simple_lock
Thread 3 - acquired simple_lock
Thread 3 - released simple_lock
```

## <a name="omp_test_nest_lock"></a><a name="omp-test-nest-lock"></a>omp_test_nest_lock

入れ子にできるロックを設定しようとしますが、スレッドの実行をブロックしません。

```cpp
int omp_test_nest_lock(
   omp_nest_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_nest_lock で初期化`omp_nest_lock_t`された型の変数[omp_init_nest_lock](#omp-init-nest-lock)。

### <a name="remarks"></a>解説

詳細については[、「3.2.5 omp_test_lockとomp_test_nest_lock関数](../../../parallel/openmp/3-2-5-omp-test-lock-and-omp-test-nest-lock-functions.md)」を参照してください。

### <a name="example"></a>例

```cpp
// omp_test_nest_lock.cpp
// compile with: /openmp
#include <stdio.h>
#include <omp.h>

omp_nest_lock_t nestable_lock;

int main() {
   omp_init_nest_lock(&nestable_lock);

   #pragma omp parallel num_threads(4)
   {
      int tid = omp_get_thread_num();
      while (!omp_test_nest_lock(&nestable_lock))
         printf_s("Thread %d - failed to acquire nestable_lock\n",
                tid);

      printf_s("Thread %d - acquired nestable_lock\n", tid);

      if (omp_test_nest_lock(&nestable_lock)) {
         printf_s("Thread %d - acquired nestable_lock again\n",
                tid);
         printf_s("Thread %d - released nestable_lock\n",
                tid);
         omp_unset_nest_lock(&nestable_lock);
      }

      printf_s("Thread %d - released nestable_lock\n", tid);
      omp_unset_nest_lock(&nestable_lock);
   }

   omp_destroy_nest_lock(&nestable_lock);
}
```

```Output
Thread 1 - acquired nestable_lock
Thread 0 - failed to acquire nestable_lock
Thread 1 - acquired nestable_lock again
Thread 0 - failed to acquire nestable_lock
Thread 1 - released nestable_lock
Thread 0 - failed to acquire nestable_lock
Thread 1 - released nestable_lock
Thread 0 - failed to acquire nestable_lock
Thread 3 - acquired nestable_lock
Thread 0 - failed to acquire nestable_lock
Thread 3 - acquired nestable_lock again
Thread 0 - failed to acquire nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 3 - released nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 3 - released nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 0 - acquired nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 0 - acquired nestable_lock again
Thread 2 - failed to acquire nestable_lock
Thread 0 - released nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 0 - released nestable_lock
Thread 2 - failed to acquire nestable_lock
Thread 2 - acquired nestable_lock
Thread 2 - acquired nestable_lock again
Thread 2 - released nestable_lock
Thread 2 - released nestable_lock
```

## <a name="omp_unset_lock"></a><a name="omp-unset-lock"></a>omp_unset_lock

ロックを解除します。

```cpp
void omp_unset_lock(
   omp_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_lockで初期化された`omp_lock_t`型の変数は[omp_init_lock](#omp-init-lock)、スレッドによって所有され、関数で実行されます。

### <a name="remarks"></a>解説

詳細については[、3.2.4 omp_unset_lockおよびomp_unset_nest_lock関数](../../../parallel/openmp/3-2-4-omp-unset-lock-and-omp-unset-nest-lock-functions.md)を参照してください。

### <a name="example"></a>例

の使用例については[、「omp_init_lock」](#omp-init-lock)を`omp_unset_lock`参照してください。

## <a name="omp_unset_nest_lock"></a><a name="omp-unset-nest-lock"></a>omp_unset_nest_lock

ネスト可能ロックを解放します。

```cpp
void omp_unset_nest_lock(
   omp_nest_lock_t *lock
);
```

### <a name="parameters"></a>パラメーター

*ロック*<br/>
omp_init_nest_lock で初期化`omp_nest_lock_t`された型の変数[omp_init_nest_lock](#omp-init-nest-lock)が、スレッドによって所有され、関数で実行されます。

### <a name="remarks"></a>解説

詳細については[、3.2.4 omp_unset_lockおよびomp_unset_nest_lock関数](../../../parallel/openmp/3-2-4-omp-unset-lock-and-omp-unset-nest-lock-functions.md)を参照してください。

### <a name="example"></a>例

の使用例`omp_unset_nest_lock`については[、「omp_init_nest_lock」](#omp-init-nest-lock)を参照してください。
