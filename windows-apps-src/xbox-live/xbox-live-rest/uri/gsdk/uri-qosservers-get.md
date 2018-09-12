---
title: 取得する (/qosservers)
assetID: 8b940c1b-947c-eab3-78ed-4384f57ea0bd
permalink: en-us/docs/xboxlive/rest/uri-qosservers-get.html
author: KevinAsgari
description: " 取得する (/qosservers)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 71a4787bf6b139d1a638ec783c0293d70a8ee239
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3881882"
---
# <a name="get-qosservers"></a>取得する (/qosservers)
URI が利用可能な QoS サーバーの一覧を取得する Xbox Live エンジンで使用するために、クライアントによって呼び出されます。 これらの Uri のドメイン`gameserverds.xboxlive.com`と`gameserverms.xboxlive.com`します。
 
  * [必要な要求ヘッダー](#ID4EBB)
  * [必要な応答ヘッダー](#ID4EUC)
  * [応答本文](#ID4EVD)
 
<a id="ID5EG"></a>

 
## <a name="host-name"></a>ホスト名

gameserverds.xboxlive.com
 
<a id="ID4EBB"></a>

 
## <a name="required-request-headers"></a>必要な要求ヘッダー
 
要求を作成する場合、次の表に示すように、ヘッダーは必要です。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | 
| Content-Type| application/json| 提出されたデータの種類です。| 
| Host| gameserverds.xboxlive.com|  | 
| Content-Length|  | 要求のオブジェクトの長さ。| 
| x xbl コントラクト バージョン| 1| API コントラクト バージョン。| 
  
<a id="ID4EUC"></a>

 
## <a name="required-response-headers"></a>必要な応答ヘッダー
 
応答には常に、次の表に示すように、ヘッダーが含まれます。
 
| ヘッダー| 設定値| 説明| 
| --- | --- | --- | --- | --- | --- | 
| Content-Type| application/json| 応答本文内のデータの種類です。| 
| Content-Length|  | 応答本文の長さ。| 
  
<a id="ID4EVD"></a>

 
## <a name="response-body"></a>応答本文
 
呼び出しが成功した場合、サービスは、次のメンバーを含む JSON オブジェクトを返します。
 
| メンバー| 説明| 
| --- | --- | --- | --- | --- | --- | --- | --- | 
| qosservers| サーバー情報の配列です。| 
| serverFqdn| サーバーの完全修飾ドメイン名。| 
| serverSecureDeviceAddress| サーバーのセキュア デバイス アドレス。| 
| targetLocation| サーバーの地理的な場所です。| 
 
<a id="ID4EUE"></a>

 
### <a name="sample-response"></a>応答の例
 

```cpp
{ 
  "qosServers" : 
  [ 
    { "serverFqdn" : "xblqosncus.cloudapp.net", "serverSecureDeviceAddress" : "&lt;base-64 encoded blob>", "targetLocation" : "North Central US" },
    { "serverFqdn" : "xblqoswus.cloudapp.net", "serverSecureDeviceAddress" : "&lt;base-64 encoded blob>", "targetLocation" : "West US" },
  ]
}

      
```

   
<a id="ID4EBF"></a>

 
## <a name="see-also"></a>関連項目
 [/qosservers](uri-qosservers.md)

  