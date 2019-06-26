---
title: 補足のプロパティを使用します。
description: Windows で実装された方法で補足のプロパティと詳細の使用の概要
ms.date: 01/10/2017
ms.topic: article
keywords: windows 10、uwp、WinRT API では、インデクサー、検索
localizationpriority: medium
ms.openlocfilehash: 2a77bfc37d853efd28bde9bc3043d072888822f2
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369264"
---
# <a name="using-supplemental-properties"></a>補足のプロパティを使用します。  

## <a name="summary"></a>概要  
- 補足のプロパティは、ファイルを変更することがなくプロパティを持つタグ ファイルにアプリを許可します。 
- を計算することは困難プロパティがある場合またはファイルを変更できないに役立ちます。 
- 他のプロパティ システムを使用して、Windows のプロパティと同じ補足プロパティを使用して  

## <a name="introduction"></a>概要 
過去数年で魅力的な新しいアプリの多くは、作成された日付などの基本的な事項を超えるファイルから便利なプロパティを抽出するユーザー ファイルの CPU 集約型の操作を実行している必要があります。 これらのアプリは、画像、メールやテキスト分析でグループのドキュメントをインテントの抽出内の認識をまとめてオブジェクトの操作を行います。 これは、方法で駆動強力なコンピューティング向けのほとんどの Pc で公開されています。   

すぐに検索可能にするには、このメタデータに使用できるユーザー指数関数的により生産性を向上します。 興味深いは、単に、娘が、画像を知ることが、彼女の祖母の彼女の作品の画像を検索できるははるかに多くに便利です。 コンピューターのフィールより個人とより alive のエクスペリエンスになります。 ユーザーがコンピューターでに問い合わせる、大切なを見つけるのに役立ちます。 

数十年間、Windows 上の高速検索のソリューションが、インデクサーをされているし、Creators Update で更新が行われてこれらの新しいシナリオをサポートするためにします。 アプリでは、タグのファイル システムで抽出するもの以外の追加のプロパティでできますようになりました。 これらのプロパティは、ファースト クラスの市民として扱われます。  

