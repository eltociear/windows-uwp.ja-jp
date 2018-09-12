---
title: XuidList (JSON)
assetID: 06938a52-e582-a15b-ec7f-4b053dfc28ad
permalink: en-us/docs/xboxlive/rest/json-xuidlist.html
author: KevinAsgari
description: " XuidList (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 3853140ce5e7c3f7710f489709945fc70b6703b4
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881737"
---
# <a name="xuidlist-json"></a>XuidList (JSON)
操作を実行するに Xuid のリスト。 
<a id="ID4EN"></a>

 
## <a name="xuidlist"></a>XuidList
 
XuidList オブジェクトには、次の仕様があります。
 
| メンバー| 種類| 説明| 
| --- | --- | --- | 
| xuid| 文字列の配列| 操作を実行する必要がありますまたは返されるデータの Xbox ユーザー ID (XUID) 値の一覧。| 
  
<a id="ID4EMB"></a>

 
## <a name="sample-json-syntax"></a>JSON 構文の例
 

```json
{
    "xuids": [
        "2533274790395904", 
        "2533274792986770", 
        "2533274794866999"
    ]
}
    
```

  
<a id="ID4EVB"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EXB"></a>

 
##### <a name="parent"></a>Parent 

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)

  
<a id="ID4EBC"></a>

 
##### <a name="reference"></a>リファレンス 

[POST (/users/{ownerId}/ユーザー/xuid)](../uri/people/uri-usersowneridpeoplexuidspost.md)

   