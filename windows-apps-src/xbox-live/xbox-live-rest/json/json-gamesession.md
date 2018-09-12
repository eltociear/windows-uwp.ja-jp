---
title: GameSession (JSON)
assetID: 325af9ae-a9a9-5b36-8342-1aff5aff01d1
permalink: en-us/docs/xboxlive/rest/json-gamesession.html
author: KevinAsgari
description: " GameSession (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: a0ed4b66c50baa89432f44d53e313f042138b7de
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881824"
---
# <a name="gamesession-json"></a>GameSession (JSON)
マルチプレイヤー セッションのゲーム データを表す JSON オブジェクト。 
<a id="ID4ER"></a>

  
 
GameSession JSON オブジェクトには、次の仕様があります。
 
| メンバー| 種類| 説明| 
| --- | --- | --- | 
| creationTime| DateTime| 日付と、セッションが作成された、UTC で。 | 
| customData| 8 ビットの符号なし整数の配列| ゲーム固有のセッション データの 1024 バイトです。 この値は、サーバーに不透明です。 | 
| displayName| string| 表示名ゲームのセッション 128 文字の最大長。 この値は、サーバーに不透明です。 | 
| hasEnded| ブール値| セッションが終了した場合は true、それ以外の場合。 それ以上のデータがセッションに提出されたことを防止 true マーク読み取り専用とゲーム セッションにこのフィールドを設定します。 | 
| isClosed| ブール値| セッションが閉じられていていない追加のプレイヤーは、追加された、false それ以外の場合は true。 この値が true の場合は、セッションに参加するための要求が拒否されます。 | 
| maxPlayers| 32 ビットの符号付き整数| セッションを同時にすることができるプレイヤーの最大数。 値の範囲は、2 ~ 16 です。 セッションにプレイヤーの最大数が含まれているとはさらに、セッションに参加するための要求が拒否されます。 | 
| playersCanBeRemovedBy| PlayerAcl| その他のプレイヤーをセッションから削除が許可されているプレイヤーを示す値。 値は取ります、一目、および AnyPlayer です。 | 
| 名簿| プレイヤー オブジェクトの配列| セッション内のプレイヤーの配列です。 ロースターは、現在のプレイヤーとプレイヤーがセッションで以前が含まれています。 ロースター内のプレイヤーの順序は不変です。 新しいプレイヤーは、配列の末尾に追加されます。 | 
| seatsAvailable| 32 ビットの符号付き整数| プレイヤーの最大数に達する前に、セッションがまだ参加したプレイヤーの数。 この値は読み取り専用であり常に maxPlayers フィールドの値よりも少なくなります。 | 
| sessionId| string| セッションが作成されると、MPSD によって割り当てられているセッションの ID。 この値は、セッションに格納されている情報にアクセスするときに通常 URI に含められます。| 
| titleId| 32 ビットの符号なし整数| ゲーム セッションの作成、タイトルの ID です。| 
| variant| 32 ビットの符号付き整数| ゲームのバリアントです。 この値は、サーバーに不透明です。| 
| visibility| VisibilityLevel| セッションの可視性を示す値。 指定できる値は: PlayersCurrentlyInSession、PlayersEverInSession、すべてのユーザーとします。| 
  
<a id="ID4EEF"></a>

 
## <a name="sample-json-syntax"></a>JSON 構文の例
 

```json
{
    "sessionId": "702e5aaf-e7bd-4a7c-abea-9dd4be10edec",
    "titleId": 1297287259,
    "variant": 1,
    "displayName": "Contoso Cards",
    "creationTime": "2011-06-23T17:13:06Z",
    "customData": null,
    "maxPlayers": 4,
    "seatsAvailable": 4,
    "isClosed": false,
    "hasEnded": false,
    "roster": [],
    "visibility": "PlayersCurrentlyInSession",
    "playersCanBeRemovedBy": "Self",
 }
    
```

  
<a id="ID4ENF"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EPF"></a>

 
##### <a name="parent"></a>Parent 

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)

  
<a id="ID4EZF"></a>

 
##### <a name="reference"></a>リファレンス 

[GameMessage (JSON)](json-gamemessage.md)

 [GameSessionSummary (JSON)](json-gamesessionsummary.md)

 [プレイヤー (JSON)](json-player.md)

   