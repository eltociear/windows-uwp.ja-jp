---
title: ユーザー/me/コンシューマブル/{itemID}
assetID: 45724827-5e35-326f-3f17-f49e606d9e08
permalink: en-us/docs/xboxlive/rest/uri-inventoryconsumablesitemurl.html
author: KevinAsgari
description: ユーザーの Xbox コンシューマブルの項目の rESTful エンドポイントです。
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 7ed278542fa538a1297069b0f7d67d413e180f30
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881724"
---
# <a name="usersmeconsumablesitemid"></a>ユーザー/me/コンシューマブル/{itemID}
特定のコンシューマブルなインベントリ項目の詳細情報の完全なセットにアクセスします。
これらの Uri のドメインが`inventory.xboxlive.com`します。

  * [URI パラメーター](#ID4EV)

<a id="ID4EV"></a>


## <a name="uri-parameters"></a>URI パラメーター

| パラメーター| 型| 説明|
| --- | --- | --- |
| itemID| string| 単一のインベントリ項目の各ユーザーに一意の ID|

<a id="ID4ERB"></a>


## <a name="valid-methods"></a>有効なメソッド

[POST ({itemID})](uri-inventoryconsumablesitemurlpost.md)

&nbsp;&nbsp;または、コンシューマブルなインベントリ項目の一部が使用されていることを示しますとデクリメント、要求された時間の長さによって、コンシューマブルの数量。

<a id="ID4E4B"></a>


## <a name="see-also"></a>関連項目

<a id="ID4E6B"></a>


##### <a name="parent"></a>Parent

[Marketplace Uri](atoc-reference-marketplace.md)


<a id="ID4EJC"></a>


##### <a name="further-information"></a>詳細情報

[EDS 一般的なヘッダー](../../additional/edscommonheaders.md)

 [EDS パラメーター](../../additional/edsparameters.md)

 [EDS は、絞り込み条件をクエリします。](../../additional/edsqueryrefiners.md)

 [その他の参照](../../additional/atoc-xboxlivews-reference-additional.md)