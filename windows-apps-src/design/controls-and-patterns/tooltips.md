---
author: Jwmsft
Description: Use a tooltip to reveal more info about a control before asking the user to perform an action.
title: ヒント
ms.assetid: A21BB12B-301E-40C9-B84B-C055FD43D307
label: Tooltips
template: detail.hbs
ms.author: jimwalk
ms.date: 05/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP
pm-contact: yulikl
design-contact: kimsea
dev-contact: stpete
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: dfd702f9ba6e28e1902ea8e595287ba10b46f4bb
ms.sourcegitcommit: 588171ea8cb629d2dd6aa2080e742dc8ce8584e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
ms.locfileid: "1895284"
---
# <a name="tooltips"></a>ヒント

ヒントは、他のコントロールまたはオブジェクトにリンクされた短い説明です。 ヒントを使うと、UI では直接説明されていない、なじみのないオブジェクトをユーザーが理解しやすくなります。 ヒントは、ユーザーがコントロールにフォーカスを移動する、コントロール上で長押しする、またはマウス ポインターをコントロール上にホバーすると、自動的に表示されます。 また、ヒントは数秒経過するか、ユーザーが指、ポインター、またはキーボード/ゲームパッドのフォーカスを移動すると消えます。

![ヒント](images/controls/tool-tip.png)

> **重要な API**: [ToolTip クラス](/uwp/api/Windows.UI.Xaml.Controls.ToolTip)、[ToolTipService クラス](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.tooltipservice)

## <a name="is-this-the-right-control"></a>適切なコントロールの選択

ユーザーに操作の実行を指示する前に、ヒントを使ってコントロールに関する詳しい情報を表示します。 ヒントは慎重に使い、タスクを完了しようとしているユーザーにとって明らかに重要である場合にのみ追加します。 1 つの目安は、情報が同じエクスペリエンスのどこかで入手できる場合、ヒントは必要ありません。 価値あるヒントによって、不明瞭な操作を明確にします。

ヒントはどのような場合に使えばよいでしょうか。 それを判断するには、以下の質問を考えます。

- **情報はポインターのホバーに基づいて表示すべきですか?**
    そうでない場合は、別のコントロールを使います。 ヒントは、ユーザーの操作の結果としてのみ表示します。自動的には表示しません。

- **コントロールにはテキスト ラベルがありますか?**
    ない場合は、ヒントを使ってラベルを表示します。 UX の設計では、ほとんどのコントロールにインラインでラベルを付けることをお勧めします。それらのコントロールには、ヒントは必要ありません。 アイコンだけが表示されるツール バー コントロールとコマンド ボタンには、ヒントが必要です。

- **説明や追加情報がオブジェクトに対して役立ちますか?**
    そうであれば、ヒントを使います。 ただし、このテキストは、主要なタスクに必須なものではなく、補助的なものである必要があります。 必須なものであれば、直接 UI に配置して、ユーザーが探さなくても済むようにします。

- **表示する補助的な情報は、エラー、警告、または状態ですか?**
    その場合は、ポップアップなど、他の UI 要素を使います。

- **ユーザーがヒントを操作する必要がありますか?**
    その場合は、別のコントロールを使います。 ヒントはマウスを動かすと消えるため、ユーザーはヒントを操作できません。

- **ユーザーが補助的な情報を印刷する必要がありますか?**
    その場合は、別のコントロールを使います。

- **ユーザーがヒントを煩わしいと感じますか?**
    その場合は、別の手段を使うことを検討します。何もしない、という選択肢もあります。 煩わしいと感じる可能性があってもヒントを使う場合は、ユーザーがヒントをオフにできるようにします。

## <a name="example"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/ToolTip">アプリを開き、ToolTip の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlUIBasics">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

Bing 地図アプリのヒントです。

![Bing 地図アプリのヒントです](images/control-examples/tool-tip-maps.png)

## <a name="create-a-tooltip"></a>ToolTip の作成

[ToolTip](/uwp/api/Windows.UI.Xaml.Controls.ToolTip) は、その所有者である別の UI 要素に割り当てる必要があります。 [ToolTipService](/uwp/api/windows.ui.xaml.controls.tooltipservice) クラスは静的メソッドを提供し、ToolTip を表示します。

