---
title: _stricmp、_wcsicmp、_mbsicmp、_stricmp_l、_wcsicmp_l、_mbsicmp_l
ms.date: 4/2/2020
api_name:
- _stricmp_l
- _mbsicmp
- _wcsicmp
- _mbsicmp_l
- _stricmp
- _wcsicmp_l
- _o__mbsicmp
- _o__mbsicmp_l
- _o__stricmp
- _o__stricmp_l
- _o__wcsicmp
- _o__wcsicmp_l
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
- ntoskrnl.exe
- ucrtbase.dll
- api-ms-win-crt-multibyte-l1-1-0.dll
- api-ms-win-crt-string-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _ftcsicmp
- _stricmp
- wcsicmp_l
- _wcsicmp
- _tcsicmp
- _strcmpi
- stricmp_l
- _mbsicmp
- _fstricmp
- mbsicmp_l
- mbsicmp
helpviewer_keywords:
- _wcsicmp function
- _stricmp_l function
- fstricmp function
- _tcsicmp function
- ftcsicmp function
- string comparison [C++], lowercase
- _wcsicmp_l function
- _fstricmp function
- strings [C++], comparing
- mbsicmp function
- _ftcsicmp function
- _mbsicmp_l function
- wcsicmp_l function
- _stricmp function
- _mbsicmp function
- tcsicmp function
- stricmp_l function
- mbsicmp_l function
- _strcmpi function
ms.assetid: 0e1ee515-0d75-435a-a445-8875d4669b50
ms.openlocfilehash: 786c2bd2738bb82b3edac5c811ccfd3f9f8bc854
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82920010"
---
# <a name="_stricmp-_wcsicmp-_mbsicmp-_stricmp_l-_wcsicmp_l-_mbsicmp_l"></a>_stricmp、_wcsicmp、_mbsicmp、_stricmp_l、_wcsicmp_l、_mbsicmp_l

文字列の大文字と小文字を区別しない比較を実行します。

> [!IMPORTANT]
> **_mbsicmp**と **_mbsicmp_l**は、Windows ランタイムで実行されるアプリケーションでは使用できません。 詳細については、「[ユニバーサル Windows プラットフォーム アプリでサポートされていない CRT 関数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)」を参照してください。

## <a name="syntax"></a>構文

```C
int _stricmp(
   const char *string1,
   const char *string2
);
int _wcsicmp(
   const wchar_t *string1,
   const wchar_t *string2
);
int _mbsicmp(
   const unsigned char *string1,
   const unsigned char *string2
);
int _stricmp_l(
   const char *string1,
   const char *string2,
   _locale_t locale
);
int _wcsicmp_l(
   const wchar_t *string1,
   const wchar_t *string2,
   _locale_t locale
);
int _mbsicmp_l(
   const unsigned char *string1,
   const unsigned char *string2,
   _locale_t locale
);
```

### <a name="parameters"></a>パラメーター

*string1*、 *string2*<br/>
Null で終わる比較対象の文字列。

*locale*<br/>
使用するロケール。

## <a name="return-value"></a>戻り値

戻り値は、次のように*string1*と*string2*の関係を示します。

|戻り値|説明|
|------------------|-----------------|
|< 0|*string1*が*string2*未満|
|0|*string1*と*string2*の同一|
|> 0|*string1*が*string2*より大きい|

エラーが発生した場合、 **_mbsicmp**は **_NLSCMPERROR**を返し\<ます。これは、 \<.h> および mbstring.h> で定義されています。

## <a name="remarks"></a>解説

