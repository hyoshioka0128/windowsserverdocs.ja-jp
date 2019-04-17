---
title: インストールし、拡張機能の管理
description: インストールし、Windows Admin Center (Project Honolulu) で拡張機能の管理
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c775dd5a3011115bbb031c0b9e4e24a8911d378e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296704"
---
# インストールし、拡張機能の管理

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center は各接続の種類とツールが拡張機能をインストール、アンインストールおよび更新を個別に拡張可能なプラットフォームとして構築されています。 Microsoft とその他の開発者によって公開された新しい拡張機能の検索をインストールし、Windows Admin Center のインストール全体を更新することがなく、それらを個別に更新します。 別の NuGet フィードを構成またはファイル共有でき、組織内で内部的に使用する拡張機能を配布できます。

## 拡張機能をインストールします。

Windows Admin Center は、フィード、指定した NuGet から利用可能な拡張機能に表示されます。 既定では、Windows Admin Center を指すフィード マイクロソフトの公式 NuGet マイクロソフトおよびその他の開発者によって公開された拡張機能をホストします。

1. 左側のウィンドウの右上の _gt [**設定**] ボタンを**拡張機能**をクリックします。 
2. **利用可能な拡張機能**] タブには、インストール可能なフィードの拡張機能が表示されます。
3. **詳細**ウィンドウで、拡張機能の説明、バージョン、発行元およびその他の情報を表示する拡張機能をクリックします。
4. **インストール**を拡張機能をインストールする] をクリックします。 ゲートウェイは、この変更を加えるに昇格モードで実行する必要がある場合、UAC 昇格のプロンプトが表示されます。 インストールが完了したら、お使いのブラウザーは自動的に更新し、Windows Admin Center は、新しい拡張機能がインストールされていると再読み込みします。 インストールしようとしている拡張機能が以前にインストールされた拡張機能の更新プログラムの場合は、更新プログラムをインストールする**には、最新の更新**ボタンをクリックできます。 インストールされている拡張機能を表示して、更新プログラムが [**状態**] 列で利用可能なかどうかに**インストールされている拡張機能**] タブに移動することもできます。

## さまざまなフィードからの拡張機能をインストールします。

Windows Admin Center は、複数のフィードをサポートしていると、表示して、一度に 1 つ以上のフィードからパッケージを管理することができます。 任意の NuGet フィード NuGet V2 Api をサポートするまたはから拡張機能をインストールするため、ファイル共有を Windows Admin Center に追加することができます。

1. 左側のウィンドウの右上の _gt [**設定**] ボタンを**拡張機能**をクリックします。
2. 右側のウィンドウで、[**フィード**] タブをクリックします。
3. 別のフィードを追加する**追加**] をクリックします。 NuGet フィードとは、NuGet V2 フィードの URL を入力します。 NuGet フィード プロバイダーまたは管理者は、URL の情報を提供できる必要があります。 ファイル共有では、ファイルの完全なパスを入力で拡張機能パッケージ ファイル (これは .nupkg) が格納されている共有します。
4. **[追加]** をクリックします。 ゲートウェイは、この変更を加えるに昇格モードで実行する必要がある場合、UAC 昇格のプロンプトが表示されます。

**利用可能な拡張機能**の一覧では、登録されているすべてのフィードからの拡張機能を説明します。 各拡張機能は、**パッケージのフィード**列を使用してからどのフィードを確認できます。

## 拡張機能のアンインストール

既にインストールされている拡張機能のアンインストールしたり、でも Windows Admin Center のインストールの一部としてプレインストールされていたすべてのツールをアンインストールすることができます。

1. 左側のウィンドウの右上の _gt [**設定**] ボタンを**拡張機能**をクリックします。 
2. インストールされているすべての拡張機能を表示する、**インストールされている拡張機能**] タブをクリックします。
3. 削除するには、拡張機能を選択し、[**アンインストール**] をクリックします。

アンインストールが完了、お使いのブラウザーは自動的に更新、削除拡張子を持つ Windows Admin Center を再読み込みされます。 Windows Admin Center の一部としてプレインストールされているツールをアンインストールした場合、ツールは、**利用可能な拡張機能**] タブに再インストール可能になります。

