---
title: Windows 管理センターの拡張機能の公開
description: Windows 管理センター用の拡張機能の公開 (Project ホノルル)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 357c37ec395e5c51f3c3f946414f38ea5f95e9e4
ms.sourcegitcommit: eaf3fb57517b9110082edad356b12daf3345bb2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593993"
---
# <a name="publishing-extensions"></a>拡張機能の公開

>適用先:Windows Admin Center、Windows Admin Center Preview

拡張機能を開発したら、それを発行し、他のユーザーがテストまたは使用できるようにします。 発行者と発行の目的に応じて、以下に示すオプションがいくつかあります。これらのオプションについては、公開の手順と要件を参照してください。

## <a name="publishing-options"></a>公開オプション

Windows 管理センターでサポートされる構成可能なパッケージソースには、主に次の3つのオプションがあります。
* Microsoft のパブリック Windows 管理センター NuGet フィード
* 独自のプライベート NuGet フィード
* ローカルまたはネットワークのファイル共有

### <a name="publishing-to-the-windows-admin-center-extension-feed"></a>Windows 管理センターの拡張機能フィードへの発行

既定では、Windows 管理センターは、Microsoft の Windows 管理センター製品チームによって管理されている NuGet フィードに接続されています。 Microsoft によって開発された新しい拡張機能の早期プレビュー版は、このフィードに公開され、Windows 管理センターのユーザーが使用できるようになります。 拡張機能のビルドとリリースを計画している外部の開発者は、このフィードへ[の発行要求を送信](#publishing-your-extension-to-the-windows-admin-center-feed)することもできます。

### <a name="publishing-to-a-different-nuget-feed"></a>別の NuGet フィードへの発行

独自の NuGet フィードを作成して、[プライベートソースを設定したり、nuget ホスティングサービスを使用したりするためのさまざまなオプション](https://docs.microsoft.com/nuget/hosting-packages/overview)の1つを使用して、拡張機能を公開することもできます。 NuGet フィードは、NuGet v2 API をサポートしている必要があります。 現在、Windows 管理センターではフィード認証がサポートされていないため、すべてのユーザーに読み取りアクセスを許可するようにフィードを構成する必要があります。

### <a name="publishing-to-a-file-share"></a>ファイル共有への発行

拡張機能へのアクセスを組織または制限されたユーザーグループに限定するには、SMB ファイル共有を拡張機能フィードとして使用できます。 この場合、フィードへのアクセスを許可するために、ファイル共有とフォルダーのアクセス許可が適用されます。

## <a name="preparing-your-extension-for-release"></a>リリース用に拡張機能を準備する

次の開発に関するトピックを必ず読み、検討してください。

- [ツールの可視性の制御](guides/dynamic-tool-display.md)
- [文字列とローカライズ](guides/strings-localization.md)

### <a name="consider-releasing-as-a-preview-release"></a>プレビューリリースとしてリリースすることを検討してください

評価のために拡張機能のプレビューバージョンをリリースする場合は、次のことをお勧めします。

- Nuspec ファイル内の拡張機能のタイトルの末尾に "(Preview)" を追加します。
- Nuspec ファイルでの拡張機能の説明の制限事項について説明します。

## <a name="creating-an-extension-package"></a>拡張機能パッケージの作成

Windows 管理センターでは、拡張機能の配布とダウンロードに NuGet パッケージとフィードを利用しています。  パッケージを出荷するには、プラグインと拡張機能を含む NuGet パッケージを生成する必要があります。  1つのパッケージには、UI 拡張機能とゲートウェイプラグインの両方を含めることができます。次のセクションでは、このプロセスについて説明します。

### <a name="1-build-your-extension"></a>1. 拡張機能をビルドする

拡張機能のパッケージ化を開始する準備ができたら、すぐにファイルシステムに新しいディレクトリを作成し、コンソールを開いて、CD に追加します。  これは、パッケージを構成するすべての nuspec およびコンテンツディレクトリを格納するために使用されるルートディレクトリになります。  このドキュメントの期間中は、このフォルダーを "NuGet パッケージ" として参照します。

#### <a name="ui-extensions"></a>UI 拡張機能

UI 拡張機能に必要なすべてのコンテンツを収集するプロセスを開始するには、ツールで "gulp build" を実行し、ビルドが成功したことを確認します。  このプロセスでは、拡張機能のルートディレクトリ (src ディレクトリの同じレベル) にある "バンドル" という名前のフォルダーに、すべてのコンポーネントがまとめてパッケージ化されます。  このディレクトリとそのすべての内容を "NuGet パッケージ" フォルダーにコピーします。

#### <a name="gateway-plugins"></a>ゲートウェイプラグイン

ビルドインフラストラクチャを使用して (これは、Visual Studio を開いて [ビルド] ボタンをクリックするだけで、簡単に行うことができます)、プラグインをコンパイルしてビルドします。  ビルド出力ディレクトリを開き、プラグインを表す Dll をコピーして、"Package" という名前の "NuGet Package" ディレクトリ内の新しいフォルダーに配置します。  FeatureInterface dll をコピーする必要はありません。コードを表す Dll だけをコピーします。

### <a name="2-create-the-nuspec-file"></a>2. nuspec ファイルを作成する

NuGet パッケージを作成するには、最初に nuspec ファイルを作成する必要があります。 Nuspec ファイルは、NuGet パッケージのメタデータを含む XML マニフェストです。 このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。  このファイルを "NuGet パッケージ" フォルダーのルートに配置します。

Nuspec ファイルの例と、必須または推奨されるプロパティの一覧を次に示します。 完全なスキーマについては、 [nuspec のリファレンス](https://docs.microsoft.com/nuget/reference/nuspec)を参照してください。 任意のファイル名を使用して、nuspec ファイルをプロジェクトのルートフォルダーに保存します。

> [!IMPORTANT]
> ```<id>```Nuspec ファイルの値は、プロジェクトのファイル内の値と一致する必要があります。そうしないと、発行された ```"name"``` ```manifest.json``` 拡張機能が Windows 管理センターで正常に読み込まれません。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="https://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <id>contoso.project.extension</id>
    <version>1.0.0</version>
    <title>Contoso Hello Extension</title>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.hello-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Hello World extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright> 
    <tags></tags>
  </metadata>
  <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
  </files>
</package>
```

#### <a name="required-or-recommended-properties"></a>必須または推奨プロパティ

| プロパティ名 | 必須/推奨 | 説明 |
| ---- | ---- | ---- |
| packageType | 必須 | Windows 管理センターの拡張機能に定義されている NuGet パッケージの種類である "Windowsadmincenter Extension" を使用します。 |
| id | 必須 | フィード内の一意のパッケージ識別子。 この値は、プロジェクトのファイルの manifest.jsの "name" 値と一致する必要があります。  ガイダンスについては、[一意のパッケージ識別子の選択](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。 |
| title | Windows 管理センターフィードへの発行に必要 | Windows 管理センターの拡張機能マネージャーに表示されるパッケージのフレンドリ名。 |
| version | 必須 | 拡張機能のバージョン。 [セマンティックバージョン管理 (SemVer 規約)](http://semver.org/spec/v1.0.0.html)を使用することをお勧めしますが、必須ではありません。 |
| 作成者 | 必須 | 会社の代理として発行する場合は、会社名を使用します。 |
| description | 必須 | 拡張機能の機能についての説明を入力します。 |
| iconUrl | Windows 管理センターフィードに発行するときに推奨 | 拡張機能マネージャーに表示するアイコンの URL。 |
| projectUrl | Windows 管理センターフィードへの発行に必要 | 拡張機能の web サイトの URL。 別の web サイトがない場合は、NuGet フィードのパッケージ web ページの URL を使用します。 |
| licenseUrl | Windows 管理センターフィードへの発行に必要 | 拡張機能の使用許諾契約書の URL。 |
| files | 必須 | これら2つの設定は、Windows 管理センターが UI 拡張機能とゲートウェイプラグインに対して想定するフォルダー構造を設定します。 |

### <a name="3-build-the-extension-nuget-package"></a>3. 拡張機能の NuGet パッケージをビルドする

前の手順で作成した nuspec ファイルを使用して、NuGet パッケージを作成します。 nupkg ファイルをアップロードして、NuGet フィードに発行することができます。

1. [NuGet クライアントツールの web サイト](https://docs.microsoft.com/nuget/install-nuget-client-tools)から nuget.exe CLI ツールをダウンロードします。
2. "nuget.exe pack [. nuspec file name]" を実行して、nupkg ファイルを作成します。

### <a name="4-signing-your-extension-nuget-package"></a>4. 拡張機能の NuGet パッケージに署名する

拡張機能に含まれているすべての .dll ファイルは、信頼された証明機関 (CA) の証明書で署名する必要があります。 既定では、Windows 管理センターが実稼働モードで実行されていると、署名されていない .dll ファイルは実行されません。

また、パッケージの整合性を保証するために拡張機能 NuGet パッケージに署名することを強くお勧めしますが、これは必須の手順ではありません。

### <a name="5-test-your-extension-nuget-package"></a>5. 拡張機能の NuGet パッケージをテストする

これで、拡張機能パッケージをテストする準備ができました。 Nupkg ファイルを NuGet フィードにアップロードするか、ファイル共有にコピーします。 別のフィードまたはファイル共有のパッケージを表示およびダウンロードするには、NuGet フィードまたはファイル共有を指すように[フィードの構成を変更](../configure/using-extensions.md#installing-extensions-from-a-different-feed)する必要があります。 テスト時には、拡張機能マネージャーでプロパティが正しく表示されていることを確認し、拡張機能を正常にインストールしてアンインストールすることができます。

## <a name="publishing-your-extension-to-the-windows-admin-center-feed"></a>Windows 管理センターフィードへの拡張機能の発行

Windows 管理センターフィードに発行することで、Windows 管理センターのユーザーが拡張機能を使用できるようにすることができます。 Windows 管理センター SDK はまだプレビュー段階であるため、開発の問題の解決に役立つように、お客様と緊密に連携して、ユーザーに高品質の製品とエクスペリエンスを提供できるようにしたいと考えています。

拡張機能の初期バージョンをリリースする前に、リリース前に少なくとも2-3 週間後に拡張機能のレビュー要求をマイクロソフトに送信して、十分な情報を確認し、必要に応じて拡張機能に変更を加えることをお勧めします。 拡張機能を発行する準備ができたら、それをレビューのために送信する必要があります。承認されている場合は、フィードに発行します。

その後、拡張機能の更新プログラムをリリースする場合は、レビューのために別の要求を送信する必要があります。 変更の範囲によっては、更新レビューのターンアラウンド時間は一般的に短くなります。

### <a name="submit-an-extension-review-request-to-microsoft"></a>拡張機能レビュー要求を Microsoft に送信する

拡張機能のレビュー要求を送信するには、次の情報を入力して、に電子メールで送信し [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request) ます。 1週間以内に電子メールに返信します。

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### <a name="submit-your-extension-package-for-review-and-publishing"></a>レビューおよび発行のために拡張機能パッケージを送信する

[拡張機能パッケージを作成](#creating-an-extension-package)するための上記の手順に従ってください。 nuspec ファイルが適切に定義され、ファイルが署名されていることを確認してください。 また、次のようなプロジェクト web サイトを用意することもお勧めします。

- スクリーンショットやビデオを含む拡張機能の詳細な説明
- フィードバックまたは質問を受信するための電子メールアドレスまたは web サイト機能

拡張機能を発行する準備ができたら、に電子メールを送信 [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) します。拡張機能パッケージを送信する方法については、こちらで説明します。 パッケージを受け取ったら、それを確認し、承認された場合は Windows 管理センターフィードに発行します。