## <a name="windows-properties"></a>Windows プロパティ 
[Windows プロパティ システム](https://docs.microsoft.com/windows/desktop/properties/windows-properties-system)年間のファイルとの対話のキーの一部となっています。 これにより、アプリのすべての異なるファイル形式や言語にファイルを表示できる内部構造を知らなくても、ファイルからプロパティを読み取るができます。 すべてが抽象化することが開発者として、行う必要があるものはリストの要求し、昇順または降順を指定します。  

プロパティ システムが Windows のインデクサーと絡まり合って – そのスコープ内のファイルからすべてのプロパティを読み取りに格納します。 後でときにアプリが要求を変更するには、日付で並べ替えられるフォルダー内のすべての .docx の一覧については、インデクサー John Smith が作成したものを除いてできる一覧を返します。 すぐにします。  

システムの処理の欠点は、すべてのプロパティを必要とするためのインデクサーには保存すぐに使用できるファイルに関するです。 これをハードの時間の要件であるためにの計算に長い時間がかかる重要なプロパティについて理解しておくことを制限します。  

簡単にプロパティを使用して、アプリは、データベースの操作と同様に、ファイルのプロパティの並べ替えられたセットを依頼するか、または検索エンジンを使用するようにクエリを渡すことができます。 インデクサーは、クエリを処理し、結果を返します。 これを開発者に提供 (たとえば検索 jpg ファイルのみ)、フィルターを結合する柔軟性、ユーザーのクエリ (ファイル名が「鳥」で始まる) を使用します。 

## <a name="supplemental-properties"></a>補足のプロパティ 

補足のプロパティと同様に動作正規の Windows プロパティ 1 つの非常に重要な違い: インデクサーにファイルが追加されたときに書き込まれるは行いません。 補足のプロパティは、後で、システム上の別のアプリを追加する必要があります。 これは、2 分後からオブジェクトの認識が完了または日後にある可能性があります。 

プロパティが書き込まれた後検索、フィルター処理、並べ替え、またはそのシステムの他のプロパティと同じようにグループ化します。 使用できますで結合されたクエリ、システム上の他のプロパティを持つか、補足かどうか。 これは、再書き込みを行うことがなく、既存のファイル システム コードを簡単に補足プロパティを結合する柔軟性を提供します。  

### <a name="example-scenarios"></a>シナリオ例 

何千もの補足のプロパティの書き込みがさまざまなプロパティがありますが、このチュートリアルに戻ると保持する主要なシナリオのいくつかあります。  

#### <a name="tagging-pictures-with-extracted-properties"></a>抽出されたプロパティで画像をタグ付け 
これらのアプリは、イメージ内のオブジェクトなど、システムが把握するイメージからの特徴の抽出を ML トレーニング済みモデルを使用できます。 イメージの特定のオブジェクトを取得し、および後で、検索やグループ化のため、プロパティ システムに追加できます。  

#### <a name="tagging-files-with-an-app-specific-id"></a>アプリ固有の ID を持つファイルをタグ付け 
多くのアプリのファイル同期では、サーバーとクライアントのさまざまなデバイスの間で移動するために、ファイルを追跡するために、独自の一意の ID を使用します。 同期クライアントは、ファイルの影響を与えずに、プロパティ システムにこの ID を記述できます。 この ID は、高速アクセスを後でアプリに対して使用できると他のアプリ、システム同期プロバイダーと通信するときの読み取りに使用できるようになりました。 

補足のプロパティを使用するための他の多くのオプションがありますが、これらの両方の高速検索や検索に必要なため、良い例のように、情報システムが認識できないし、ファイル自体に追加できません。  

### <a name="using-supplemental-properties"></a>補足のプロパティを使用します。 
補足プロパティを使用すると、ファイル システムへの通常のプロパティの書き込みと同じです。 StorageFiles とプロパティの使用を選んだ場合は、これを省略できます。 それ以外の場合、1 つのプロパティをファイルに書き出しと同じプロパティを戻すを後で読み取りの簡単なサンプルを見てみましょう。  

### <a name="writing-supplemental-properties"></a>補足のプロパティの書き込み  
サンプルは、わかりやすくするために、検出された最初のファイルのみ変更が、アプリが検出されたすべてのファイルにプロパティを追加は一般にします。  

```csharp
// Only indexed jpg files are going to be used 
QueryOptions option = new QueryOptions(CommonFileQuery.DefaultQuery, new string[] { ".jpg" }); 
option.IndexerOption = IndexerOption.OnlyUseIndexer; 
// Typically an app would loop over all the files in the library, updating them all with the new 
// value. To make the sample easier to understand however, this app is only going to update the  
// first file it finds 
var query = KnownFolders.PicturesLibrary.CreateFileQueryWithOptions(option); 
StorageFile file = (await query.GetFilesAsync()).FirstOrDefault(); 
if (file == null) 
{ 
    log("No jpg file found in the library. Stopping"); 
    return; 
} 
log("Found file: " + file.Path); 
// Selecting the property to modify and writing it out 
List<KeyValuePair<string, object>> props = new List<KeyValuePair<string, object>>();             
props.Add(new KeyValuePair<string, object>("System.Supplemental.ResourceId", fileId)); 
await file.Properties.SavePropertiesAsync(props); 
```

重要なチェックがある場合は、プロパティを記述する前に、場所のインデックスを作成します。 このサンプルでは、場所をインデックス作成のみをフィルター処理、クエリ オプションを使用します。 これを実行できない場合は、親フォルダー ([ファイル] のインデックス付きの状態を確認できます。GetParentAsync() します。GetIndexedStateAsync()) します。 どちらの方法には、同じ結果が生じる場合します。 

### <a name="reading-supplemental-properties"></a>補足のプロパティの読み取り 
もう一度、補足のプロパティの読み取りは、他のファイル システム プロパティを読み取ると同じです。 このサンプルでは、アプリがのみ 1 つのプロパティ ファイルからの読み取り、StorageFile が既にがもと同時に他のプロパティを読み取ることできます。  

```csharp
// An object to hold the result from the indexer, and a string to store  
// the value in once we have confirmed it is valid. 
object uncheckedResourceId; 
string resourceId = ""; 
// Fetching the key value pair from the indexer 
IDictionary<string,object> returnedProps =  
    await file.Properties.RetrievePropertiesAsync(new string[] { "System.Supplemental.ResourceId" });             
if (returnedProps.TryGetValue("System.Supplemental.ResourceId", out uncheckedResourceId)) 
{ 
    if (uncheckedResourceId != null && !String.IsNullOrEmpty(uncheckedResourceId.ToString())) 
    { 
        resourceId = uncheckedResourceId.ToString(); 
    } 
} 
```
チェックは、プロパティ システムから返される値が期待どおりになっていることを確認します。 可能性はありませんが、アプリが書き込まれるため、値がクリアされたことができます。 これについては、以下で詳しく説明します。  

### <a name="implementation-notes"></a>実装に関する注意事項 
補足のプロパティのデザインに加えられたいくつかの微妙な選択肢があります。 実装を支援するには、次のセクションでは、機能エンジニア リング設計仕様からコピーしました。 機能の設計方法と制限事項が存在する理由に、glimpse に関する情報を提供します。 

### <a name="supplemental-properties-available"></a>使用できる補足プロパティ 
アプリを最初に使用できる 2 つのプロパティがあります。System.Supplemental.ResourceId System.Supplemental.AlbumID. 追加できる他の必要性がある場合 アルバムの ID は、多様なアプリケーション用に使用できる複数値文字列と ResourceId は、同期のクラウド プロバイダーの一意の ID として使用されます。 

#### <a name="file-system-support"></a>ファイル システムのサポート 
FAT 形式のリムーバブル メディアは、重要なシナリオ、補足のプロパティは FAT と NTFS ドライブをサポートします。 これにより、補足のプロパティは、デバイスの種類に関係なくすべてのユーザーに利用できるものが保証されます。   

### <a name="non-indexed-locations"></a>インデックスのない場所  
デスクトップで多数のインデックス化されていないフォルダーがあります。 このような場合は、アプリが補足のプロパティにアクセスする可能性がありますも。 ただし、補足のプロパティでは、インデックス付きの場所の外部で使用できません。 理由はいくつかのトレードオフが行われました。  

- 既定ですべてのライブラリおよびクラウド ストレージの場所のインデックスが作成されます。   
  これらの場所を主に使用するには、その UWP アプリには。 インデックス付き (システムやネットワーク ドライブ) ではない他の場所があるが、ユーザー データを格納するため、使用頻度の低い。 

- WinRT API サーフェスの設計では、インデクサーが使用可能なほとんどの場合を前提としています。  
  したがって、インデクサーは既に使用可能なほとんどのアプリの関心のある場所です。 インデックスのない場所にデータを保存するユーザーが見つかった場合、最も簡単なソリューションがその場所をインデックスに追加することになります。 プロパティを補足し、作業、列挙体は、高速になり、アプリが変更できる場所を追跡します。

### <a name="reading-or-writing-supplemental-properties-from-a-file-in-a-non-indexed-location"></a>読み取りまたは書き込み Non-Indexed 場所にあるファイルからの補足のプロパティ 
アプリが現在インデックス付けされていない場所に補足プロパティを記述しようとする場合は、API 呼び出しは例外をスローします。 .Docx ファイルは (無効な引数) に System.Music.AlbumArtist の更新を試行したときに、としてスローされる例外と同じ例外になります。  
 
### <a name="change-notifications"></a>通知を変更します。  
UWP の変更通知され、変更の追跡は、標準のプロパティのように、補足のプロパティに対して動作する続行されます。 これにより、アプリがアプリのいずれかに行われているすべての変更を追跡するためにデータを指定します。 
  
### <a name="invalidating-properties"></a>プロパティを無効にします。  
ファイルの補足のプロパティは、ファイルを変更またはシステムに移動したときに古くなる可能性があります。 アプリのデータのプッシュは、データが有効か、システムは解明自体にするためのツールを提供だけを更新する必要がある場合について、情報のあるものになります。  
 
場合は、ファイルが変更されたがいない移動または名前が変更された、ファイルのすべての補足プロパティは変更されません。 アプリは既存の API サーフェスでの変更通知を登録し、必要に応じてプロパティを更新することになります。 
 
ファイルを移動すると、プロパティが無効にましょう。 アプリは削除するかの変更通知の受信、作成、名前の変更、または方法によって移動操作では正確に実行されます。 アプリが変更通知を受信した後は、ファイルを検査し、必要に応じて、ファイルの補足のプロパティを更新することがあります。 
 
### <a name="indexer-rebuilds"></a>インデクサーを再構築します。  
場合によってはシステム インデックスは、さまざまな理由の 1 つの再構築する必要があります。-プロパティ スキーマを変更することが、ユーザーには、EDP が有効にする可能性があります。 または単なるデータベース ファイルが破損します。 このような場合は、補足のプロパティは保持されません。 私たちは、インデックスが再構築されるが、いくつかの主要なブロックがあった場合に、補足のプロパティを保持するために作業を行うと見なされます。  

### <a name="protecting-the-data"></a>データを保護します。 
ディスク エラーまたは悪意のあるソフトウェアによって、データベース ファイルが破損している場合は、そのファイルに格納されたデータを保護することは不可能なります。 システムの他の場所またはデータベースの残りの部分から何らかの形で分離を格納する必要があります。 

既に多くのインデックスが破損する可能性が低くする作業を行っている、ためこのケースの発生率をとにかくこれ低減されます。  
再構築中には、ファイルとそのメタデータの間のマッピングの保持 

インデックス再構築、データを保護できます、場合でも、インデックスが再構築されるときに、ファイルが変更されたかどうかを把握することはできません。 インデックスは、ファイルから保護するデータは、ファイルを変更または移動する場合に有効なできなくする可能性があります。  
動作 

場合はインデクサーの再構築では、補足のすべてのデータが失われます。 アプリは、再構築中に失われた、インデクサーにデータを戻す担当になります。 これにより、余分な負荷をアプリの配置しますと思われる妥当なので、すべてのデータのマスターの状態は常に保持します。  

### <a name="recovering"></a>回復します。 
インデックスが再構築されるアプリが気付き後の都合のよい、補足のプロパティが更新されます。  
### <a name="privacy"></a>プライバシー 
ファイルが書き込まれるプロパティの一部はユーザーに禁止するその他のアプリケーションと共有するようにでしょう。 アプリのプロパティへの書き込みは、情報が、いずれかに private を指定しようとしていることを示すことができるよう、アプリケーションで他の少数のアプリケーションと共有またはパブリック システム上のすべてのアプリにします。  

これは、一部の機能の早期採用者の面白い機能では可能性のある、設計に多くの価値を追加するパブリック プロパティの取得を移動も感じてください。 したがって、これには、優れたとしてマークされています、引き続きを必要な場合、値を非表示をサポートしていない機能をビルドする必要があります。 任意の設計で考慮すべき重要なので後で追加することがより多くのシナリオを開きます。  

## <a name="conclusions"></a>結論 
これで、補足のプロパティは、システムで複数のファイルのプロパティを格納する簡単な方法です。 それらを使用してをすることはもちろん、省略可能ですが、アプリ、エッジの並べ替えし、データを迅速に検索することはできませんが、他のアプリ経由で。 

お楽しみにしてこれらのプロパティの使用を開始するアプリを表示します。 使用する方法、ヘッダーご連絡ください下のコメントに質問がある場合 