---
title: アクティベーション (C++)
ms.date: 11/04/2016
helpviewer_keywords:
- OLE server applications [MFC], activation
- OLE items [MFC], visual editing
- activation [MFC]
- OLE [MFC], in-place activation
- OLE [MFC], activation
- in-place activation, embedded and linked items
- activating objects
- visual editing, activation
- visual editing
- documents [MFC], OLE
- embedded objects [MFC]
- OLE [MFC], editing
- in-place activation
- activation [MFC], embedded OLE items
- OLE activation [MFC]
ms.assetid: ed8357d9-e487-4aaa-aa6b-2edc4de25dfa
ms.openlocfilehash: 47640a59180348bd3513013b65029a775545e211
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84619183"
---
# <a name="activation-c"></a>アクティベーション (C++)

この記事では、OLE アイテムのビジュアル編集でのアクティブ化の役割について説明します。 ユーザーが OLE 項目をコンテナードキュメントに埋め込んだ後、それを使用する必要がある場合があります。 これを行うには、ユーザーが項目をダブルクリックします。これにより、その項目がアクティブになります。 アクティブ化のために最も頻繁に使用されるアクティビティは編集中です。 現在の OLE 項目の多くは、編集のためにアクティブ化されると、現在のフレームウィンドウのメニューとツールバーが変更され、その項目を作成したサーバーアプリケーションに属しているものが反映されます。 インプレースアクティブ化と呼ばれるこの動作を使用すると、コンテナードキュメントのウィンドウを離れることなく、複合ドキュメント内の埋め込みアイテムを編集できます。

また、埋め込み OLE 項目を別のウィンドウで編集することもできます。 これは、コンテナーまたはサーバーアプリケーションがインプレースアクティベーションをサポートしていない場合に発生します。 この場合、ユーザーが埋め込みアイテムをダブルクリックすると、サーバーアプリケーションが別のウィンドウで起動し、埋め込みアイテムが独自のドキュメントとして表示されます。 ユーザーは、このウィンドウの項目を編集します。 編集が完了すると、ユーザーはサーバーアプリケーションを終了し、コンテナーアプリケーションに戻ります。

別の方法として、ユーザーは [**編集**] メニューの [ ** \<object> 開く**] をクリックして [編集を開く] を選択できます。 これにより、オブジェクトが別のウィンドウで開きます。

> [!NOTE]
> 別のウィンドウでの埋め込み項目の編集は、OLE のバージョン1では標準動作でしたが、一部の OLE アプリケーションではこのスタイルの編集のみがサポートされている場合があります。

インプレースライセンス認証は、ドキュメント中心のアプローチをドキュメントの作成に昇格させます。 ユーザーは複合ドキュメントを1つのエンティティとして処理し、アプリケーション間を切り替えることなく作業できます。 ただし、埋め込みアイテムに対してのみ使用され、リンクされたアイテムに対しては使用されません。別のウィンドウで編集する必要があります。 これは、リンクされたアイテムが実際には別の場所に格納されているためです。 リンクアイテムの編集は、データの実際のコンテキスト (つまり、データが格納されている場所) 内で行われます。 別のウィンドウでリンクアイテムを編集すると、データが別のドキュメントに属していることがユーザーに通知されます。

MFC では、入れ子になったインプレースアクティベーションはサポートされていません。 コンテナー/サーバーアプリケーションをビルドし、そのコンテナー/サーバーが別のコンテナーに埋め込まれていて、埋め込み先でアクティブ化されている場合は、埋め込みオブジェクトを埋め込むことはできません。

ユーザーがダブルクリックした場合、埋め込みアイテムは、アイテムに対して定義されている動詞によって異なります。 詳細については、「 [Activation: verb](activation-verbs.md)」を参照してください。

## <a name="see-also"></a>関連項目

[OLE●ole○](ole-in-mfc.md)<br/>
[Containers](containers.md)<br/>
[サーバー](servers.md)
