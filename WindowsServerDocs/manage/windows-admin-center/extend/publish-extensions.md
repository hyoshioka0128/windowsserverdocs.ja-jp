---
title: Windows Admin Center の拡張機能を公開
description: Windows Admin Center (プロジェクト ホノルル) の拡張機能を公開
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 762bd4613fa8ad6cdfb5b44745a7ce78b331499d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820423"
---
# <a name="publishing-extensions"></a>公開の拡張機能

>適用先:Windows Admin Center、Windows Admin Center プレビュー

拡張機能を開発したら、発行し、テストまたは使用する他のユーザーに使用できるようにします。 対象ユーザーと発行の目的に応じて以下の手順と発行のための要件と共に導入する予定がいくつかのオプションがあります。

## <a name="publishing-options"></a>公開オプション

Windows Admin Center をサポートする構成可能なパッケージ ソースの主な 3 つのオプションがあります。
* Microsoft のパブリック Windows Admin Center NuGet フィード
* 独自のプライベート NuGet フィード
* ローカルまたはネットワーク ファイル共有

### <a name="publishing-to-the-windows-admin-center-extension-feed"></a>フィード、Windows Admin Center の拡張機能への発行

NuGet に既定では、Windows Admin Center が接続されている microsoft Windows Admin Center の製品チームによって管理されるフィード。 Microsoft によって開発された新しい拡張機能の初期のプレビュー バージョンは、このフィードに発行され、Windows Admin Center ユーザーが使用できる可能性があります。 外部の開発者がビルドし、公開されている拡張機能をリリースする予定の場合も[要求を送信](#publishing-your-extension-to-the-windows-admin-center-feed)このフィードに発行します。

### <a name="publishing-to-a-different-nuget-feed"></a>フィードのさまざまな NuGet への発行

独自の NuGet を使用して、多数の 1 つに、拡張機能を公開するフィードを作成することも[秘密のソースを設定またはサービスをホストしている NuGet を使用するためのさまざまなオプション](https://docs.microsoft.com/nuget/hosting-packages/overview)します。 NuGet フィードには、NuGet v2 API をサポートする必要があります。 Windows Admin Center でフィードの認証が現在サポートされていないために、フィードは、すべてのユーザーへの読み取りアクセスを許可するように構成する必要があります。

### <a name="publishing-to-a-file-share"></a>ファイル共有への発行

拡張機能のアクセスを制限するには、組織またはユーザーのグループに限定するフィードの拡張機能として SMB ファイル共有を使用することができます。 この場合、ファイル共有およびフォルダーのアクセス許可も、フィードへのアクセスを許可されます。

## <a name="preparing-your-extension-for-release"></a>リリースの拡張機能の準備

確認し、開発の次のトピックを検討してください。

- [ツールの表示を制御します。](guides/dynamic-tool-display.md)
- [文字列とローカライズ](guides/strings-localization.md)

### <a name="consider-releasing-as-a-preview-release"></a>プレビュー リリースとしてリリースを検討してください。

場合は評価目的で、拡張機能のプレビュー バージョンをリリースすることをお勧めします。

- .Nuspec ファイルの拡張機能のタイトルの最後に「(プレビュー)」を追加します。
- .Nuspec ファイルの拡張機能の説明での制限事項について説明します

## <a name="creating-an-extension-package"></a>拡張機能パッケージの作成

Windows Admin Center では、NuGet パッケージと配布および拡張機能をダウンロードするためのフィードを利用します。  送付先であるパッケージの順番は、プラグインと拡張機能を含む NuGet パッケージを生成する必要があります。  1 つのパッケージは、ゲートウェイ プラグインだけでなく、UI の拡張機能に含めることができ、次のセクションでプロセスを説明します。

### <a name="1-build-your-extension"></a>1. 拡張機能をビルドします。

拡張機能をパッケージ化、ファイル システムに新しいディレクトリを作成する準備が完了したら、すぐに、コンソールと CD を開きます。  これはすべて、nuspec とコンテンツのディレクトリ、パッケージを構成するに使用するルート ディレクトリになります。  このフォルダーは、このドキュメントの間"NuGet Package"としてから参照されます。

#### <a name="ui-extensions"></a>UI 拡張機能

UI 拡張機能に必要なすべての内容を収集する場合のプロセスを開始するには、ツールで「gulp ビルド」を実行しビルドが成功したかどうかを確認します。  このプロセスは、「バンドル」という名前のフォルダー内のすべてのコンポーネントは、(src ディレクトリの同じレベル) で、拡張機能のルート ディレクトリにあるパッケージ。  このディレクトリとすべてのコピー「NuGet パッケージ」フォルダーに内容ですね。

#### <a name="gateway-plugins"></a>ゲートウェイのプラグイン

(Visual Studio を開き、ビルド ボタンをクリックするだけでこれに可能性があります)、ビルドのインフラストラクチャを使用してコンパイルし、プラグインを構築します。  ビルド出力ディレクトリを開き、プラグインを表す、dll をコピーして「パッケージ」と呼ばれる"NuGet Package"ディレクトリ内の新しいフォルダーに配置します。  FeatureInterface dll で、コードを表す dll だけをコピーする必要はありません。

### <a name="2-create-the-nuspec-file"></a>2. .Nuspec ファイルを作成します。

NuGet パッケージを作成するには、まず .nuspec ファイルを作成する必要があります。 .Nuspec ファイルには、NuGet パッケージのメタデータを含む XML マニフェストです。 このマニフェストを使用して、パッケージを作成して、コンシューマーに情報を提供します。  「NuGet パッケージ」フォルダーのルートには、このファイルを配置します。

.Nuspec ファイルの例と必須または推奨されるプロパティの一覧を次に示します。 完全なスキーマでは、次を参照してください。、 [.nuspec リファレンス](https://docs.microsoft.com/nuget/reference/nuspec)します。 .Nuspec ファイルを任意のファイル名を持つプロジェクトのルート フォルダーに保存します。

> [!IMPORTANT]
> ```<id>``` .Nuspec ファイル内の値が一致する必要があります、```"name"```プロジェクトの値```manifest.json```発行済みの拡張機能は、そうしないと、ファイルは、Windows Admin Center で正常に読み込みません。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <packageTypes>
      <packageType name="WindowsAdminCenterExtension" />
    </packageTypes>  
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

| プロパティ名 | 必要な/推奨 | 説明 |
| ---- | ---- | ---- |
| PackageType | 必須 | Windows Admin Center の拡張機能に対して定義されている NuGet パッケージの種類である"WindowsAdminCenterExtension"を使用します。 |
| id | 必須 | フィード内で一意のパッケージの識別子。 この値は、プロジェクトの manifest.json ファイルに"name"値と一致する必要があります。  参照してください[一意のパッケージ識別子を選択する](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)のガイダンスについてはします。 |
| title | Windows Admin Center をフィードに発行するために必要な | Windows Admin Center 拡張機能マネージャーに表示されるパッケージのフレンドリ名。 |
| version | 必須 | 拡張機能のバージョン。 使用して[セマンティック バージョン管理 (SemVer 規則)](http://semver.org/spec/v1.0.0.html)推奨されますが、必要ありません。 |
| 作成者 | 必須 | 会社の代わりをパブリッシュする場合は、会社名を使用します。 |
| description | 必須 | 拡張機能の機能の説明を提供します。 |
| IconUrl | Windows Admin Center をフィードに発行するときをお勧めします | 拡張機能マネージャーに表示するアイコンの URL です。 |
| ProjectUrl | Windows Admin Center をフィードに発行するために必要な | 拡張機能の web サイトの URL です。 別の web サイトがいない場合は、NuGet フィードでパッケージの web ページの URL を使用します。 |
| licenseUrl | Windows Admin Center をフィードに発行するために必要な | 拡張機能の使用許諾契約書への URL。 |
| ファイル | 必須 | これら 2 つの設定は、Windows Admin Center UI 拡張機能とゲートウェイのプラグインが期待するフォルダー構造を設定します。 |

### <a name="3-build-the-extension-nuget-package"></a>3.拡張機能の NuGet パッケージをビルドします。

上記で作成した .nuspec ファイルを使用して、NuGet パッケージの .nupkg ファイルをアップロードして NuGet フィードにパブリッシュすることができますを今すぐ作成します。

1. Nuget.exe CLI ツールをからダウンロード、 [NuGet クライアント ツールの web サイト](https://docs.microsoft.com/nuget/install-nuget-client-tools)します。
2. .Nupkg ファイルを作成するには、「nuget.exe パック [.nuspec ファイル名]」を実行します。

### <a name="4-signing-your-extension-nuget-package"></a>4。拡張 NuGet パッケージの署名

拡張機能に含まれるすべての .dll ファイルは、信頼された証明機関 (CA) から証明書で署名する必要があります。 既定では、符号なしの .dll ファイルは、Windows Admin Center が実稼働モードで実行されているときに実行されてからはブロックされます。

これは必須の手順ではありませんが、パッケージの整合性を確保する拡張機能の NuGet パッケージの署名をも強くお勧めします。

### <a name="5-test-your-extension-nuget-package"></a>5。拡張 NuGet パッケージをテストします。

拡張パッケージは、テストの準備ができました! NuGet フィードにし、.nupkg ファイルをアップロードまたはファイル共有にコピーします。 を表示して、別のフィードまたはファイル共有からパッケージをダウンロードする必要があります[、フィードの構成変更](../configure/using-extensions.md#installing-extensions-from-a-different-feed)NuGet フィードをポイントするか、またはファイル共有にします。 をテストする場合は、拡張機能マネージャーで正しく表示プロパティと正常にインストールして、拡張機能のアンインストールを確認します。

## <a name="publishing-your-extension-to-the-windows-admin-center-feed"></a>フィード、Windows Admin Center を拡張機能を公開します。

フィード Windows Admin Center への発行、すること、拡張機能使用可能な任意の Windows Admin Center のユーザーにします。 Windows Admin Center SDK はまだプレビュー段階であるために、開発の問題を解決して、高品質の製品を提供することができるかどうかを確認し、ユーザー エクスペリエンスに役立つと緊密に連携いただきます。

拡張機能の初期のバージョンをリリースする前に、2 ~ 3 週間以上とすると、必要に応じて、拡張機能を変更することを確認するための十分な時間があることを確認するリリースの前に microsoft 拡張機能のレビュー要求を送信することをお勧めします。 拡張機能が公開する準備をすることで、レビュー用に送信する必要があり、承認された場合のフィードに公開されます。

その後、拡張機能への更新をリリースする場合は、確認のための別の要求を送信する必要があります。 変更の範囲によって異なりますレビューの更新プログラムのターンアラウンド時間が短い通常必要があります。

### <a name="submit-an-extension-review-request-to-microsoft"></a>Microsoft 拡張機能のレビュー要求を送信します。

拡張機能のレビュー要求を送信する、次の情報を入力しを電子メールとして送信[ wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request)します。 私たちはから 1 週間以内の電子メールに返信します。

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### <a name="submit-your-extension-package-for-review-and-publishing"></a>確認と発行のため、拡張機能パッケージを送信します。

上記の指示に従うことを確認[拡張機能パッケージを作成する](#creating-an-extension-package).nuspec ファイルが正しく定義されているし、ファイルに署名します。 次を含むプロジェクトの web サイトがあることをお勧めします。

- スクリーン ショットやビデオを含む拡張機能の詳細な説明
- 意見やご質問を受信する電子メール アドレスまたは web サイトの機能

拡張機能を公開する準備ができたら、メールを送る[ wacextensionrequest@microsoft.com ](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review)手順については、拡張機能パッケージを送信すると。 パッケージをお送りを確認して承認されると、Windows Admin Center をフィードに発行します。