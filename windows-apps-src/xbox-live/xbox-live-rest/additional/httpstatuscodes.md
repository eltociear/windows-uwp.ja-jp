---
title: 標準の HTTP ステータス コード
assetID: 7a19de56-7acd-ad2b-e8e6-53126991093b
permalink: en-us/docs/xboxlive/rest/httpstatuscodes.html
author: KevinAsgari
description: " 標準の HTTP ステータス コード"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 856b387825734fb7c6973293bc7004a79d05c207
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882070"
---
# <a name="standard-http-status-codes"></a>標準の HTTP ステータス コード
 
標準的なハイパー テキスト トランスポート プロトコル (HTTP) では、さまざまなクライアント要求に対する応答としてサーバーによって返されるステータス コードについて説明します。 Xbox Live サービスのメソッドは、要求の状態を記述する HTTP プロトコルに準拠した状態コードを返します。
 
Xbox Live サービスと、一般的な意味によって返されるステータス コードの一覧を示します。
 
<a id="ID4EAB"></a>

 
## <a name="xbox-live-services-status-codes"></a>Xbox Live サービスの状態コード
 
| コード| 理由フレーズ| 説明| 
| --- | --- | --- | 
| 200| OK| 要求が成功しました。| 
| 201| Created| エンティティが作成されました。| 
| 202| Accepted| 要求は受け入れられましたが、まだ完了していません。| 
| 204| No Content| 要求が完了したらが、コンテンツを返すにはありません。| 
| 301| 完全に移動| サービスについては、さまざまな URI に移動します。| 
| 302| 見つかった| 要求されたリソースは、さまざまな URI で一時的に存在します。| 
| 307| 一時的なリダイレクト| このリソースの URI が一時的に変更されました。| 
| 400| Bad Request| サービスは、形式が正しくない要求を理解していない可能性があります。 通常、無効なパラメーターです。| 
| 401| 権限がありません| 要求には、ユーザー認証が必要です。| 
| 403| Forbidden| 要求は、ユーザーまたはサービスは許可されません。| 
| 404| Not Found します。| 指定されたリソースは見つかりませんでした。| 
| 406| 許容できません。| リソースのバージョンがサポートされていません。| 
| 408| 要求のタイムアウト| 要求にかかった時間が長すぎます。| 
| 409| Conflict| リソースの現在の状態と競合するため、要求を完了しませんでした。| 
| 410| 無効| 要求されたリソースが利用可能ではなくなりました。| 
| 412| Precondition Failed| サーバーで、要求者は、要求に前提条件のいずれかが満たしていません。| 
| 416| 範囲が満たされていませんが要求| 要求された範囲は使用できません。| 
| 500| 内部サーバー エラー| サーバーには、要求を満たすことを禁止する予期しない状態が発生しました。| 
| 501| 実装されていません。| サーバーは、要求を満たすために必要な機能をサポートしません。| 
| 503| Service Unavailable| 要求がスロット リングされた、(例: 5 秒後) を秒単位でクライアント再試行値後にもう一度要求を行ってください。| 
 

> [!NOTE] 
> 一部のリソースとメソッドは、そのリソースやメソッドのコンテキスト内で特定の状態コードの意味の特定の情報を提供します。 詳しくは、リソースやメソッドを使用しているのドキュメントを参照してください。 

  
<a id="ID4E3BAC"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4E5BAC"></a>

 
##### <a name="parent"></a>Parent  

[その他の参照](atoc-xboxlivews-reference-additional.md)

  
<a id="ID4EKCAC"></a>

 
##### <a name="reference--universal-resource-identifier-uri-referenceuriatoc-xboxlivews-reference-urismd"></a>参照[ユニバーサル リソース識別子 (URI) の参照](../uri/atoc-xboxlivews-reference-uris.md)

 [その他の参照](atoc-xboxlivews-reference-additional.md)

  
<a id="ID4EZCAC"></a>

 
##### <a name="external-links--w3org-http11-status-code-definitionshttpwwww3orgprotocolsrfc2616rfc2616-sec10htmlsec10"></a>外部リンク[W3.org: http/1.1 ステータス コード定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10)

   