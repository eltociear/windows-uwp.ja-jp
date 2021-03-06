---
description: 広告ユニットの視認性を向上させる方法について説明します。
title: 広告ユニットの視認性の最適化
ms.date: 02/18/2020
ms.topic: article
keywords: windows 10, uwp, 広告, 宣伝, ガイドライン, 視認性
ms.localizationpriority: medium
ms.openlocfilehash: 06d870fbc631611bcfc453698cd9aa4fc844da5d
ms.sourcegitcommit: 71f9013c41fc1038a9d6c770cea4c5e481c23fbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77506807"
---
# <a name="optimize-the-viewability-of-your-ad-units"></a>広告ユニットの視認性の最適化

>[!WARNING]
> 2020年6月1日から、Microsoft Ad 収益化 platform for Windows UWP アプリがシャットダウンされます。 [詳細情報](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/db8d44cb-1381-47f7-94d3-c6ded3fea36f/microsoft-ad-monetization-platform-shutting-down-june-1st?forum=aiamgr)

[[広告パフォーマンス] レポート](../publish/advertising-performance-report.md)には、広告ユニットの視認性のメトリックが含まれます。 広告業界は配信されるインプレッションだけではなく見やすいインプレッションを重視する方向に移行しているため、視認性は重要なメトリックです。 広告主は見やすいインプレッションに入札する傾向があります。これは、見やすいインプレッションでは広告がユーザーによって表示される可能性が高いためです。  

IAB の視認性のガイドラインに合わせて、バナー広告のインプレッションは、次の条件を満たしている場合に見やすいとみなされます。

* ピクセル要件: 広告の 50% 以上のピクセルがアプリの表示可能領域にあった。
* 時間の要件: ピクセル要件を満たす時間が広告のレンダリング後、連続で 1 秒以上であった。

ビデオ広告インプレッションは、次の条件を満たしている場合は、見やすいとみなされます。

* ピクセル要件: 広告の 50% 以上のピクセルがアプリの表示可能部分にあった。
* 時間の要件: ビデオがピクセル要件を満たし、広告のレンダリング後、連続で 2 秒間再生された。

視認性は、次の数式を使用して計算されます。

**Viewability = [表示インプレッション] * 100/[広告インプレッションの合計]**

## <a name="guidelines-to-improve-ad-unit-viewability"></a>広告ユニットの視認性を向上させるためのガイドライン

広告ユニットの見やすいインプレッションを最適化するには、次のガイドラインに従います。

1. **パフォーマンス測定**&nbsp;&nbsp;[[広告パフォーマンス] レポート](../publish/advertising-performance-report.md)を使用して各広告ユニットの表示可能なメトリックを確認します。
2.  **広告コントロールを適切に配置**&nbsp;&nbsp;一般に、広告の最も見やすい位置は 1 面トップです (つまり、ユーザーがスクロールしないで見ることができるページの可視部分の下部です)。 ページの上部に表示される広告は、あまり見やすくありません。 ページの各要素を検証しアプリで表示可能領域を最適化できる方法を確認することを検討してください。 アプリのバック グラウンドに広告コントロールが配置されていないことを確認します。
3.  **ページの長さの管理**&nbsp;&nbsp;短いページ コンテンツは、より見やすくなります。 アプリのページを長くする必要がある場合は、無限スクロールを実装してください。
4.  **広告の位置の修正**&nbsp;&nbsp;ユーザーがスクロールしても広告が固定位置にとどまるようにしてください。 これにより、表示回数が増え、ビューアビリティ レートが向上します。
5.  **不透明度の設定**&nbsp;&nbsp;広告コントロールを含むコンテナーの不透明度が 100% に設定されていることを確認します。
6.  **遅延読み込みの実装**&nbsp;&nbsp;ユーザーが広告コントロールを含むビュー内までスクロールするまで広告を読み込まないでください。 これにより、ユーザーが表示する広告の表示時間が長くなります。
7.  **さまざまな広告サイズのテスト**&nbsp;&nbsp;いくつかの広告サイズを選択し、[[広告パフォーマンス] レポート](../publish/advertising-performance-report.md)を使用して、それぞれの広告の視認性を測定します。 最適に機能する広告サイズを選択します。
8.  **アプリの設計の再確認**&nbsp;&nbsp;アプリ ページ設計を強化し、ページの読み込み時間を短縮してください。 ユーザーは、迅速に読み込まれるページにより長くとどまる傾向があります。
