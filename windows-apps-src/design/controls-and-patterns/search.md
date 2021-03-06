---
Description: 検索は、ユーザーがアプリでコンテンツを見つけることができる 2 つの方法のうちの 1 つです。 この記事のガイダンスでは、検索エクスペリエンスの構成要素、検索スコープ、実装、コンテキストでの検索の例について説明します。
title: 検索とページ内検索
ms.assetid: C328FAA3-F6AE-4970-8372-B413F1290C39
label: Search
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: miguelrb
design-contact: ksulliv
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 5c6eb22fbe0488fa9a36160ce9e704d10727e4c9
ms.sourcegitcommit: 76e8b4fb3f76cc162aab80982a441bfc18507fb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "66364482"
---
# <a name="search-and-find-in-page"></a>検索とページ内検索

 

検索は、ユーザーがアプリでコンテンツを見つけることができる 2 つの方法のうちの 1 つです。 この記事のガイダンスでは、検索エクスペリエンスの構成要素、検索スコープ、実装、コンテキストでの検索の例について説明します。

> **重要な API**: [AutoSuggestBox クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.AutoSuggestBox)

## <a name="elements-of-the-search-experience"></a>検索エクスペリエンスの構成要素


**入力。**   テキストは検索入力の最も一般的なモードであり、このガイドで重点的に説明します。 その他の一般的な入力モードには音声やカメラがありますが、通常、それらにはデバイス ハードウェアを操作する機能が必要であり、追加のコントロールやカスタム UI がアプリ内で必要になる場合があります。

**ゼロ入力。**   ユーザーが入力フィールドをアクティブにしてからテキストを入力するまでに、"ゼロ入力キャンバス" と呼ばれるものを表示できます。 通常、ゼロ入力キャンバスは、アプリのキャンバスに表示され、ユーザーがクエリの入力を開始したときに、このコンテンツが[自動提案](auto-suggest-box.md)で置き換えられます。 最近の検索履歴、トレンド検索、状況依存の検索候補、ヒントが、すべてゼロ入力状態の候補となります。

![ゼロ入力キャンバスでの Cortana の例](images/search-cortana-example.png)

 

**クエリの生成/自動提案。**   クエリの生成により、ユーザーが入力を開始するとすぐにゼロ入力のコンテンツが置き換えられます。 ユーザーがクエリ文字列を入力すると、入力プロセスを高速化し、有効なクエリを生成できるように、継続的に更新される一連のクエリ候補、または不明瞭解消オプションが表示されます。 このクエリ候補の表示動作は、[自動提案コントロール](auto-suggest-box.md)に組み込まれ、検索内部にアイコンを表示する方法にもなります (マイク アイコンやコミット アイコンなど)。 これ以外のすべての動作は、アプリに基づきます。

![クエリの生成/自動提案の例](images/search-autosuggest-example.png)

 

**結果セット。**   検索結果は、通常は検索入力フィールドのすぐ下に表示されます。 これは必須ではありませんが、入力と結果の並置によりコンテキストが維持され、ユーザーは前のクエリの編集や新しいクエリの入力をすぐに開始できます。 このつながりは、ヒント テキストを、結果セットを作成したクエリで置き換えることで、さらに強化できます。

前のクエリの編集と新しいクエリの入力の両方を効率的に開始できるようにする 1 つの方法として、フィールドが再アクティブ化されたときに、前のクエリを強調表示します。 これにより、任意のキー入力によって前の文字列が置き換えられますが、文字列が保持されるため、ユーザーはカーソルを移動して、前の文字列を編集または追加することができます。

結果のセットは、コンテンツを最適に伝える任意の形式で表示できます。 [リスト ビュー](lists.md)は十分な柔軟性を備えており、ほとんどの検索に最適です。 グリッド ビューはイメージまたはその他のメディアに適しており、地図を使って空間的な配布を伝えることができます。

## <a name="search-scopes"></a>検索範囲


検索は共通の機能であり、シェルおよび多くのアプリ内で検索 UI がユーザーに表示されます。 検索のエントリ ポイントは同じように視覚化される傾向がありますが、広い範囲 (Web またはデバイスの検索) から狭い範囲 (ユーザーの連絡先一覧) までの結果を提供できます。 検索エントリ ポイントは、検索対象のコンテンツに対して並置する必要があります。

