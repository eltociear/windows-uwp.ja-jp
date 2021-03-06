---
Description: Windows アプリでセカンダリタイルを使用するタイミングと場所について説明します。
title: セカンダリタイルの設計ガイダンス
label: Secondary tiles
template: detail.hbs
ms.date: 05/25/2017
ms.topic: article
keywords: Windows 10、UWP、セカンダリ タイル、ガイダンス、ガイドライン、ベスト プラクティス
ms.localizationpriority: medium
ms.openlocfilehash: 400b0d48fd68c720d613325d1938c0c4a70931a7
ms.sourcegitcommit: 0dee502484df798a0595ac1fe7fb7d0f5a982821
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82971027"
---
# <a name="secondary-tile-guidance"></a>セカンダリ タイルのガイダンス


セカンダリ タイルを使うと、スタート メニューからアプリ内の特定の領域に、一貫した方法で効率的に直接アクセスすることができます。 ユーザーはセカンダリ タイルをスタート メニューに "ピン留め" するかどうかを選択できますが、アプリ内のピン留めできる領域は開発者によって決められます。 詳しくは、「[セカンダリ タイルの概要](secondary-tiles.md)」をご覧ください。 アプリでセカンダリ タイルを有効にし、関連する UI を設計するときは、次のガイドラインを考慮してください。

> [!NOTE]
> セカンダリ タイルをスタート メニューにピン留めできるのはユーザーだけです。アプリでプログラムによってピン留めすることはできません。 タイルの削除もユーザーがコントロールし、セカンダリ タイルをスタート メニューや親アプリ内から削除することができます。


## <a name="recommendations"></a>Recommendations

アプリでセカンダリ タイルを有効にするときは、以下の推奨事項を考慮してください。

* 対象のコンテンツがピン留めできる場合は、セカンダリ タイルを作る [スタートにピン留めする] ボタンをアプリ バーに表示する必要があります。
* ユーザーが [スタートにピン留めする] をクリックした場合、UI スレッドから直ちに API を呼び出して、[セカンダリ タイルをピン留め](secondary-tiles-pinning.md)する必要があります。
* 対象のコンテンツが既にピン留めされている場合は、アプリ バーの [スタートにピン留めする] ボタンを [スタートからピン留めを外す] ボタンに置き換えます。 [スタートからピン留めを外す] ボタンは、既存のセカンダリ タイルを削除する必要があります。
* 対象のコンテンツがピン留めできない場合は、[スタートにピン留めする] ボタンを表示しません (または、[スタートにピン留めする] ボタンを無効にします)。
* [スタートにピン留めする] ボタンと [スタートからピン留めを外す] ボタンには、システムが提供するグリフを使います (Windows.UI.Xaml.Controls.Symbol または WinJS.UI.AppBarIcon のピン留めとピン止め解除のメンバーをご覧ください)。
* ボタンのテキストは標準の "スタートにピン留めする" と "スタートからピン留めを外す" を使います。 システムによって提供されるピン留めとピン留め解除のグリフを使うときは、既定のテキストをオーバーライドする必要があります。
* "次のトラックにスキップ" タイルのように、親アプリと対話するための、事実上のコマンド ボタンとしてセカンダリ タイルを使わないでください。


## <a name="additional-usage-guidance-for-devs"></a>開発者向けのその他の使い方のガイダンス

* アプリの起動時には、常にセカンダリ タイルを列挙する必要があります。セカンダリ タイルの追加や削除を把握していない場合があるためです。 スタート画面のアプリ バーを使ってセカンダリ タイルを削除すると、タイトルも削除されます。 セカンダリ タイルによって使われていたリソースは、アプリ自体で解放する必要があります。 クラウドを通じてセカンダリ タイルがコピーされた場合、セカンダリ タイル上のタイルまたはバッジの現在の通知、スケジュールされた通知、プッシュ通知チャネル、定期的な通知で使われる URI (Uniform Resource Identifier) はタイルと共にコピーされないので、再設定する必要があります。
* アプリでは、セカンダリ タイルに意味のある再作成可能な一意の ID を使う必要があります。 アプリにとって意味のある予測可能なセカンダリ タイル ID を使うことにより、新しいコンピューターの新規インストールでセカンダリ タイルが表示されたときに、アプリはそれらのタイルで実行する処理を判断できるようになります。
  * 実行時に、アプリは特定のタイルが存在するかどうかを照会できます。
  * セカンダリ タイルのプラットフォームに、特定のアプリに属するすべてのセカンダリ タイルのセットを返すよう要求できます。 これらのタイルに意味のある一意の ID を使うことにより、アプリはセカンダリ タイルのセットを調べ、適切なアクションを実行できます。 たとえば、ソーシャル メディア アプリの場合、ID によってタイルの作成対象である個々の連絡先を識別できます。
* スタート画面のすべてのタイルと同様に、セカンダリ タイルは新しいコンテンツで頻繁に更新できる動的な表示機能です。 セカンダリ タイルでは、他のタイルと同じメカニズムを使って通知や最新情報を表示できます。 詳しくは、「[通知配信方法の選択](choosing-a-notification-delivery-method.md)」をご覧ください。


## <a name="related"></a>関連項目

* [セカンダリ タイルの概要](secondary-tiles.md)
* [セカンダリ タイルをピン留めする](secondary-tiles-pinning.md)
* [タイル アセット](app-assets.md)
* [タイル コンテンツのドキュメント](create-adaptive-tiles.md)
* [ローカル タイル通知の送信](sending-a-local-tile-notification.md)
