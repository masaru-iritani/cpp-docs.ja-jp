---
title: snprintf、_snprintf、_snprintf_l、_snwprintf、_snwprintf_l
description: 書式設定されたデータを文字列に書き込む snprintf、_snprintf、_snprintf_l、_snwprintf、 _snwprintf_の API リファレンスです。
ms.date: 08/27/2020
api_name:
- _snwprintf
- _snprintf
- _snprintf_l
- _snwprintf_l
- snprintf
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
- ntoskrnl.exe
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _snprintf
- snprintf_l
- snwprintf_l
- sntprintf
- snprintf
- _sntprintf
- _sntprintf_l
- sntprintf_l
- snwprintf
- _snprintf_l
- _snwprintf
- _snwprintf_l
helpviewer_keywords:
- snwprintf_l function
- sntprintf_l function
- snprintf_l function
- _snwprintf_l function
- _sntprintf_l function
- _snwprintf function
- _snprintf function
- _sntprintf function
- _snprintf_l function
- snwprintf function
- snprintf function
- sntprintf function
- formatted text [C++]
ms.assetid: 5976c9c8-876e-4ac9-a515-39f3f7fd0925
ms.openlocfilehash: b4d8865d5297afe3d48f2bb48cc85a0d10535dfd
ms.sourcegitcommit: c8f1605354724a13566bc3b0fac3c5d98265f1d0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062199"
---
# <a name="snprintf-_snprintf-_snprintf_l-_snwprintf-_snwprintf_l"></a>snprintf、_snprintf、_snprintf_l、_snwprintf、_snwprintf_l

文字列に書式付きデータを書き込みます。 これらの関数のセキュリティを強化したバージョンを使用できます。「 [_snprintf_s, _snprintf_s_l, _snwprintf_s, _snwprintf_s_l](snprintf-s-snprintf-s-l-snwprintf-s-snwprintf-s-l.md)」をご覧ください。

## <a name="syntax"></a>構文

```C
int snprintf(
   char *buffer,
   size_t count,
   const char *format [,
   argument] ...
);
int _snprintf(
   char *buffer,
   size_t count,
   const char *format [,
   argument] ...
);
int _snprintf_l(
   char *buffer,
   size_t count,
   const char *format,
   locale_t locale [,
   argument] ...
);
int _snwprintf(
   wchar_t *buffer,
   size_t count,
   const wchar_t *format [,
   argument] ...
);
int _snwprintf_l(
   wchar_t *buffer,
   size_t count,
   const wchar_t *format,
   locale_t locale [,
   argument] ...
);
template <size_t size>
int _snprintf(
   char (&buffer)[size],
   size_t count,
   const char *format [,
   argument] ...
); // C++ only
template <size_t size>
int _snprintf_l(
   char (&buffer)[size],
   size_t count,
   const char *format,
   locale_t locale [,
   argument] ...
); // C++ only
template <size_t size>
int _snwprintf(
   wchar_t (&buffer)[size],
   size_t count,
   const wchar_t *format [,
   argument] ...
); // C++ only
template <size_t size>
int _snwprintf_l(
   wchar_t (&buffer)[size],
   size_t count,
   const wchar_t *format,
   locale_t locale [,
   argument] ...
); // C++ only
```

### <a name="parameters"></a>パラメーター

*格納*<br/>
出力の格納場所。

*count*<br/>
格納する最大文字数。

*format*<br/>
書式指定文字列。

*argument*<br/>
省略可能な引数。

*locale*<br/>
使用するロケール。

詳細については、「[書式指定構文: printf 関数と wprintf 関数](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md)」をご覧ください。

## <a name="return-value"></a>戻り値

**Len**には、書式設定されたデータ文字列の長さを指定します。終端の null は含まれません。 **Len**と**count**は、 **snprintf**と **_snprintf**の文字数と **_snwprintf**のワイド文字数です。

すべての関数について、 **len**  <  *count*の場合は**len**文字が*バッファー*に格納され、null 終端記号が追加され、 **len**が返されます。

**Snprintf**関数は、 **len**が*count*以上の場合に、null 終端記号をに配置することによって、出力を切り捨て `buffer[count-1]` ます。 返される値は **len**で、 *count* が十分に大きい場合に出力された文字数です。 **Snprintf**関数は、エンコードエラーが発生した場合に負の値を返します。