**_Stricmp**関数は、各文字を小文字に変換した後に*string1*と*string2*を比較し、その関係を示す値を返します。 **_stricmp**は **_stricoll**とは異なります。 **_stricmp**の比較は**LC_CTYPE**によってのみ影響を受け、どの文字が大文字か小文字かを決定します。 **_Stricoll**関数は、ロケールの**LC_CTYPE**と**LC_COLLATE**の両方のカテゴリに従って文字列を比較します。これには、大文字と小文字の順序と照合順序の両方が含まれます。 **LC_COLLATE**カテゴリの詳細については、「 [setlocale](setlocale-wsetlocale.md)と[ロケールのカテゴリ](../../c-runtime-library/locale-categories.md)」を参照してください。 **_L**サフィックスが付いていないこれらの関数のバージョンでは、ロケールに依存する動作に現在のロケールを使用します。 サフィックスが付いているバージョンは、代わりに渡されたロケールを使用する点を除き、同じです。 ロケールが設定されていない場合は、C ロケールが使用されます。 詳細については、「 [Locale](../../c-runtime-library/locale.md)」を参照してください。

> [!NOTE]
> **_stricmp**は **_strcmpi**と同じです。 これらは同じように使用できますが、 **_stricmp**は優先される標準です。

**_Strcmpi**関数は **_stricmp**と同じであり、旧バージョンとの互換性のためだけに用意されています。

**_Stricmp**では小文字の比較が行われるため、予期しない動作が発生する可能性があります。

**_Stricmp**による大文字と小文字の変換が比較の結果に与える影響を示すために、2つの文字列が JOHN_HENRY になっているとします。 "_" の ASCII 値は小文字の S よりも小さいので、JOHN_HENRY は JOHNSTON よりも小さいとみなされます。実際、91 ～ 96 の ASCII 値を持つ文字はすべて、他の文字よりも小さいと判断されます。

**_Stricmp**の代わりに[strcmp](strcmp-wcscmp-mbscmp.md)関数を使用した場合、JOHN_HENRY はジョンストンよりも大きくなります。

**_wcsicmp**と **_mbsicmp**は **_stricmp**のワイド文字バージョンとマルチバイト文字バージョンです。 **_Wcsicmp**の引数と戻り値はワイド文字列です。これらの **_mbsicmp**はマルチバイト文字列です。 **_mbsicmp**は、現在のマルチバイトコードページに従ってマルチバイト文字のシーケンスを認識し、エラーが発生した場合に **_NLSCMPERROR**を返します。 詳細については、「[コード ページ](../../c-runtime-library/code-pages.md)」を参照してください。 それ以外では、これらの関数の動作は同じです。

**_wcsicmp**と**wcscmp**の動作は同じですが、 **wcscmp**では、引数を比較する前に小文字に変換しない点が異なります。 **_mbsicmp**と **_mbscmp**の動作は同じですが、 **_mbscmp**では、引数を比較する前に小文字に変換しない点が異なります。

Latin 1 文字を使用するには、 **_wcsicmp**に[setlocale](setlocale-wsetlocale.md)を呼び出す必要があります。 既定では、C ロケールが有効になっているので、たとえば、ä は Ä と等しいと見なされません。 **_Wcsicmp**の呼び出しの前に、C ロケール以外のロケールで**setlocale**を呼び出します。 次の例では **_wcsicmp**がロケールに依存しているかどうかを示します。

```C
// crt_stricmp_locale.c
By default, this function's global state is scoped to the application. To change this, see [Global state in the CRT](../global-state.md).

#include <string.h>
#include <stdio.h>
#include <locale.h>

int main() {
   setlocale(LC_ALL,"C");   // in effect by default
   printf("\n%d",_wcsicmp(L"ä", L"Ä"));   // compare fails
   setlocale(LC_ALL,"");
   printf("\n%d",_wcsicmp(L"ä", L"Ä"));   // compare succeeds
}
```

別の方法として[、_create_locale _wcreate_locale を呼び出し、](create-locale-wcreate-locale.md)返されたロケールオブジェクトをパラメーターとして **_wcsicmp_l**に渡す方法があります。

これらのすべての関数では、パラメーターの検証が行われます。 *String1*または*string2*が null ポインターの場合は、「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、無効なパラメーターハンドラーが呼び出されます。 実行の継続が許可された場合、これらの関数は **_NLSCMPERROR**を返し、 **errno**を**EINVAL**に設定します。

