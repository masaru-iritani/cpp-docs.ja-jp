---
title: _ecvt_s
ms.date: 4/2/2020
api_name:
- _ecvt_s
- _o__ecvt_s
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
- api-ms-win-crt-convert-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- ecvt_s
- _ecvt_s
helpviewer_keywords:
- _ecvt_s function
- ecvt_s function
- numbers, converting
- converting double numbers
ms.assetid: d52fb0a6-cb91-423f-80b3-952a8955d914
ms.openlocfilehash: e76ebd065d323a9ae501ce6a7a5790389c7d5dad
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87234212"
---
# <a name="_ecvt_s"></a>_ecvt_s

数値を **`double`** 文字列に変換します。 これは、「[CRT のセキュリティ機能](../../c-runtime-library/security-features-in-the-crt.md)」の説明にあるとおり、セキュリティが強化されたバージョンの [_ecvt](ecvt.md) です。

## <a name="syntax"></a>構文

```C
errno_t _ecvt_s(
   char * _Buffer,
   size_t _SizeInBytes,
   double _Value,
   int _Count,
   int *_Dec,
   int *_Sign
);
template <size_t size>
errno_t _ecvt_s(
   char (&_Buffer)[size],
   double _Value,
   int _Count,
   int *_Dec,
   int *_Sign
); // C++ only
```

### <a name="parameters"></a>パラメーター

*_Buffer*<br/>
変換の結果である数字の文字列へのポインターが格納されます。

*_SizeInBytes*<br/>
バッファーのサイズ (バイト単位)。

*_Value*<br/>
変換される数値。

*_Count*<br/>
格納する桁数。

*_Dec*<br/>
格納された小数点位置。

*_Sign*<br/>
変換後の数値の符号。

## <a name="return-value"></a>戻り値

正常終了した場合は 0 を返します。 障害が発生した場合、戻り値はエラー コードを示します。 エラー コードは、Errno.h で定義されています。 詳細については、「[errno、_doserrno、_sys_errlist、および _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)」を参照してください。

パラメーターが次の表の無効な値の場合は、「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、この関数は無効なパラメーター ハンドラーを呼び出します。 実行の継続が許可された場合、この関数は**errno**を**einval**に設定し、 **einval**を返します。

### <a name="error-conditions"></a>エラー条件

|*_Buffer*|*_SizeInBytes*|_Value|_Count|_Dec|_Sign|戻り値|*バッファー*内の値|
|---------------|--------------------|-------------|-------------|-----------|------------|------------------|-----------------------|
|**NULL**|any|any|any|any|any|**EINVAL**|変更されません。|
|Not **NULL** (有効なメモリを指す)|<=0|any|any|any|any|**EINVAL**|変更されません。|
|any|any|any|any|**NULL**|any|**EINVAL**|変更されません。|
|any|any|any|any|any|**NULL**|**EINVAL**|変更されません。|

## <a name="security-issues"></a>セキュリティの問題

*バッファー*が有効なメモリを指しておらず、が**NULL**でない場合、 **_ecvt_s**はアクセス違反を生成する可能性があります。

## <a name="remarks"></a>解説

**_Ecvt_s**関数は、浮動小数点数を文字列に変換します。 *_Value*パラメーターは、変換される浮動小数点数です。 この関数は、最大*数*の *_Value*を文字列として格納し、null 文字 (' \ 0 ') を追加します。 *_Value*の桁数が *_Count*を超える場合は、下位の桁が丸められます。 *Count*の桁数よりも小さい場合は、文字列に0が埋め込まれます。

文字列には数字だけが格納されます。 小数点の位置と *_Value*の符号は、 *_Dec*から取得し、呼び出しの後に *_Sign*できます。 *_Dec*パラメーターは、文字列の先頭に対する小数点の位置を示す整数値を指します。 0 または負の整数値は、最初の桁の左側に小数点があることを示します。 *_Sign*パラメーターは、変換後の数値の符号を示す整数を指します。 整数値が 0 の場合、数値は正の値です。 それ以外の場合、数値は負の値です。

長さ **_CVTBUFSIZE**のバッファーは、浮動小数点値に対して十分です。

**_Ecvt_s**と **_fcvt_s**の違いは、 *_Count*パラメーターの解釈です。 出力文字列の合計桁数として*カウント***を解釈する (_s****)。一方、** 小数点の後の桁数として *カウント*を解釈します。

C++ では、テンプレートのオーバーロードによってこの関数を簡単に使用できます。オーバーロードでは、バッファー長を自動的に推論できるため、サイズ引数を指定する必要がなくなります。 詳細については、「[セキュリティ保護されたテンプレート オーバーロード](../../c-runtime-library/secure-template-overloads.md)」を参照してください。

この関数のデバッグバージョンは、最初にバッファーを0xFE で埋めます。 この動作を無効にするには、[_CrtSetDebugFillThreshold](crtsetdebugfillthreshold.md) を使用します。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

## <a name="requirements"></a>必要条件

|機能|必須ヘッダー|オプション ヘッダー|
|--------------|---------------------|---------------------|
|**_ecvt_s**|\<stdlib.h>|\<errno.h>|

互換性について詳しくは、「 [Compatibility](../../c-runtime-library/compatibility.md)」をご覧ください。

## <a name="example"></a>例

```C
// ecvt_s.c
#include <stdio.h>
#include <stdlib.h>
#include <errno.h>

int main( )
{
    char * buf = 0;
    int decimal;
    int sign;
    int err;

    buf = (char*) malloc(_CVTBUFSIZE);
    err = _ecvt_s(buf, _CVTBUFSIZE, 1.2, 5, &decimal, &sign);

    if (err != 0)
    {
        printf("_ecvt_s failed with error code %d\n", err);
        exit(1);
    }

    printf("Converted value: %s\n", buf);
}
```

```Output
Converted value: 12000
```

## <a name="see-also"></a>関連項目

[データ変換](../../c-runtime-library/data-conversion.md)<br/>
[浮動小数点のサポート](../../c-runtime-library/floating-point-support.md)<br/>
[atof、_atof_l、_wtof、_wtof_l](atof-atof-l-wtof-wtof-l.md)<br/>
[_ecvt](ecvt.md)<br/>
[_fcvt_s](fcvt-s.md)<br/>
[_gcvt_s](gcvt-s.md)<br/>
