---
title: PeopleList (JSON)
assetID: ac538652-c10c-44e5-c1e3-5314ebe8ba83
permalink: en-us/docs/xboxlive/rest/json-peoplelist.html
author: KevinAsgari
description: " PeopleList (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 44102cb2ee1c996be9d0b42626f11a64ffb5c377
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881723"
---
# <a name="peoplelist-json"></a>PeopleList (JSON)
[ユーザー](json-person.md)オブジェクトのコレクションです。 
<a id="ID4ER"></a>

 
## <a name="peoplelist"></a>PeopleList
 
PeopleList オブジェクトには、次の仕様があります。
 
| メンバー| 種類| 説明| 
| --- | --- | --- | 
| People| [ユーザー](json-person.md)の配列| ユーザーのリストを構成する、[ユーザー](json-person.md)オブジェクトの数。| 
| totalCount| 32 ビットの符号なし整数| セットで利用できる[ユーザー](json-person.md)オブジェクトの合計数。 この値は、ページングすること、最新の応答だけでなく、セット全体のサイズを表すために、クライアントで使用できます。 値の例: 680 します。| 
  
<a id="ID4EAC"></a>

 
## <a name="sample-json-syntax"></a>JSON 構文の例
 

```json
{
    "people": [
        {
            "xuid": "2603643534573573",
            "isFavorite": true,
            "isFollowingCaller": false,
            "socialNetworks": ["LegacyXboxLive"]
        },
        {
            "xuid": "2603643534573572",
            "isFavorite": true,
            "isFollowingCaller": false,
            "socialNetworks": ["LegacyXboxLive"]
        },
        {
            "xuid": "2603643534573577",
            "isFavorite": false,
            "isFollowingCaller": false
        },
    ],
    "totalCount": 3
}
    
```

  
<a id="ID4EJC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4ELC"></a>

 
##### <a name="parent"></a>Parent 

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)

  
<a id="ID4EVC"></a>

 
##### <a name="reference"></a>リファレンス 

[取得する (/users/{ownerId} 人/)](../uri/people/uri-usersowneridpeopleget.md)

 [POST (/users/{ownerId}/ユーザー/xuid)](../uri/people/uri-usersowneridpeoplexuidspost.md)

   