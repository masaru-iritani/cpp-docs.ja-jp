---
title: 診断サービス
ms.date: 11/04/2016
helpviewer_keywords:
- diagnosi [MFC]s, diagnostic services
- diagnostic macros [MFC], list of general MFC
- services [MFC], diagnostic
- MFC, diagnostic services
- general diagnostic functions and variables [MFC]
- diagnostics [MFC], diagnostic functions and variables
- diagnostics [MFC], list of general MFC
- diagnosis [MFC], diagnostic functions and variables
- diagnosis [MFC], list of general MFC
- general diagnostic macros in MFC
- diagnostic macros [MFC]
- diagnostic services [MFC]
- object diagnostic functions in MFC
- diagnostics [MFC], diagnostic services
- diagnostic functions and variables [MFC]
ms.assetid: 8d78454f-9fae-49c2-88c9-d3fabd5393e8
ms.openlocfilehash: 931545e6a79ecaa59d147e48265649ef20466fbd
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88837399"
---
# <a name="diagnostic-services"></a>診断サービス

Microsoft Foundation Class ライブラりは、プログラムのデバッグをより簡単にする多くの診断サービスを提供します。 これらの診断サービスには、プログラムのメモリー割り当てを追跡したり、実行時にオブジェクトの内容をダンプしたり、実行時にデバッグ メッセージを表示したりできるようにするマクロやグローバル関数が含まれます。 診断サービスのマクロとグローバル関数は、次のカテゴリに分類されます。

- 汎用診断マクロ

- 汎用診断関数と変数

- オブジェクト診断関数

これらのマクロと関数は、MFC のデバッグ バージョンとリリース バージョンの `CObject` から派生するすべてのクラスで使用できます。 ただし、DEBUG_NEW と検証を除くすべてのバージョンでは、リリースバージョンでは何も実行されません。

デバッグ ライブラリ内の割り当てられるすべてのメモリ ブロックは、一連の "ガード バイト" で囲まれます。 これらのバイトが間違ったメモリ書き込みによって乱される場合、診断ルーチンが問題を報告できます。 行:

