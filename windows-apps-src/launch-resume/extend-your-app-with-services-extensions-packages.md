---
author: TylerMSFT
title: サービス、拡張機能、パッケージでアプリを拡張する
description: ユニバーサル Windows プラットフォーム (UWP) アプリが更新された際に実行されるバックグラウンド タスクの作成方法を説明します。
ms.author: twhitney
ms.date: 05/7/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP, 拡張, コンポーネント化, アプリ サービス, パッケージ, 拡張機能
ms.localizationpriority: medium
ms.openlocfilehash: 6920b448146f25433335234ec67fde473e096cbd
ms.sourcegitcommit: 517c83baffd344d4c705bc644d7c6d2b1a4c7e1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
ms.locfileid: "1843655"
---
# <a name="extend-your-app-with-services-extensions-and-packages"></a>サービス、拡張機能、パッケージでアプリを拡張する

Windows 10 には、アプリの拡張とコンポーネント化に役立つさまざまなテクノロジがあります。 次の表は、シナリオで使用する必要があるテクノロジを判断するのに役立ちます。 その後で、シナリオとテクノロジについて簡単に説明します。

| シナリオ                           | リソース パッケージ   | アセット パッケージ      | オプション パッケージ   | フラット バンドル        | アプリの拡張機能      | アプリ サービス        | ストリーミング インストール  |
|------------------------------------|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|:------------------:|
| サード パーティー コード プラグイン            |                    |                    |                    |                    | :heavy_check_mark: |                    |                    |
| インプロセス コード プラグイン              |                    |                    | :heavy_check_mark: |                    |                    |                    |                    |
| UX アセット (文字列/画像)         | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |
| オンデマンド コンテンツ <br/> (例: 追加の階層) |      |                    | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |
| ライセンスと取得の分離 |                    |                    | :heavy_check_mark: |                    | :heavy_check_mark: | :heavy_check_mark: |                    |
| アプリ内取得                 |                    |                    | :heavy_check_mark: |                    | :heavy_check_mark: |                    |                    |
| インストール時間の最適化              | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |                    | :heavy_check_mark: |
| ディスク使用量の削減              | :heavy_check_mark: |                    | :heavy_check_mark: |                    |                    |                    |                    |
| パッケージ化の最適化                 |                    | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |                    |                    |                    |
| 公開までの時間の短縮             | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |                    |                    |                    |

## <a name="scenario-descriptions-the-rows-in-the-table-above"></a>シナリオの説明 (上のテーブルの行)

**サード パーティー プラグイン**  

ストアからダウンロードしてアプリで実行できるコードです。 たとえば、Microsoft Edge ブラウザーの拡張機能などです。

**インプロセス コード プラグイン**  

アプリのプロセス内で実行されるコードです。 C++ でのみサポートされています。 コンテンツが含まれる場合もあります。 コードはプロセス内で実行されるため、より高いレベルの信頼が想定されます。 サードパーティーのこの種の拡張機能は開かないようにすることもできます。

**UX アセット (文字列/画像)**  

ローカライズされた文字列、画像、その他の UI コンテンツなど、ロケールなどの要因を基準に分ける必要があるユーザー インターフェイス アセットです。

**オンデマンド コンテンツ**  

後でダウンロードするコンテンツです。 たとえば、新しいレベル、スキン、機能をダウンロードできるアプリ内購入などです。

**ライセンスと取得の分離**  

アプリから独立してコンテンツのライセンス付与と取得を行うことができます。

**アプリ内取得**  

アプリ内部からコンテンツを取得するための、プログラムによるサポートがあるかどうかを示します。

**インストール時間の最適化**

ストアからアプリを取得して実行を開始するまでにかかる時間を短縮する機能を提供します。

**ディスク使用量の削減** 必要なアプリやリソースのみを含めることでアプリのサイズを削減します。

**パッケージ化の最適化** 大規模または複雑なアプリのためのアプリのパッケージ化プロセスを最適化します。

**公開までの時間の短縮** Microsoft Store、ローカル共有、または Web サーバーでアプリを公開するのにかかる時間を最小限に抑えます。

## <a name="technology-descriptions-the-columns-in-the-table-above"></a>テクノロジの説明 (上のテーブルの列)

**リソース パッケージ**

リソース パッケージは、アプリで複数のディスプレイ サイズとシステム言語に対応できるようにするアセットのみのパッケージです。 リソース パッケージは、ユーザー言語、システム スケール、および DirectX 機能をターゲットにしており、さまざまなユーザー シナリオに合わせてアプリを調整できます。 アプリ パッケージには複数のリソースが含まれている可能性がありますが、OS はユーザー デバイスごとに適切なリソースだけをダウンロードするため、帯域幅とディスク領域が節約されます。

**アセット パッケージ**アセット パッケージは、アプリで使用される実行可能ファイルまたは非実行可能ファイルの一般的な一元化されたソースです。 これらは、通常、非プロセッサまたは言語固有のファイルです。 たとえば、1 つのアセット パッケージの画像のコレクション、および別のアセット パッケージのビデオが含まれる可能性があります。両方ともアプリで使用されます。 たとえば、1 つのアセット パッケージの画像のコレクション、および別のアセット パッケージのビデオが含まれる可能性があります。 アプリで複数のアーキテクチャと複数言語をサポートする場合、これらのアセットはアーキテクチャ パッケージまたはリソース パッケージに含まれる可能性がありますが、これは、異なるアーキテクチャ パッケージ間で複数回アセットが複製され、ディスク領域を占有することも意味します。 アセット パッケージを使用している場合は、アプリ パッケージ全体に 1 回のみ含める必要があります。 詳細については、「[アセット パッケージの概要](../packaging/asset-packages.md)」を参照してください。