一般的な検索スコープは次のとおりです。

**グローバル**と**コンテキスト/絞り込み。**   クラウドとローカル コンテンツの複数のソースを対象に検索を実行します。 結果には、URL、ドキュメント、メディア、操作、アプリなどが含まれます。

**Web。**   Web インデックスを検索します。 結果には、ページ、エンティティ、回答が含まれます。

**自分のコンテンツ。**   デバイス、クラウド、ソーシャル グラフなどを対象に検索を実行します。 結果はさまざまですが、ユーザー アカウントへの接続によって制限されます。

ヒントのテキストを使って検索スコープを伝えます。 たとえば、次のものがあります。

"Windows と Web を検索する"

"連絡先の一覧を検索する"

"メールボックスを検索する"

"検索の設定"

"場所を探す"

![検索のヒントのテキストの例](images/search-windowsandweb.png)

 

検索入力ポイントの範囲を効果的に伝えることにより、実行中の検索の機能がユーザーの期待事項を満たし、不満が発生する可能性を減らすことができます。

## <a name="implementation"></a>実装


ほとんどのアプリでは、検索のエントリ ポイントとしてテキスト入力フィールドを用意することをお勧めします。これにより、目立つ視覚的なフットプリントが提供されます。 さらに、ヒントのテキストは検索機能を支援し、検索スコープを伝えることができます。 検索がよりセカンダリ操作であるか、またはスペースに制約がある場合、検索アイコンは、関連する入力フィールドのないエントリ ポイントとなります。 アイコンとして視覚化するときは、次の例のように、必ずモーダルな検索ボックスの余地があることを確認します。

検索アイコンをクリックする前:

![検索アイコンと折りたたまれている検索ボックスの例](images/search-icon-collapsed.png)

 

検索アイコンをクリックした後:

![検索アイコンと展開された検索ボックスの例](images/search-icon-expanded.png)

 

検索では、常にエントリ ポイントに右向きの虫眼鏡グリフを使います。 使用するグリフは Segoe UI Symbol、16 進数の文字のコード 0xE0094 で、通常は 15 epx のフォント サイズです。

検索のエントリ ポイントは、多数のさまざまな領域に配置でき、それによって検索スコープとコンテキストの両方が伝わります。 さまざまなエクスペリエンスや外部からの結果をアプリに収集する検索は、通常、グローバル コマンド バーやナビゲーションなど、最上位にあるアプリのクロム内に配置されます。

検索スコープが狭くなるかにコンテキストに依存するにつれて、通常、配置は検索するコンテンツとより直接的に関連付けられます (キャンバス上、リスト ヘッダーとして、状況依存のコマンド バー内など)。 いずれの場合も、検索入力と結果のつながり、または絞り込まれたコンテンツが視覚的に明確になります。

スクロール可能なリストの場合、常に検索入力を表示すると便利です。 検索入力は固定し、コンテンツが背後をスクロールするようにすることをお勧めします。

ゼロ入力とクエリの生成機能は、コンテキスト/絞り込み検索ではオプションであり、リストはユーザーの入力によってリアルタイムで絞り込まれます。 例外には、受信トレイのフィルター オプション (宛先:&lt;入力文字列&gt;、差出人: &lt;入力文字列&gt;、件名: &lt;入力文字列&gt;) など、クエリの書式設定の候補が表示される場合などがあります。

## <a name="example"></a>例


このセクションの例では、コンテキストに検索を配置します。

Windows ツール バーの操作としての検索:

![Windows ツール バーの操作としての検索の例](images/search-toolbar-action.png)

 

アプリ キャンバスでの入力としての検索:

![アプリ キャンバスでの検索の例](images/search-canvas-contacts.png)

 

ナビゲーション ウィンドウでの検索:

![ナビゲーション メニューの検索の例](images/search-navmenu.png)

 

検索が頻繁にアクセスされないか、コンテキスト依存が高い場合に予約されるのが最適なインライン検索:

![インライン検索の例](images/patterns-search-results-desktop.png)


## <a name="guidelines-for-find-in-page"></a>ページ内検索のガイドライン


ページ内検索により、ユーザーは現在のテキスト本文からテキストの一致を検索できるようになります。 ページ内検索が提供される最も一般的なアプリは、ドキュメント ビューアー、リーダー、ブラウザーです。

