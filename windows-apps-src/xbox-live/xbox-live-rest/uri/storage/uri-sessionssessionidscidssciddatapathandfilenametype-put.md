---
title: PUT (/sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type})
assetID: 40005e52-cd24-38ed-cfed-2c590cc2276f
permalink: en-us/docs/xboxlive/rest/uri-sessionssessionidscidssciddatapathandfilenametype-put.html
author: KevinAsgari
description: " PUT (/sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type})"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: df924f8665424bf540eb1651cfa69737080588d5
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881735"
---
# <a name="put-sessionssessionidscidssciddatapathandfilenametype"></a>PUT (/sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type})
ファイルをアップロードします。 メタデータとデータが送信される 1 つのメッセージで、または一連の小さいブロックのデータやメタデータが送信される複数のブロック アップロードとして完全なアップロードでは、データをアップロードできます。 1 つのメッセージとしては 4 つのメガバイト数よりも小さいファイルのみを送信できます。 複数のブロックのアップロードの種類の json データはサポートされていません。 これらの Uri のドメインが`titlestorage.xboxlive.com`します。
 
  * [URI パラメーター](#ID4EX)
  * [Authorization](#ID4EEB)
  * [オプションのクエリ文字列パラメーター](#ID4ERB)
  * [必要な要求ヘッダー](#ID4ENE)
  * [オプションの要求ヘッダー](#ID4EWF)
  * [要求本文](#ID4EZG)
  * [HTTP ステータス コード](#ID4EEH)
  * [応答本文](#ID4EXEAC)
 
<a id="ID4EX"></a>

 
## <a name="uri-parameters"></a>URI パラメーター 
 
| パラメーター| 型| 説明| 
| --- | --- | --- | 
| sessionId| string| 検索するセッションの ID です。| 
| scid| guid| ルックアップ サービス構成の ID です。| 
| pathAndFileName| string| アクセスする項目のパスとファイル名。 パス部分 (となどを含む最終的なスラッシュ) の有効な文字が大文字 (A ~ Z)、(a ~ z) 小文字の英字、数字 (0 ~ 9)、アンダー スコア (_) を含めるし、スラッシュ (/)。パス部分を空にすることがあります。有効な文字 (すべての最終的なスラッシュ後) ファイル名の部分には、大文字 (A ~ Z)、(a ~ z) 小文字の英字、数字 (0 ~ 9) が含まれているアンダー スコア (_)、ピリオド (.)、およびハイフン (-)。 ファイル名を空にする場合がありますはいない期間の終了または 2 つの連続するピリオドが含まれては。| 
| type| 文字列| データの形式です。 値はバイナリまたは json です。| 
  
<a id="ID4EEB"></a>

 
## <a name="authorization"></a>Authorization 
 
要求は、Xbox LIVE の有効な承認ヘッダーを含める必要があります。 呼び出し元がこのリソースへのアクセス許可されていない場合、サービスは、403 Forbidden 応答を返します。 ヘッダーが見つからないか無効な場合は、サービスは、401 承認されていない応答を返します。 
  
<a id="ID4ERB"></a>

 
## <a name="optional-query-string-parameters"></a>オプションのクエリ文字列パラメーター 
 
1 つのメッセージのアップロードは、クエリ文字列パラメーターがあります。
 
| パラメーター| 型| 説明| 
| --- | --- | --- | --- | --- | --- | 
| clientFileTime| DateTime| どのクライアント上のファイルの日付/時刻は、最終ファイルをアップロードします。| 
| displayName| string| ユーザーに表示する必要がありますファイルの名前です。| 
 
複数のブロックのアップロードは、クエリ文字列パラメーターがあります。
 
| パラメーター| 型| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| clientFileTime| DateTime| どのクライアント上のファイルの日付/時刻は、最終ファイルをアップロードします。| 
| displayName| string| ユーザーに表示する必要がありますファイルの名前です。| 
| continuationToken| string| 前回のアップロード要求の応答には、継続トークン。 最初のブロックの場合は、これを指定しない必要があります。 | 
| finalBlock| bool| ファイルの最後のブロックを true に設定します。 その他のすべてのブロックでは false に設定します。| 
  
<a id="ID4ENE"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| x xbl コントラクト バージョン| 1| API コントラクト バージョン。| 
| Authorization| XBL3.0 x = [ハッシュ]。[トークン]| STS 認証トークン。 STSTokenString は、認証要求によって返されるトークンに置き換えられます。 STS トークンを取得して、承認ヘッダーの作成について詳しくは、用いた認証と Xbox LIVE サービス要求の承認を参照してください。| 
  
<a id="ID4EWF"></a>

 
## <a name="optional-request-headers"></a>オプションの要求ヘッダー
 
| ヘッダー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| If-Match| 操作を完了するにより既存項目に一致する必要がある ETag を指定します。| 
| If-None-Match| 操作を完了するにより既存項目に一致する必要があります ETag を指定します。| 
  
<a id="ID4EZG"></a>

 
## <a name="request-body"></a>要求本文 
 
要求本文には、アップロードされているファイルの内容が含まれています。 1 つのメッセージのアップロード、本体は、ファイルの完全な内容です。 複数のブロックのアップロードの本文は、クエリ文字列パラメーターで指定されたファイルの部分です。 
  
<a id="ID4EEH"></a>

 
## <a name="http-status-codes"></a>HTTP ステータス コード 
 
サービスは、このリソースには、この方法で行った要求に対する応答としてでは、このセクションでステータス コードのいずれかを返します。 Xbox Live サービスで使用される標準の HTTP ステータス コードの一覧は、[標準の HTTP ステータス コード](../../additional/httpstatuscodes.md)を参照してください。
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 200| OK | 要求が成功しました。| 
| 201| Created | エンティティが作成されました。| 
| 400| Bad Request | サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
| 401| 権限がありません | 要求には、ユーザー認証が必要です。| 
| 403| Forbidden | 要求は、ユーザーまたはサービスは許可されません。| 
| 404| Not Found します。 | 指定されたリソースは見つかりませんでした。| 
| 406| 許容できません。 | リソースのバージョンがサポートされていません。| 
| 408| 要求のタイムアウト | 要求にかかった時間が長すぎます。| 
| 500| 内部サーバー エラー | サーバーには、要求を満たすことを禁止する予期しない状態が発生しました。| 
| 503| Service Unavailable | 要求がスロット リングされた、(例: 5 秒後) を秒単位でクライアント再試行値後にもう一度要求を行ってください。| 
  
<a id="ID4EXEAC"></a>

 
## <a name="response-body"></a>応答本文 
 
呼び出しでは、複数のブロック要求が成功した場合は、サービスは、次のブロックを渡す continution トークンを返します。
 
<a id="ID4EDFAC"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
{
    "continuationToken":"abcd1234-1111-2222-3333-abcd12345678-1"
}
         
```

   
<a id="ID4EPFAC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4ERFAC"></a>

 
##### <a name="parent"></a>Parent  

[/sessions/{sessionId}/scids/{scid}/data {{pathandfilename}, {type}](uri-sessionssessionidscidssciddatapathandfilenametype.md)

   