---
title: Windows Admin Center のインストール
description: 複数のユーザーが Web ブラウザーを使用して Windows Admin Center にアクセスできるように、Windows PC 上またはサーバー上に Windows Admin Center をインストールする方法を説明します。
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: cab128a3da9fa58c598cebcdf188058631c33977
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "75950007"
---
# <a name="install-windows-admin-center"></a>Windows Admin Center のインストール

> 適用先:Windows Admin Center、Windows Admin Center Preview

このトピックでは、複数のユーザーが Web ブラウザーを使用して Windows Admin Center にアクセスできるように、Windows PC 上またはサーバー上に Windows Admin Center をインストールする方法について説明します。

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../overview.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="determine-your-installation-type"></a>インストールの種類を決定する

[サポートされているオペレーティング システム](https://docs.microsoft.com/windows-server/manage/windows-admin-center/plan/installation-options#installation-supported-operating-systems)を含む[インストール オプション](../plan/installation-options.md)について確認します。 Azure にある VM 上に Windows Admin Center をインストールするには、「[Windows Admin Center を Azure にデプロイする](../azure/deploy-wac-in-azure.md)」を参照してください。

## <a name="install-on-windows-10"></a>Windows 10 へのインストール

Windows 10 に Windows Admin Center をインストールする場合、既定でポート 6516 が使用されますが、別のポートを指定することもできます。 また、デスクトップ ショートカットを作成したり、Windows Admin Center を利用して TrustedHosts を管理したりすることもできます。

> [!NOTE]
> ワークグループ環境の場合、またはドメイン内でローカル管理者の資格情報を使用する場合は、TrustedHosts を変更する必要があります。 この設定を行わなかった場合は、[TrustedHosts を手動で構成する](../support/troubleshooting.md#configure-trustedhosts)必要があります。

**[スタート]** メニューから Windows Admin Center を起動すると、既定のブラウザーで開きます。

初めて Windows Admin Center を起動したときに、デスクトップの通知領域にアイコンが表示されます。 このアイコンを右クリックし、 **[開く]** を選択して既定のブラウザーでツールを開くか、 **[終了]** を選択してバックグラウンド プロセスを終了します。

## <a name="install-on-windows-server-with-desktop-experience"></a>デスクトップ エクスペリエンスを搭載した Windows Server へのインストール

Windows Server では、Windows Admin Center がネットワーク サービスとしてインストールされます。 サービスがリッスンするポートを指定する必要があり、それには HTTPS 用の証明書が必要です。 インストーラーによってテスト用の自己署名証明書を作成するか、コンピューターに既にインストールされている証明書のサムプリントを指定することができます。 生成された証明書を使用する場合は、サーバーの DNS 名と一致している必要があります。 独自の証明書を使用する場合は、証明書に指定されている名前がコンピューター名と一致していることを確認します (ワイルドカードの証明書はサポートされていません)。また、Windows Admin Center を使用して TrustedHosts を管理することもできます。

> [!NOTE]
> ワークグループ環境の場合、またはドメイン内でローカル管理者の資格情報を使用する場合は、TrustedHosts を変更する必要があります。 この設定を行わなかった場合は、[TrustedHosts を手動で構成する](../support/troubleshooting.md#configure-trustedhosts)必要があります。

インストールが完了したら、リモート コンピューターからブラウザーを開き、インストーラーの最後の手順に示されている URL に移動します。

> [!WARNING]
> 自動的に生成された証明書は、インストール後 60 日で期限が切れます。

## <a name="install-on-server-core"></a>Server Core へのインストール

Windows Server の Server Core インストールがある場合は、(管理者として実行されている) コマンド プロンプトから Windows Admin Center をインストールできます。 ポートと SSL 証明書を、それぞれ `SME_PORT` および `SSL_CERTIFICATE_OPTION` 引数を使用して指定します。 既存の証明書を使用する場合は、`SME_THUMBPRINT` を使用してそのサムプリントを指定します。

> [!WARNING]
> Windows Admin Center をインストールすると、WinRM サービスが再起動され、すべてのリモート PowerShells セッションがサービス提供されます。 ローカルの Cmd または PowerShell からインストールすることをお勧めします。 WinRM サービスの再起動によって損なわれてしまうオートメーション ソリューションがインストールに含まれる場合は、パラメーター ```RESTART_WINRM=0``` をインストールの引数に追加できますが、Windows Admin Center が機能するためには WinRM を再起動する必要があります。

次のコマンドを実行して Windows Admin Center をインストールし、自己署名証明書を自動生成します。

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

次のコマンドを実行して、既存の証明書を使用して Windows Admin Center をインストールします。

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> PowerShell からドットとスラッシュによる相対パス表記 (`.\<WindowsAdminCenterInstallerName>.msi` など) を使用して `msiexec` を起動しないでください。 その表記はサポートされていないため、インストールは失敗します。 `.\` プレフィックスを削除するか、MSI への完全パスを指定してください。

## <a name="upgrading-to-a-new-version-of-windows-admin-center"></a>新しいバージョンの Windows Admin Center へのアップグレード

Windows Admin Center の非プレビュー バージョンは、Microsoft Update を使用して更新することも、手動インストールにより更新することもできます。

新しいバージョンの Windows Admin Center にアップグレードすると、設定は保持されます。 Windows Admin Center の Insider Preview バージョンのアップグレードは、正式にはサポートされていません。クリーン インストールを行うことをお勧めしますが、Micorosoft によるブロックは行われていません。

## <a name="updating-the-certificate-used-by-windows-admin-center"></a>Windows Admin Center で使用される証明書の更新

Windows Admin Center をサービスとして展開する場合、HTTPS 用の証明書を指定する必要があります。 後でこの証明書を更新するには、インストーラーを再実行して、```change``` を選択します。
