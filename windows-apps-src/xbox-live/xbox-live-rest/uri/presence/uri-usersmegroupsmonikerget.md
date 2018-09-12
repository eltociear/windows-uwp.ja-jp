---
title: 取得する (ユーザー/me/グループ/{モニカー})
assetID: c2527a08-411b-d4e4-422f-a8438804bfe6
permalink: en-us/docs/xboxlive/rest/uri-usersmegroupsmonikerget.html
author: KevinAsgari
description: " 取得する (ユーザー/me/グループ/{モニカー})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: b308668dd24d72b57167a90d5eb297203c2e60c1
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881928"
---
# <a name="get-usersmegroupsmoniker-"></a>取得する (ユーザー/me/グループ/{モニカー})
[グループの presencerecord を要求してを取得します。 これらの Uri のドメインが`userpresence.xboxlive.com`します。
 
  * [注釈](#ID4EV)
  * [URI パラメーター](#ID4E5)
  * [クエリ文字列パラメーター](#ID4EJB)
  * [Authorization](#ID4EKC)
  * [リソースのプライバシーの設定の効果](#ID4EQD)
  * [必要な要求ヘッダー](#ID4EEH)
  * [オプションの要求ヘッダー](#ID4EMBAC)
  * [要求本文](#ID4EMCAC)
  * [HTTP ステータス コード](#ID4EXCAC)
  * [必要な応答ヘッダー](#ID4E3GAC)
  * [省略可能な応答ヘッダー](#ID4EMJAC)
  * [応答本文](#ID4E5KAC)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>注釈
 
ユーザーの要求に関連するモニカーによって指定されたグループ内のユーザーを取得し、それらのユーザーの presencerecord を要求してを返します。 プライバシーやコンテンツの分離で区切られているデータは単には返されません。
  
<a id="ID4E5"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | 
| モニカー| string| ユーザーのグループを定義する文字列です。 現時点では受け入れられるだけモニカーでは、大文字の 'P'"People"でです。| 
  
<a id="ID4EJB"></a>

 
## <a name="query-string-parameters"></a>クエリ文字列パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | --- | --- | --- | 
| level| string| このクエリ文字列で指定された詳細レベルを返します。 有効なオプションには、「ユーザー」、「デバイス」、"title"、"all"が含まれます。「ユーザー」レベルは、DeviceRecord 入れ子になったオブジェクトがない presencerecord を要求してオブジェクトです。 「デバイス」レベルでは、TitleRecord 入れ子になったオブジェクトがない presencerecord を要求してと DeviceRecord オブジェクトです。 "Title"レベルでは、ActivityRecord 入れ子になったオブジェクトがない presencerecord を要求して、DeviceRecord、および TitleRecord オブジェクトです。 "All"レベルでは、すべての入れ子になったオブジェクトを含むレコード全体です。このパラメーターが指定されていない場合、サービスのタイトルのレベルに既定値 (タイトルの詳細までは、このユーザーのプレゼンスを返す、)。| 
  
<a id="ID4EKC"></a>

 
## <a name="authorization"></a>Authorization
 
承認要求の使用 | 要求| 種類| 必須?| 値の例| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| <b>Xuid</b>| 64 ビットの符号付き整数| 必須| 1234567890| 
  
<a id="ID4EQD"></a>

 
## <a name="effect-of-privacy-settings-on-resource"></a>リソースのプライバシーの設定の効果
 
サービスは常に返します 200 OK 要求自体が整形式である場合。 ただし、プライバシー チェックを渡さない場合、応答からの情報をフィルター処理がされます。
 
リソースのプライバシーの設定の効果 | ユーザーの要求| ターゲット ユーザーのプライバシー設定| 動作| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| me| -| 前述のようにします。| 
| フレンド| すべてのユーザー| 前述のようにします。| 
| フレンド| フレンドのみ| 前述のようにします。| 
| フレンド| ブロック| ように、サービスがデータをフィルター処理します。| 
| ユーザーのフレンドではないです。| すべてのユーザー| 前述のようにします。| 
| ユーザーのフレンドではないです。| フレンドのみ| ように、サービスがデータをフィルター処理します。| 
| ユーザーのフレンドではないです。| ブロック| ように、サービスがデータをフィルター処理します。| 
| サード パーティのサイト| すべてのユーザー| ように、サービスがデータをフィルター処理します。| 
| サード パーティのサイト| フレンドのみ| ように、サービスがデータをフィルター処理します。| 
| サード パーティのサイト| ブロック| ように、サービスがデータをフィルター処理します。| 
  
<a id="ID4EEH"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
| ヘッダー| 型| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Authorization| string| HTTP の認証の資格情報を認証します。 値の例:"XBL3.0 x =&lt;userhash > です。&lt;トークン >"。| 
| x xbl コントラクト バージョン| string| この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求はのみにルーティングすると、サービスの認証トークンを要求ヘッダーの妥当性を確認した後。 値の例: 3、vnext します。| 
| Accept| string| コンテンツの種類の受け入れられる。 1 つだけのプレゼンスがサポートは<b>アプリケーション/json</b>はも指定ヘッダーで。| 
| 同意言語| string| 応答で文字列を許容できるロケールです。 値の例: EN-US にします。| 
| Host| string| サーバーのドメイン名。 値の例: userpresence.xboxlive.com します。| 
  
<a id="ID4EMBAC"></a>

 
## <a name="optional-request-headers"></a>オプションの要求ヘッダー
 
| ヘッダー| 型| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| X RequestedServiceVersion|  | この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求はのみにルーティングすると、サービスの認証トークンを要求ヘッダーの妥当性を確認した後。 既定値: 1 です。| 
  
<a id="ID4EMCAC"></a>

 
## <a name="request-body"></a>要求本文
 
この要求の本文には、オブジェクトは送信されません。
  
<a id="ID4EXCAC"></a>

 
## <a name="http-status-codes"></a>HTTP ステータス コード
 
サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| OK| セッションが正常に取得されます。| 
| 400| Bad Request| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
| 401| 権限がありません| 要求には、ユーザー認証が必要です。| 
| 403| Forbidden| 要求は、ユーザーまたはサービスは許可されません。| 
| 404| Not Found します。| 指定されたリソースは見つかりませんでした。| 
| 405| Method Not Allowed| HTTP メソッドは、サポートされていないコンテンツの種類で使用されました。| 
| 406| 許容できません。| リソースのバージョンがサポートされていません。| 
| 500| 要求のタイムアウト| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
| 503| 要求のタイムアウト| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
  
<a id="ID4E3GAC"></a>

 
## <a name="required-response-headers"></a>必要な応答ヘッダー
 
| ヘッダー| 型| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl コントラクト バージョン| string| この要求を送信する必要があります、Xbox LIVE サービスの名前/数をビルドします。 要求はのみにルーティングすると、サービスの認証トークンを要求ヘッダーの妥当性を確認した後。 値の例: 1、vnext します。| 
| Content-Type| string| 要求の本文の mime タイプ。 値の例:<b>アプリケーション/json</b>します。| 
| キャッシュ コントロール| string| キャッシュ動作を指定するていねい要求します。 値の例:「は」。| 
| X XblCorrelationId| string| サーバーが返すし、クライアントで何が受信されたを関連付けるにサービスで生成された値。 値の例:"4106d0bc-1cb3-47bd-83fd-57d041c6febe"。| 
| X コンテンツの種類オプション| string| SDL に準拠した値を返します。 値の例:"nosniff"。| 
| Date| string| メッセージが送信された日付/時刻。 値の例:"火曜日、17 年 2012年 11 月 10時 33分: 31 GMT"。| 
  
<a id="ID4EMJAC"></a>

 
## <a name="optional-response-headers"></a>省略可能な応答ヘッダー
 
| ヘッダー| 型| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Retry-after| string| 503 HTTP エラーに返されます。 クライアントに呼び出しを再試行するまで待機する時間に知らせることができます。 値の例:「120」。| 
| Content-Length| string| 応答本文の長さ。 値の例:「527」。| 
| コンテンツ エンコード| string| 応答の種類をエンコードします。 値の例:"gzip"。| 
  
<a id="ID4E5KAC"></a>

 
## <a name="response-body"></a>応答本文
 
この API は、要求から Xuid ごとに 1 つ presencerecord を要求してオブジェクトの配列を返します。
 
<a id="ID4EGLAC"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
[
     {
         xuid:"0123456789",
         state:"online",
         devices:
         [
             {
                 type:"D",
                 titles:
                 [
                     {
                         id:"12341234",
                         name:"Contoso 5",
                         lastModified:"2012-09-17T07:15:23.4930000",
                         placement:"full",
                         state:"active",
                         activity:
                         {
                             richPresence:"Playing on Nirvana"
                         },
                     }
                 ]
             }
         ]
     },
     {
         xuid:"0123456780",
         state:"online",
         devices:
         [
             {
                 type:"D",
                 titles:
                 [
                     {
                         id:"12341235",
                         name:"Contoso Waypoint",
                         lastModified:"2012-09-17T07:15:23.4930000",
                         placement;"full",
                         state:"active",
                         activity:
                         {
                             richPresence:"Viewing stats"
                         },
                     }
                 ]
             }
         ]
     },
     {
         xuid:"0123456781",
         state:"online",
         devices:
         [
             {
                 type:"Win8",
                 titles:
                 [
                     {
                         id:"23452345",
                         name:"Contoso Gamehelp",
                         state:"active",
                         timestamp:"2012-09-17T07:15:23.4930000",
                         activity:
                         {
                             richPresence:"Viewing help"
                         }
                     }
                 ]
             }
         ]
     }
 ]
         
```

   
<a id="ID4EQLAC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4ESLAC"></a>

 
##### <a name="parent"></a>Parent 

[ユーザー/me/グループ/{モニカー}](uri-usersmegroupsmoniker.md)

   