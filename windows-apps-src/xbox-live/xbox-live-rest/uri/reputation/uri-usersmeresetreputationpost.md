---
title: POST (/ユーザー/me/resetreputation)
assetID: 1a4fed45-f608-dac2-3384-2ee493112f7b
permalink: en-us/docs/xboxlive/rest/uri-usersmeresetreputationpost.html
author: KevinAsgari
description: " POST (/ユーザー/me/resetreputation)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 1a8bfe8a76b83c78886c48f7e15de274fe89a52a
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882418"
---
# <a name="post-usersmeresetreputation"></a>POST (/ユーザー/me/resetreputation)
により、実施チームは、アカウント ハイジャック (たとえば) した後、いくつかの任意の値を現在のユーザーの評判スコアを設定します。 これらの Uri のドメインが`reputation.xboxlive.com`します。
 
  * [注釈](#ID4EV)
  * [Authorization](#ID4E5)
  * [必要な要求ヘッダー](#ID4ETB)
  * [要求本文](#ID4END)
  * [HTTP ステータス コード](#ID4EDE)
  * [応答本文](#ID4EFH)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>注釈
 
このメソッドは、Retail を除くすべてのサンド ボックスの他のすべてのパートナーとテスト目的で、Retail を除くすべてのサンド ボックス内のユーザーによっても呼び出すことがあります。 この要求は、「基本」評判スコアをユーザーに設定し、肯定的なフィードバック良い評価の彼は重みをすべて消去アウトことに注意してください。この呼び出しを行った後、ユーザーの実際の評判は、基本スコアと自分のアンバサダー ボーナスと自分のフォロワー ボーナスになります。
  
<a id="ID4E5"></a>

 
## <a name="authorization"></a>Authorization
 
パートナーから: **PartnerClaim**実施チームから、市販のサンド ボックスすべてのサンド ボックスに対して、 **PartnerClaim**します。
 
ユーザーから: 製品版、 **XuidClaim** **TitleClaim**を除くすべてのサンド ボックスにします。
  
<a id="ID4ETB"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
すべて:**コンテンツの種類: アプリケーション/json**します。
 
パートナーから: **X Xbl コントラクト バージョン**(現在のバージョンは 101)、 **X-Xbl のサンド ボックス**。
 
ユーザーから: **X Xbl コントラクト バージョン**(現在のバージョンは 101)。
 
| ヘッダー| 型| 説明| 
| --- | --- | --- | 
| Authorization| string| HTTP の認証の資格情報を認証します。 値の例:"XBL3.0 x =&lt;userhash > です。&lt;トークン >"。| 
| X RequestedServiceVersion|  | この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求はのみにルーティングすると、サービスの認証トークンを要求ヘッダーの妥当性を確認した後。 既定値: 101 します。| 
  
<a id="ID4END"></a>

 
## <a name="request-body"></a>要求本文
 
<a id="ID4ETD"></a>

 
### <a name="sample-request"></a>要求の例
 
要求本文は、単純な[ResetReputation (JSON)](../../json/json-resetreputation.md)ドキュメントです。
 

```cpp
{
    "fairplayReputation": 75,
    "commsReputation": 75,
    "userContentReputation": 75
}
      
```

   
<a id="ID4EDE"></a>

 
## <a name="http-status-codes"></a>HTTP ステータス コード
 
サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | --- | --- | --- | 
| 200| OK| OK。| 
| 400| Bad Request| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
| 401| 権限がありません| 要求には、ユーザー認証が必要です。| 
| 404| Not Found します。| 指定されたリソースは見つかりませんでした。| 
| 500| 内部サーバー エラー| サーバーには、要求を満たすことを禁止する予期しない状態が発生しました。| 
| 503| Service Unavailable| 要求がスロット リングされた、(例: 5 秒後) を秒単位でクライアント再試行値後にもう一度要求を行ってください。| 
  
<a id="ID4EFH"></a>

 
## <a name="response-body"></a>応答本文
 
成功した場合、応答本文は空です。 失敗した場合、 [ServiceError (JSON)](../../json/json-serviceerror.md)のドキュメントが返されます。
 
<a id="ID4ERH"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
{
    "code": 4000,
    "source": "ReputationFD",
    "description": "No targetXuid field was supplied in the request"
}
         
```

   
<a id="ID4E2H"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4E4H"></a>

 
##### <a name="parent"></a>Parent 

[/users/me/resetreputation](uri-usersmeresetreputation.md)

   