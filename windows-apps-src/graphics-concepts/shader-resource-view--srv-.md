---
title: "シェーダー リソース ビュー (SRV) と順序指定されていないアクセス ビュー (UAV)"
description: "シェーダー リソース ビューは、通常、シェーダーがアクセスできる形式でテクスチャをラップします。 順序指定されていないアクセス ビューも同様の機能を提供しますが、任意の順序で、テクスチャ (やその他のリソース) の読み取りや書き込みを行うことができます。"
ms.assetid: 4505BCD2-0EDA-40F2-887C-EC081FE32E8F
keywords: "シェーダー リソース ビュー (SRV)"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.openlocfilehash: 2413c37dc7a19f110597a4e5664c6d4ac7b5508c
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="shader-resource-view-srv-and-unordered-access-view-uav"></a>シェーダー リソース ビュー (SRV) と順序指定されていないアクセス ビュー (UAV)


シェーダー リソース ビューは、通常、シェーダーがアクセスできる形式でテクスチャをラップします。 順序指定されていないアクセス ビューも同様の機能を提供しますが、任意の順序で、テクスチャ (やその他のリソース) の読み取りや書き込みを行うことができます。

テクスチャを 1 つだけラップするのが、おそらく最もシンプルなシェーダー リソース ビューの形です。 より複雑な例としては、サブリソース (ミップマップ テクスチャの個々の配列、プレーン、または色)、3D テクスチャ、1D テクスチャのグラデーションなどのコレクションがあります。

順序指定されていないアクセス ビューは、パフォーマンスの面ではややコストが高くなりますが、たとえばテクスチャの読み取りと同時に書き込みをすることができます。 そのため、更新されたテクスチャをグラフィック パイプラインによって他の目的に再利用できます。 シェーダー リソース ビューは、読み取り専用です (これは、最も一般的なリソースの使い方です)。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ビュー](views.md)

 

 



