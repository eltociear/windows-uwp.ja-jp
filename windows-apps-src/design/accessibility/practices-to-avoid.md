---
author: Xansky
Description: Lists the practices to avoid if you want to create an accessible Universal Windows Platform (UWP) app.
ms.assetid: 024A9B70-9821-45BB-93F1-61C0B2ECF53E
title: アクセシビリティ対応にするために避ける事項
label: Accessibility practices to avoid
template: detail.hbs
ms.author: mhopkins
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: dc7a7592a47556cb9ae65cdc559a301ee9b25997
ms.sourcegitcommit: 0ab8f6fac53a6811f977ddc24de039c46c9db0ad
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
ms.locfileid: "1652931"
---
# <a name="accessibility-practices-to-avoid"></a>アクセシビリティ対応にするために避ける事項

アクセシビリティ対応のユニバーサル Windows プラットフォーム (UWP) アプリを作成する際は、こちらの避ける事項の一覧をご覧ください。 

* **既定の Windows コントロールか、Microsoft UI オートメーション サポートを既に実装しているコントロールを使うことができる場合には、カスタム UI 要素を作成しないようにします。** Windows の標準コントロールは、既定でアクセシビリティに対応しており、追加する必要があるのは、通常、アプリ固有のわずかなアクセシビリティ属性のみです。 それに対し、純粋なカスタム コントロールに [**AutomationPeer**](https://msdn.microsoft.com/library/windows/apps/BR209185) サポートを実装するのは、これより複雑です (「[カスタム オートメーション ピア](custom-automation-peers.md)」をご覧ください)。
* **静的テキストなどの非対話型の要素をタブ オーダーに含めないようにします** (たとえば、対話的に操作できない要素に[ **TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) プロパティを設定することは避けます)。 非対話型の要素をタブ オーダーに含めると、キーボード ナビゲーションの効率が下がるため、キーボードのアクセシビリティ ガイドラインで推奨されていません。 多くの支援技術では、支援技術のユーザーにアプリのインターフェイスを表示する方法に関するロジックの一部として、要素をフォーカスする機能とタブ オーダーが使われています。 タブ オーダーにテキスト専用要素が含まれると、タブ オーダーに対話型の要素 (ボタン、チェック ボックス、テキスト入力フィールド、コンボ ボックス、リストなど) しか含まれていないと想定しているユーザーを混乱させる可能性があります。
* **UI 要素の絶対配置 ([**Canvas**](https://msdn.microsoft.com/library/windows/apps/BR209267) 要素内など) は、しばしば表示の順序が (事実上の論理的な順序である) 子要素の宣言の順序と異なるため、使用を避けます。** スクリーン リーダーが UI 要素を正しい順序で読み取ることができるように、これらの要素をできるだけドキュメントの順序または論理的な順序に並べます。 UI 要素の視覚的な順序がドキュメントの順序または論理的な順序とは異なる可能性がある場合は、正しい読み取り順序を定義するために明示的なタブ インデックス値 ([**TabIndex**](https://msdn.microsoft.com/library/windows/apps/BR209461) に設定) を使います。
* **色を情報を伝える唯一の手段として使わないようにします。** 色覚に障碍があるユーザーは、色によるステータス インジケーターのような色を通じてのみ伝えられる情報は受け取ることができません。 他の視覚的な合図 (テキストが望ましい) を含めるようにして、情報にアクセスできるようにします。
* アプリの機能に本当に必要でない限り、**アプリのキャンバス全体を自動的に更新しないようにします。** ページの内容を自動的に更新する必要がある場合には、ページの一部の領域だけを更新するようにします。 支援技術では通常、更新されたアプリのキャンバスは、実質的な変更がわずかな場合でも、完全に新しい構造であると見なす必要があります。 このため、更新されたアプリのドキュメント ビューや説明を再作成し、支援技術を使うユーザーに再提示する必要があります。
  
  ユーザーが開始する意図的なページのナビゲーションによってアプリの構造が更新されることは、問題ありません。 ただし、ナビゲーションを開始する UI 項目に適切な ID または名前を設定し、呼び出すとコンテキストが変更されてページが再読み込みされることがわかるようにしてください。

  > [!NOTE]
  > 領域内のコンテンツを更新する場合は、要素上の [**AccessibilityProperties.LiveSetting**](https://msdn.microsoft.com/library/windows/apps/JJ191516) アクセシビリティ プロパティを既定以外の設定である **Polite** または **Assertive** に設定することをお勧めします。 支援技術の中には、ライブ領域の Accessible Rich Internet Applications (ARIA) 概念にこの設定をマップして、コンテンツの領域が変更されたことをユーザーに通知できるものもあります。

* **1 秒間に 4 回以上光る UI 要素は使わないようにします。** 明滅する要素は一部の人にとって発作を起こす原因になります。 明滅する UI 要素の使用は避けた方が良いでしょう。
* **ユーザー コンテキストを変えたり自動的に機能をアクティブ化しないようにします。** コンテキストやアクティブ化の変更は、フォーカスのある UI 要素上でユーザーが直接操作したときにだけ行うようにします。 ユーザー コンテキストの変更には、フォーカスの変更、新しいコンテンツの表示、別のページへの移動が含まれます。 ユーザーと無関係に行われるコンテキストの変更は、障碍のあるユーザーを混乱させる可能性があります。 この要件の例外としては、サブメニューの表示、フォームの検証、別のコントロールでのヘルプ テキストの表示、非同期イベントへの応答によるコンテキストの変更などがあります。

<span id="related_topics"/>

## <a name="related-topics"></a>関連トピック  
* [アクセシビリティ](accessibility.md)
* [ストア内のアクセシビリティ](accessibility-in-the-store.md)
* [アクセシビリティのチェック リスト](accessibility-checklist.md)