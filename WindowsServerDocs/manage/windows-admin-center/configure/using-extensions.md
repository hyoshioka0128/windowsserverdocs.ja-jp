---
title: インストールして、拡張機能の管理
description: インストールして、Windows Admin Center (プロジェクト ホノルル) で拡張機能の管理
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c775dd5a3011115bbb031c0b9e4e24a8911d378e
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63748407"
---
# <a name="install-and-manage-extensions"></a>インストールして、拡張機能の管理

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center は各接続の種類とツールが拡張機能をインストール、アンインストールおよび更新を個別に拡張可能プラットフォームとして構築されています。 Microsoft または他の開発者によって発行された新しい拡張機能を検索し、インストールして、Windows Admin Center インストール全体を更新することがなく、それらを個別に更新できます。 別の NuGet フィードの構成、ファイル共有またはし、組織内で内部的に使用する拡張機能の配布などもできます。

## <a name="installing-an-extension"></a>拡張機能のインストール

Windows Admin Center は、指定された NuGet フィードから使用できる拡張機能を紹介します。 既定では、Windows Admin Center ポイント Microsoft の公式 NuGet フィードを Microsoft または他の開発者によって発行された拡張機能をホストします。

1. をクリックして、**設定**上部右にあるボタン > 左側のウィンドウで次のようにクリックします。**拡張**。 
2. **使用可能な拡張** タブがインストール可能なフィードで拡張機能を一覧表示します。
3. 拡張機能の説明、バージョン、パブリッシャーおよびその他の情報を表示する拡張機能をクリックして、**詳細**ウィンドウ。
4. クリックして**インストール**拡張機能をインストールします。 場合は、ゲートウェイは、この変更を行う管理者特権モードで実行する必要があります、UAC の昇格時のプロンプトが表示されます。 インストールが完了したら、お使いのブラウザーが自動的に更新され、Windows Admin Center は、新しい拡張機能がインストールされていると再読み込みされます。 拡張機能しようとする場合のインストールには、以前にインストールされた拡張機能の更新プログラムをクリックする、**を最新の更新**クリックすると、更新プログラムをインストールします。 移動することもできます。、**拡張機能のインストールされている**で更新プログラムがある場合は、インストールされている表示拡張機能を参照してください タブ、**状態**列。

## <a name="installing-extensions-from-a-different-feed"></a>別のフィードから拡張機能のインストール

Windows Admin Center は、複数のフィードをサポートしていると、表示して、一度に 1 つ以上のフィードからパッケージを管理します。 あらゆる NuGet フィードをサポートする、NuGet V2 Api またはファイル共有は、拡張機能をインストールするため Windows Admin Center に追加できます。

1. をクリックして、**設定**上部右にあるボタン > 左側のウィンドウで次のようにクリックします。**拡張**。
2. 右側のウィンドウで、をクリックして、**フィード**タブ。
3. をクリックして、**追加**別のフィードを追加するボタンをクリックします。 NuGet フィード、NuGet V2 フィード URL を入力します。 NuGet フィード プロバイダーまたは管理者は、URL の情報を提供できる必要があります。 ファイル共有の場合は、ファイルの完全なパスを入力します。 共有拡張機能パッケージ ファイル (.nupkg) が格納されます。
4. **[追加]** をクリックします。 場合は、ゲートウェイは、この変更を行う管理者特権モードで実行する必要があります、UAC の昇格時のプロンプトが表示されます。

**使用可能な拡張**リスト登録されているすべてのフィードからの拡張機能が表示されます。 各拡張機能を使用してから、どのフィードをチェックすることができます、**パッケージ フィード**列。

## <a name="uninstalling-an-extension"></a>拡張機能をアンインストールします。

既にインストールされているすべての拡張機能をアンインストールまたはでも Windows Admin Center のインストールの一部としてプレインストールされた任意のツールをアンインストールできます。

1. をクリックして、**設定**上部右にあるボタン > 左側のウィンドウで次のようにクリックします。**拡張**。 
2. をクリックして、**拡張機能のインストールされている**タブにはインストールされているすべての拡張機能を表示します。
3. クリックし、アンインストールするには、拡張機能の選択**アンインストール**します。

アンインストールが完了し、ブラウザーが自動的に更新される、Windows Admin Center は、拡張機能の削除と再読み込みされます。 ツールがで再インストールする Windows Admin Center の一部として事前インストールされたツールをアンインストールした場合、**使用可能な拡張**タブ。

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>インターネットに接続していないコンピューターで拡張機能のインストール

Windows Admin Center は、インターネットに接続されていない、またはプロキシの背後にあるコンピューターにインストールされてにアクセスして、Windows Admin Center がフィードから拡張機能をインストールできません可能性があります。 手動でまたは PowerShell スクリプトを使用して、拡張機能パッケージをダウンロードし、ファイル共有またはローカル ドライブからパッケージを取得する Windows Admin Center を構成します。

### <a name="manually-downloading-extension-packages"></a>拡張機能パッケージを手動でダウンロード

1. インターネットに接続された別のコンピューターで web ブラウザーを開き、次の URL に移動します。 [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

  * Msft sme.myget.org と拡張機能パッケージを表示するログインにアカウントを作成する必要があります。

2. パッケージ詳細ページを表示するをインストールするパッケージの名前をクリックします。
3. をクリックして、**ダウンロード**パッケージ詳細ページの右側のペインのリンクし、拡張機能の .nupkg ファイルをダウンロードします。
4. すべてのパッケージをダウンロードするには、手順 2. および 3. を繰り返します。
5. Windows Admin Center がインストールされているコンピューターからアクセスできるファイル共有またはコンピューターのローカル ディスクには、パッケージ ファイルをコピーします。
6. [別のフィードから拡張機能をインストールする手順に従って](#installing-extensions-from-a-different-feed)します。

### <a name="downloading-packages-with-a-powershell-script"></a>PowerShell スクリプトを使用してパッケージをダウンロード

多くのスクリプトに使用できるある NuGet フィードから NuGet パッケージをダウンロードするためのインターネットです。 使用して、 [Jon Galloway によって提供されるスクリプト](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)マイクロソフトのシニア プログラム マネージャーです。

1. 」の説明に従って、[ブログの投稿](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)NuGet パッケージとして、スクリプトのインストール、またはコピーして、PowerShell ISE にスクリプトを貼り付けます。
2. 編集、NuGet にスクリプトの最初の行のフィードの v2 の URL です。 公式の Windows Admin Center からのパッケージ フィードをダウンロードする場合は、下記の URL を使用します。

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. スクリプトを実行し、次のローカル フォルダー、フィードからすべての NuGet パッケージにダウンロードされます: %USERPROFILE%\Documents\NuGetLocal
4. [別のフィードから拡張機能をインストールする手順に従って](#installing-extensions-from-a-different-feed)します。

## <a name="manage-extensions-with-powershell"></a>PowerShell を使用した拡張機能を管理します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center プレビューには、ゲートウェイの拡張機能を管理する PowerShell モジュールが含まれています。

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

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Windows Admin Center SDK を使用した拡張機能の構築について詳しく学習](../extend/extensibility-overview.md)します。