**Snprintf**以外のすべての関数について、 **len**  =  *count*の場合**は len**文字が*バッファー*に格納され、null 終端文字は追加されず、 **len**が返されます。 **Len**  >  *count*、 *count*文字が*buffer*に格納されている場合、null 終端記号は追加されず、負の値が返されます。

*Buffer*が null ポインターで、 *count*が0の場合、出力の書式を設定するために必要な文字数として**len**が返されます。終端の null は含まれません。 同じ *引数* と *ロケール* のパラメーターを使用して呼び出しを成功させるには、少なくとも **len** + 1 文字を保持するバッファーを割り当てます。

*Buffer*が null ポインターで、 *count*が0以外の場合、または*format*が null ポインターの場合は、「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、無効なパラメーターハンドラーが呼び出されます。 実行の継続が許可された場合、これらの関数は-1 を返し、 **errno** を **EINVAL**に設定します。

エラー コードの詳細については、「[errno、_doserrno、_sys_errlist、および _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)」を参照してください。

## <a name="remarks"></a>注釈

**Snprintf**関数と関数の **_snprintf**ファミリでは、*バッファー*内の文字*数*を書式指定して格納します。 **Snprintf**関数は、常に終端の null 文字を格納し、必要に応じて出力を切り捨てます。 **_Snprintf**ファミリの関数は、書式設定された文字列の長さが厳密に*カウント*文字未満の場合にのみ、終端の null 文字を追加します。 各 *引数* (存在する場合) は変換され、 *形式*の対応する書式指定に従って出力されます。 形式は通常の文字で構成され、 [printf](printf-printf-l-wprintf-wprintf-l.md)の*format*引数と同じ形式と機能を持ちます。 重なり合う文字列間でコピーした場合の動作は未定義です。

> [!IMPORTANT]
> *format* にユーザー定義の文字列を指定しないでください。 **_Snprintf**関数は null 終端処理を保証しないため (特に戻り値が*count*の場合)、null 終端文字を追加するコードが続くことを確認してください。 詳しくは、「 [バッファー オーバーランの回避](/windows/win32/SecBP/avoiding-buffer-overruns)」をご覧ください。

Visual Studio 2015 と Windows 10 の UCRT 以降、 **snprintf** は **_snprintf**と同じではなくなりました。 **Snprintf**関数の動作は、C99 標準に準拠するようになりました。

**_snwprintf** は **_snprintf**のワイド文字バージョンです。 **_snwprintf** するポインター引数はワイド文字列です。 **_Snwprintf**でのエンコードエラーの検出は、 **_snprintf**とは異なる場合があります。 **_snwprintf**は、 **swprintf**と同様に、出力を型 **ファイル**の出力先ではなく文字列に書き込みます。

**_L**サフィックスを持つこれらの関数のバージョンは、現在のスレッドロケールの代わりに渡されたロケールパラメーターを使用する点を除いて同じです。

C++ では、これらの関数にテンプレートのオーバーロードがあります。このオーバーロードは、より安全な新しいバージョンを呼び出します。 詳細については、「[セキュリティ保護されたテンプレート オーバーロード](../../c-runtime-library/secure-template-overloads.md)」を参照してください。

### <a name="generic-text-routine-mappings"></a>汎用テキスト ルーチンのマップ

|Tchar.h のルーチン|_UNICODE および _MBCS が未定義の場合|_MBCS が定義されている場合|_UNICODE が定義されている場合|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_sntprintf**|**_snprintf**|**_snprintf**|**_snwprintf**|
|**_sntprintf_l**|**_snprintf_l**|**_snprintf_l**|**_snwprintf_l**|

## <a name="requirements"></a>必要条件

|ルーチンによって返される値|必須ヘッダー|
|-------------|---------------------|
|**snprintf**、 **_snprintf**、  **_snprintf_l**|\<stdio.h>|
|**_snwprintf**、 **_snwprintf_l**|\<stdio.h> または \<wchar.h>|

互換性について詳しくは、「 [Compatibility](../../c-runtime-library/compatibility.md)」をご覧ください。

## <a name="example"></a>例