**オプション パッケージ**

オプション パッケージは、アプリ パッケージの元の機能を補完または拡張するために使用されます。 アプリを公開した後に、しばらく経ってからオプション パッケージ公開したり、アプリとオプション パッケージの両方を同時に公開したりすることができます。 オプション パッケージを利用してアプリを拡張することによって、別のアプリ パッケージとしてコンテンツを配信して収益を得られるメリットがあります。 オプション パッケージは一般的に、元のアプリ開発者によって開発されることを意図しています。それは、(アプリ拡張機能とは異なり) オプション パッケージがメイン アプリの ID を使用して実行されるためです。 オプション パッケージの定義方法に応じて、コード、アセット、またはコードとアセットの両方をオプション パッケージからメイン アプリに読み込むことができます。 個別に収益化、ライセンス付与、および配信できるコンテンツでアプリを強化することを検討している場合は、オプション パッケージが適切です。 実装の詳細については、「[オプション パッケージと関連セットの作成](https://docs.microsoft.com/windows/uwp/packaging/optional-packages)」を参照してください。

**フラット バンドル**
[フラット バンドル アプリ パッケージ](../packaging/flat-bundles.md)は通常のアプリ バンドルに似ていますが、フォルダー内にすべてのアプリ パッケージを含めるのではなく、フラット バンドルにはそれらのアプリ パッケージへの*参照*のみ含まれる点が異なります。 ファイル自体ではなくアプリ パッケージへの参照を含めることで、フラット バンドルはアプリをパッケージ化してダウンロードするのにかかる時間を短縮します。

**アプリの拡張機能**

[アプリの拡張機能](https://docs.microsoft.com/uwp/api/windows.applicationmodel.appextensions) で、他の UWP アプリから提供されるコンテンツをホストすることができます。 それらのアプリの読み取り専用コンテンツを検出、列挙し、アクセスすることもできます。

拡張機能がアプリでサポートされている場合、開発者はだれでもそのアプリの拡張機能を提出できます。 したがって、ホスト アプリは事前にテストされていない拡張機能を読み込む際に、堅牢であることが求められます。 拡張機能は信頼できないと見なされる必要があります。

アプリケーションで拡張機能のコードを読み込むことはできません。 コードを実行する必要がある場合は、アプリ サービスを検討してください。

**アプリ サービス**

Windows アプリ サービスでは、UWP アプリからほかのユニバーサル Windows アプリにサービスを提供できるようにすることで、アプリ間通信を実現します。 アプリ サービスでは、同じデバイス上のアプリから呼び出せる UI を持たないサービスを作成できます。また、Windows 10 バージョン 1607 以降では、リモート デバイスからも呼び出せます。 詳しくは、「[アプリ サービスの作成と利用](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service)」をご覧ください。

アプリ サービスは、他の UWP アプリにサービスを提供する UWP アプリです。 これは、デバイス上にある Web サービスのようなものです。 アプリ サービスは、バック グラウンド タスクとしてホスト アプリで実行され、そのサービスを他のアプリに提供することができます。 たとえば、アプリ サービスによって、他のアプリで使用できるバー コード スキャナー サービスが提供される場合があります。 また、アプリのエンタープライズ スイートに共通のスペル チェック アプリ サービスを備えておき、そのサービスを同じスイート内の他のアプリから利用可能にする場合もあるでしょう。

**UWP アプリ ストリーミング インストール**

ストリーミング インストールは、ユーザーにアプリを配信する方法を最適化する手段です。 アプリ全体がダウンロードされるのを待ってからユーザーが使用できるようになるのではなく、必要な部分がダウンロードされた時点で、そのアプリを利用できます。 基本的なライセンス認証と起動に必要なセクションと、アプリの他の部分の追加コンテンツにアプリを分割するかどうかは、開発者の任意です。 詳しい情報と実装の詳細については、「[UWP アプリ ストリーミング インストール](https://docs.microsoft.com/windows/uwp/packaging/streaming-install)」を参照してください。

## <a name="see-also"></a>関連項目

[アプリ サービスの作成と利用](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service)  
[アセット パッケージの概要](../packaging/asset-packages.md)  
[パッケージ レイアウトを使ったパッケージの作成](../packaging/packaging-layout.md)  
[オプション パッケージと関連セットの作成](https://docs.microsoft.com/windows/uwp/packaging/optional-packages)  
[アセット パッケージとパッケージ圧縮を使った開発](../packaging/package-folding.md)  
[UWP アプリ ストリーミング インストール](https://docs.microsoft.com/windows/uwp/packaging/streaming-install)  
[フラット バンドル アプリ パッケージ](../packaging/flat-bundles.md)  
[Windows.ApplicationModel.AppService 名前空間](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.AppService)  
[Windows.ApplicationModel.Extensions 名前空間](https://docs.microsoft.com/uwp/api/windows.applicationmodel.appextensions)  