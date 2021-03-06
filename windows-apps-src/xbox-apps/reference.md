---
title: Xbox Device Portal REST API
description: Xbox One の UWP に関する API リファレンスです。
ms.date: 10/25/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 5ae8e953-0465-487b-81dd-54a85c904daf
ms.localizationpriority: medium
ms.openlocfilehash: d8fdcf01d7d1f72624d73acf2d10ce28dfb75e04
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57656997"
---
# <a name="xbox-device-portal-rest-api"></a>Xbox Device Portal REST API

このセクションには、コンソールの構成と管理をリモートから行うために使用する Xbox Device Portal REST API に関するリファレンス トピックが記載されています。

| URI        | 説明 |
|------------|-------------|
|[/api/app/packagemanager/register](wdp-loose-folder-register-api.md)| ルース フォルダーに含まれているアプリを登録します。 |
|[/api/app/packagemanager/upload](wdp-folder-upload.md)| フォルダー全体を本体にアップロードします。 |
|[/ext/app/sshpins](uwp-sshpins-api.md)| 信頼されたすべての SSH ピンをリモートでクリアします。 Visual Studio UWP 開発では、PIN のペアリングをもう一度行う必要があります。 |
|[/ext/app/deployinfo](uwp-deployinfo-api.md)| 1 つ以上のインストール パッケージの展開情報を要求します。 |
|[fiddler/ext](wdp-fiddler-api.md)| Fiddler のネットワーク トレースを有効または無効にします。 |
|[/ext/httpmonitor/sessions](wdp-httpMonitor-api.md)| Xbox でフォーカスのあるアプリから HTTP トラフィックを取得します。 |
|[networkcredential/ext](uwp-networkcredentials-api.md)| ネットワーク資格情報を追加、削除、または更新します。 |
|[ext/remoteinput](uwp-remoteinput-api.md)| キーボード、マウス、コントローラーの入力を Xbox にリモートで送信します。 |
|[/ext/remoteinput/controllers](uwp-remoteinput-controllers-api.md)| 接続された物理コントローラーの数を取得するか、またはすべての物理コントローラーをオフにします。 |
|[ext/スクリーン ショット](wdp-media-capture-api.md)| 現在本体に表示されている画面の PNG 画像をキャプチャします。 |
|[ext/設定](wdp-xboxsettings-api.md)| Xbox One 開発者向け設定にアクセスします。 |
|[/ext/smb/developerfolder](wdp-smb-api.md)| 開発用 PC のエクスプローラーを使用して、本体上にある開発者向けフォルダーにアクセスします。 |
|[ext/ユーザー](wdp-user-management.md)| Xbox One 本体のユーザーを管理します。 |
|[/ext/xbox/info](wdp-xboxinfo-api.md)| Xbox One デバイスに関する情報を提供します。 |
|[/ext/xboxlive/sandbox](wdp-sandbox-api.md)| Xbox Live サンド ボックスを管理します。 |

## <a name="see-also"></a>関連項目

- [Xbox One の UWP](index.md)
- [Windows Device Portal](../debug-test-perf/device-portal.md)