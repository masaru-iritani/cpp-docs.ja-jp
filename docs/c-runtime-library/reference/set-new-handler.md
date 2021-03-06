---
title: _set_new_handler
ms.date: 4/2/2020
api_name:
- _set_new_handler
- _o__set_new_handler
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-runtime-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _set_new_handler
- set_new_handler
helpviewer_keywords:
- _set_new_handler function
- set_new_handler function
- error handling
- transferring control to error handler
ms.assetid: 1d1781b6-5cf8-486a-b430-f365e0bb023f
ms.openlocfilehash: cd6e4df47b28e84bb0ac5ee857cfa1a3e7cf805a
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87218547"
---
# <a name="_set_new_handler"></a>_set_new_handler

演算子がメモリの割り当てに失敗した場合は、エラー処理機構に制御を転送し **`new`** ます。

## <a name="syntax"></a>構文

```cpp
_PNH _set_new_handler( _PNH pNewHandler );
```

### <a name="parameters"></a>パラメーター

*pNewHandler*<br/>
アプリケーションによって提供されたメモリ処理関数へのポインター。 引数が 0 の場合、新しいハンドラーは削除されます。

## <a name="return-value"></a>戻り値

前の関数を後で復元できるように、 **_set_new_handler**によって登録された前の例外処理関数へのポインターを返します。 前の関数が設定されていない場合は、戻り値を使用して既定の動作を復元できます。この値には**NULL**を指定できます。

## <a name="remarks"></a>解説

C++ の **_set_new_handler**関数は、演算子がメモリの割り当てに失敗した場合に制御を取得する例外処理関数を指定し **`new`** ます。 が失敗した場合 **`new`** 、ランタイムシステムは、引数として渡された例外処理関数を **_set_new_handler**に自動的に呼び出します。 新しい .h で定義されている **_PNH**は、型を返し **`int`** 、 **size_t**型の引数を受け取る関数へのポインターです。 **Size_t**を使用して、割り当てる領域のサイズを指定します。

既定のハンドラーはありません。

**_set_new_handler**は、基本的にはガベージコレクションスキームです。 ランタイム システムは、関数がゼロ以外の値を返すたびに割り当てを再試行し、関数がゼロを返すと失敗します。

プログラムで **_set_new_handler**関数が発生すると、引数リストで指定された例外処理関数がランタイムシステムに登録されます。

```cpp
// set_new_handler1.cpp
By default, this function's global state is scoped to the application. To change this, see [Global state in the CRT](../global-state.md).

#include <new.h>

int handle_program_memory_depletion( size_t )
{
   // Your code
}

int main( void )
{
   _set_new_handler( handle_program_memory_depletion );
   int *pi = new int[BIG_NUMBER];
}
```

**_Set_new_handler**関数に最後に渡された関数のアドレスを保存し、後で再開することができます。

```cpp
   _PNH old_handler = _set_new_handler( my_handler );
   // Code that requires my_handler
   // . . .
   _set_new_handler( old_handler )
   // Code that requires old_handler
   // . . .
```

C++ の [_set_new_mode](set-new-mode.md) 関数は、[malloc](malloc.md) 用の新しいハンドラー モードを設定します。 新しいハンドラーモードは、エラー発生時に**malloc**が **_set_new_handler**によって設定された新しいハンドラールーチンを呼び出すかどうかを示します。 既定では、 **malloc**は、メモリの割り当てに失敗したときに新しいハンドラールーチンを呼び出しません。 この既定の動作を無効にすると、 **malloc**がメモリの割り当てに失敗したときに、 **malloc**は、同じ理由で失敗したときと同じ方法で新しいハンドラールーチンを呼び出します **`new`** 。 既定の動作をオーバーライドするには、次の関数を呼び出します。

```cpp
_set_new_mode(1);
```

この呼び出しはプログラムの最初の方で指定するか、Newmode.obj にリンクします。

ユーザー定義が指定されている場合 `operator new` 、新しいハンドラー関数は失敗時に自動的には呼び出されません。

詳細については、「*C++ 言語リファレンス*」の「[new](../../cpp/new-operator-cpp.md)」および「[delete](../../cpp/delete-operator-cpp.md)」を参照してください。

動的にリンクされたすべての Dll または実行可能ファイルに対して1つの **_set_new_handler**ハンドラーがあります。を呼び出す場合でも、ハンドラーを別の DLL または実行可能ファイルによって設定されたハンドラーの代わりに置き換えることが **_set_new_handler**ます。

## <a name="requirements"></a>必要条件

|ルーチンによって返される値|必須ヘッダー|
|-------------|---------------------|
|**_set_new_handler**|\<new.h>|

互換性について詳しくは、「 [Compatibility](../../c-runtime-library/compatibility.md)」をご覧ください。

## <a name="example"></a>例

この例では、割り当てが失敗した場合に、MyNewHandler に制御が移ります。 MyNewHandler に渡される引数は、要求されたバイト数です。 MyNewHandler から返される値は、割り当てを再試行する必要があるかどうかを示すフラグです。ゼロ以外の値は割り当てを再試行すべきことを示し、ゼロの値は割り当てが失敗したことを示します。

```cpp
// crt_set_new_handler.cpp
// compile with: /c
#include <stdio.h>
#include <new.h>
#define BIG_NUMBER 0x1fffffff

int coalesced = 0;

int CoalesceHeap()
{
   coalesced = 1;  // Flag RecurseAlloc to stop
   // do some work to free memory
   return 0;
}
// Define a function to be called if new fails to allocate memory.
int MyNewHandler( size_t size )
{
   printf("Allocation failed. Coalescing heap.\n");

   // Call a function to recover some heap space.
   return CoalesceHeap();
}

int RecurseAlloc() {
   int *pi = new int[BIG_NUMBER];
   if (!coalesced)
      RecurseAlloc();
   return 0;
}

int main()
{
   // Set the failure handler for new to be MyNewHandler.
   _set_new_handler( MyNewHandler );
   RecurseAlloc();
}
```

```Output
Allocation failed. Coalescing heap.

This application has requested the Runtime to terminate it in an unusual way.
Please contact the application's support team for more information.
```

## <a name="see-also"></a>関連項目

[メモリの割り当て](../../c-runtime-library/memory-allocation.md)<br/>
[calloc](calloc.md)<br/>
[空け](free.md)<br/>
[realloc](realloc.md)<br/>
