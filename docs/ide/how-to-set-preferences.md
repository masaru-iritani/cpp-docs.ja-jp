---
title: Visual Studio で C++ コーディングの基本設定を設定する
ms.description: Customize C++ formatting, colors, layout, line numbers, and menus in the Visual Studio IDE.
ms.topic: overview
ms.date: 09/27/2019
ms.openlocfilehash: e3a665ead7a314b343ec3320e95b189f83a38a47
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81365390"
---
# <a name="set-your-c-coding-preferences-in-visual-studio"></a>Visual Studio で C++ コーディングの基本設定を設定する

Visual Studio をパーソナライズすることで、C++ のコーディング体験をより便利で生産的で楽しいものにすることができます。 次のようにすることができます。

- メニューとツールバーをカスタマイズします。
- ウィンドウレイアウトを配置します。
- 色のテーマを設定します。
- ClangFormat のいくつかのスタイルを含む C++ 書式設定規則を指定します。
- カスタムキーボードショートカットを作成します。

複数のマシン間で設定を同期し、複数の設定セットを作成して保存し、チームメイトと共有することができます。 拡張機能は Visual Studio マーケットプレースからインストールでき、動作をカスタマイズするための追加オプションを提供できます。 詳細については、「 [IDE の個人用設定](/visualstudio/ide/personalizing-the-visual-studio-ide)」を参照してください。

## <a name="arrange-window-layout"></a>ウィンドウレイアウトの配置

Visual Studio ウィンドウ内では、領域はメイン メニュー、ツール バー、コード エディター (またはドキュメント ウィンドウ)、およびツール ウィンドウ (ソリューション エクスプローラーやエラー一覧など) に分割されます。 一部のウィンドウは、同じ位置で互いに重なっています。 たとえば、ソリューション エクスプローラー、クラス ビュー、リソース ビュー、およびソース管理エクスプローラーは、すべて同じ既定の位置を共有します。 フレームの下部にあるタブを選択して、それらのタブを切り替えます。 これらのウィンドウを同時に表示するには、タイトル バーでウィンドウの 1 つをドラッグして新しい位置に移動します。 Visual Studio のメイン ウィンドウの境界線のいずれかにドッキングするか、フローティングすることができます。

次のスクリーンショットは、**チーム エクスプローラー**ウィンドウが既定の位置からコード エディターの左側の新しいドッキング位置にドラッグされている様子を示しています。 青い色の色の領域は、マウス ボタンを離したときにウィンドウが配置される場所を示します。

![レイアウトの変更が強調表示された Visual Studio チーム エクスプローラー ウィンドウのスクリーンショット](media/window-layout-move-team-explorer.png)

ドキュメント ウィンドウでは、開いている各ファイルがタブ付きフレームに含まれます。 ツール ウィンドウと同様に、これらのタブを浮動またはロックできます。 詳細については、「 [Visual Studio でのウィンドウ レイアウトのカスタマイズ](/visualstudio/ide/customizing-window-layouts-in-visual-studio)」を参照してください。

すべてのツール ウィンドウを非表示にしてコード エディタ ウィンドウを最大化するには **、Alt** + **キーを押しながら Enter キー** + **を**押して*全画面表示モード*を切り替えます。

## <a name="set-c-coding-styles-and-formatting"></a>C++ のコーディング スタイルと書式を設定する