```C
// crt_snprintf.c
// compile with: /W3
#include <stdio.h>
#include <stdlib.h>

#if !defined(__cplusplus)
typedef int bool;
const bool true = 1;
const bool false = 0;
#endif

#define FAIL 0 // change to 1 and see what happens

int main(void)
{
   char buffer[200];
   const static char s[] = "computer"
#if FAIL
"computercomputercomputercomputercomputercomputercomputercomputer"
"computercomputercomputercomputercomputercomputercomputercomputer"
"computercomputercomputercomputercomputercomputercomputercomputer"
"computercomputercomputercomputercomputercomputercomputercomputer"
#endif
   ;
   const char c = 'l';
   const int i = 35;
#if FAIL
   const double fp = 1e300; // doesn't fit in the buffer
#else
   const double fp = 1.7320534;
#endif
   /* !subtract one to prevent "squeezing out" the terminal null! */
   const int bufferSize = sizeof(buffer)/sizeof(buffer[0]) - 1;
   int bufferUsed = 0;
   int bufferLeft = bufferSize - bufferUsed;
   bool bSuccess = true;
   buffer[0] = 0;

   /* Format and print various data: */

   if (bufferLeft > 0)
   {
      int perElementBufferUsed = _snprintf(&buffer[bufferUsed],
      bufferLeft, "   String: %s\n", s ); // C4996
      // Note: _snprintf is deprecated; consider _snprintf_s instead
      if (bSuccess = (perElementBufferUsed >= 0))
      {
         bufferUsed += perElementBufferUsed;
         bufferLeft -= perElementBufferUsed;
         if (bufferLeft > 0)
         {
            int perElementBufferUsed = _snprintf(&buffer[bufferUsed],
            bufferLeft, "   Character: %c\n", c ); // C4996
            if (bSuccess = (perElementBufferUsed >= 0))
            {
               bufferUsed += perElementBufferUsed;
               bufferLeft -= perElementBufferUsed;
               if (bufferLeft > 0)
               {
                  int perElementBufferUsed = _snprintf(&buffer
                  [bufferUsed], bufferLeft, "   Integer: %d\n", i ); // C4996
                  if (bSuccess = (perElementBufferUsed >= 0))
                  {
                     bufferUsed += perElementBufferUsed;
                     bufferLeft -= perElementBufferUsed;
                     if (bufferLeft > 0)
                     {
                        int perElementBufferUsed = _snprintf(&buffer
                        [bufferUsed], bufferLeft, "   Real: %f\n", fp ); // C4996
                        if (bSuccess = (perElementBufferUsed >= 0))
                        {
                           bufferUsed += perElementBufferUsed;
                        }
                     }
                  }
               }
            }
         }
      }
   }

   if (!bSuccess)
   {
      printf("%s\n", "failure");
   }
   else
   {
      /* !store null because _snprintf doesn't necessarily (if the string
       * fits without the terminal null, but not with it)!
       * bufferUsed might be as large as bufferSize, which normally is
       * like going one element beyond a buffer, but in this case
       * subtracted one from bufferSize, so we're ok.
       */
      buffer[bufferUsed] = 0;
      printf( "Output:\n%s\ncharacter count = %d\n", buffer, bufferUsed );
   }
   return EXIT_SUCCESS;
}
```

```Output
Output:
   String: computer
   Character: l
   Integer: 35
   Real: 1.732053

character count = 69
```

## <a name="see-also"></a>関連項目

[ストリーム入出力](../../c-runtime-library/stream-i-o.md)<br/>
[sprintf、_sprintf_l、swprintf、_swprintf_l、 \_ _swprintf_l](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[fprintf、_fprintf_l、fwprintf、_fwprintf_l](fprintf-fprintf-l-fwprintf-fwprintf-l.md)<br/>
[printf、_printf_l、wprintf、_wprintf_l](printf-printf-l-wprintf-wprintf-l.md)<br/>
[scanf、_scanf_l、wscanf、_wscanf_l](scanf-scanf-l-wscanf-wscanf-l.md)<br/>
[sscanf、_sscanf_l、swscanf、_swscanf_l](sscanf-sscanf-l-swscanf-swscanf-l.md)<br/>
[vprintf 関数](../../c-runtime-library/vprintf-functions.md)<br/>
