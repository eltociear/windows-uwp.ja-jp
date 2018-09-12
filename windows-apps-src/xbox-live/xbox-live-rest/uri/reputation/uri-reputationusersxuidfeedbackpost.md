---
title: POST (/users/xuid({xuid})/feedback)
assetID: 48a7a510-a658-f2a3-c6bc-28a3610006e7
permalink: en-us/docs/xboxlive/rest/uri-reputationusersxuidfeedbackpost.html
author: KevinAsgari
description: " POST (/users/xuid({xuid})/feedback)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 8cb56b51e2d558b2a4ef05d117244d464756e6ec
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881779"
---
# <a name="post-usersxuidxuidfeedback"></a>POST (/users/xuid({xuid})/feedback)
シェルを使用してではなく、ゲームでフィードバック オプションを追加したい場合に、タイトルから使われます。 これらの Uri のドメインが`reputation.xboxlive.com`します。
 
  * [URI パラメーター](#ID4EZ)
  * [必要な要求ヘッダー](#ID4EEB)
  * [要求本文](#ID4ENC)
  * [必要なヘッダー](#ID4EDE)
  * [Authorization](#ID4EXF)
  * [HTTP ステータス コード](#ID4EEG)
  * [応答本文](#ID4EZH)
 
<a id="ID4EZ"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | 
| xuid| ulong| Xbox ユーザー ID (XUID)、ユーザーが報告されるのです。| 
  
<a id="ID4EEB"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
| ヘッダー| 型| 説明| 
| --- | --- | --- | --- | --- | --- | 
| Authorization| string| HTTP の認証の資格情報を認証します。 値の例:"XBL3.0 x =&lt;userhash > です。&lt;トークン >"。| 
| X RequestedServiceVersion|  | この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求はのみにルーティングすると、サービスの認証トークンを要求ヘッダーの妥当性を確認した後。 既定値: 101 します。| 
  
<a id="ID4ENC"></a>

 
## <a name="request-body"></a>要求本文 
 
<a id="ID4EVC"></a>

 
### <a name="required-members"></a>必要なメンバー 
 
要求は、[フィードバック](../../json/json-feedback.md)のオブジェクトを含める必要があります。 
  
<a id="ID4EED"></a>

 
### <a name="prohibited-members"></a>禁止されているメンバー 
 
要求では、他のすべてのメンバーが禁止されています。
  
<a id="ID4ETD"></a>

 
### <a name="sample-request"></a>要求の例 
 

```cpp
{
    "sessionRef":
    {
        "scid": "372D829B-FA8E-471F-B696-07B61F09EC20",
        "templateName": "CaptureFlag5",
        "name": "Halo556932",
    },
    "feedbackType": "CommsAbusiveVoice",
    "textReason": "He called me a doodoo-head!",
    "voiceReasonId": null,
    "evidenceId": null
}

      
```

   
<a id="ID4EDE"></a>

 
## <a name="required-headers"></a>必要なヘッダー
 
次のヘッダーは、Xbox Live サービス要求を行ったとき必要があります。
 
| <b>ヘッダー</b>| <b>値</b>| <b>Deacription</b>| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl コントラクト バージョン| 101| API コントラクト バージョン。| 
| Authorization| XBL3.0 x = [ハッシュ]。[トークン]| STS 認証トークン。 STSTokenString は、認証要求によって返されるトークンに置き換えられます。| 
Content-Type| 
application/json| 
提出されたデータの種類です。| 
  
<a id="ID4EXF"></a>

 
## <a name="authorization"></a>Authorization
 
要求は、Xbox Live の有効な承認ヘッダーを含める必要があります。 呼び出し元がこのリソースへのアクセス許可されていない場合、サービスは、403 Forbidden コードを返します。 ヘッダーが見つからないか無効な場合は、サービスは、401 承認されていないコードを返します。
  
<a id="ID4EEG"></a>

 
## <a name="http-status-codes"></a>HTTP ステータス コード
 
サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 204| No Content| 要求が完了したらが、コンテンツを返すにはありません。| 
| 401| 権限がありません| 要求には、ユーザー認証が必要です。| 
| 404| Not Found します。| 指定されたリソースは見つかりませんでした。| 
| 406| 許容できません。| リソースのバージョンがサポートされていません。| 
| 408| 要求のタイムアウト| 要求にかかった時間が長すぎます。| 
| 409| Conflict| 継続トークンが無効になった。| 
  
<a id="ID4EZH"></a>

 
## <a name="response-body"></a>応答本文 
 
呼び出しが成功した場合は、この応答からのオブジェクトは返されません。 それ以外の場合、サービスは、 [ServiceError](../../json/json-serviceerror.md)オブジェクトを返します。
  
<a id="ID4EOAAC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EQAAC"></a>

 
##### <a name="parent"></a>Parent 

[/users/xuid({xuid})/feedback](uri-reputationusersxuidfeedback.md)

  
<a id="ID4E3AAC"></a>

 
##### <a name="reference"></a>リファレンス 

[フィードバック (JSON)](../../json/json-feedback.md)

 [ServiceError (JSON)](../../json/json-serviceerror.md)

   