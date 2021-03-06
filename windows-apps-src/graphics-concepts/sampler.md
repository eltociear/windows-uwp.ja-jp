---
title: サンプラー
description: テクスチャまたはその他のリソースから入力値を読み取るプロセスをサンプリングと呼びます。 \ 0034;サンプラー\ 0034; は、リソースから読み込まれるオブジェクトです。
ms.assetid: 7ECE13BB-9FC5-44A3-B1B2-2FE163F1D627
keywords:
- サンプラー
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: e80e160e1225e510ab95f52cbd9f21049c890457
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57663657"
---
# <a name="sampler"></a>サンプラー


テクスチャまたはその他のリソースから入力値を読み取るプロセスをサンプリングと呼びます。 ”サンプラー” は、リソースから読み込まれるオブジェクトです。

テクスチャからのサンプリングや画面領域へのレンダリングを行うと、多くの問題やアーティファクトが発生します。 たとえば、レンダリングする領域が 50 x 50 ピクセルで、テクスチャが 16 x 16 ピクセルまたは 256 x 256 ピクセルの場合、テクスチャをかなり拡大または縮小する必要があります。 このサイズの不一致が原因で不要なアーティファクトが発生します。そこで、そのようなアーティファクトを軽減するために、フィルタリング手法が使用されます。 小さいテクスチャを大きいレンダリング領域に使用する場合によく使用されるフィルタリング手法の 1 つは、"バイリニア" フィルタリングです。

レンダリング領域がビューに対して鋭角の場合、別の問題が発生します (for example, a 256 by 256 texture being rendered to a area 100 pixels wide but only 5 pixels deep because of the viewing angle). この場合は、しばしば "異方性" フィルタリングが適用されます。 異方性フィルタリングでは、適度なぼかしでエイリアシング効果を取り除けるため、バイリニア フィルタリングよりも画質は優れていますが、計算の負荷は高くなります。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ビュー](views.md)

 

 