インデントや中かっこの位置など、コードの書式設定オプションを指定できます。 これを行うには、**ツール** > **オプション** > **テキスト エディター** > **C/C++** > **の書式設定**に移動します (または**Ctrl + Q を**入力して「書式設定」を検索します)。 または、[いずれかの ClangFormat](https://clang.llvm.org/docs/ClangFormat.html)スタイル (または独自のカスタム ClangFormat スタイル) を指定することもできます。

![ClangFormat オプションのスクリーンショット](media/clang-format-ide.png)

すべての書式設定オプションの詳細については、「[オプション、 テキスト エディター、 C/C++ 、 書式設定](/visualstudio/ide/reference/options-text-editor-c-cpp-formatting)」を参照してください。

## <a name="set-the-color-theme"></a>配色テーマの設定

明るいまたは暗い背景を設定するには **、Ctrl + Qを**入力して「カラーテーマ」を検索します。 これらの情報は、[**ツール** > **オプション環境]** > **Environment**に進み、[**色のテーマ**] を選択して見つけることもできます。

![カラーテーマのスクリーンショット](media/tools-options-color-theme.png)

たとえば、暗いテーマは次のとおりです。

![暗い色をテーマにした Visual Studio のスクリーンショット](media/tools-options-dark-theme.png)

## <a name="customize-code-colorization"></a>コードの色付けのカスタマイズ

Visual Studio 2019 では、3 つの定義済みの*配色*から選択できます。 これらは、エディターでのコード要素の色付け方法を指定します。 テーマを選択するには、[**ツール** > **オプション]** > **テキスト エディタ** > **C/C++** > **ビュー**に移動し、[**配色]** を選択します。

![C++ カラー スキーム オプションのスクリーンショット (強調表示された拡張)](media/color-schemes.png)

**Visual Studio 2017**と呼ばれる配色では、ほとんどのコード要素は単に黒です。 **拡張**配色では、関数、ローカル変数、マクロ、およびその他の要素が色分けされます。 拡張 **(グローバル対メンバー)** スキームでは、グローバル関数と変数はクラスメンバーと対比するように色分けされます。 既定のモードは**Enhanced**で、次のようになります。

![拡張配色のスクリーンショット](media/color-scheme-enhanced.png)

どのテーマや配色がアクティブであるかに関係なく、個々のコード要素のフォントと色をカスタマイズできます。 これを行うには、**ツール** > **オプション** > **環境** > **のフォントと色**に移動します(または**Ctrl + Q**を入力して「フォント」を検索します)。 C++ オプションが表示されるまで、表示項目のリストを下にスクロールします。

![C++ フォントと色のオプションのスクリーンショット](media/tools-options-cpp-colors.png)

ここで設定した色は、配色に対して定義されている値を上書きします。 配色パターンの既定の色に戻す場合は、色を **[既定値]** に戻します。

## <a name="customize-the-toolbars"></a>ツールバーのカスタマイズ

ツールバーは、メニューやキーボードショートカットを使用するのではなく、シングルクリックでコマンドを実行する便利な方法を提供します。 Visual Studio には、ツール バーの標準セットが含まれています。 標準的な C++ 開発では、最も便利なツール バーは、標準、テキスト エディター、ビルド、デバッグ、ソース管理、およびファイルの比較です。 Windows の開発では、ダイアログ エディターとイメージ エディターは、ダイアログ ボックスのレイアウトやアイコンの編集に役立ちます。

ツールバーのアイコンにカーソルを合わせると、それがどのコマンドを表しているかを確認できます。

![ツール バー アイコンのスクリーンショット (ホバー時に使用可能なコマンド情報の例)](media/toolbar-mouse-hover.png)

下向き矢印を選択して、コマンドの追加や削除、またはカスタム ツールバーの作成を行うことができます。 ツールバーを新しい位置に移動するには、左側の点線でドラッグします。

![下向き矢印と点線の棒が強調表示されたツールバーのスクリーンショット](media/toolbar-move-edit.png).

詳細については、「 [[方法] Visual Studio でメニューとツール バーをカスタマイズする](/visualstudio/ide/how-to-customize-menus-and-toolbars-in-visual-studio)」を参照してください。

## <a name="show-or-hide-line-numbers"></a>行番号の表示/非表示

エディター ウィンドウの左側に行番号を表示するかどうかを指定できます。 [**オプション]** の **[C/C++]** で、[**全般**] を選択します。 [**設定]** セクションで、設定に応じて **[行番号**] をオンまたはオフにします。

![行番号が強調表示された一般オプションのスクリーンショット](media/tools-options-line-numbers.png)

## <a name="create-keyboard-shortcuts"></a>キーボード ショートカットを作成する

Visual Studio の多くのコマンドには *、キーボード ショートカット*、キーの組み合わせ、Ctrl キー、Alt キー、および Shift キーがあります。 これらのキーボード ショートカットを変更したり、Visual Studio で独自のショートカットキーを作成したりできます。  > **ツール** > **オプション****Environment**環境 > **キーボード**に移動します(または**Ctrl + Qを**入力して「ショートカット」を検索します)。 詳細については、「 [Visual Studio でのキーボード ショートカットの識別とカスタマイズ](/visualstudio/ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio)」を参照してください。
