---
title: /handles/{ハンドル id を使用}
assetID: 5b722d3e-fe80-fec5-a26b-8b3db6422004
permalink: en-us/docs/xboxlive/rest/uri-handleshandleid.html
author: KevinAsgari
description: " /handles/{ハンドル id を使用}"
ms.author: kevinasg
ms.date: 20-12-2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One
ms.localizationpriority: medium
ms.openlocfilehash: 47dda291a9a86ccbee69e1e51ca71be373f5dc1d
ms.sourcegitcommit: 72710baeee8c898b5ab77ceb66d884eaa9db4cb8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2018
ms.locfileid: "3882533"
---
# <a name="handleshandleid"></a>/handles/{ハンドル id を使用}
識別子により指定されたセッション ハンドルの削除を取得する操作をサポートしています。 

> [!NOTE] 
> この URI は、2015年マルチプレイヤーでは使用され、以降そのマルチプレイヤーのバージョンにのみ適用されます。 テンプレート コントラクト 104/105 以降で使用して設計されています。  

 
<a id="ID4EQ"></a>

 
## <a name="domain"></a>ドメイン
sessiondirectory.xboxlive.com  
<a id="ID4EV"></a>

 
## <a name="uri-parameters"></a>URI パラメーター
 
| パラメーター| 型| 説明| 
| --- | --- | --- | --- | 
| ハンドル id を使用| GUID| セッションのハンドルを一意の ID。| 
  
<a id="ID4ERB"></a>

 
## <a name="valid-methods"></a>有効なメソッド

[(/Handles/{ハンドル id を使用}) を削除します。](uri-handleshandleiddelete.md)

&nbsp;&nbsp;ハンドル ID で指定されたハンドルを削除します。

[(/Handles/{ハンドル id}) を取得します。](uri-handleshandleidget.md)

&nbsp;&nbsp;ハンドル ID で指定されたハンドルを取得します。
 
<a id="ID4E4B"></a>

 
## <a name="see-also"></a>関連項目
 
<a id="ID4E6B"></a>

 
##### <a name="parent"></a>Parent 

[セッション ディレクトリ Uri](atoc-reference-sessiondirectory.md)

   