## <a name="dos-and-donts"></a>推奨と非推奨


-   ユーザーがページ内のテキストを検索できるように、ページ内検索機能を備えたコマンド バーをアプリ内に配置します。 配置について詳しくは、「例」をご覧ください。

    -   ページ内検索を提供するアプリでは、必要なすべてのコントロールがコマンド バーに含まれている必要があります。
    -   ページ検索以外に多くの機能をアプリに含める場合は、ページ内検索のすべてのコントロールが含まれる別のコマンド バーへのエントリ ポイントとしてトップ レベルのコマンド バーに **[検索]** ボタンを追加できます。
    -   ユーザーがタッチ キーボードを操作しているときもページ内検索のコマンド バーが表示されるようにします。 タッチ キーボードは、ユーザーが入力ボックスをタップすると表示されます。 ページ内検索のコマンド バーは、タッチ キーボードに隠れないように上へ移動する必要があります。

    -   ユーザーが表示を操作しているときもページ内検索を利用できるようにする。 ユーザーは、ページ内検索を使いながら表示内のテキストを操作する必要があります。 たとえば、ユーザーはテキストを読むために、ドキュメントを拡大表示または縮小表示したり、表示をパンしたりすることがあります。 ユーザーがページ内検索を使い始めたら、コマンド バーはページ内検索を終了するための **[閉じる]** ボタンと共に表示されたままにする必要があります。

    -   キーボード ショートカット (Ctrl + F) を有効にする。 キーボード ショートカット Ctrl + F を実装し、ページ内検索のコマンド バーをユーザーがすぐに呼び出すことができるようにします。

    -   ページ内検索機能の基本要素を含める。 ページ内検索を実装するために必要な UI 要素を次に示します。

        -   入力ボックス
        -   [前へ] ボタンと [次へ] ボタン
        -   一致数
        -   [閉じる] (デスクトップのみ)
    -   表示で一致した結果が強調表示され、スクロールして次の一致が画面に表示されるようにする。 ユーザーは、 **[前へ]** ボタンと **[次へ]** ボタンの使用、スクロール バーの使用、またはタッチによる直接操作によってドキュメントをすばやく移動できます。

    -   検索と置換の機能が基本的なページ内検索機能と共に機能するようにする。 検索と置換の機能があるアプリでは、ページ内検索が検索と置換の機能の妨げにならないようにします。

-   ページ上にあるテキスト一致数をユーザーに示すために、一致カウンターを追加します。
-   キーボード ショートカット (Ctrl + F) を有効にする。

## <a name="examples"></a>例


ページ内検索機能にアクセスする簡単な方法を提供します。 ここに示すモバイル UI の例では、展開可能なメニューで、2 つの追加コマンドの後に [ページ内を検索] が表示されています。

![ページ内検索の例 1](images/findinpage-01.png)

 

ユーザーは、[ページ内を検索] を選択してから検索語句を入力します。 検索語句の入力中に、テキスト入力候補を表示できます。

![ページ内検索の例 2](images/findinpage-02.png)

 

検索で一致するテキストがなかった場合は、結果ボックスに "検索結果が見つかりませんでした" というテキストを表示します。

![ページ内検索の例 3](images/findinpage-03.png)

 

検索で一致するテキストがあった場合は、最初の語句を区別できる色で強調表示します。以降の一致は、例に示されているように、同じカラー パレットのもう少し淡いトーンで強調表示します。

![ページ内検索の例 4](images/findinpage-04.png)

 

ページ内検索には、一致カウンターがあります。

![ページ内検索の一致カウンターの例](images/findinpage-counter.png)




## <a name="implementing-find-in-page"></a>**ページ内検索の実装**

-   ドキュメント ビューアー、リーダー、ブラウザーは、ページ内検索が提供される最も一般的なアプリの種類であり、全画面での表示/読み取りエクスペリエンスをユーザーに提供します。
-   ページ内検索機能は補助的な機能であり、コマンド バーに配置する必要があります。

コマンドをコマンド バーに追加する方法について詳しくは、「[コマンド バー](app-bars.md)」をご覧ください。

 


## <a name="related-articles"></a>関連記事

* [自動提案ボックス](auto-suggest-box.md)


 

 
