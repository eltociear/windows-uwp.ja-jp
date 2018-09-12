---
title: inventoryItem (JSON)
assetID: 446cca28-b2d3-1b84-f973-94065519b391
permalink: en-us/docs/xboxlive/rest/json-inventoryitem.html
author: KevinAsgari
description: " inventoryItem (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 0a7521de7da4ebd31f0a1d8c59bb7c0134eddc08
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881560"
---
# <a name="inventoryitem-json"></a>inventoryItem (JSON)
コアのインベントリ項目の権利を付与できる標準の項目を表します。
<a id="ID4EN"></a>


## <a name="inventoryitem"></a>inventoryItem

InventoryItem オブジェクトには、次の仕様があります。

| メンバー| 種類| 説明|
| --- | --- | --- |
| url| string| この特定のインベントリ項目の一意の識別子。|
| itemType| string| 項目の種類。 現在の値します。 <ul><li><b>Unknown</b></li><li><b>Game</b></li><li><b>映画</b></li><li> <b>TVShow</b></li><li><b>MusicVideo</b></li><li><b>GameTrial</b></li><li><b>ViralVideo</b></li><li><b>TVEpisode</b></li><li><b>TVSeason</b></li><li><b>TVSeries</b></li><li><b>VideoPreview</b></li><li><b>ポスター</b></li><li><b>ポッド キャスト</b></li><li><b>画像</b></li><li><b>BoxArt</b></li><li><b>ArtistPicture</b></li><li><b>GameContent</b></li><li><b>GameDemo</b></li><li><b>テーマ</b></li><li><b>XboxOriginalGame</b></li><li><b>GamerTile</b></li><li><b>ArcadeGame</b></li><li><b>GameConsumable</b></li><li><b>アルバム</b></li><li><b>AlbumDisc</b></li><li><b>AlbumArt</b></li><li><b>GameVideo</b></li><li><b>BackgroundArt</b></li><li><b>TVTrailer</b></li><li><b>GameTrailer</b></li><li><b>VideoShort</b></li><li><b>バンドル</b></li><li><b>XnaCommunityGame</b></li><li><b>プロモーション</b></li><li><b>MovieTrailer</b></li><li><b>SlideshowPreviewImage</b></li><li><b>ServerBackedGames</b></li><li><b>Marketplace</b></li><li><b>AvatarItem</b></li><li><b>LiveApp</b></li><li><b>WebGame</b></li><li><b>MobileGame</b></li><li><b>MobilePdlc</b></li><li><b>MobileConsumable</b></li><li><b>App</b></li><li><b>MetroGame</b></li><li><b>MetroGameContent</b></li><li><b>MetroGameConsumable</b></li><li><b>GameLayer</b></li><li><b>GameActivity</b></li><li><b>GameV2</b></li><li><b>SubscriptionV2</b></li><li><b>サブスクリプション</b><br/><br/> **注:** ゲームが**GameV2**によって指定される、コンシューマブルなアドオンです**GameConsumable**、および永続的な DLC は**GameContent**します。 |
  | コンテナー | string | これは、この項目が含まれる「コンテナー」のセットです。 特定のコンテナーに参加している項目のユーザーのインベントリを照会できます。 これらのコンテナーは、購入して、項目がインベントリに追加されるときに決定されます。 |
  | 取得 | DateTime | 日付と時刻の項目は、ユーザーのインベントリに追加されました。 |
  | startDate | DateTime | 日付と時刻になった、または使用可能になります。 |
  | endDate | DateTime | 日付と時刻になった、または使用できなくなります。 |
  | 状態 | string | 項目の状態。 値は、**有効になっている**、**中断**、**有効期限切れ**、**取り消される**と、**更新**を許可します。  |
  | trial | ブール値 | 必須。 この権利が; 試用版である場合は true。それ以外の場合は false です。 権利の試用版を購入し、通常版を購入する場合は、両方が表示されます。 |
  | trialTimeRemaining | TimeSpan | Null 許容されます。 どのくらいの時間は、分単位で、試用版に残っています。 |
  | コンシューマブル | array | 項目がコンシューマブルの場合は、その現在の数量と同様に、コンシューマブルなインベントリ項目の一意の識別子 (リンク) の場合は、なインライン表現が含まれます。 |

<a id="ID4EMAAC"></a>


## <a name="sample-json-syntax"></a>JSON 構文の例


```json
inventoryItem {
  "url": string,
  "itemType": "Music" | "Video" | "Game" | "AvatarItem" | "Subscription" | "DLC" | "Consumable" | ...,
  "obtained": DateTime,
  "beginDate": DateTime,
  "endDate": DateTime,
  "state": "Unavailable" | "Available" | "Suspended" | "Expired",
  "trial": true,
  "trialTimeRemaining":"23:12:14",
  ("consumable": {"url": string, "quantity": int})
}

```


<a id="ID4EVAAC"></a>


## <a name="consumable-inventory-item"></a>コンシューマブルなインベントリ項目

コンシューマブルなエンティティでは、コンシューマブルの項目のプロパティの最小セットを表示します。

| メンバー| 種類| 説明|
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| url| string| 特定のコンシューマブルなインベントリ項目の一意の識別子。|
| quantity| 32 ビットの符号付き整数| このインベントリ項目の現在の数量。|


```json
consumableInventoryItem {
  "url": string,
  "quantity": int
}

```


<a id="ID4E4BAC"></a>


## <a name="see-also"></a>関連項目

<a id="ID4E6BAC"></a>


##### <a name="parent"></a>Parent

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)


<a id="ID4EJCAC"></a>


##### <a name="reference"></a>リファレンス

[/users/me/inventory](../uri/marketplace/uri-inventory.md)

 [インベントリ/コンシューマブル/{itemID}/](../uri/marketplace/uri-inventoryconsumablesitemurl.md)

 [/inventory/{itemID}](../uri/marketplace/uri-inventoryitemurl.md)