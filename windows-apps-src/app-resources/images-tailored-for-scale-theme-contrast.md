---
author: stevewhims
Description: "アプリで、表示倍率、テーマ、ハイ コントラスト、その他の実行時のコンテキストに合わせた画像を含む画像リソース ファイルを読み込むことができます。"
title: "表示倍率、テーマ、ハイ コントラスト、その他の設定に合わせた画像とアセットの読み込み"
template: detail.hbs
ms.author: stwhi
ms.date: 10/10/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: "Windows 10, UWP, リソース, 画像, アセット, MRT, 修飾子"
localizationpriority: medium
ms.openlocfilehash: d7ff64340de4688a53b5b6aee9bf18c26128de07
ms.sourcegitcommit: 44a24b580feea0f188c7eae36e72e4a4f412802b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
<link rel="stylesheet" href="https://az835927.vo.msecnd.net/sites/uwp/Resources/css/custom.css">

# <a name="load-images-and-assets-tailored-for-scale-theme-high-contrast-and-others"></a>表示倍率、テーマ、ハイ コントラスト、その他の設定に合わせた画像とアセットの読み込み

アプリで、[表示倍率](../layout/screen-sizes-and-breakpoints-for-responsive-design.md)、テーマ、ハイ コントラスト、その他の実行時のコンテキストに合わせた画像リソース ファイル (またはその他のアセット ファイル) を読み込むことができます。 これらの画像は、命令型コードや XAML マークアップ (**Image** の **Source** プロパティなど) から参照できます。 また、アプリ パッケージ マニフェスト (`Package.appxmanifest` ファイル) に (たとえば、Visual Studio マニフェスト デザイナーの [ビジュアル資産] タブでアプリ アイコンの値として) 表示することや、タイルやトースト通知に表示することもできます。 画像のファイル名に修飾子を使用し、必要に応じて [**ResourceContext**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live) を使って動的に読み込むことによって、ユーザーの実行時の表示倍率、テーマ、ハイ コントラスト、言語、その他のコンテキストの設定に最も一致する最適な画像ファイルを読み込むことができます。

画像リソースは、画像リソース ファイルに含まれています。 画像はアセット、画像を含むファイルはアセット ファイルと考えることができ、これらの種類のリソース ファイルはプロジェクトの \Assets フォルダーにあります。 画像リソース ファイルの名前に修飾子を使用する方法の詳細については、「[言語、スケール、その他の修飾子用にリソースを調整する](tailor-resources-lang-scale-contrast.md)」をご覧ください。

