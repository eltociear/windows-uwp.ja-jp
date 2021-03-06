---
title: マルチパス テクスチャ ブレンド
description: Direct3D アプリケーションでは、複数のレンダリング パスでさまざまなテクスチャを 1 つのプリミティブに適用することで、多彩な特殊効果を実現することができます。
ms.assetid: FB4D6E3F-4EF5-4D20-BF7E-1008E790E30C
keywords:
- マルチパス テクスチャ ブレンド
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: d6b1e8958874ede50a18f2d2446c8f156361210e
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57589897"
---
# <a name="multipass-texture-blending"></a>マルチパス テクスチャ ブレンド


Direct3D アプリケーションでは、複数のレンダリング パスでさまざまなテクスチャを 1 つのプリミティブに適用することで、多彩な特殊効果を実現することができます。 これは、一般に*マルチパス テクスチャ ブレンド*と呼ばれます。 通常、マルチパス テクスチャ ブレンドは、さまざまなテクスチャから複数のカラーを適用して、複雑なライティング モデルやシェーディング モデルの効果をエミュレートするために使用されます。 このような適用は*ライト マッピング*と呼ばれます。 「[テクスチャでのライト マッピング](light-mapping-with-textures.md)」をご覧ください。

**注**  デバイスによっては、複数のテクスチャを適用する単一のパスでプリミティブに対応します。 「[テクスチャ ブレンド](texture-blending.md)」をご覧ください。

 

ユーザーのハードウェアで複数テクスチャ ブレンドがサポートされていない場合、アプリケーションはマルチパス テクスチャ ブレンドを使って同じ視覚効果を実現できます。 ただし、アプリケーションは複数テクスチャ ブレンドを使ったときに生じる可能性があるフレーム レートに対応できません。

C/C++ アプリケーションでマルチパス テクスチャ ブレンドを実行するには

1.  テクスチャ ステージ 0 でテクスチャを設定します。
2.  必要な色およびアルファ ブレンドの引数と操作を選択します。 既定の設定は、マルチパス テクスチャ ブレンドに最適です。
3.  シーン内の適切なオブジェクトをレンダリングします。
4.  テクスチャ ステージ 0 で次のテクスチャを設定します。
5.  レンダー状態を設定し、必要に応じてソース ブレンドとターゲット ブレンドを調整します。 システムが、これらのパラメーターに従って、レンダー ターゲット サーフェスで新しいテクスチャと既存のピクセルをブレンドします。
6.  必要な数のテクスチャに対して手順 3、4、5 を繰り返します。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[テクスチャのブレンド](texture-blending.md)

 

 




