---
title: 方向フラグ
ms.date: 11/04/2016
helpviewer_keywords:
- direction flag
ms.assetid: 0836b4af-dbbb-4ab8-a4b2-156f2e2099e2
ms.openlocfilehash: 04e096c6a62f806f4c214745a8401b1730eda3a6
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2020
ms.locfileid: "79443387"
---
# <a name="direction-flag"></a>方向フラグ

方向フラグは、すべての Intel x86 互換の CPU 固有の CPU フラグです。 MOVS、MOVSD、MOVSW などの REP (繰り返し) プレフィックスを使用するすべてのアセンブリ命令に適用されます。 方向フラグがオフの場合、適用される命令に渡されたアドレスは増加します。

C ランタイム ルーチンでは、方向フラグがオフになっていることを前提としています。 C ランタイム関数とともに他の関数を使用している場合は、他の関数が方向フラグを変更しないようにする、または方向フラグを元の状態に復元する必要があります。 入力時に方向フラグがオフになっていると、ランタイム コードがより高速かつ効率的になります。

文字列操作ルーチンやバッファー操作ルーチンなどの C ランタイム ライブラリ関数では、方向フラグがオフになっていることを想定してあります。

## <a name="see-also"></a>参照

[CRT ライブラリの機能](../c-runtime-library/crt-library-features.md)
