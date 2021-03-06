---
title: リンカ ツール エラー LNK2004
ms.date: 11/04/2016
f1_keywords:
- LNK2004
helpviewer_keywords:
- LNK2004
ms.assetid: 07645371-e67b-4a2c-b0e0-dde24c94ef7e
ms.openlocfilehash: 0d26ab12c5b82d52b7dcbb176d9bfa033d7ddfee
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80194838"
---
# <a name="linker-tools-error-lnk2004"></a>リンカ ツール エラー LNK2004

gp 相対 fixup が ' target ' にオーバーフローしています。短いセクション ' section ' が大きすぎるか、範囲を超えています。

セクションが大きすぎます。

このエラーを解決するには、短いセクションのサイズを小さくします。そのためには、#pragma セクション ("sectionname"、read、write、long) を介して長いセクションにデータを明示的に配置し、データ定義と宣言で `__declspec(allocate(".sectionname"))` を使用します。  たとえば、次のように入力します。

```
#pragma section(".data$mylong", read, write, long)
__declspec(allocate(".data$mylong"))
char    rg0[1] = { 1 };
char    rg1[2] = { 1 };
char    rg2[4] = { 1 };
char    rg3[8] = { 1 };
char    rg4[16] = { 1 };
char    rg5[32] = { 1 };
```

また、論理的にグループ化されたデータを、8バイトを超えるデータのコレクションとなる独自の構造に移動することもできます。この場合、コンパイラは long data セクションで割り当てます。  たとえば、次のように入力します。

```
// from this...
int     w1  = 23;
int     w2 = 46;
int     w3 = 23*3;
int     w4 = 23*4;

// to this...
struct X {
    int     w1;
    int     w2;
    int     w3;
    int     w4;
} x  = { 23, 23*2, 23*3, 23*4 };
```

このエラーには、致命的なエラー `LNK1165`が続きます。
