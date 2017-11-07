---
title: "圧縮テクスチャ形式"
description: "このセクションでは、圧縮テクスチャ形式の内部構造について説明します。"
ms.assetid: 24D17B9F-8CA7-4006-9E0F-178C6B3CAEC9
keywords: "圧縮テクスチャ形式"
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.openlocfilehash: 1bf94307093913c3b89b1d2a80e1e77d8dec81eb
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="compressed-texture-formats"></a>圧縮テクスチャ形式


このセクションでは、圧縮テクスチャ形式の内部構造について説明します。 圧縮形式への変換、および圧縮形式からの変換には Direct3D 関数を使用できるため、圧縮テクスチャの使用にこれらの詳細は必要ありません。 ただし、圧縮サーフェス データを直接操作する場合は、この情報が役に立ちます。

Direct3D では、テクスチャ マップを 4 x 4 のテクセル ブロックに分割する圧縮形式が使用されます。 テクスチャに透明度がない場合、つまりテクスチャが不透明な場合、または透明度が 1 ビット アルファで指定されている場合、8 バイトのブロックでテクスチャ マップ ブロックが表現されます。 テクスチャ マップに透明なテクセルが含まれており、アルファ チャネルが使用されている場合は、16 バイトのブロックでテクスチャ マップ ブロックが表されます。

単一のテクスチャはすべて、16 テクセルのグループごとにデータを 64 ビットまたは 128 ビットで格納するように指定する必要があります。 64 ビットのブロック、つまり BC1 形式をテクスチャに使用する場合、同一のテクスチャ内にブロック単位で不透明の形式と 1 ビット アルファの形式を混在させることができます。 つまり、color\_0 と color\_1 の符号なし整数の絶対値の比較が、16 テクセルのブロックごとに独立して実行されます。

128 ビット ブロックを使用する場合、テクスチャ全体にアルファ チャネルを明示的モード (BC2 形式) または補間モード (BC3 形式) で指定する必要があります。 カラーの場合と同様に、補間モードを選択すると、8 つの補間アルファまたは 6 つの補間アルファのモードをブロック単位で使用することができます。 ここでも、alpha\_0 と alpha\_1 の絶対値の比較がブロックごとに独立して実行されます。

BCn 形式のピッチは、ブロック単位ではなくバイト単位で測定されます。 たとえば、幅が 16 である場合、1 ピッチは 4 ブロックになります (BC1 の場合は 4\*8、BC2 または BC3 の場合は 4\*16)。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[圧縮テクスチャ リソース](compressed-texture-resources.md)

 

 



