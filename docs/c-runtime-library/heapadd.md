---
title: _heapadd
ms.date: 11/04/2016
api_name:
- _heapadd
api_location:
- msvcr100.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr80.dll
- msvcrt.dll
- msvcr110.dll
- msvcr90.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- heapadd
- _heapadd
helpviewer_keywords:
- _heapadd function
- memory, adding to heaps
- heaps, adding memory
- heapadd function
ms.assetid: 4d691fe2-2763-49f4-afb1-62738b7cd3ff
ms.openlocfilehash: c5eeb66ff0e6fb05063ec395e12cd97106ad724d
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81351329"
---
# <a name="_heapadd"></a>_heapadd

ヒープにメモリを追加します。

> [!IMPORTANT]
> この関数は、現在使用されていません。 Visual Studio 2015 以降では、CRT で使用できません。

## <a name="syntax"></a>構文

```
int _heapadd(
   void *memblock,
   size_t size
);
```

#### <a name="parameters"></a>パラメーター

*memblock*<br/>
ヒープ メモリへのポインター。

*サイズ*<br/>
追加するメモリのサイズ (バイト単位)。

## <a name="return-value"></a>戻り値

成功すると、`_heapadd` は 0 を返します。それ以外の場合、この関数は -1 を返し、`errno` を `ENOSYS` に設定します。

このリターン コードとその他のリターン コードの詳細については、「 [_doserrno、errno、_sys_errlist、および _sys_nerr](../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)」を参照してください。

## <a name="remarks"></a>解説

Visual C++ のバージョン 4.0 以降では、新しいデバッグ機能をサポートするために、基になるヒープ構造が C ランタイム ライブラリに移動しました。 その結果、 `_heapadd` は、Win32 API に基づいているすべてのプラットフォームでサポートされなくなりました。

## <a name="requirements"></a>必要条件

|ルーチン|必須ヘッダー|オプション ヘッダー|
|-------------|---------------------|---------------------|
|`_heapadd`|\<malloc.h>|\<errno.h>|

互換性の詳細については、「C ランタイム ライブラリ」の「 [互換性](../c-runtime-library/compatibility.md) 」を参照してください。

## <a name="see-also"></a>関連項目

[メモリ割り当て](../c-runtime-library/memory-allocation.md)<br/>
[無料](../c-runtime-library/reference/free.md)<br/>
[_heapchk](../c-runtime-library/reference/heapchk.md)<br/>
[_heapmin](../c-runtime-library/reference/heapmin.md)<br/>
[_heapset](../c-runtime-library/heapset.md)<br/>
[_heapwalk](../c-runtime-library/reference/heapwalk.md)<br/>
[malloc](../c-runtime-library/reference/malloc.md)<br/>
[realloc](../c-runtime-library/reference/realloc.md)
