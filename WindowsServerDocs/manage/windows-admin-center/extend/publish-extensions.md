---
title: Windows Admin Center の拡張機能の公開
description: Windows Admin Center (Project Honolulu) の拡張機能の公開
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 762bd4613fa8ad6cdfb5b44745a7ce78b331499d
ms.sourcegitcommit: 3883eebbba70bfea0221e510863ee1a724a5f926
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2018
ms.locfileid: "5783754"
---
# 拡張機能の公開

>適用対象: Windows Admin Center、Windows Admin Center Preview

拡張機能で開発した後はする発行し、テストまたは使用する他のユーザーに利用できるようにします。 によっては、対象ユーザーと公開の目的は、手順を実行および公開するための要件と共に以下紹介するいくつかのオプションがあります。

## 公開のオプション

Windows Admin Center をサポートするソースの構成可能なパッケージの 3 つの主要なオプションがあります。
* Microsoft のパブリック Windows Admin Center NuGet フィード
* 独自のプライベート NuGet フィード
* ローカルまたはネットワーク ファイル共有

### Windows Admin Center の拡張機能をフィードへの発行

既定では、Windows Admin Center が接続されている、NuGet をフィードの Microsoft Windows Admin Center 製品チームが維持されます。 Microsoft により開発された新しい拡張機能の初期プレビュー バージョンは、このフィードに公開され、Windows Admin Center のユーザーが利用できる可能性があります。 外部開発者の計画をビルドして拡張機能のリリースを公開する場合、このフィードへの公開のため[の要求を送信](#publishing-your-extension-to-the-windows-admin-center-feed)にもあります。

### さまざまな NuGet への公開のフィード

多くの[サービスをホストしているプライベート ソースを設定または、NuGet を使用するためのさまざまなオプション](https://docs.microsoft.com/nuget/hosting-packages/overview)のいずれかを使用して、拡張機能を公開するフィード、独自の NuGet を作成することもできます。 NuGet フィードには、NuGet v2 API をサポートする必要があります。 現在、Windows Admin Center では、フィードの認証をサポートしていない、ので、フィードをすべてのユーザーへの読み取りアクセス許可を構成する必要があります。

### ファイル共有への公開

拡張機能のアクセスを制限するには、組織や、限られたユーザーのグループには、フィードを拡張機能として、SMB ファイル共有を使用できます。 この例では、ファイル共有とフォルダーのアクセス許可は、フィードへのアクセスを許可するために適用されます。

## 拡張機能のリリースの準備

必ずを読み、次のトピックの開発を検討してください。

- [ツールの可視性の制御](guides/dynamic-tool-display.md)
- [文字列とローカライズ](guides/strings-localization.md)

### リリース プレビュー リリースとして検討します。

評価用の拡張機能のプレビュー バージョンをリリースする場合ことをお勧めします。

- .Nuspec ファイルの拡張機能のタイトルの末尾に「(プレビュー)」を追加します。
- .Nuspec ファイル内の拡張機能の説明で制限事項を説明します。

## 拡張機能パッケージを作成します。

Windows Admin Center は、NuGet パッケージと配布および拡張機能をダウンロードするためのフィードを利用します。  出荷するパッケージの順序では、プラグインの実行と拡張機能を含む NuGet パッケージを生成する必要があります。  1 つのパッケージは、UI の拡張機能として、ゲートウェイ プラグインの両方を含めることができ、次のセクションでプロセスを説明します。

### 1.、拡張機能を構築します。

拡張機能をパッケージ化を開始するには、ファイル システムに新しいディレクトリを作成する準備ができたら、すぐに、コンソールと CD を開きます。  使用して、ディレクトリを含むすべての nuspec とコンテンツは、パッケージを構成するルート ディレクトリになります。  このドキュメントの期間中「NuGet パッケージ」としてこのフォルダーが参照されます。

#### UI の拡張機能

UI の拡張機能に必要なすべてのコンテンツを収集する場合のプロセスを開始するには、お使いのツールで"gulp build"を実行し、ビルドが成功したかどうかを確認します。  このプロセスは、"bundle"という名前のフォルダー内のすべてのコンポーネントは、拡張機能 (src ディレクトリの同じレベル) でのルート ディレクトリにあるパッケージ。  このディレクトリとすべてのコピーの「NuGet パッケージ」フォルダーに内容です。

#### ゲートウェイ プラグイン

(これが、簡単な Visual Studio を開き、ビルドのボタンをクリックして)、ビルド インフラストラクチャを使用してコンパイルし、プラグインを構築します。  ビルドの出力ディレクトリを開いて、プラグインを表す、dll のコピーし、「パッケージ」と呼ばれる「NuGet パッケージ」ディレクトリ内の新しいフォルダーに配置しています。  FeatureInterface dll、コードを表すあるいは単にコピーする必要はありません。

### 2. .nuspec ファイルを作成します。

NuGet パッケージを作成するには、まず .nuspec ファイルを作成する必要があります。 .Nuspec ファイルには、NuGet パッケージのメタデータが含まれている XML マニフェストです。 このマニフェストは、パッケージをビルドして一般ユーザーに情報を提供の両方に使用されます。  このファイルは、「NuGet パッケージ」フォルダーのルートに配置します。

.Nuspec ファイルの例と、必要なまたは推奨されるプロパティの一覧を次に示します。 完全なスキーマ[.nuspec リファレンス](https://docs.microsoft.com/nuget/reference/nuspec)をご覧ください。 .Nuspec ファイルを好みのファイル名で、プロジェクトのルート フォルダーに保存します。

> [!IMPORTANT]
> ```<id>``` .Nuspec ファイル内の値が一致する必要がある、```"name"```値で、プロジェクトの```manifest.json```、公開されている拡張収まらない場合は、ファイルは、Windows Admin Center で正常に読み込まします。

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

#### 必要なまたはプロパティをお勧めします。

| プロパティ名 | 必要な/推奨 | 説明 |
| ---- | ---- | ---- |
| packageType | 必須かどうか | Windows Admin Center の拡張機能に定義されている NuGet パッケージの種類である"WindowsAdminCenterExtension"を使用します。 |
| id | 必須かどうか | フィード内で一意のパッケージの識別子。 この値は、プロジェクトの manifest.json ファイルで"name"の値と一致する必要があります。  ガイダンスについては[、パッケージの一意の識別子を選択する](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)を参照してください。 |
| title | Windows Admin Center をフィードへの公開に必要な | Windows Admin Center 拡張機能マネージャーに表示されるパッケージのフレンドリ名。 |
| version | 必須かどうか | 拡張機能のバージョン。 [セマンティック バージョン (SemVer 規則)](http://semver.org/spec/v1.0.0.html)を使用してはお勧めしますが、必要ありません。 |
| 作成者 | 必須かどうか | 会社の代理として公開する場合は、会社名を使用します。 |
| description | 必須かどうか | 拡張機能の機能の説明を提供します。 |
| iconUrl | Windows Admin Center をフィードに公開するときの推奨 | 拡張機能マネージャーでを表示するアイコンの URL。 |
| projectUrl | Windows Admin Center をフィードへの公開に必要な | 拡張機能の web サイトへの URL。 別の web サイトを用意していない場合は、フィード NuGet でパッケージの web ページの URL を使用します。 |
| licenseUrl | Windows Admin Center をフィードへの公開に必要な | 拡張機能の使用許諾契約書への URL。 |
| ファイル | 必須かどうか | これら 2 つの設定は、Windows Admin Center の UI の拡張機能とゲートウェイ プラグインの実行を想定しているフォルダー構造を設定します。 |

### 3. 拡張機能の NuGet パッケージをビルドします。

上記で作成した .nuspec ファイルを使用して、NuGet パッケージこれは .nupkg ファイルをアップロードしてフィード NuGet を公開するようになりました作成します。

1. [NuGet クライアント ツールの web サイト](https://docs.microsoft.com/nuget/install-nuget-client-tools)から nuget.exe CLI ツールをダウンロードします。
2. これは .nupkg ファイルを作成するには、"nuget.exe pack [.nuspec ファイル名]"を実行します。

### 4. 拡張 NuGet パッケージへの署名

拡張機能に含まれているすべての .dll ファイルは、信頼された証明機関 (CA) からの証明書で署名する必要があります。 既定では、署名されていない .dll ファイルは Windows Admin Center が実稼働モードで実行されているときに実行されるがブロックされます。

これは、必要な手順ではありませんが、パッケージの整合性を確保する拡張機能の NuGet パッケージの署名をも強くお勧めします。

### 5. 拡張 NuGet パッケージをテストします。

拡張機能パッケージは、テストの準備ができました! これは .nupkg ファイルをアップロードして NuGet フィードまたはファイル共有にコピーします。 表示し、さまざまなフィードまたはファイル共有からパッケージをダウンロードが必要があります[、フィードの構成の変更](../configure/using-extensions.md#installing-extensions-from-a-different-feed)に、NuGet フィードまたはファイルをポイントする共有します。 テストするときは、拡張機能マネージャーで正しく表示プロパティと、正常にインストールし、拡張機能のアンインストールを確認します。

## フィードを Windows Admin Center の拡張機能の公開

によって、Windows Admin Center のフィードへの公開は拡張機能をすべての Windows Admin Center ユーザーに使えるようにすることができます。 Windows Admin Center SDK では、プレビューの中であるために、開発上の問題を解決し、高品質の製品を提供することができるかどうかを確認し、ユーザー エクスペリエンスを支援すると密接に連携したい場合がします。

拡張機能の初期バージョンをリリースするには前、に、少なくとも 2 ~ 3 週間と必要な場合、拡張機能をすべて変更を加えることを確認するための十分な時間があることを確認するリリースの前に Microsoft に拡張レビュー要求を提出することをお勧めします。 拡張機能が公開する準備ができたらをマイクロソフトに送信する必要があり、承認された場合のフィードへの公開されます。

その後、拡張機能の更新プログラムをリリースする場合は、確認のための別の要求を提出する必要があります。 変更の範囲、に応じて間のレビューへの更新の完了までの時間の短い一般場合があります。

### Microsoft の拡張機能レビュー要求を送信します。

拡張レビュー要求を送信するには、次の情報を入力し、 [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request)に記載されたメールを送信します。 1 週間以内、メールに返信しますされます。

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### レビューと公開のため、拡張機能パッケージを提出します。

[拡張機能パッケージを作成](#creating-an-extension-package)するため、上記の手順を実行して、.nuspec ファイルが適切に定義し、ファイルに署名してください。 以下を含むプロジェクトの web サイトがあることもお勧めします。

- 拡張機能のスクリーン ショットやビデオなどの詳細な説明
- メール アドレスまたは web サイトの機能に関するフィードバックまたは質問を受信するには

拡張機能を公開する準備ができたら、電子メール[wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review)を送信しては、拡張機能パッケージを送信する方法の手順を提供します。 パッケージを受信します確認し、承認された場合、Windows Admin Center をフィードに発行しますがします。