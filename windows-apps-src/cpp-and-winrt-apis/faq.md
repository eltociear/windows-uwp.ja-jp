---
author: stevewhims
description: C++/WinRT での Windows ランタイム API の作成と使用に関する質問への回答です。
title: C++/WinRT についてよく寄せられる質問
ms.author: stwhi
ms.date: 05/07/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: wwindows 10, uwp, 標準, c++, cpp, winrt, プロジェクション, 頻繁, 質問, 質問, faq
ms.localizationpriority: medium
ms.openlocfilehash: 80c27332c05e285fdad6b8ec8deddd82d24a6e4a
ms.sourcegitcommit: 9a17266f208ec415fc718e5254d5b4c08835150c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2018
ms.locfileid: "2889241"
---
# <a name="frequently-asked-questions-about-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt"></a>[C++/WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt) についてよく寄せられる質問
C++/WinRT での Windows ランタイム API の作成と使用に関する質問への回答です。

> [!NOTE]
> 質問の内容が、表示されたエラー メッセージに関するものである場合は、「[C++/WinRT に関する問題のトラブルシューティング](troubleshooting.md)」のトピックも参照してください。

## <a name="what-are-the-requirements-for-the-cwinrt-visual-studio-extension-vsixhttpsakamscppwinrtvsix"></a> [C++/WinRT Visual Studio Extension (VSIX)](https://aka.ms/cppwinrt/vsix) の要件
[VSIX](https://aka.ms/cppwinrt/vsix) の最小要件は、Windows SDK ターゲット バージョン 10.0.17134.0 (Windows 10、バージョン 1803) です。 Visual Studio 2017 (バージョン 15.6 以上、15.7 以上を推奨) も必要になります 。 `.vcxproj` ファイルの `<PropertyGroup Label="Globals">` に `<CppWinRTEnabled>true</CppWinRTEnabled>` があるかどうかによって、VSIX を使用するプロジェクトを特定できます。 詳しくは、「[C++/WinRT の Visual Studio サポートと VSIX](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix)」をご覧ください。

## <a name="whats-a-runtime-class"></a>*ランタイム クラス*とは
ランタイム クラスは、通常実行可能な境界を越えて、モダン COM インターフェイス経由でアクティブ化および使用可能な型です。 ただし、ランタイム クラスは、それを実装するコンパイル ユニット内でも使用できます。 インターフェイス定義言語 (IDL) でランタイム クラスを宣言し、C++/WinRT を使用した標準の C++ で実装することができます。

## <a name="what-do-the-projected-type-and-the-implementation-type-mean"></a>*プロジェクションされる型*と*実装型*とは
Windows ランタイム クラス (ランタイム クラス) を*使用*する場合のみ、*プロジェクションされる型*を排他的に処理します。 C++/WinRT は*言語のプロジェクション*であるため、プロジェクションされる型は、C++/WinRT を使用した C++ に*プロジェクション*される Windows ランタイムの画面に表示されます。 詳しくは、「[C++/WinRT での API の使用](consume-apis.md)」を参照してください。

*実装型*にはランタイム クラスの実装が含まれるため、ランタイム クラスを実装するプロジェクトでのみ利用可能です。 ランタイム クラス (Windows ランタイム コンポーネント プロジェクト、つまり XAML UI を使用するプロジェクト) を実装するプロジェクトで作業している場合、ランタイム クラスの実装型と C++/WinRT にプロジェクションされたランタイム クラスを表すプロジェクションされる型との違いを習熟することが重要です。 詳細については、「[C++/WinRT での API の作成](author-apis.md)」を参照してください。

## <a name="do-i-need-to-declare-a-constructor-in-my-runtime-classs-idl"></a>使用するランタイム クラスの IDL でコンストラクターを宣言する必要性
ランタイム クラスが実装するコンパイル ユニット (Windows ランタイム クライアント アプリで一般的に使用するための Windows ランタイム コンポーネント) 以外で使用されるように設計されている場合のみ IDL のコンストラクターを宣言する際の目的と影響の詳細については、「[ランタイム クラス コンストラクター](author-apis.md#runtime-class-constructors)」を参照してください。

## <a name="why-is-the-linker-giving-me-a-lnk2019-unresolved-external-symbol-error"></a>リンカーで "LNK2019: 外部シンボルは未解決です" というエラーが表示されるのはなぜですか。
未解決のシンボルが (**winrt** 名前空間内の) C++/WinRT プロジェクションの Windows 名前空間ヘッダーからの API である場合、その API は含まれているヘッダー内で事前宣言されていますが、その定義は含まれていないヘッダー内にあります。 API の名前空間で付けられた名前のヘッダーを含めてから、リビルドしてください。 詳細については、「[C++/WinRT プロジェクション ヘッダー](consume-apis.md#cwinrt-projection-headers)」を参照してください。

未解決のシンボルが [RoInitialize](https://msdn.microsoft.com/library/br224650) などの Windows ランタイムの自由関数である場合、[WindowsApp.lib](/uwp/win32-and-com/win32-apis) の包括的なライブラリを明示的にプロジェクトに含める必要があります。 C++/WinRT プロジェクションは、これらの一部の自由 (非メンバー) 関数とエントリ ポイントに依存します。 アプリケーションでいずれかの [C++/WinRT Visual Studio Extension (VSIX)](https://aka.ms/cppwinrt/vsix) プロジェクト テンプレートを使用する場合は、`WindowsApp.lib` が自動的にリンクされます。 それ以外の場合、プロジェクトのリンク設定を使用して含めるか、またはソース コードでそれを行うことができます。

```cppwinrt
#pragma comment(lib, "windowsapp")
```

## <a name="should-i-implement-windowsfoundationiclosableuwpapiwindowsfoundationiclosable-and-if-so-how"></a>[**Windows::Foundation::IClosable**](/uwp/api/windows.foundation.iclosable) を実装するかどうかとその方法
自身のデストラクターのリソースを解放するランタイム クラスを使用し、そのランタイム クラスが実装するコンパイル ユニット (Windows ランタイム クライアント アプリで一般的に使用するための Windows ランタイム コンポーネント) 以外で使用されるように設計されている場合、確定終了処理が不足する言語でランタイム クラスの使用をサポートするために、**IClosable** も実装することをお勧めします。 デストラクター、[**IClosable::Close**](/uwp/api/windows.foundation.iclosable.Close)、または両方が呼び出されたときにリソースが解放されるようにしてください。 **IClosable::Close** は必要に応じて呼び出すことができます。

## <a name="do-i-need-to-call-iclosablecloseuwpapiwindowsfoundationiclosablewindowsfoundationiclosableclose-on-runtime-classes-that-i-consume"></a>使用するランタイム クラスで [**IClosable::Close**](/uwp/api/windows.foundation.iclosable#Windows_Foundation_IClosable_Close_) を読み出す必要性
**IClosable** は確定終了処理が不足する言語をサポートします。 そのため、シャットダウン状態やデッドロック状態といった非常にまれな場合を除いて、C++/WinRT から **IClosable::Close** を呼び出さないでください。 たとえば、**Windows.UI.Composition** を使用していて、設定順序でオブジェクトを破棄する場合、その代わりとして、C++/WinRT ラッパーを破棄することができます。

## <a name="can-i-use-llvmclang-to-compile-with-cwinrt"></a>LLVM/Clang を使用して C++/WinRT でコンパイルすることはできますか。
C++/WinRT の LLVM および Clang ツール チェーンはサポートしていませんが、C++/WinRT の標準への準拠を検証するためにそれを内部で使用します。 たとえば、マイクロソフトが内部で行っている内容をエミュレートする場合は、次に説明するような実験を試してみることができます。

[LLVM ダウンロード ページ](https://releases.llvm.org/download.html)に移動し、**[Download LLVM 6.0.0] (LLVM 6.0.0 のダウンロード)** > **[Pre-Built Binaries] (事前ビルドされたバイナリ)** を探し、**[Clang for Windows (64-bit)] (Windows の Clang (64 ビット))** をダウンロードします。 インストール中に、コマンド プロンプトから起動できるように、PATH システム変数に LLVM を追加することを選択します。 この実験の目的上、"Failed to find MSBuild toolsets directory (MSBuild ツールセット ディレクトリの検索に失敗しました)" または "MSVC integration install failed (MSVC 統合インストールに失敗しました)" というエラーが表示された場合には無視できます。 LLVM/Clang を起動するさまざまな方法があります。次の例は、1 つの方法のみを示しています。

```
C:\ExperimentWithLLVMClang>type main.cpp
// main.cpp
#pragma comment(lib, "windowsapp")
#pragma comment(lib, "ole32")

#include "winrt/Windows.Foundation.h"
#include <stdio.h>
#include <iostream>

using namespace winrt;

int main()
{
    winrt::init_apartment();
    Windows::Foundation::Uri rssFeedUri{ L"https://blogs.windows.com/feed" };
    std::wcout << rssFeedUri.Domain().c_str() << std::endl;
}

C:\ExperimentWithLLVMClang>clang-cl main.cpp /EHsc /I ..\.. -Xclang -std=c++17 -Xclang -Wno-delete-non-virtual-dtor -o app.exe

C:\ExperimentWithLLVMClang>app
windows.com
```

C++/WinRT では C++17 標準の機能を使用するため、そのサポートを受けるために必要なコンパイラ フラグを使用する必要があります。そのようなフラグはコンパイラによって異なります。

Visual Studio は、マイクロソフトがサポートし、C++/WinRT 用に推奨する開発ツールです。 「[C++/WinRT の Visual Studio サポートと VSIX](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-and-the-vsix)」を参照してください。

## <a name="why-doesnt-the-generated-implementation-function-for-a-read-only-property-have-the-const-qualifier"></a>読み取り専用プロパティの生成された関数がない理由、`const`限定子よいですか。

期待どおり[MIDL 3.0](/uwp/midl-3/)で読み取り専用プロパティを宣言するときに、`cppwinrt.exe`される、実装の機能を生成するツール`const`-修飾 (定数関数は、*この*ポインターを定数として処理)。

確かに可能な限り、定数の使用をお勧めが`cppwinrt.exe`のどの実装に関する関数あるいは定数する可能性がある理由ツール自体は行われません。 この例のように、定数、実装関数のいずれかを選択できます。

```cppwinrt
struct MyStringable : winrt::implements<MyStringable, winrt::Windows::Foundation::IStringable>
{
    winrt::hstring ToString() const
    {
        return L"MyStringable";
    }
};
```

削除することができます`const` **ToString**の区切り記号をする必要があるいくつかの実装でオブジェクトの状態を変更する必要があることを決定します。 メンバーの両方ではなく関数、定数、または非定数を作成します。 つまり、しないオーバー ロードの実装の機能に`const`します。

定数の場所に配置他の別の実装関数を除いてに画像が Windows ランタイム関数予測にします。 次のコードを検討してください。

```cppwinrt
int main()
{
    winrt::Windows::Foundation::IStringable s{ winrt::make<MyStringable>() };
    auto result{ s.ToString() };
}
```

**ToString**上の呼び出し、Visual Studio で**宣言へ移動**] コマンドが表示されますを Windows ランタイム**IStringable::ToString**の投影 C + +/WinRT は次のとおりです。

```
winrt::hstring ToString() const;
```

投影に対して関数は、それらの実装の対象を選択する方法に関係なく定数です。 バック グラウンドで投影インターフェイスを呼び出し、アプリケーション バイナリ (ABI)、COM インターフェイス ポインターを使って、通話には、どの金額です。 予測**ToString**とのやり取り唯一の状態は、その COM インターフェイス ポインター確実がないので、関数、定数、ポインターを変更する必要があります。 これにより、 **IStringable**を参照する保証**IStringable**参照では、通話を発信していることを何も変わらない、これにより、定数を使用しても**ToString**を呼び出すことができます。

理解を次の例の`const`C + の実装の詳細については、+/WinRT 予測と実装します。プランのコード検疫が形成されます。 このようなものがない`const`COM もメンバー関数) (Windows ランタイム ABI にします。

## <a name="do-you-have-any-recommendations-for-decreasing-the-code-size-for-cwinrt-binaries"></a>C + コード サイズを小さくに関する推奨事項は +/WinRT バイナリですか?

Windows ランタイム オブジェクトを使用する場合は、以上バイナリのコードを生成するために必要なを発生させることによって、アプリケーションに影響を及ぼすを持ってことができますので、次に示すコーディングのパターンをしないでください。

```cppwinrt
anobject.b().c().d();
anobject.b().c().e();
anobject.b().c().f();
```

Windows ランタイム世界では、コンパイラことはできませんの値をキャッシュ`c()`または、インターフェイスを介して、間接的と呼ばれる方法ごとに ('. ')。 調整すると、しない限り、その他の仮想呼び出しと参照オーバーヘッド カウントを結果に表示されます。 上記のパターンでは、倍のコードに厳密に必要なを簡単に作成可能性があります。 代わりに、場所に実行できます。 次に示すパターンを希望します。 少なくコードを生成し、実行時のパフォーマンスが向上も大幅にします。

```cppwinrt
auto a{ anobject.b().c() };
a.d();
a.e();
a.f();
```

上記の推奨パターン対象だけでなく C + +/WinRT はすべての Windows ランタイム言語予測します。

> [!NOTE]
> このトピックで質問の回答が得られない場合は、[Stack Overflow で `c++-winrt` タグ](https://stackoverflow.com/questions/tagged/c%2b%2b-winrt)を使用してヘルプ情報を見つけることができます。