---
title: '&lt;charconv&gt;'
ms.date: 07/22/2020
f1_keywords:
- <charconv>
helpviewer_keywords:
- charconv header
ms.openlocfilehash: 59807749105512e0eb61acfdf60ef463febbc3a8
ms.sourcegitcommit: 1f009ab0f2cc4a177f2d1353d5a38f164612bdb1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87230191"
---
# <a name="ltcharconvgt"></a>&lt;charconv&gt;

文字シーケンスを整数または浮動小数点値にすばやく変換します。
このライブラリを使用する方法の1つは、JSON およびテキストファイルに浮動小数点値を記述し、ラウンドトリップすることです。

変換関数は、パフォーマンスのためにチューニングされており、最短ラウンドトリップ動作もサポートしています。 最短のラウンドトリップ動作は、数値が文字に変換されるときに、その文字を浮動小数点型に変換するときに元の数値の復旧を可能にするために、十分な有効桁数のみが書き込まれることを意味します。 この機能を提供する他の CRT または STL 関数はありません。

ライブラリを使用する利点の一部を `<charconv>` 次に示します。

- 数値を表す文字のシーケンスは、null で終わる必要はありません。 同様に、数値が文字に変換された場合、結果は null で終了しません。
- 変換関数はメモリを割り当てません。 バッファーは常に所有しています。
- 変換関数は、をスローしません。 これらは、エラー情報を含む構造体を返します。
- 変換は、実行時の丸めモードに依存しません。
- 変換はロケールに対応していません。 コンマを使用するロケールでは、小数点は常に '. ' ではなく '. ' として出力され、解析されます。

## <a name="requirements"></a>必要条件

**ヘッダー:**\<charconv>

**名前空間:** std

/std: c++ 17 以降が必要です。

## <a name="members"></a>メンバー

### <a name="types"></a>型

| Type | [説明] |
|-|:-|
| [chars_format](chars-format-class.md) | 科学的、16進数などの書式設定の種類を指定します。 |
| [from_chars_result](from-chars-result-structure.md) | 変換の結果を保持 `from_chars` します。 |
| [to_chars_result](to-chars-result-structure.md) | 変換の結果を保持 `to_chars` します。 |

### <a name="functions"></a>関数

| 機能 | 説明 |
|-|:-|
| [from_chars](charconv-functions.md#from_chars) | 文字を integer、float、または double に変換します。 |
| [to_chars](charconv-functions.md#to_chars)| 整数、float、または double を文字に変換します。 |

## <a name="see-also"></a>関連項目

[ヘッダー ファイル リファレンス](cpp-standard-library-header-files.md)