XAML では、**ToolTipService.Tooltip** 添付プロパティを使用して ToolTip を所有者に割り当てます。

```xaml
<Button Content="Submit" ToolTipService.ToolTip="Click to submit"/>
```

コードで、[ToolTipService.SetToolTip](/uwp/api/windows.ui.xaml.controls.tooltipservice.settooltip) メソッドを使用して ToolTip を所有者に割り当てます。

```xaml
<Button x:Name="submitButton" Content="Submit"/>
```

```csharp
ToolTip toolTip = new ToolTip();
toolTip.Content = "Click to submit";
ToolTipService.SetToolTip(submitButton, toolTip);
```

### <a name="content"></a>コンテンツ

任意のオブジェクトを ToolTip の[コンテンツ](/uwp/api/windows.ui.xaml.controls.contentcontrol.content)として使用できます。 ToolTip で[イメージ](/uwp/api/windows.ui.xaml.controls.image)を使用する例を次に示します。

```xaml
<TextBlock Text="store logo">
    <ToolTipService.ToolTip>
        <Image Source="Assets/StoreLogo.png"/>
    </ToolTipService.ToolTip>
</TextBlock>
```

### <a name="placement"></a>配置

既定では、ToolTip はポインターの上部に中央揃えで表示されます。 配置はアプリ ウィンドウによって制約されていないため、ToolTip が部分的に表示されたり、完全にアプリ ウィンドウの境界の外部に表示されたりすることがあります。

ToolTip が参照しているコンテンツを隠している場合は、配置を調整できます。 [Placement](/uwp/api/windows.ui.xaml.controls.tooltip.placement) プロパティまたは **ToolTipService.Placement** 添付プロパティを使用してポインターの上下または左右に ToolTip を配置します。 [VerticalOffset](/uwp/api/windows.ui.xaml.controls.tooltip.verticaloffset) プロパティと [HorizontalOffset](/uwp/api/windows.ui.xaml.controls.tooltip.horizontaloffset) プロパティを設定してポインターと ToolTip 間の距離を変更することができます。

```xaml
<!-- A TextBlock with an offset ToolTip. -->
<TextBlock Text="TextBlock with an offset ToolTip.">
    <ToolTipService.ToolTip>
        <ToolTip Content="Offset ToolTip."
                 HorizontalOffset="20" VerticalOffset="30"/>
    </ToolTipService.ToolTip>
</TextBlock>
```

## <a name="recommendations"></a>推奨事項

- ヒントは慎重に使います (または使わない)。 ヒントは作業の中断になります。 ヒントはポップアップと同じように煩わしい場合があるため、大きな付加価値がない限り使わないでください。
- ヒントのテキストは簡潔なものにします。 ヒントは短い文やフレーズに適しています。 大きなテキストのまとまりは圧迫感を与えることがあり、ユーザーが読み終える前にヒントがタイムアウトする可能性があります。
- 役に立つ補足的なヒント テキストを作成します。 ヒントのテキストは、情報として役に立つ必要があります。 表示しなくても明らかな情報や、既に画面上に表示されている内容の繰り返しなどは避けます。 ヒントのテキストは常に表示されているわけではないため、ユーザーが必ずしも読まなくても問題がないような、補足的な情報である必要があります。 重要な情報は、名前から判別できるコントロール ラベルを使うか、補足的なテキストを適切な場所に配置することで伝えるようにします。
- 状況に応じて画像を使います。 ヒント内に画像を使うとよい場合もあります。 たとえば、ユーザーがハイパーリンクの上にカーソルを置いたときに、ヒントを使ってリンク先ページのプレビューを表示できます。
- 既に UI に表示されているテキストは、ヒントとして表示しないでください。 たとえば、ボタンと同じテキストを表示するヒントをボタンに表示しないでください。
- ヒント内に対話的なコントロールを配置しないでください。
- 対話的に見えるような画像をヒント内に配置しないでください。

## <a name="get-the-sample-code"></a>サンプル コードを入手する

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlUIBasics) - インタラクティブな形で XAML コントロールのすべてを参照できます。

## <a name="related-articles"></a>関連記事

- [ToolTip クラス](https://msdn.microsoft.com/library/windows/apps/br227608)