### <a name="generic-text-routine-mappings"></a>汎用テキスト ルーチンのマップ

|TCHAR.H のルーチン|_UNICODE および _MBCS が未定義の場合|_MBCS が定義されている場合|_UNICODE が定義されている場合|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tcsicmp**|**_stricmp**|**_mbsicmp**|**_wcsicmp**|

## <a name="requirements"></a>必要条件

|ルーチン|必須ヘッダー|
|-------------|---------------------|
|**_stricmp**、 **_stricmp_l**|\<string.h>|
|**_wcsicmp**、 **_wcsicmp_l**|\<string.h> または \<wchar.h>|
|**_mbsicmp**、 **_mbsicmp_l**|\<mbstring.h>|

互換性の詳細については、「[互換性](../../c-runtime-library/compatibility.md)」を参照してください。

## <a name="example"></a>例

```C
// crt_stricmp.c

#include <string.h>
#include <stdio.h>
#include <stdlib.h>

char string1[] = "The quick brown dog jumps over the lazy fox";
char string2[] = "The QUICK brown dog jumps over the lazy fox";

int main( void )
{
   char tmp[20];
   int result;

   // Case sensitive
   printf( "Compare strings:\n   %s\n   %s\n\n", string1, string2 );
   result = strcmp( string1, string2 );
   if( result > 0 )
      strcpy_s( tmp, _countof(tmp), "greater than" );
   else if( result < 0 )
      strcpy_s( tmp, _countof(tmp), "less than" );
   else
      strcpy_s( tmp, _countof(tmp), "equal to" );
   printf( "   strcmp:   String 1 is %s string 2\n", tmp );

   // Case insensitive (could use equivalent _stricmp)
   result = _stricmp( string1, string2 );
   if( result > 0 )
      strcpy_s( tmp, _countof(tmp), "greater than" );
   else if( result < 0 )
      strcpy_s( tmp, _countof(tmp), "less than" );
   else
      strcpy_s( tmp, _countof(tmp), "equal to" );
   printf( "   _stricmp:  String 1 is %s string 2\n", tmp );
}
```

```Output
Compare strings:
   The quick brown dog jumps over the lazy fox
   The QUICK brown dog jumps over the lazy fox

   strcmp:   String 1 is greater than string 2
   _stricmp:  String 1 is equal to string 2
```

## <a name="see-also"></a>関連項目

[文字列操作](../../c-runtime-library/string-manipulation-crt.md)<br/>
[memcmp、wmemcmp](memcmp-wmemcmp.md)<br/>
[_memicmp、_memicmp_l](memicmp-memicmp-l.md)<br/>
[strcmp、wcscmp、_mbscmp](strcmp-wcscmp-mbscmp.md)<br/>
[strcoll 系関数](../../c-runtime-library/strcoll-functions.md)<br/>
[strncmp、wcsncmp、_mbsncmp、_mbsncmp_l](strncmp-wcsncmp-mbsncmp-mbsncmp-l.md)<br/>
[_strnicmp、_wcsnicmp、_mbsnicmp、_strnicmp_l、_wcsnicmp_l、_mbsnicmp_l](strnicmp-wcsnicmp-mbsnicmp-strnicmp-l-wcsnicmp-l-mbsnicmp-l.md)<br/>
[strrchr、wcsrchr、_mbsrchr、_mbsrchr_l](strrchr-wcsrchr-mbsrchr-mbsrchr-l.md)<br/>
[_strset、_strset_l、_wcsset、_wcsset_l、_mbsset、_mbsset_l](strset-strset-l-wcsset-wcsset-l-mbsset-mbsset-l.md)<br/>
[strspn、wcsspn、_mbsspn、_mbsspn_l](strspn-wcsspn-mbsspn-mbsspn-l.md)<br/>