## インターネット接続いないコンピューターで、拡張機能をインストールします。

Windows Admin Center は、インターネットに接続されていない、またはプロキシの背後にあるコンピューターにインストールされてにアクセスして、Windows Admin Center のフィードから拡張機能をインストールできません可能性があります。 手動または PowerShell スクリプトでは、拡張機能パッケージをダウンロードして、ファイル共有またはローカル ドライブからパッケージを取得する Windows Admin Center を構成できます。

### 拡張機能パッケージを手動でダウンロード

1. 別のコンピューターでインターネット接続には、web ブラウザーを開き、次の URL に移動します。[https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

  * Msft sme.myget.org と拡張機能パッケージの表示へのログインにアカウントを作成する必要があります。

2. パッケージの詳細ページを表示するインストールするパッケージの名前をクリックします。
3. パッケージの詳細ページの右側のウィンドウで**ダウンロード**リンクをクリックし、拡張機能のこれは .nupkg ファイルをダウンロードします。
4. すべてのパッケージをダウンロードするのには、手順 2 ~ 3 を繰り返します。
5. Windows Admin Center が、インストールされているコンピューターからアクセスできるファイル共有にまたはコンピューターのローカル ディスクには、パッケージ ファイルをコピーします。
6. [さまざまなフィードからの拡張機能をインストールする手順に従ってください](#installing-extensions-from-a-different-feed)ください。

### PowerShell スクリプトを使用したパッケージのダウンロード

多くのスクリプト利用できるがフィード NuGet から NuGet パッケージをダウンロードするため、インターネット上です。 [Jon Galloway によって提供されるスクリプト](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)、Microsoft のシニア プログラム マネージャーを使用します。

1. 、[ブログの投稿](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)で説明した、NuGet パッケージ、またはコピーとして、スクリプトをインストールし、PowerShell ISE にスクリプトを貼り付けます。
2. 編集、NuGet をスクリプトの最初の行のフィードの v2 URL です。 フィードから Windows Admin Center の公式のパッケージをダウンロードする場合は、以下の URL を使用します。

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. スクリプトを実行し、すべての NuGet パッケージは、フィードから次のローカル フォルダーにダウンロードされます: %USERPROFILE%\Documents\NuGetLocal
4. [さまざまなフィードからの拡張機能をインストールする手順に従ってください](#installing-extensions-from-a-different-feed)ください。

## PowerShell での拡張機能を管理します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center Preview には、ゲートウェイの拡張機能を管理する PowerShell モジュールが含まれます。

```powershell
# Add the module to the current session
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ExtensionTools"
# Available cmdlets: Get-Feed, Add-Feed, Remove-Feed, Get-Extension, Install-Extension, Uninstall-Extension, Update-Extension

# List feeds
Get-Feed "https://wac.contoso.com"

# Add a new extension feed
Add-Feed -GatewayEndpoint "https://wac.contoso.com" -Feed "\\WAC\our-private-extensions"

# Remove an extension feed
Remove-Feed -GatewayEndpoint "https://wac.contoso.com" -Feed "\\WAC\our-private-extensions"

# List all extensions
Get-Extension "https://wac.contoso.com"

# Install an extension (locate the latest version from all feeds and install it)
Install-Extension -GatewayEndpoint "https://wac.contoso.com" "msft.sme.containers"

# Install an extension (latest version from a specific feed, if the feed is not present, it will be added)
Install-Extension -GatewayEndpoint "https://wac.contoso.com" "msft.sme.containers" -Feed "https://aka.ms/sme-extension-feed"

# Install an extension (install a specific version)
Install-Extension "https://wac.contoso.com" "msft.sme.certificate-manager" "0.133.0"

# Uninstall-Extension
Uninstall-Extension "https://wac.contoso.com" "msft.sme.containers"

# Update-Extension
Update-Extension "https://wac.contoso.com" "msft.sme.containers"
```

### [Windows Admin Center SDK 拡張機能の構築に関する詳細を表示](../extend/extensibility-overview.md)します。