[!code-cpp[NVC_MFCCObjectSample#14](../../mfc/codesnippet/cpp/diagnostic-services_1.cpp)]

実装ファイルでは、のすべての呼び出しに、 **`new`** メモリの割り当てが行われたときのファイル名と行番号が格納されます。 関数 [CMemoryState::D umpallobjectssince](cmemorystate-structure.md#dumpallobjectssince) は、この追加情報を表示し、メモリリークを識別できるようにします。 診断出力の追加情報については、クラス [CDumpContext](../../mfc/reference/cdumpcontext-class.md) も参照してください。

さらに、C ランタイム ライブラリは、アプリケーションのデバッグに使用できる診断関数のセットもサポートしています。 詳細については、「ランタイムライブラリリファレンス」の「 [デバッグルーチン](../../c-runtime-library/debug-routines.md) 」を参照してください。

### <a name="mfc-general-diagnostic-macros"></a>MFC 汎用診断マクロ

|名前|説明|
|-|-|
|[アサート](#assert)|ライブラリのデバッグ バージョンで、指定された式が FALSE に評価された場合、メッセージを出力し、プログラムを中止します。|
|[ASSERT_KINDOF](#assert_kindof)|オブジェクトが、指定されたクラスのオブジェクト、または指定されたクラスから派生したクラスのオブジェクトであることをテストします。|
|[ASSERT_VALID](#assert_valid)|その `AssertValid` メンバー関数 (通常は `CObject`からオーバーライドされる) を呼び出すことにより、オブジェクトの内部の有効性をテストします。|
|[DEBUG_NEW](#debug_new)|デバッグ モードのすべてのオブジェクト割り当てにファイル名と行番号を指定します。これは、メモリー リークを見つけるのに役立ちます。|
|[DEBUG_ONLY](#debug_only)|ASSERT に類似していますが、式の値のテストは行いません。デバッグ モードでのみ実行されるコードで役立ちます。|
|[と ENSURE_VALID を確認する](#ensure)|データの正確性を検証するために使用します。|
|[THIS_FILE](#this_file)|は、コンパイルするファイルの名前に展開されます。|
|[トレース](#trace)|ライブラリのデバッグ バージョンで `printf`に類似した機能を提供します。|
|[か](#verify)|ASSERT と類似していますが、ライブラリのリリース バージョンとデバッグ バージョンで式を評価します。|

### <a name="mfc-general-diagnostic-variables-and-functions"></a>MFC 汎用診断関数と変数

|名前|説明|
|-|-|
|[afxDump](#afxdump)|デバッガーの出力ウィンドウまたはデバッグ端末に [CDumpContext](../../mfc/reference/cdumpcontext-class.md) 情報を送信するグローバル変数。|
|[afxMemDF](#afxmemdf)|デバッグ メモリ アロケーターの動作を制御するグローバル変数。|
|[AfxCheckError](#afxcheckerror)|エラーかどうかを確認するため、そしてもしエラーであれば、適切なエラーをスローするために、渡される SCODE のテストに使用するグローバル変数。|
|[AfxCheckMemory](#afxcheckmemory)|現在割り当てられているすべてのメモリの整合性を確認します。|
|[AfxDebugBreak](#afxdebugbreak)|実行の中断を発生させます。|
|[afxDump](#cdumpcontext_in_mfc)|デバッガーにある間に呼び出さると、デバッグ中にオブジェクトの状態をダンプします。|
|[afxDump](#afxdump)|デバッグ中にオブジェクトの状態をダンプする内部関数。|
|[AfxDumpStack](#afxdumpstack)|現在のスタックのイメージを生成します。 この関数は、常に、静的にリンクされます。|
|[AfxEnableMemoryLeakDump](#afxenablememoryleakdump)|メモリ リーク ダンプを有効にします。|
|[AfxEnableMemoryTracking](#afxenablememorytracking)|メモリのトラッキングをオンまたはオフにします。|
|[AfxIsMemoryBlock](#afxismemoryblock)|メモリ ブロックが正しく割り当てられていることを確認します。|
|[AfxIsValidAddress](#afxisvalidaddress)|メモリ アドレスの範囲がプログラムの境界内にあることを確認します。|
|[AfxIsValidString](#afxisvalidstring)|文字列へのポインターが有効かどうかを判断します。|
|[AfxSetAllocHook](#afxsetallochook)|各メモリ割り振りでの関数の呼び出しを有効にします。|

### <a name="mfc-object-diagnostic-functions"></a>MFC オブジェクト診断関数

|名前|説明|
|-|-|
|[AfxDoForAllClasses](#afxdoforallclasses)|ランタイム型チェックをサポートする `CObject`から派生したすべてのクラスで、指定された関数を実行します。|
|[AfxDoForAllObjects](#afxdoforallobjects)|で割り当てられたすべてのから派生したオブジェクトに対して、指定された関数を実行 `CObject` **`new`** します。|

### <a name="mfc-compilation-macros"></a>MFC コンパイルマクロ

|名前|説明|
|-|-|
|[_AFX_SECURE_NO_WARNINGS](#afx_secure_no_warnings)|非推奨の MFC 関数の使用について、コンパイラの警告を表示しません。|

## <a name="_afx_secure_no_warnings"></a><a name="afx_secure_no_warnings"></a> _AFX_SECURE_NO_WARNINGS

非推奨の MFC 関数の使用について、コンパイラの警告を表示しません。

### <a name="syntax"></a>構文

```
_AFX_SECURE_NO_WARNINGS
```

### <a name="example"></a>例

このコードサンプルでは、_AFX_SECURE_NO_WARNINGS が定義されていない場合、コンパイラの警告が発生します。

```cpp
// define this before including any afx files in *pch.h* (*stdafx.h* in Visual Studio 2017 and earlier)
#define _AFX_SECURE_NO_WARNINGS
```

```cpp
CRichEditCtrl* pRichEdit = new CRichEditCtrl;
pRichEdit->Create(WS_CHILD|WS_VISIBLE|WS_BORDER|ES_MULTILINE,
   CRect(10,10,100,200), pParentWnd, 1);
char sz[256];
pRichEdit->GetSelText(sz);
```

## <a name="afxdebugbreak"></a><a name="afxdebugbreak"></a> AfxDebugBreak

この関数を呼び出すと、 `AfxDebugBreak` MFC アプリケーションのデバッグバージョンの実行中に、(への呼び出しの位置で) 中断が発生します。

### <a name="syntax"></a>構文

```cpp
void AfxDebugBreak( );
```

### <a name="remarks"></a>解説

`AfxDebugBreak` MFC アプリケーションのリリースバージョンには影響しないため、削除する必要があります。 この関数は、MFC アプリケーションでのみ使用してください。 Win32 API バージョンのを使用して、 `DebugBreak` 非 MFC アプリケーションで中断を発生させます。

### <a name="requirements"></a>必要条件

**ヘッダー:** afxver_

## <a name="assert"></a><a name="assert"></a> アサート

引数を評価します。

```
ASSERT(booleanExpression)
```

### <a name="parameters"></a>パラメーター

*booleanExpression*<br/>
0以外または0に評価される式 (ポインター値を含む) を指定します。

### <a name="remarks"></a>解説

結果が0の場合、マクロは診断メッセージを出力し、プログラムを中止します。 条件が0以外の場合は、何も実行されません。

診断メッセージにフォームがあります

`assertion failed in file <name> in line <num>`

ここで、 *name* はソースファイルの名前、 *num* はソースファイルで失敗したアサーションの行番号です。

MFC のリリースバージョンでは、ASSERT は式を評価しないため、プログラムは中断されません。 環境に関係なく式を評価する必要がある場合は、ASSERT の代わりに VERIFY マクロを使用します。

> [!NOTE]
> この関数は、MFC のデバッグバージョンでのみ使用できます。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#44](../../mfc/codesnippet/cpp/diagnostic-services_2.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="assert_kindof"></a><a name="assert_kindof"></a> ASSERT_KINDOF

このマクロは、ポインターが指すオブジェクトが、指定されたクラスのオブジェクトであるか、または指定されたクラスから派生したクラスのオブジェクトであることをアサートします。

```
ASSERT_KINDOF(classname, pobject)
```

### <a name="parameters"></a>パラメーター

*classname*<br/>
派生クラスの名前 `CObject` 。

*pobject*<br/>
クラスオブジェクトへのポインター。

### <a name="remarks"></a>解説

*Pobject*パラメーターは、オブジェクトへのポインターである必要があり、にすることができ **`const`** ます。 が指すオブジェクトとクラスは、ランタイムクラス情報をサポートする必要があり `CObject` ます。 たとえば、 `pDocument` が `CMyDoc` クラスまたはその派生クラスのオブジェクトへのポインターであることを確認するには、次のコードを記述します。

[!code-cpp[NVC_MFCDocView#194](../../mfc/codesnippet/cpp/diagnostic-services_3.cpp)]

マクロの使用 `ASSERT_KINDOF` は、コーディングとまったく同じです。

[!code-cpp[NVC_MFCDocView#195](../../mfc/codesnippet/cpp/diagnostic-services_4.cpp)]

この関数は、[DECLARE_DYNAMIC] (実行時-declare_dynamic または [DECLARE_SERIAL](run-time-object-model-services.md#declare_serial) マクロで宣言されたクラスに対してのみ機能します。

> [!NOTE]
> この関数は、MFC のデバッグバージョンでのみ使用できます。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="assert_valid"></a><a name="assert_valid"></a> ASSERT_VALID

オブジェクトの内部状態の有効性について想定をテストするには、を使用します。

```
ASSERT_VALID(pObject)
```

### <a name="parameters"></a>パラメーター

*pObject*<br/>
`CObject`メンバー関数のオーバーライドバージョンを持つから派生したクラスのオブジェクトを指定し `AssertValid` ます。

### <a name="remarks"></a>解説

ASSERT_VALID は、 `AssertValid` 引数として渡されたオブジェクトのメンバー関数を呼び出します。

MFC のリリースバージョンでは、ASSERT_VALID は何も行いません。 デバッグバージョンでは、ポインターが検証され、NULL がチェックされ、オブジェクト自体の `AssertValid` メンバー関数が呼び出されます。 これらのテストのいずれかが失敗した場合は、 [アサート](#assert)と同じ方法で警告メッセージが表示されます。

> [!NOTE]
> この関数は、MFC のデバッグバージョンでのみ使用できます。

詳細と例については、「 [MFC アプリケーションのデバッグ](/visualstudio/debugger/mfc-debugging-techniques)」を参照してください。

### <a name="example"></a>例

[!code-cpp[NVC_MFCCObjectSample#19](../../mfc/codesnippet/cpp/diagnostic-services_5.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="debug_new"></a><a name="debug_new"></a> DEBUG_NEW

メモリリークの検出を支援します。

```
#define  new DEBUG_NEW
```

### <a name="remarks"></a>解説

プログラム内のすべての場所で DEBUG_NEW を使用すると、通常は演算子を使用して **`new`** ヒープストレージを割り当てることができます。

デバッグモード ( **_DEBUG** シンボルが定義されている場合) では、DEBUG_NEW は、割り当てられた各オブジェクトのファイル名と行番号を追跡します。 次に、 [CMemoryState::D umpallobjectssince](cmemorystate-structure.md#dumpallobjectssince) メンバー関数を使用すると、DEBUG_NEW で割り当てられた各オブジェクトが、割り当てられたファイル名と行番号と共に表示されます。

DEBUG_NEW を使用するには、ソースファイルに次のディレクティブを挿入します。

[!code-cpp[NVC_MFCCObjectSample#14](../../mfc/codesnippet/cpp/diagnostic-services_1.cpp)]

このディレクティブを挿入すると、プリプロセッサによって DEBUG_NEW が挿入され **`new`** ます。 プログラムのリリースバージョンをコンパイルすると、DEBUG_NEW は単純な操作に解決され、 **`new`** ファイル名と行番号の情報は生成されません。

> [!NOTE]
> 以前のバージョンの MFC (4.1 およびそれ以前) で `#define` は、IMPLEMENT_DYNCREATE または IMPLEMENT_SERIAL マクロを呼び出したすべてのステートメントの後にステートメントを配置する必要がありました。 これはもう不要です。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="debug_only"></a><a name="debug_only"></a> DEBUG_ONLY

デバッグモード ( **_DEBUG** シンボルが定義されている場合) では、DEBUG_ONLY はその引数を評価します。

```
DEBUG_ONLY(expression)
```

### <a name="remarks"></a>解説

リリースビルドでは、DEBUG_ONLY はその引数を評価しません。 これは、デバッグビルドでのみ実行する必要があるコードがある場合に便利です。

DEBUG_ONLY マクロは、and で囲んでいる *式* と同じです `#ifdef _DEBUG` `#endif` 。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#32](../../mfc/codesnippet/cpp/diagnostic-services_6.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

### <a name="ensure-and-ensure_valid"></a><a name="ensure"></a> と ENSURE_VALID を確認する

データの正確性を検証するために使用します。

### <a name="syntax"></a>構文

```
ENSURE(  booleanExpression )
ENSURE_VALID( booleanExpression  )
```

### <a name="parameters"></a>パラメーター

*booleanExpression*<br/>
テストするブール式を指定します。

### <a name="remarks"></a>解説

これらのマクロの目的は、パラメーターの検証を強化することです。 マクロを使用すると、コード内の不適切なパラメーターをさらに処理できなくなります。 ASSERT マクロとは異なり、マクロはアサーションの生成に加えて例外をスローします。

マクロは、プロジェクトの構成に従って2つの方法で動作します。 マクロは ASSERT を呼び出し、アサーションが失敗した場合は例外をスローします。 したがって、デバッグ構成 (_DEBUG が定義されている場合) では、リリース構成でマクロがアサーションと例外を生成するのに対し、マクロは例外のみを生成します (ASSERT はリリース構成の式を評価しません)。

マクロ ENSURE_ARG は、確実にマクロとして機能します。

ENSURE_VALID は ASSERT_VALID マクロ (デバッグビルドでのみ効果がある) を呼び出します。 また、ポインターが NULL の場合、ENSURE_VALID は例外をスローします。 NULL テストは、デバッグ構成とリリース構成の両方で実行されます。

これらのテストのいずれかが失敗した場合は、アサートと同じ方法で警告メッセージが表示されます。 マクロは、必要に応じて無効な引数の例外をスローします。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="this_file"></a><a name="this_file"></a> THIS_FILE

は、コンパイルするファイルの名前に展開されます。

### <a name="syntax"></a>構文

```
THIS_FILE
```

### <a name="remarks"></a>解説

この情報は、ASSERT マクロと VERIFY マクロによって使用されます。 アプリケーションウィザードとコードウィザードでは、作成したソースコードファイルにマクロが配置されます。

### <a name="example"></a>例

```cpp
#ifdef _DEBUG
#undef THIS_FILE
static char THIS_FILE[] = __FILE__;
#endif

// __FILE__ is one of the six predefined ANSI C macros that the
// compiler recognizes.
```

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="trace"></a><a name="trace"></a> トレース

指定された文字列を現在のアプリケーションのデバッガーに送信します。

```
TRACE(exp)
TRACE(DWORD  category,  UINT  level, LPCSTR lpszFormat, ...)
```

### <a name="remarks"></a>解説

トレースの詳細については、「 [ATLTRACE2](../../atl/reference/debugging-and-error-reporting-macros.md#atltrace2) 」を参照してください。 TRACE と ATLTRACE2 の動作は同じです。

MFC のデバッグバージョンでは、このマクロは、指定された文字列を現在のアプリケーションのデバッガーに送信します。 リリースビルドでは、このマクロは何もコンパイルされません (コードがまったく生成されることはありません)。

詳細については、「 [MFC アプリケーションのデバッグ](/visualstudio/debugger/mfc-debugging-techniques)」を参照してください。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="verify"></a><a name="verify"></a> か

MFC のデバッグバージョンでは、はその引数を評価します。

```
VERIFY(booleanExpression)
```

### <a name="parameters"></a>パラメーター

*booleanExpression*<br/>
0以外または0に評価される式 (ポインター値を含む) を指定します。

### <a name="remarks"></a>解説

結果が0の場合、マクロは診断メッセージを出力し、プログラムを停止します。 条件が0以外の場合は、何も実行されません。

診断メッセージにフォームがあります

`assertion failed in file <name> in line <num>`

ここで、 *name* はソースファイルの名前、 *num* はソースファイルで失敗したアサーションの行番号です。

MFC のリリースバージョンでは、VERIFY は式を評価しますが、プログラムを印刷または中断しません。 たとえば、式が関数呼び出しの場合は、呼び出しが行われます。

### <a name="example"></a>例

[!code-cpp[NVC_MFCDocView#198](../../mfc/codesnippet/cpp/diagnostic-services_7.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxdump-cdumpcontext-in-mfc"></a><a name="cdumpcontext_in_mfc"></a> afxDump (MFC の CDumpContext)

アプリケーションで基本的なオブジェクトダンプ機能を提供します。

```
CDumpContext  afxDump;
```

### <a name="remarks"></a>解説

`afxDump`は、デバッガー [CDumpContext](../../mfc/reference/cdumpcontext-class.md)の `CDumpContext` 出力ウィンドウまたはデバッグターミナルに情報を送信できる定義済みの CDumpContext オブジェクトです。 通常は、の `afxDump` パラメーターとしてを指定し `CObject::Dump` ます。

Windows NT とすべてのバージョンの Windows で `afxDump` は、アプリケーションをデバッグするときに Visual C++ の出力-デバッグウィンドウに出力が送信されます。

この変数は、MFC のデバッグバージョンでのみ定義されています。 の詳細につい `afxDump` ては、「 [MFC アプリケーションのデバッグ](/visualstudio/debugger/mfc-debugging-techniques)」を参照してください。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#23](../../mfc/codesnippet/cpp/diagnostic-services_8.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxdump-internal"></a><a name="afxdump"></a> AfxDump (内部)

デバッグ中にオブジェクトの状態をダンプするために MFC で使用される内部関数です。

### <a name="syntax"></a>構文

```cpp
void AfxDump(const CObject* pOb);
```

### <a name="parameters"></a>パラメーター

*pOb*<br/>
から派生したクラスのオブジェクトへのポインター `CObject` 。

### <a name="remarks"></a>解説

`AfxDump` オブジェクトのメンバー関数を呼び出し、 `Dump` 変数によって指定された場所に情報を送信し `afxDump` ます。 `AfxDump` は、MFC のデバッグバージョンでのみ使用できます。

プログラムのコードではを呼び出さないでください `AfxDump` 。代わりに、 `Dump` 適切なオブジェクトのメンバー関数を呼び出す必要があります。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxmemdf"></a><a name="afxmemdf"></a> afxMemDF

この変数は、デバッガーまたはプログラムからアクセスでき、割り当ての診断を調整できます。

```
int  afxMemDF;
```

### <a name="remarks"></a>解説

`afxMemDF` には、列挙体で指定されているように、次の値を指定でき `afxMemDF` ます。

- `allocMemDF` デバッグアロケーター (デバッグライブラリの既定の設定) を有効にします。

- `delayFreeMemDF` メモリの解放を遅らせます。 プログラムはメモリブロックを解放しますが、アロケーターはそのメモリを基になるオペレーティングシステムに返しません。 これにより、プログラムの最大メモリ負荷が発生します。

- `checkAlwaysMemDF``AfxCheckMemory`メモリが割り当てられるか解放されるたびに、を呼び出します。 これにより、メモリの割り当てと割り当て解除が大幅に遅くなります。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#30](../../mfc/codesnippet/cpp/diagnostic-services_9.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxcheckerror"></a><a name="afxcheckerror"></a> AfxCheckError

この関数は、渡された SCODE をテストして、エラーであるかどうかを確認します。

```cpp
void AFXAPI AfxCheckError(SCODE sc);
throw CMemoryException*
throw COleException*
```

### <a name="remarks"></a>解説

エラーの場合、関数は例外をスローします。 渡された SCODE が E_OUTOFMEMORY 場合、関数は[AfxThrowMemoryException](exception-processing.md#afxthrowmemoryexception)を呼び出して[CMemoryException](../../mfc/reference/cmemoryexception-class.md)をスローします。 それ以外の場合、関数は[AfxThrowOleException](exception-processing.md#afxthrowoleexception)を呼び出すことによって[COleException](../../mfc/reference/coleexception-class.md)をスローします。

この関数を使用すると、アプリケーション内の OLE 関数に対する呼び出しの戻り値を確認できます。 アプリケーションでこの関数を使用して戻り値をテストすることで、最小限のコードでエラー状態に適切に対応できます。

> [!NOTE]
> この関数は、デバッグビルドと非デバッグビルドで同じ効果を持ちます。

### <a name="example"></a>例

[!code-cpp[NVC_MFCOleContainer#33](../../mfc/codesnippet/cpp/diagnostic-services_10.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxcheckmemory"></a><a name="afxcheckmemory"></a> AfxCheckMemory

この関数は、空きメモリプールを検証し、必要に応じてエラーメッセージを出力します。

```
BOOL  AfxCheckMemory();
```

### <a name="return-value"></a>戻り値

メモリエラーがない場合は0以外。それ以外の場合は0です。

### <a name="remarks"></a>解説

関数がメモリの破損を検出しなかった場合は、何も出力しません。

現在ヒープに割り当てられているすべてのメモリブロックがチェックされます。これには、 **`new`** **malloc** 関数や Windows 関数など、基になるメモリアロケーターの直接呼び出しで割り当てられたメモリブロックは含まれません `GlobalAlloc` 。 破損しているブロックが見つかった場合は、デバッガーの出力にメッセージが出力されます。

行を含める場合

[!code-cpp[NVC_MFCCObjectSample#14](../../mfc/codesnippet/cpp/diagnostic-services_1.cpp)]

プログラムモジュールでは、後続のを呼び出す `AfxCheckMemory` と、メモリが割り当てられたファイル名と行番号が表示されます。

> [!NOTE]
> モジュールにシリアル化可能なクラスの1つ以上の実装が含まれている場合は、 `#define` 最後の IMPLEMENT_SERIAL マクロ呼び出しの後に行を配置する必要があります。

この関数は、MFC のデバッグバージョンでのみ動作します。

### <a name="example"></a>例

[!code-cpp[NVC_MFCCObjectSample#26](../../mfc/codesnippet/cpp/diagnostic-services_11.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxdump-mfc"></a><a name="afxdump"></a> AfxDump (MFC)

デバッガーでこの関数を呼び出して、デバッグ中にオブジェクトの状態をダンプします。

```cpp
void AfxDump(const CObject* pOb);
```

### <a name="parameters"></a>パラメーター

*pOb*<br/>
から派生したクラスのオブジェクトへのポインター `CObject` 。

### <a name="remarks"></a>解説

`AfxDump` オブジェクトのメンバー関数を呼び出し、 `Dump` 変数によって指定された場所に情報を送信し `afxDump` ます。 `AfxDump` は、MFC のデバッグバージョンでのみ使用できます。

プログラムのコードではを呼び出さないでください `AfxDump` 。代わりに、 `Dump` 適切なオブジェクトのメンバー関数を呼び出す必要があります。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxdumpstack"></a><a name="afxdumpstack"></a> AfxDumpStack

このグローバル関数を使用すると、現在のスタックのイメージを生成できます。

```cpp
void AFXAPI AfxDumpStack(DWORD dwTarget = AFX_STACK_DUMP_TARGET_DEFAULT);
```

### <a name="parameters"></a>パラメーター

*dwTarget*<br/>
ダンプ出力の対象を示します。 使用できる値は、ビットごとの OR ( **&#124;**) 演算子を使用して組み合わせることができます。次に例を示します。

- AFX_STACK_DUMP_TARGET_TRACE は、 [TRACE](#trace) マクロを使って出力を送信します。 トレースマクロは、デバッグビルドでのみ出力を生成します。リリースビルドでは、出力は生成されません。 また、トレースは、デバッガー以外の他のターゲットにリダイレクトすることもできます。

- AFX_STACK_DUMP_TARGET_DEFAULT は、ダンプ出力を既定のターゲットに送信します。 デバッグビルドの場合、出力はトレースマクロに送られます。 リリースビルドでは、出力はクリップボードに移動します。

- AFX_STACK_DUMP_TARGET_CLIPBOARD は、出力をクリップボードにのみ送信します。 データはクリップボードに CF_TEXT クリップボード形式を使用してプレーンテキストとして配置されます。

- AFX_STACK_DUMP_TARGET_BOTH は、出力をクリップボードとトレースマクロに同時に送信します。

- AFX_STACK_DUMP_TARGET_ODS は、Win32 関数を使って直接デバッガーに出力を送信し `OutputDebugString()` ます。 このオプションを選択すると、デバッガーがプロセスにアタッチされたときにデバッグビルドとリリースビルドの両方でデバッガー出力が生成されます。 AFX_STACK_DUMP_TARGET_ODS は常にデバッガーに到達し (アタッチされている場合)、リダイレクトできません。

### <a name="remarks"></a>解説

次の例は、 `AfxDumpStack` MFC ダイアログアプリケーションのボタンハンドラーからを呼び出すことによって生成される1行の出力を反映しています。

```Output
=== begin AfxDumpStack output ===
00427D55: DUMP2\DEBUG\DUMP2.EXE! void AfxDumpStack(unsigned long) + 181 bytes
0040160B: DUMP2\DEBUG\DUMP2.EXE! void CDump2Dlg::OnClipboard(void) + 14 bytes
0044F884: DUMP2\DEBUG\DUMP2.EXE! int _AfxDispatchCmdMsg(class CCmdTarget *,
unsigned int,int,void ( CCmdTarget::*)(void),void *,unsigned int,struct
AFX_CMDHANDLE
0044FF7B: DUMP2\DEBUG\DUMP2.EXE! virtual int CCmdTarget::OnCmdMsg(unsigned
int,int,void *,struct AFX_CMDHANDLERINFO *) + 626 bytes
00450C71: DUMP2\DEBUG\DUMP2.EXE! virtual int CDialog::OnCmdMsg(unsigned
int,int,void *,struct AFX_CMDHANDLERINFO *) + 36 bytes
00455B27: DUMP2\DEBUG\DUMP2.EXE! virtual int CWnd::OnCommand(unsigned
int,long) + 312 bytes
00454D3D: DUMP2\DEBUG\DUMP2.EXE! virtual int CWnd::OnWndMsg(unsigned
int,unsigned int,long,long *) + 83 bytes
00454CC0: DUMP2\DEBUG\DUMP2.EXE! virtual long CWnd::WindowProc(unsigned
int,unsigned int,long) + 46 bytes
004528D9: DUMP2\DEBUG\DUMP2.EXE! long AfxCallWndProc(class CWnd *,struct
HWND__ *,unsigned int,unsigned int,long) + 237 bytes
00452D34: DUMP2\DEBUG\DUMP2.EXE! long AfxWndProc(struct HWND__ *,unsigned
int,unsigned int,long) + 129 bytes
BFF73663: WINDOWS\SYSTEM\KERNEL32.DLL! ThunkConnect32 + 2148 bytes
BFF928E0: WINDOWS\SYSTEM\KERNEL32.DLL! UTUnRegister + 2492 bytes
=== end AfxDumpStack() output ===
```

上記の出力の各行には、最後の関数呼び出しのアドレス、関数呼び出しを含むモジュールの完全なパス名、およびという関数プロトタイプが示されています。 関数の正確なアドレスでスタックに対する関数呼び出しが行われない場合は、バイトのオフセットが表示されます。

たとえば、次の表は、上記の出力の最初の行を示しています。

|出力|説明|
|------------|-----------------|
|`00427D55:`|最後の関数呼び出しの戻り先アドレス。|
|`DUMP2\DEBUG\DUMP2.EXE!`|関数呼び出しを含むモジュールの完全なパス名。|
|`void AfxDumpStack(unsigned long)`|関数プロトタイプが呼び出されました。|
|`+ 181 bytes`|関数プロトタイプ (この場合は) のアドレスから `void AfxDumpStack(unsigned long)` 戻り先アドレス (この場合は) までのオフセット (バイト単位) `00427D55` 。|

`AfxDumpStack` は、MFC ライブラリの debug および nondebug バージョンで使用できます。ただし、この関数は、実行可能ファイルが共有 DLL で MFC を使用している場合でも、常に静的にリンクされます。 共有ライブラリの実装では、関数は MFCS42 にあります。LIB ライブラリ (およびそのバリエーション)。

この関数を正常に使用するには:

- ファイル IMAGEHLP.DLL はパス上にある必要があります。 この DLL がない場合は、関数によってエラーメッセージが表示されます。 IMAGEHLP.DLL によって提供される関数セットの詳細については、「 [イメージヘルプライブラリ](/windows/win32/Debug/image-help-library) 」を参照してください。

- スタック上のフレームを持つモジュールには、デバッグ情報が含まれている必要があります。 デバッグ情報が含まれていない場合でも、関数はスタックトレースを生成しますが、トレースの詳細は低くなります。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxenablememoryleakdump"></a><a name="afxenablememoryleakdump"></a> AfxEnableMemoryLeakDump

AFX_DEBUG_STATE デストラクター内のメモリリークダンプを有効または無効にします。

```
BOOL AFXAPI AfxEnableMemoryLeakDump(BOOL bDump);
```

### <a name="parameters"></a>パラメーター

*bDump*<br/>
からTRUE は、メモリリークダンプが有効であることを示します。FALSE は、メモリリークダンプが無効であることを示します。

### <a name="return-value"></a>戻り値

このフラグの以前の値。

### <a name="remarks"></a>解説

アプリケーションが MFC ライブラリをアンロードしたときに、MFC ライブラリがメモリ リークを確認します。 この時点で、Visual Studio の [ **デバッグ** ] ウィンドウからメモリリークがユーザーに報告されます。

アプリケーションが MFC ライブラリの前に別のライブラリを読み込んだ場合、そのライブラリ内の一部のメモリ割り当てが誤ってメモリ リークとして報告されます。 誤ったメモリ リークが原因で、MFC ライブラリがそれらを報告したときに、アプリケーションがゆっくりと終了する可能性があります。 このような場合、 `AfxEnableMemoryLeakDump` を使用してメモリ リーク ダンプを無効にします。

> [!NOTE]
> この方法を使用してメモリ リーク ダンプをオフにすると、アプリケーションで有効なメモリ リークのレポートを受け取らなくなります。 この方法を使用するのは、メモリ リーク ダンプに誤ったメモリ リークが含まれているという確信がある場合のみにする必要があります。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxenablememorytracking"></a><a name="afxenablememorytracking"></a> AfxEnableMemoryTracking

診断メモリの追跡は、通常、MFC のデバッグバージョンで有効になります。

```
BOOL AfxEnableMemoryTracking(BOOL bTrack);
```

### <a name="parameters"></a>パラメーター

*bTrack*<br/>
この値を TRUE に設定すると、メモリ追跡が有効になります。FALSE の場合はオフになります。

### <a name="return-value"></a>戻り値

追跡-有効化フラグの前の設定。

### <a name="remarks"></a>解説

この関数を使用すると、ブロックが正しく割り当てられていることがわかっているコードセクションでの追跡を無効にできます。

の詳細につい `AfxEnableMemoryTracking` ては、「 [MFC アプリケーションのデバッグ](/visualstudio/debugger/mfc-debugging-techniques)」を参照してください。

> [!NOTE]
> この関数は、MFC のデバッグバージョンでのみ動作します。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#24](../../mfc/codesnippet/cpp/diagnostic-services_12.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxismemoryblock"></a><a name="afxismemoryblock"></a> AfxIsMemoryBlock

メモリアドレスをテストして、の診断バージョンによって割り当てられた現在アクティブなメモリブロックを表していることを確認し **`new`** ます。

```
BOOL AfxIsMemoryBlock(
    const void* p,
    UINT nBytes,
    LONG* plRequestNumber = NULL);
```

### <a name="parameters"></a>パラメーター

*irtran-p*<br/>
テストするメモリブロックを指します。

*nBytes*<br/>
メモリブロックの長さをバイト単位で格納します。

*plRequestNumber*<br/>
**`long`** は、メモリブロックの割り当てシーケンス番号を使用して入力される整数を指します。現在アクティブなメモリブロックを表していない場合は0を指します。

### <a name="return-value"></a>戻り値

メモリブロックが現在割り当てられていて、長さが正しい場合は0以外の値。それ以外の場合は0です。

### <a name="remarks"></a>解説

また、指定したサイズを、割り当てられた元のサイズと比較して確認します。 関数が0以外の値を返した場合、割り当てシーケンス番号が *Plrequestnumber*に返されます。 この数は、ブロックが他のすべての割り当てに対して相対的に割り当てられた順序を表し **`new`** ます。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#27](../../mfc/codesnippet/cpp/diagnostic-services_13.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxisvalidaddress"></a><a name="afxisvalidaddress"></a> AfxIsValidAddress

メモリアドレスをテストして、プログラムのメモリ領域内に完全に含まれていることを確認します。

```
BOOL AfxIsValidAddress(
    const void* lp,
    UINT nBytes,
    BOOL bReadWrite = TRUE);
```

### <a name="parameters"></a>パラメーター

*世代*<br/>
テスト対象のメモリアドレスを指します。

*nBytes*<br/>
テストするメモリのバイト数を格納します。

*bReadWrite*<br/>
メモリが読み取りと書き込みのどちらであるか (TRUE)、または読み取りのみである (FALSE) かを指定します。

### <a name="return-value"></a>戻り値

デバッグビルドでは、指定されたメモリブロックがプログラムのメモリ空間内に完全に含まれている場合は0以外の。それ以外の場合は0です。

非デバッグビルドでは、 *lp* が NULL でない場合は0以外になります。それ以外の場合は0です。

### <a name="remarks"></a>解説

アドレスは、によって割り当てられたブロックに制限されません **`new`** 。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#28](../../mfc/codesnippet/cpp/diagnostic-services_14.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxisvalidstring"></a><a name="afxisvalidstring"></a> AfxIsValidString

文字列へのポインターが有効かどうかを判断するには、この関数を使用します。

```
BOOL  AfxIsValidString(
    LPCSTR lpsz,
    int nLength = -1);
```

### <a name="parameters"></a>パラメーター

*lpsz*<br/>
テストするポインター。

*nLength*<br/>
テストする文字列の長さをバイト単位で指定します。 値が-1 の場合は、文字列が null で終わることを示します。

### <a name="return-value"></a>戻り値

デバッグビルドでは、指定されたポインターが指定されたサイズの文字列を指している場合は0以外の値。それ以外の場合は0です。

非デバッグビルドでは、 *lpsz* が NULL でない場合は0以外になります。それ以外の場合は0です。

### <a name="example"></a>例

[!code-cpp[NVC_MFC_Utilities#29](../../mfc/codesnippet/cpp/diagnostic-services_15.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxsetallochook"></a><a name="afxsetallochook"></a> AfxSetAllocHook

各メモリブロックが割り当てられる前に、指定された関数の呼び出しを有効にするフックを設定します。

```
AFX_ALLOC_HOOK AfxSetAllocHook(AFX_ALLOC_HOOK pfnAllocHook);
```

### <a name="parameters"></a>パラメーター

*pfnAllocHook*<br/>
呼び出す関数の名前を指定します。 割り当て関数のプロトタイプについては、「解説」を参照してください。

### <a name="return-value"></a>戻り値

割り当てを許可する場合は0以外の。それ以外の場合は0です。

### <a name="remarks"></a>解説

Microsoft Foundation Class ライブラリのデバッグメモリアロケーターは、ユーザー定義のフック関数を呼び出して、ユーザーがメモリ割り当てを監視し、割り当てが許可されているかどうかを制御できるようにします。 割り当て用のフック関数は、次のようにプロトタイプ宣言されます。

**Bool AFXAPI AllocHook (size_t** `nSize` **, bool** `bObject` **, LONG** `lRequestNumber` **);**

*nSize*<br/>
提案されたメモリ割り当てのサイズ。

*bObject*<br/>
が派生したオブジェクトの割り当てである場合は TRUE `CObject` 。それ以外の場合は FALSE。

*lRequestNumber*<br/>
メモリ割り当てのシーケンス番号。

AFXAPI 呼び出し規約は、呼び出し先がスタックからパラメーターを削除する必要があることを意味します。

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxdoforallclasses"></a><a name="afxdoforallclasses"></a> AfxDoForAllClasses

アプリケーションのメモリ領域内のすべてのシリアル化可能な派生クラスに対して、指定された反復関数を呼び出し `CObject` ます。

```cpp
void
AFXAPI AfxDoForAllClasses(
    void (* pfn)(const CRuntimeClass* pClass, void* pContext),
    void* pContext);
```

### <a name="parameters"></a>パラメーター

*pfn*<br/>
各クラスに対して呼び出される反復関数を指します。 関数の引数は、オブジェクトへのポインター `CRuntimeClass` と、呼び出し元が関数に提供する追加データへの void ポインターです。

*pContext*<br/>
呼び出し元が反復関数に渡すことができる省略可能なデータを指します。 このポインターは NULL にすることができます。

### <a name="remarks"></a>解説

シリアル化可能 `CObject` な派生クラスは、DECLARE_SERIAL マクロを使用して派生したクラスです。 PContext でに渡されるポインター `AfxDoForAllClasses` は*pContext* 、呼び出されるたびに、指定された反復関数に渡されます。

> [!NOTE]
> この関数は、MFC のデバッグバージョンでのみ動作します。

### <a name="example"></a>例

[!code-cpp[NVC_MFCCollections#113](../../mfc/codesnippet/cpp/diagnostic-services_16.cpp)]

[!code-cpp[NVC_MFCCollections#114](../../mfc/codesnippet/cpp/diagnostic-services_17.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** afx

## <a name="afxdoforallobjects"></a><a name="afxdoforallobjects"></a> AfxDoForAllObjects

で割り当てられたから派生したすべてのオブジェクトに対して、指定された反復関数を実行し `CObject` **`new`** ます。

```cpp
void AfxDoForAllObjects(
    void (* pfn)(CObject* pObject, void* pContext),
    void* pContext);
```

### <a name="parameters"></a>パラメーター

*pfn*<br/>
各オブジェクトに対して実行する反復関数を指します。 関数の引数は、へのポインターであり、 `CObject` 呼び出し元が関数に提供する余分なデータへの void ポインターです。

*pContext*<br/>
呼び出し元が反復関数に渡すことができる省略可能なデータを指します。 このポインターは NULL にすることができます。

### <a name="remarks"></a>解説

Stack、global、または embedded オブジェクトは列挙されません。 PContext でに渡されるポインターは、呼び出されるたび `AfxDoForAllObjects` に、指定された反復関数に渡されます。 *pContext*

> [!NOTE]
> この関数は、MFC のデバッグバージョンでのみ動作します。

### <a name="example"></a>例

[!code-cpp[NVC_MFCCollections#115](../../mfc/codesnippet/cpp/diagnostic-services_18.cpp)]

[!code-cpp[NVC_MFCCollections#116](../../mfc/codesnippet/cpp/diagnostic-services_19.cpp)]

## <a name="see-also"></a>関連項目

[マクロとグローバル](mfc-macros-and-globals.md)<br/>
[CObject::D ump](cobject-class.md#dump)
