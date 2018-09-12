---
title: PUT (/users/xuid(xuid)/lists/PINS/{listname})
assetID: f7964d2e-a8c8-2caa-ca97-e0d76ef586f4
permalink: en-us/docs/xboxlive/rest/uri-usersxuidlistspinslistnameput.html
author: KevinAsgari
description: " PUT (/users/xuid(xuid)/lists/PINS/{listname})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: fe69fe9e59fd3c7e523f9823438ff9d9b0b7916a
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882132"
---
# <a name="put-usersxuidxuidlistspinslistname"></a>PUT (/users/xuid(xuid)/lists/PINS/{listname})
要求本文内の各項目に指定されたインデックスに従ってリスト内の項目を更新します。 これらの Uri のドメインが`eplists.xboxlive.com`します。
 
  * [注釈](#ID4EV)
  * [URI パラメーター](#ID4E1B)
  * [Authorization](#ID4EFC)
  * [HTTP ステータス コード](#ID4ESC)
  * [必要な要求ヘッダー](#ID4EPH)
  * [要求本文](#ID4EGBAC)
  * [応答本文](#ID4EWBAC)
 
<a id="ID4EV"></a>

 
## <a name="remarks"></a>注釈
 
この呼び出しは、要求の本文内の各項目に指定されたインデックスに従ってリスト内の項目に更新されます。 この呼び出しは、一覧に項目を挿入されませんなり、項目が指定されたインデックスが存在しない場合はし、呼び出しが 400 無効な要求の状態を返します。 複数の項目を 1 つの呼び出しで更新することができますが、現在の一覧ですべて存在する必要があります。 つまり、すべてを取得するように更新または更新を取得します。
 
この呼び出しは、**インデックス**ではなく**itemId**を指定するのに更新する項目をことができます。 これを行うには、サービスに送信される**IndexedItems**構造内のインデックスを「-1」を使用します。 明らかにこの例では、 **itemId**変更できませんして更新プログラムの一部としては、その他のメタデータ フィールドへの変更のみ動作するようにします。 **プロバイダー**/**providerId**コンボことができます**itemId**ではなく、項目を識別します。 内部では、サービスは、これらの項目とを更新する適切なインデックスの図の一覧を検索します。 項目が見つからない場合は、400 無効な要求の状態が返され、項目は更新されません。
 
この呼び出しに必要な**場合-マッチ: versionNumber**インデックスを使用して、項目を識別する場合、要求に含まれるヘッダー。 使用して項目の項目を識別する Id (一覧は、重複を許可しない) 場合、 **If-match**ヘッダーは省略可能です。 存在する場合、 **If-match**ヘッダーが常に検証されます。 ヘッダーの**versionNumber**はリストの現在のバージョン番号です。 一致し、現在の一覧のバージョン番号、HTTP 412 Precondition Failed の状態コードが返されると、応答の本文いないが含まれて一覧の最新のメタデータがない含まれている (および必須)、または場合は、現在のバージョン番号にはが含まれます。 これは、互いに踏み潰すさまざまなクライアントからの更新プログラムを防ぐためです。
  
<a id="ID4E1B"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | 
| xuid| string| Xbox ユーザー ID (XUID)。| 
| listtype| string| (その使用方法と動作) の一覧の種類です。 常に「ピン」これらのメソッドを関連します。| 
| リスト| string| 一覧の名前 (際に特定の listtype の一覧がどの)。 常に"XBLPins"の項目を Pin にします。| 
  
<a id="ID4EFC"></a>

 
## <a name="authorization"></a>Authorization
 
この呼び出しは、**承認**ヘッダーで、XSTS SAML トークンを想定しています。 Xuid クレームは、呼び出し元を識別するには、その SAML トークン内に存在する必要があります。 この値は、呼び出し元に該当する一覧データへのアクセス権かどうかを使用します。 一覧自体では、同様の Xuid を識別し、一覧については、URI が追加します。 これを使用して、します、今後、一覧へのアクセスの共有のサポートがいる機能ではありませんこの時点で。 現時点では、ユーザーがアクセスするすべてのリストが独自と共有アクセスができなくなります。 したがって、URI の Xuid は SAML 要求トークンの Xuid と一致する必要があります。 

> [!NOTE] 
> 現時点では、XBL 認証 2.0 と 3.0 トークンの両方がサポートされています。 


  
<a id="ID4ESC"></a>

 
## <a name="http-status-codes"></a>HTTP ステータス コード
 
サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | --- | --- | --- | --- | 
| 200| OK| 要求は正常に完了しました。 応答本文では、(GET) 用、要求されたリソースを含める必要があります。 POST、PUT 要求は、最新の状態の一覧のメタデータ (一覧のバージョン、数など) に表示されます。| 
| 201| Created| 新しい一覧が作成されました。 これは、最初の挿入の一覧に返されます。 応答には、一覧の最新の状態のメタデータが含まれています。 と場所ヘッダーには、リストの URI が含まれています。| 
| 304| Not Modified| 取得で返されます。 クライアントに一覧の最新バージョンがあることを示します。 サービスは、一覧のバージョンを<b>If-match</b>ヘッダーで値を比較します。 これらが等しい場合、304 取得データなしで返されます。| 
| 400| Bad Request| 要求が正しくありません。 無効な値、または URI またはクエリ文字列パラメーターの型にすることができます。 不足している必要なパラメーターの結果ことができます。 またはデータの値、または要求に存在しないか、無効なバージョンの API が示されます。 <b>X XBL コントラクト バージョン</b>ヘッダーを参照してください。| 
| 401| 権限がありません| 要求には、ユーザー認証が必要です。| 
| 403| Forbidden| 要求は、ユーザーまたはサービスは許可されません。| 
| 404| Not Found します。| 呼び出し元では、リソースへのアクセスはありません。 これは、このような一覧が作成されていないことを示します。| 
| 412| Precondition Failed| 一覧のバージョンが変更されていて、変更要求が失敗したことを示します。 変更要求は、挿入、更新、または削除します。 サービスは、一覧のバージョンの<b>If-match</b>ヘッダーを確認します。 一覧の現在のバージョンが一致しない場合、操作は失敗し、これは、現在の一覧メタデータ (を現在のバージョンを含む) と共に返されます。| 
| 500| 内部サーバー エラー| サービスはサーバー側のエラーのための要求を拒否しています。| 
| 501| 実装されていません。| 呼び出し元では、サーバーで実装されていない URI を要求します。 (現在だけの場合、要求の対象となるがホワイト リスト名。)| 
| 503| Service Unavailable| サーバーは通常負荷が高くなり、要求を拒否します。 遅延の後 (表示、 <b>retry-after 後</b>ヘッダー)、要求を再試行することができます。| 
  
<a id="ID4EPH"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
| ヘッダー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Authorization| 認証し、要求を承認するために使用 STS トークンが含まれています。 トークンが XSTS サービスからと、要求の 1 つとして、XUID を含める必要があります。 | 
| X XBL コントラクト バージョン| 要求された (正の整数) をされている API バージョンを指定します。 バージョン 2 でピンをサポートしています。 このヘッダーが存在しないか、サービスは、400-を返します、値がサポートされていない状態の説明に「サポートされていないか、不足しているコントラクト バージョン ヘッダー」を含む要求が正しくありません。| 
| Content-Type| 要求/応答の本文のコンテンツは json または xml であるかどうかを指定します。 サポートされる値は"アプリケーション/json"と"アプリケーション/xml"| 
| If-Match| このヘッダーは、変更要求を行うときに、リストの現在のバージョン番号を含める必要があります。 変更要求の使用 PUT、POST、または動詞を削除します。 現在のバージョン一覧の"If-match"ヘッダー内のバージョンが一致しない場合、http/412 で、要求は拒否されます: precondition failed リターン コード。 (省略可能)使用できますの取得、現在の一覧のバージョンし一覧データがないと、HTTP 304 存在と渡されたバージョンに一致する場合は変更されませんコードが返されます。 | 
  
<a id="ID4EGBAC"></a>

 
## <a name="request-body"></a>要求本文
 
<a id="ID4EMBAC"></a>

 
### <a name="sample-request"></a>要求の例
 

```cpp
{"IndexedItems":
 [{ "Index": 0, 
     "Item": 
     {
    "ContentType": "Movie",
    "ItemId": "3a5095a5-eac3-4215-944d-27bc051faa47",
    "ProviderId": null,
    "Provider": null,
    "ImageUrl": "http://www.bing.com/thumb/...",
    "Title": "The Dark Knight",
    "SubTitle":null, 
    "Locale": "en-us",
    "DeviceType": "XboxOne"
}
}]}      
      
```

   
<a id="ID4EWBAC"></a>

 
## <a name="response-body"></a>応答本文
 
<a id="ID4E3BAC"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
{
  "ListVersion":  1,
  "ListCount":  1,
  "MaxListSize": 200,
  "AllowDuplicates": "true",
  "AccessSetting":  "OwnerOnly"
}        
         
```

   
<a id="ID4EGCAC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4EICAC"></a>

 
##### <a name="parent"></a>Parent 

[ユーザー/xuid (xuid)//ピン/{リスト} の一覧を示します](uri-usersxuidlistspinslistname.md)

   