---
title: _spawnl、_wspawnl
ms.date: 11/04/2016
api_name:
- _wspawnl
- _spawnl
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
- api-ms-win-crt-process-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- wspawnl
- _wspawnl
- _spawnl
helpviewer_keywords:
- spawnl function
- processes, creating
- _spawnl function
- processes, executing new
- _wspawnl function
- wspawnl function
- process creation
ms.assetid: dd4584c9-7173-4fc5-b93a-6e7d3c2316d7
ms.openlocfilehash: 4b51faae4ba6f371f712e4c39374ae9717c90bed
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88834376"
---
# <a name="_spawnl-_wspawnl"></a>_spawnl、_wspawnl

新しいプロセスを作成して実行します。

> [!IMPORTANT]
> この API は、Windows ランタイムで実行するアプリケーションでは使用できません。 詳細については、「[ユニバーサル Windows プラットフォーム アプリでサポートされていない CRT 関数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)」を参照してください。

## <a name="syntax"></a>構文

```C
intptr_t _spawnl(
   int mode,
   const char *cmdname,
   const char *arg0,
   const char *arg1,
   ... const char *argn,
   NULL
);
intptr_t _wspawnl(
   int mode,
   const wchar_t *cmdname,
   const wchar_t *arg0,
   const wchar_t *arg1,
   ... const wchar_t *argn,
   NULL
);
```

### <a name="parameters"></a>パラメーター

*mode*<br/>
呼び出しプロセスの実行モード。

*cmdname*<br/>
実行されるファイルのパス。

*arg0*、 *arg1*、... *argn*<br/>
引数へのポインターのリスト。 *Arg0*引数は通常、 *cmdname*へのポインターです。 引数 *arg1* ~ *argn* は、新しい引数リストを形成する文字列へのポインターです。 *Argn*の後に、引数リストの末尾を示す**NULL**ポインターが必要です。

## <a name="return-value"></a>戻り値

同期 **_spawnl**または **_wspawnl** (*モード*用に指定された **_P_WAIT** ) からの戻り値は、新しいプロセスの終了ステータスです。 非同期 **_spawnl**または **_wspawnl** (*モード*で指定された **_P_NOWAIT**または **_P_NOWAITO** ) からの戻り値がプロセスハンドルです。 プロセスが正常に終了した場合、終了ステータスは 0 です。 生成されたプロセスが明示的に0以外の引数で **終了** ルーチンを呼び出す場合は、終了ステータスを0以外の値に設定できます。 新しいプロセスが明示的に終了ステータスを正の値に設定しなかった場合、正の値の終了ステータスは中止または割り込みによる異常終了を示します。 戻り値-1 はエラーを示します (新しいプロセスは開始されません)。 この場合、 **errno** は次のいずれかの値に設定されます。

| 値 | 説明 |
|--|--|
| **E2BIG** | 引数リストが 1024 バイトを超えています。 |
| **EINVAL** | *モード* 引数が無効です。 |
| **ENOENT** | ファイルまたはパスが見つかりません。 |
| **ENOEXEC** | 指定されたファイルが実行可能ファイルでないか、無効な実行可能ファイル形式です。 |
| **ENOMEM** | 新しいプロセスを実行するのに十分なメモリがありません。 |

リターン コードの詳細については、「[_doserrno、errno、_sys_errlist、および _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)」を参照してください。

これらの関数では、パラメーターの検証が行われます。 *Cmdname*または*arg0*が空の文字列または null ポインターの場合は、「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、無効なパラメーターハンドラーが呼び出されます。 実行の継続が許可された場合、これらの関数は **errno** を **EINVAL**に設定し、-1 を返します。 新しいプロセスは起動されません。

## <a name="remarks"></a>解説

これらの各関数は新しいプロセスを作成して実行し、各コマンド ライン引数を個別のパラメーターとして渡します。

## <a name="requirements"></a>必要条件

|ルーチンによって返される値|必須ヘッダー|
|-------------|---------------------|
|**_spawnl**|\<process.h>|
|**_wspawnl**|\<stdio.h> または \<wchar.h>|

互換性について詳しくは、「 [Compatibility](../../c-runtime-library/compatibility.md)」をご覧ください。

## <a name="example"></a>例

[_spawn, _wspawn Functions](../../c-runtime-library/spawn-wspawn-functions.md)の例を参照してください。

## <a name="see-also"></a>関連項目

[プロセスと環境の制御](../../c-runtime-library/process-and-environment-control.md)<br/>
[_spawn, _wspawn 関数](../../c-runtime-library/spawn-wspawn-functions.md)<br/>
[取り消し](abort.md)<br/>
[atexit](atexit.md)<br/>
[_exec, _wexec 関数](../../c-runtime-library/exec-wexec-functions.md)<br/>
[終了、_Exit、_exit](exit-exit-exit.md)<br/>
[_flushall](flushall.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_onexit、_onexit_m](onexit-onexit-m.md)<br/>
[_setmbcp](setmbcp.md)<br/>
[system、_wsystem](system-wsystem.md)<br/>
