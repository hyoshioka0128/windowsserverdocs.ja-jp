---
title: 拡張機能のインストールと管理
description: Windows 管理センター (Project ホノルル) での拡張機能のインストールと管理
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d49e25591c705afa217b2332ee48eb42c5c2f7ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357242"
---
# <a name="install-and-manage-extensions"></a>拡張機能のインストールと管理

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターは拡張可能なプラットフォームとして構築されています。各接続の種類とツールは、個別にインストール、アンインストール、更新が可能な拡張機能です。 Microsoft や他の開発者によって発行された新しい拡張機能を検索し、それらを個別にインストールおよび更新することができます。 Windows 管理センターのインストール全体を更新する必要はありません。 また、別の NuGet フィードまたはファイル共有を構成し、組織内で内部的に使用する拡張機能を配布することもできます。

## <a name="installing-an-extension"></a>拡張機能のインストール

Windows 管理センターでは、指定された NuGet フィードから利用可能な拡張機能が表示されます。 既定では、Windows 管理センターは microsoft の公式 NuGet フィードを指しており、Microsoft や他の開発者によって発行された拡張機能をホストしています。

1. 左ペインの右上にある **[設定]** ボタンをクリックし、 **[拡張機能]** をクリックし > ます。 
2. **[使用できる拡張]** タブには、インストールに使用できるフィードの拡張機能が一覧表示されます。
3. 拡張機能をクリックすると、**詳細**ウィンドウに拡張機能の説明、バージョン、発行元、およびその他の情報が表示されます。
4. **[インストール]** をクリックして拡張機能をインストールします。 この変更を行うためにゲートウェイを管理者特権モードで実行する必要がある場合は、UAC の昇格時のプロンプトが表示されます。 インストールが完了すると、ブラウザーが自動的に更新され、新しい拡張機能がインストールされた状態で Windows 管理センターが再度読み込まれます。 インストールしようとしている拡張機能が、以前にインストールした拡張機能に更新されている場合は、 **[最新の情報に更新]** ボタンをクリックして更新プログラムをインストールできます。 インストールされている **[拡張機能]** タブにアクセスして、インストールされている拡張機能を表示し、 **[状態]** 列に更新プログラムがあるかどうかを確認することもできます。

## <a name="installing-extensions-from-a-different-feed"></a>別のフィードからの拡張機能のインストール

Windows 管理センターでは複数のフィードがサポートされており、一度に複数のフィードのパッケージを表示および管理することができます。 NuGet V2 Api またはファイル共有をサポートするすべての NuGet フィードは、から拡張機能をインストールするために Windows 管理センターに追加できます。

1. 左ペインの右上にある **[設定]** ボタンをクリックし、 **[拡張機能]** をクリックし > ます。
2. 右側のウィンドウで、 **[フィード]** タブをクリックします。
3. **[追加]** ボタンをクリックして、別のフィードを追加します。 NuGet フィードの場合は、NuGet V2 フィード URL を入力します。 NuGet フィードプロバイダーまたは管理者は、URL 情報を提供できる必要があります。 ファイル共有の場合は、拡張機能パッケージファイル (nupkg) が格納されているファイル共有の完全パスを入力します。
4. **[追加]** をクリックします。 この変更を行うためにゲートウェイを管理者特権モードで実行する必要がある場合は、UAC の昇格時のプロンプトが表示されます。

**[使用できる拡張機能]** の一覧には、すべての登録済みフィードの拡張機能が表示されます。 各拡張機能がどのフィードを使用するかは、**パッケージフィード**列の使用方法を確認できます。

## <a name="uninstalling-an-extension"></a>拡張機能のアンインストール

以前にインストールした拡張機能をアンインストールすることも、Windows 管理センターのインストールの一部としてプレインストールされていたすべてのツールをアンインストールすることもできます。

1. 左ペインの右上にある **[設定]** ボタンをクリックし、 **[拡張機能]** をクリックし > ます。 
2. **[インストール済みの拡張]** タブをクリックして、インストールされているすべての拡張機能を表示します
3. アンインストールする拡張機能を選択し、 **[アンインストール]** をクリックします。

アンインストールが完了すると、ブラウザーが自動的に更新され、拡張機能が削除された状態で Windows 管理センターが再度読み込まれます。 Windows 管理センターの一部としてプレインストールされていたツールをアンインストールした場合は、 **[使用可能な拡張]** タブでツールを再インストールできます。

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>インターネットに接続していないコンピューターへの拡張機能のインストール

インターネットに接続されていないコンピューターまたはプロキシの内側にあるコンピューターに Windows 管理センターがインストールされている場合、Windows 管理センターフィードから拡張機能にアクセスしてインストールできない可能性があります。 拡張機能パッケージは、手動または PowerShell スクリプトを使用してダウンロードし、ファイル共有またはローカルドライブからパッケージを取得するように Windows 管理センターを構成することができます。

### <a name="manually-downloading-extension-packages"></a>拡張機能パッケージを手動でダウンロードする

1. インターネットに接続されている別のコンピューターで、web ブラウザーを開き、次の URL に移動します: [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

   * 拡張機能パッケージを表示するには、msft-sme.myget.org でアカウントを作成し、ログインする必要がある場合があります。

2. パッケージの詳細ページを表示するには、インストールするパッケージの名前をクリックします。
3. パッケージの詳細ページの右側のウィンドウにある **[ダウンロード]** リンクをクリックし、拡張機能の nupkg ファイルをダウンロードします。
4. ダウンロードするすべてのパッケージについて、手順 2. と 3. を繰り返します。
5. Windows 管理センターがインストールされているコンピューター、またはコンピューターのローカルディスクにアクセスできるファイル共有にパッケージファイルをコピーします。
6. [指示に従って、別のフィードから拡張機能をインストール](#installing-extensions-from-a-different-feed)します。

### <a name="downloading-packages-with-a-powershell-script"></a>PowerShell スクリプトを使用したパッケージのダウンロード

NuGet フィードから NuGet パッケージをダウンロードするために、インターネット上で利用できるスクリプトは多数あります。 ここでは、Microsoft のシニアプログラムマネージャー[である Jon Galloway によって提供されるスクリプト](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)を使用します。

1. [ブログ記事](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)で説明されているように、スクリプトを NuGet パッケージとしてインストールするか、スクリプトをコピーして PowerShell ISE に貼り付けます。
2. スクリプトの最初の行を NuGet フィードの v2 URL に編集します。 Windows 管理センターの公式フィードからパッケージをダウンロードする場合は、以下の URL を使用してください。

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. スクリプトを実行すると、フィードから次のローカルフォルダーにすべての NuGet パッケージがダウンロードされます:%USERPROFILE%\Documents\NuGetLocal
4. [指示に従って、別のフィードから拡張機能をインストール](#installing-extensions-from-a-different-feed)します。

## <a name="manage-extensions-with-powershell"></a>PowerShell を使用した拡張機能の管理

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センタープレビューには、ゲートウェイ拡張機能を管理する PowerShell モジュールが含まれています。

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

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Windows 管理センター SDK を使用した拡張機能の構築の詳細については、こちらを参照して](../extend/extensibility-overview.md)ください。