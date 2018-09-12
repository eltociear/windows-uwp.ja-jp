---
title: ユーザー/xuid (xuid)//ピン/{リスト} の一覧を示します
assetID: b6421b11-fcd1-cfdb-c1fa-6cab3dab89d9
permalink: en-us/docs/xboxlive/rest/uri-usersxuidlistspinslistname.html
author: KevinAsgari
description: " ユーザー/xuid (xuid)//ピン/{リスト} の一覧を示します"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 052a83f47dc2d5b692c811850e41381c4745815c
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882340"
---
# <a name="usersxuidxuidlistspinslistname"></a>ユーザー/xuid (xuid)//ピン/{リスト} の一覧を示します
リストの項目にアクセスします。 これらの Uri のドメインが`eplists.xboxlive.com`します。
 
  * [URI パラメーター](#ID4EV)
 
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | 
| xuid| string| Xbox ユーザー ID (XUID)。| 
| listtype| string| (その使用方法と動作) の一覧の種類です。 常に「ピン」これらのメソッドを関連します。| 
| リスト| string| 一覧の名前 (際に特定の listtype の一覧がどの)。 常に"XBLPins"の項目を Pin にします。| 
  
<a id="ID4EGC"></a>

 
## <a name="valid-methods"></a>有効なメソッド

[DELETE](uri-usersxuidlistspinslistnamedelete.md)

&nbsp;&nbsp;一覧から項目を削除します。

[GET](uri-usersxuidlistspinslistnameget.md)

&nbsp;&nbsp;リストの内容を返します。

[POST](uri-usersxuidlistspinslistnamepost.md)

&nbsp;&nbsp;クエリ文字列パラメーター **insertIndex**に基づいてインデックスの一覧に項目を挿入します。

[PUT](uri-usersxuidlistspinslistnameput.md)

&nbsp;&nbsp;要求本文内の各項目に指定されたインデックスに従ってリスト内の項目を更新します。
 
<a id="ID4EZC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4E2C"></a>

 
##### <a name="parent"></a>Parent 

[ユニバーサル リソース識別子 (URI) の参照](../atoc-xboxlivews-reference-uris.md)

   