画像の一般的な修飾子には、[scale](tailor-resources-lang-scale-contrast.md#scale)、[theme](tailor-resources-lang-scale-contrast.md#theme)、[contrast](tailor-resources-lang-scale-contrast.md#contrast)、[targetsize](tailor-resources-lang-scale-contrast.md#targetsize) があります。

## <a name="qualify-an-image-resource-for-scale-theme-and-contrast"></a>スケール、テーマ、コントラストに合わせて画像リソースを修飾する

`scale` 修飾子の既定値は `scale-100` です。 そのため、次の 2 つのバリエーションは同等です (いずれもスケール 100、つまり倍率 1 の画像を提供します)。

```
\Assets\Images\logo.png
\Assets\Images\logo.scale-100.png
```

修飾子は、ファイル名の代わりにフォルダー名に使用できます。 修飾子ごとにいくつかのアセット ファイルがある場合、この方法が適しています。 わかりやすい例として、次の 2 つのバリエーションは上記の 2 つと同等です。

```
\Assets\Images\logo.png
\Assets\Images\scale-100\logo.png
```

次の例では、表示倍率、テーマ、ハイ コントラストのさまざまな設定に合わせて、`/Assets/Images/logo.png` という名前の画像リソースのバリエーションを提供する方法を示します。 この例では、フォルダー名を使用しています。

```
\Assets\Images\contrast-standard\theme-dark
    \scale-100\logo.png
    \scale-200\logo.png
\Assets\Images\contrast-standard\theme-light
    \scale-100\logo.png
    \scale-200\logo.png
\Assets\Images\contrast-high
    \scale-100\logo.png
    \scale-200\logo.png
```

## <a name="reference-an-image-or-other-asset-from-xaml-markup-and-code"></a>XAML マークアップとコードから画像やその他のアセットを参照する

画像リソースの名前 (つまり識別子) は、そのパスとファイル名からすべての修飾子を削除したものです。 前のセクションの例のようにフォルダーやファイルに名前を付けている場合、画像リソースは 1 つであり、その (絶対パスとしての) 名前は `/Assets/Images/logo.png` です。 この名前を XAML マークアップで使用する方法は次のとおりです。

**XAML**
```xml
<Image x:Name="myXAMLImageElement" Source="ms-appx:///Assets/Images/logo.png"/>
```

アプリのパッケージに付属しているファイルを参照するため、`ms-appx` URI スキームを使用していることに注意してください。 「[URI スキーム](uri-schemes.md)」をご覧ください。 同じ画像リソースを命令型コード内で参照する方法は次のとおりです。

**C#**
```csharp
this.myXAMLImageElement.Source = new BitmapImage(new Uri("ms-appx:///Assets/Images/logo.png"));
```

`ms-appx` を使用して、アプリ パッケージから任意のファイルを読み込むことができます。

**C#**
```csharp
var uri = new System.Uri("ms-appx:///Assets/anyAsset.ext");
var storagefile = await Windows.Storage.StorageFile.GetFileFromApplicationUriAsync(uri);
```

`ms-appx-web` スキームは、`ms-appx` と同じファイルにアクセスしますが、このファイルは Web コンパートメントにあります。

**XAML**
```xml
<WebView x:Name="myXAMLWebViewElement" Source="ms-appx-web:///Pages/default.html"/>
```

**C#**
```csharp
this.myXAMLWebViewElement.Source = new Uri("ms-appx-web:///Pages/default.html");
```

これらの例に示されているどのシナリオの場合も、[UriKind](https://docs.microsoft.com/en-us/dotnet/api/system.urikind) を推測する [Uri コンストラクター](https://docs.microsoft.com/en-us/dotnet/api/system.uri.-ctor?view=netcore-2.0#System_Uri__ctor_System_String_)のオーバーロードを使用します。 スキームと機関を含む有効な絶対 URI を指定するか、上記の例のように、機関の既定をアプリのパッケージに自動的に設定します。

これらの URI の例で、スキーム ("`ms-appx`" または "`ms-appx-web`") の後に "`://`" が続き、その後に絶対パスが続くことに注意してください。 絶対パスでは、先頭の "`/`" によって、パスはパッケージのルートからのパスとして解釈されます。

**Note** `ms-resource` ([文字列リソース](localize-strings-ui-manifest.md)の場合) および `ms-appx(-web)` (画像やその他のアセットの場合) URI スキームは、自動で修飾子の照合を実行して、現在のコンテキストに最も適切なリソースを見つけます。 `ms-appdata` URI スキーム (アプリ データを読み込むために使用される) は、このような自動的な照合を実行しませんが、[ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_QualifierValues) の内容に応答し、URI の完全な物理ファイル名を使用して、アプリ データから適切なアセットを明示的に読み込むことができます。 アプリ データについては、「[設定と他のアプリ データを保存して取得する](../app-settings/store-and-retrieve-app-data.md)」をご覧ください。 Web URI スキーム (`http`、`https`、`ftp` など) も、自動的な照合を実行しません。 その場合の対処方法については、「[クラウドでの画像のホスティングと読み込み](tile-toast-language-scale-contrast.md#hosting-and-loading-images-in-the-cloud)」をご覧ください。

絶対パスは、画像ファイルがプロジェクト構造での場所に残っている場合に適切な選択肢です。 画像ファイルを移動できるようにする必要があるが、参照している XAML マークアップ ファイルから相対的に同じ場所に残るように注意している場合は、絶対パスの代わりに、ファイルを格納するマークアップ ファイルからの相対パスを使用できます。 その場合、URI スキームを使用する必要はありません。 この場合も、自動的な修飾子の照合のメリットはありますが、それは XAML マークアップで相対パスを使用していることにのみ起因します。

**XAML**
```xml
<Image Source="Assets/Images/logo.png"/>
```

「[言語、スケール、ハイ コントラストに合わせたタイルとトーストのサポート](tile-toast-language-scale-contrast.md)」もご覧ください。

## <a name="qualify-an-image-resource-for-targetsize"></a>ターゲット サイズに合わせて画像リソースを修飾する

同じ画像リソースのさまざまなバリエーションで `scale` 修飾子と `targetsize` 修飾子を使用できますが、リソースの 1 つのバリエーションでその両方を使用することはできません。 また、`TargetSize` 修飾子を持たないバリエーションを少なくとも 1 つ定義する必要があります。 そのバリエーションでは、`scale` の値を定義するか、その既定値を `scale-100` にする必要があります。 したがって、`/Assets/Square44x44Logo.png` リソースのこれら 2 つのバリエーションは有効です。

```
\Assets\Square44x44Logo.scale-200.png
\Assets\Square44x44Logo.targetsize-24.png
```

また、次の 2 つのバリエーションは有効です。 

```
\Assets\Square44x44Logo.png // defaults to scale-100
\Assets\Square44x44Logo.targetsize-24.png
```

ただし、次のバリエーションは有効ではありません。

```
\Assets\Square44x44Logo.scale-200_targetsize-24.png
```

## <a name="refer-to-an-image-file-from-your-app-package-manifest"></a>アプリ パッケージ マニフェストから画像ファイルを参照する

前のセクションの 2 つの有効な例のいずれかのように、フォルダーやファイルに名前を付けている場合、アプリ アイコンの画像リソースは 1 つであり、その (相対パスとしての) 名前は `Assets\Square44x44Logo.png` です。 アプリ パッケージ マニフェストでは、単に名前でリソースを参照します。 URI スキームを使用する必要はありません。

![リソースの追加 (英語)](images/app-icon.png)

必要な処理はこれだけです。OS が自動で修飾子の照合を実行して、現在のコンテキストに最も適切なリソースを見つけます。 アプリ パッケージ マニフェスト内で、このようにローカライズまたはその他の方法で修飾できるすべての項目の一覧については、「[マニフェストのローカライズ可能な項目](/uwp/schemas/appxpackage/uapmanifestschema/localizable-manifest-items-win10?branch=live)」をご覧ください。

## <a name="qualify-an-image-resource-for-layoutdirection"></a>レイアウト方向に合わせて画像リソースを修飾する

「[画像の左右反転](../globalizing/adjust-layout-and-fonts--and-support-rtl.md#mirroring-images)」をご覧ください。

## <a name="load-an-image-for-a-specific-language-or-other-context"></a>特定の言語または他のコンテキスト用の画像を読み込む

アプリのローカライズの価値提案の詳細については、「[グローバリゼーションとローカライズ](../globalizing/globalizing-portal.md)」をご覧ください。

既定の [**ResourceContext**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live) ([**ResourceContext.GetForCurrentView**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_GetForCurrentView) から取得された) には、既定の実行時コンテキスト (つまり、現在のユーザーとコンピューターの設定) を表す、各修飾子名の修飾子の値が含まれています。 画像ファイルは、(その名前に含まれる修飾子に基づいて) 実行時コンテキストでの修飾子の値と比較されます。

ただし、アプリでシステム設定を上書きし、読み込む画像を検索するときに使用する言語、スケール、その他の修飾子の値を明示的に指定することが必要になる場合があります。 たとえば、いつ、どのハイ コントラスト画像を読み込むかを正確に制御することが必要になる場合があります。

そのためには、(既定のものを使用する代わりに) 新しい **ResourceContext** を作成し、その値をオーバーライドして、画像検索でそのコンテキスト オブジェクトを使用します。

**C#**
```csharp
var resourceContext = new Windows.ApplicationModel.Resources.Core.ResourceContext(); // not using ResourceContext.GetForCurrentView 
resourceContext.QualifierValues["Contrast"] = "high";
var namedResource = Windows.ApplicationModel.Resources.Core.ResourceManager.Current.MainResourceMap[@"Files/Assets/Logo.png"];
var resourceCandidate = namedResource.Resolve(resourceContext);
var imageFileStream = resourceCandidate.GetValueAsStreamAsync().GetResults();
var bitmapImage = new Windows.UI.Xaml.Media.Imaging.BitmapImage();
bitmapImage.SetSourceAsync(imageFileStream);
this.myXAMLImageElement.Source = bitmapImage;
```

グローバル レベルで同じ効果を実現するために、既定の **ResourceContext** で修飾子の値を上書きすることが*できます*。 ただし、その代わりに、[**ResourceContext.SetGlobalQualifierValue**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_SetGlobalQualifierValue_System_String_System_String_Windows_ApplicationModel_Resources_Core_ResourceQualifierPersistence_) を呼び出すことをお勧めします。 **SetGlobalQualifierValue** の呼び出しで一度値を設定すると、ResourceContext を検索に使用するたびに、これらの値が既定の **ResourceContext** で有効になります。 既定では、[**ResourceManager**](/uwp/api/windows.applicationmodel.resources.core.resourcemanager?branch=live) クラスは、既定の **ResourceContext** を使用します。

**C#**
```csharp
Windows.ApplicationModel.Resources.Core.ResourceContext.SetGlobalQualifierValue("Contrast", "high");
var namedResource = Windows.ApplicationModel.Resources.Core.ResourceManager.Current.MainResourceMap[@"Files/Assets/Logo.png"];
this.myXAMLImageElement.Source = new Windows.UI.Xaml.Media.Imaging.BitmapImage(namedResource.Uri);
```

## <a name="updating-images-in-response-to-qualifier-value-change-events"></a>修飾子の値の変更イベントへの応答で画像を更新する

実行中のアプリは、既定のリソースのコンテキストで修飾子の値に影響を与えるシステム設定の変更に応答できます。 これらのシステム設定のいずれかが、[**ResourceContext.QualifierValues**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live#Windows_ApplicationModel_Resources_Core_ResourceContext_QualifierValues) の [**MapChanged**](/uwp/api/windows.foundation.collections.iobservablemap_k_v_?branch=live#Windows_Foundation_Collections_IObservableMap_2_MapChanged) イベントを呼び出します。

このイベントへの応答で、既定の **ResourceContext** を使用して画像を再読み込みすることができます。これは、[**ResourceManager**](/uwp/api/windows.applicationmodel.resources.core.resourcemanager?branch=live) が既定で使用するものです。

**C#**
```csharp
public MainPage()
{
    this.InitializeComponent();

    ...

    // Subscribe to the event that's raised when a qualifier value changes.
    var qualifierValues = Windows.ApplicationModel.Resources.Core.ResourceContext.GetForCurrentView().QualifierValues;
    qualifierValues.MapChanged += new Windows.Foundation.Collections.MapChangedEventHandler<string, string>(QualifierValues_MapChanged);
}

private async void QualifierValues_MapChanged(IObservableMap<string, string> sender, IMapChangedEventArgs<string> @event)
{
    var dispatcher = this.myImageXAMLElement.Dispatcher;
    if (dispatcher.HasThreadAccess)
    {
        this.RefreshUIImages();
    }
    else
    {
        await dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal, () => this.RefreshUIImages());
    }
}

private void RefreshUIImages()
{
    var namedResource = Windows.ApplicationModel.Resources.Core.ResourceManager.Current.MainResourceMap[@"Files/Assets/Logo.png"];
    this.myImageXAMLElement.Source = new Windows.UI.Xaml.Media.Imaging.BitmapImage(namedResource.Uri);
}
```

## <a name="important-apis"></a>重要な API

* [ResourceContext](/uwp/api/windows.applicationmodel.resources.core.resourcecontext?branch=live)
* [MapChanged](/uwp/api/windows.foundation.collections.iobservablemap_k_v_?branch=live#Windows_Foundation_Collections_IObservableMap_2_MapChanged)

## <a name="related-topics"></a>関連トピック

* [言語、スケール、その他の修飾子用にリソースを調整する](tailor-resources-lang-scale-contrast.md)
* [UI とアプリ パッケージ マニフェスト内の文字列をローカライズする](localize-strings-ui-manifest.md)
* [設定と他のアプリ データを保存して取得する](../app-settings/store-and-retrieve-app-data.md)
* [言語、スケール、ハイ コントラストに合わせたタイルとトーストのサポート](tile-toast-language-scale-contrast.md)
* [マニフェストのローカライズ可能な項目](/uwp/schemas/appxpackage/uapmanifestschema/localizable-manifest-items-win10?branch=live)
* [画像の左右反転](../globalizing/adjust-layout-and-fonts--and-support-rtl.md#mirroring-images)
* [グローバリゼーションとローカライズ](../globalizing/globalizing-portal.md)