---
title: BatchRequest (JSON)
assetID: 2ca34506-8801-efc5-7c83-3c9ec5572276
permalink: en-us/docs/xboxlive/rest/json-batchrequest.html
author: KevinAsgari
description: " BatchRequest (JSON)"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 6271cdf3d94f194adee5087136c1d87ad9f214b5
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882007"
---
# <a name="batchrequest-json"></a>BatchRequest (JSON)
ユーザー、デバイス、およびタイトルなどのプレゼンス情報をフィルター処理するためのプロパティの配列です。
<a id="ID4EN"></a>


## <a name="batchrequest"></a>BatchRequest

BatchRequest オブジェクトには、次の仕様があります。

| メンバー| 種類| 説明|
| --- | --- | --- |
| ユーザー| 文字列の配列| については、一度に 1100 Xuid の最大プレゼンスがユーザーの Xuid をリストします。|
| deviceTypes| 文字列の配列| について知りたいユーザーで使用されるデバイスの種類の一覧です。 空の配列の場合、既定値はすべてのデバイスの種類 (つまり、none が除外されます)。|
| タイトル| 32 ビットの符号なし整数の配列| デバイスの一覧について理解していることをユーザーを種類します。 可能なすべてのタイトルに既定値の配列が空のままである場合 (つまり、none が除外されます)。|
| level| string| 設定可能な値: <ul><li>ユーザーのユーザーのノードを入手します。</li><li>デバイスの get ユーザーとデバイス ノード</li><li>タイトルのタイトルの基本的なレベルの情報の取得</li><li>リッチ プレゼンス情報やメディアは、すべてを取得します。</li></ul>既定値は、「タイトル」です。| 
| ガジェットの onlineOnly| ブール値| このプロパティが true の場合、バッチ操作がオフラインのユーザーが (回答が決まるものを含む) のレコードをフィルター処理します。 指定されていない場合は、オンラインとオフライン両方のユーザーが返されます。|

<a id="ID4EAD"></a>


## <a name="sample-json-syntax"></a>JSON 構文の例


```json
{
  users:
  [
    "1234567890",
    "4567890123",
    "7890123456"
  ]
}


```


<a id="ID4EJD"></a>


## <a name="see-also"></a>関連項目

<a id="ID4ELD"></a>


##### <a name="parent"></a>Parent

[JavaScript オブジェクト Notation (JSON) オブジェクト リファレンス](atoc-xboxlivews-reference-json.md)


<a id="ID4EXD"></a>


##### <a name="reference"></a>リファレンス   