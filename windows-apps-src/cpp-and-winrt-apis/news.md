---
author: stevewhims
description: ニュースや変更を C++/WinRT します。
title: 新機能、C++/WinRT
ms.author: stwhi
ms.date: 10/03/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、ニュース、ものの新機能
ms.localizationpriority: medium
ms.openlocfilehash: bc6be28e112dfdd14b3585bd88ba066fbeae382d
ms.sourcegitcommit: 933e71a31989f8063b020746fdd16e9da94a44c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2018
ms.locfileid: "4539023"
---
# <a name="whats-new-in-cwinrt"></a>新機能、C++/WinRT

次の表のニュースを含むし、に加えられる変更[、C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)一般公開バージョンの最新の Windows SDK では 10.0.17763.0 (Windows 10、バージョン 1809)。 これらの変更は、それ以降の SDK Insider Preview バージョンに存在する場合もあります。

## <a name="news-and-changes-in-windows-sdk-version-100177630-windows-10-version-1809"></a>ニュース、およびの変更、Windows SDK バージョン 10.0.17763.0 (Windows 10、バージョン 1809)

| 新規または変更された機能 | 詳細 |
| - | - |
| **変更を分割**しています。 コンパイル、C + + WinRT は、Windows SDK からのヘッダーに依存しません。 | [Windows SDK ヘッダー ファイルから分離](#isolation-from-windows-sdk-header-files)、以下をご覧ください。 |
| Visual Studio のプロジェクト システム形式が変更されました。 | 参照してください[c++ ターゲットを変更する方法/WinRT プロジェクトを Windows SDK のそれ以降のバージョンを](#how-to-retarget-your-cwinrt-project-to-a-later-version-of-the-windows-sdk)ください。 |
| 新しい関数と基底クラスまたは独自のコレクションのプロパティとコレクション型を実装するため、Windows ランタイム関数にコレクション オブジェクトを渡すことがあります。 | 参照してください[コレクション、C++/WinRT](collections.md)します。 |
| [{Binding}](/windows/uwp/xaml-platform/binding-markup-extension)マークアップ拡張機能を使用するには、C + + WinRT ランタイム クラスです。 | 詳しくとコード例では、[データ バインディングの概要](/windows/uwp/data-binding/data-binding-quickstart)をご覧ください。 |
| コルーチンをキャンセルするサポートでは、取り消しコールバックを登録することができます。 | 詳しくとコード例については、[キャンセル、非同期操作と取り消しコールバック](concurrency.md#canceling-an-asychronous-operation-and-cancellation-callbacks)をご覧ください。 |
| メンバー関数を指すデリゲートを作成するときは、強参照またはポイントで、ハンドラーが登録されている (raw*この*ポインター) ではなく、現在のオブジェクトへの弱参照を確立できます。 | 詳しくとコード例では、[安全に、イベント処理デリゲートを使用して*この*ポインターへのアクセス](weak-references.md#safely-accessing-the-this-pointer-with-an-event-handling-delegate)のセクションで**デリゲートとしてメンバー関数を使用する場合**のサブ セクションをご覧ください。 |
| 標準的な C++ に Visual Studio の適合性を向上によって発見されたバグを修正します。 LLVM および Clang ツール チェーンがよりも活用すると、検証、C++/WinRT の標準への準拠します。 | ありますされなくなったが発生した問題はありません新しいプロジェクトを[で説明されている理由コンパイルかどうか。Visual Studio 2017 を使用している (バージョン 15.8.0 以上)、および SDK バージョン 17134](faq.md#why-wont-my-new-project-compile-im-using-visual-studio-2017-version-1580-or-higher-and-sdk-version-17134) |

その他の変更。

- **変更を分割**しています。 [**winrt::get_abi(winrt::hstring const&)**](/uwp/cpp-ref-for-winrt/get-abi)返すようになりました`void*`の代わりに`HSTRING`します。 使用することができます`static_cast<HSTRING>(get_abi(my_hstring));`、HSTRING を取得します。
- **変更を分割**しています。 [**winrt::put_abi(winrt::hstring&)**](/uwp/cpp-ref-for-winrt/put-abi)返すようになりました`void**`の代わりに`HSTRING*`します。 使用することができます`reinterpret_cast<HSTRING*>(put_abi(my_hstring));`HSTRING * を取得します。
- **変更を分割**しています。 HRESULT は**winrt::hresult**として投影されるようになりました。 HRESULT (型の確認、または型の特性をサポートするためにに)、必要なかどうかは、することができます`static_cast` **winrt::hresult**します。 それ以外の場合、 **winrt::hresult**に変換 HRESULT、含める限り`unknwn.h`c++ インクルードする前に +/winrt ヘッダー。
- **変更を分割**しています。 GUID は**winrt::guid**として投影されるようになりました。 実装する Api では、GUID パラメーターの**winrt::guid**を使用する必要があります。 それ以外の場合、 **winrt::hresult**に変換、GUID を含める場合に限り`unknwn.h`c++ インクルードする前に +/winrt ヘッダー。
- **変更を分割**しています。 [**Winrt::handle_type コンス トラクター**](/uwp/cpp-ref-for-winrt/handle-type#handletypehandletype-constructor)は (はできるようになりましたが困難に不適切なコードを記述する) を明示的にすることで強化されています。 未処理のハンドルの値を割り当てる必要がある場合は、代わりに、 [**handle_type::attach 関数**](/uwp/cpp-ref-for-winrt/handle-type#handletypeattach-function)を呼び出します。
- **変更を分割**しています。 **WINRT_CanUnloadNow**および**WINRT_GetActivationFactory**のシグネチャが変更されました。 これらの関数は、すべての宣言照準します。 代わりに、含める`winrt/base.h`(c++ を含める場合に自動的に含まれるされる//winrt Windows 名前空間ヘッダー ファイル) をこれらの関数の宣言を含めます。
- [**Winrt::clock 構造体**](/uwp/cpp-ref-for-winrt/clock) **from_FILETIME/to_FILETIME**が**from_file_time/to_file_time**避けます推奨されなくなりました。
- **IBuffer**パラメーターを期待する Api が簡略化されます。 ほとんどの Api は、コレクションまたは配列を必要に応じてが十分な Api は C++ からこのような Api を使用して簡単になる必要な**IBuffer**に依存します。 この更新プログラムは、C++ 標準ライブラリのコンテナーで使用される同じデータ名前付け規則を使用して、 **IBuffer**実装の背後にあるデータへの直接アクセスを提供します。 これは、従来どおり大文字で始まるメタデータの名前との衝突もなくなります。
- コード生成の向上: コードのサイズを小さくさまざまな機能強化の向上、インラインと工場出荷時のキャッシュを最適化します。
- 不要な再帰が削除されます。 とき、コマンド ラインは特定のではなく、フォルダーに`.winmd`、`cppwinrt.exe`ツールを再帰的を検索されなくなった`.winmd`ファイル。 `cppwinrt.exe`ツールも処理重複よりインテリジェントなには、適切な形式は、ユーザーのエラーを回復力の強化`.winmd`ファイル。
- セキュリティ強化のスマート ポインター。 以前は、取り消すときに失敗したイベント revokers 移動に割り当てられた新しい値。 これスマート ポインター クラス自動割り当ての処理を減少が生じない確実に問題が明らかになりました[**winrt::com_ptr 構造体のテンプレート**](/uwp/cpp-ref-for-winrt/com-ptr)が発行されます。 **winrt::com_ptr**が修正されましたし、処理する固定イベント revokers 移動セマンティクス正しく割り当て時に取り消すことができるようにします。

> [!NOTE]
> 1.0.181002.2 のバージョンで (またはそれ以降) の[、C++/WinRT Visual Studio Extension (VSIX)](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix)インストールされると、作成する新しい C + + WinRT プロジェクトは、そのプロジェクトの[Microsoft.Windows.CppWinRT NuGet パッケージ](https://www.nuget.org/packages/Microsoft.Windows.CppWinRT/)を自動的にインストールします。 Microsoft.Windows.CppWinRT NuGet パッケージを提供強化 C + + WinRT プロジェクト ビルドのサポート、開発コンピューターと (のみ、NuGet パッケージと、VSIX ではないがインストールされている)、ビルド エージェントの間で移植プロジェクトを作成します。
>
> 既存のプロジェクトの&mdash;1.0.181002.2 のバージョンをインストールした後 (またはそれ以降) VSIX の&mdash;Visual Studio でプロジェクトを開く場合は、**プロジェクト**をクリックすることをお勧めします \> **NuGet パッケージを管理する.** \> **参照**、入力または**Microsoft.Windows.CppWinRT**を検索ボックスに貼り付ける、検索結果、項目を選択して**インストール**をそのプロジェクトのパッケージをインストールする] をクリックします。


## <a name="isolation-from-windows-sdk-header-files"></a>Windows SDK ヘッダー ファイルから分離

これは、可能性のあるコードの変更点です。

コンパイル、C + + WinRT がしなくなったから Windows SDK ヘッダー ファイルに依存します。 また、C ランタイム ライブラリ (CRT) と C++ 標準テンプレート ライブラリ (STL) のヘッダー ファイルは、Windows SDK ヘッダーを含めないでください。 およびを標準への準拠を向上、不注意の依存関係を回避できますおよびから保護する必要があるマクロの数を大幅に削減します。

このに依存しないことを意味する、C++/WinRT は複数の移植性と標準に準拠した、なり、クロス コンパイラとクロス プラットフォーム ライブラリになる可能性が強化されます。 意味、C++/cli/winrt ヘッダーいない悪影響を与える影響を受けるマクロです。

以前、C++ をそのまま場合/WinRT 今すぐそれらを含める必要がありますし、プロジェクトで、Windows ヘッダーをインクルードします。 いずれの場合でも、常のベスト プラクティスに基づくヘッダーを明示的に指定して、いない別のライブラリに含めることのままにします。

現時点では、Windows SDK ヘッダー ファイルの分離の唯一の例外は、組み込みと数値です。 これら最後の残りの依存関係のある既知の問題はありません。

プロジェクトを再度有効にする Windows SDK ヘッダーとの相互運用する必要がある場合。 たとえば、( [**IUnknown**](https://msdn.microsoft.com/library/windows/desktop/ms680509)が発行) COM インターフェイスを実装する、可能性があります。 この例では、含める`unknwn.h`c++ インクルードする前に +/winrt ヘッダー。 その原因を行うには c++/cli を従来の COM インターフェイスをサポートするためにさまざまなフックを有効にする/winrt 基本ライブラリ。 コード例については[Author COM コンポーネントにおいて、C++/WinRT](author-coclasses.md)します。 同様に、明示的に宣言型や関数を呼び出しているその他の Windows SDK ヘッダーを含めます。

## <a name="how-to-retarget-your-cwinrt-project-to-a-later-version-of-the-windows-sdk"></a>C++ のターゲットに変更する方法/以降のバージョンの Windows SDK に WinRT プロジェクト

また、最小限のコンパイラとリンカーの問題が発生する可能性があるプロジェクトの再ターゲットのメソッドでは最も労力が必要です。 (任意の Windows SDK バージョンをターゲットとして)、新しいプロジェクトを作成して、古いからは経由で新しいプロジェクトのファイルをコピーし、そのメソッドが含まれます。 古いのセクションがあります`.vcxproj`と`.vcxproj.filters`すればファイルのコピーを Visual Studio でファイルを追加することができます。

ただし、Visual Studio でプロジェクトのターゲットを変更するその他の 2 つの方法はあります。

- **一般的な**プロパティをプロジェクトに移動 \> **Windows SDK のバージョン**と選択の**すべての構成**と**すべてのプラットフォーム**です。 バージョンをターゲットにするには、 **Windows SDK バージョン**を設定します。
- **ソリューション エクスプ ローラー**でプロジェクト ノードを右クリックして、**プロジェクトの再ターゲット**] をクリックを対象とするバージョンを選択し、 **[ok]** をクリックします。

これら 2 つのメソッドのいずれかを使用した後、コンパイラやリンカーのエラーが発生するかどうかは、ソリューションをクリーンアップしてみてください (**ビルド** > **クリーンなソリューション**や、すべての一時フォルダーとファイルを手動で削除) もう一度ビルドを試みる前にします。

C++ コンパイラーが場合"*エラー C2039: 'IUnknown': のメンバーではない '\'global 名前空間'*"、追加し、`#include <unknwn.h>`の先頭に、`pch.h`ファイル (c++ インクルードする前に +/winrt ヘッダー)。

追加する必要がありますも`#include <hstring.h>`その後。

C++ リンカーを生成する場合"*エラー lnk 2019: 外部シンボルは未解決です_WINRT_CanUnloadNow@0関数で参照されている_VSDesignerCanUnloadNow@0*"を追加することで解決できます`#define _VSDESIGNER_DONT_LOAD_AS_DLL`を`pch.h`ファイル。