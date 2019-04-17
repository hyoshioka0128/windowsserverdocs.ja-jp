---
title: Windows Admin Center のインストール
description: Windows PC やサーバーに Windows Admin Center をインストールする方法。
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 496a67cfb93bf9b42b202f6a61211a085a9253b6
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296694"
---
# Windows Admin Center のインストール

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## インストールの種類を決定します。

[サポートされているオペレーティング システム](..\plan\installation-options.md#supported-operating-systems-installation)が含まれている[インストール オプション](..\plan\installation-options.md)を確認します。 Azure で VM に Windows Admin Center をインストールするには、 [Azure で Windows Admin Center を展開](../azure/deploy-wac-in-azure.md)を参照してください。

## Windows 10 へのインストール

Windows 10 に Windows Admin Center をインストールする場合、既定でポート 6515 が使用されますが、別のポートを指定することもできます。 また、デスクトップ ショートカットを作成したり、Windows Admin Center を使用して TrustedHosts を管理したりすることもできます。

> [!NOTE]
> ワークグループ環境の場合、またはドメイン内でローカル管理者の資格情報を使用する場合は、TrustedHosts を変更する必要があります。 この設定を行わなかった場合は、[TrustedHosts を手動で構成する](../support/troubleshooting.md#configure-trustedhosts)必要があります。

**[スタート]** メニューから Windows Admin Center を起動すると、既定のブラウザーで開きます。

初めて Windows Admin Center を起動したときに、デスクトップの通知領域にアイコンが表示されます。 このアイコンを右クリックし、**[開く]** を選択して既定のブラウザーでツールを開くか、**[終了]** を選択してバックグラウンド プロセスを終了します。

## Windows Server (デスクトップ エクスペリエンスあり) へのインストール

Windows Server では、Windows Admin Center がネットワーク サービスとしてインストールされます。 サービスがリッスンするポートを指定する必要があり、それには HTTPS 用の証明書が必要です。 インストーラーは、テスト用の自己署名証明書を作成するか、コンピューターに既にインストールされている証明書のサムプリントを提供することができます。 生成された証明書を使用する場合は、証明書がサーバーの DNS 名と一致する必要があります。 独自の証明書を使用する場合は、証明書で提供される名前 (ワイルドカード証明書はサポートされていません) コンピューター名に一致することを確認してください。Windows Admin center の TrustedHosts を管理するかの選択肢も付与されます。

> [!NOTE]
> ワークグループ環境の場合、またはドメイン内でローカル管理者の資格情報を使用する場合は、TrustedHosts を変更する必要があります。 この設定を行わなかった場合は、[TrustedHosts を手動で構成する](../support/troubleshooting.md#configure-trustedhosts)必要があります。

インストールが完了したらとリモート コンピューターからブラウザーを開き、インストーラーの最後の手順で表示される URL に移動します。

> [!WARNING]
> 自動的に生成された証明書は、インストール後 60 日で期限が切れます。

## Server Core のインストール

Windows Server の Server Core インストールがある場合は、(管理者として実行されている) コマンド プロンプトから Windows Admin Center をインストールできます。 ポートと SSL 証明書を、それぞれ `SME_PORT` および `SSL_CERTIFICATE_OPTION` 引数を使用して指定します。 既存の証明書を使用する場合は、`SME_THUMBPRINT` を使用してその拇印を指定します。

> [!WARNING]
> Windows Admin Center をインストールすると、すべてのリモート PowerShells セッションをサーバーは、WinRM サービスが再起動されます。 ローカルの Cmd または PowerShell からインストールすることをお勧めします。 パラメーターを追加するには、WinRM サービスを再起動して分割されるオートメーション ソリューションをインストールする場合は```RESTART_WINRM=0```するインストールの引数が WinRM する必要がありますを再起動する Windows Admin Center の関数にします。

次のコマンドを実行して Windows Admin Center をインストールし、自己署名証明書を自動生成します。

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

次のコマンドを実行して既存の証明書を使用して Windows Admin Center をインストールします。

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> PowerShell からドットとスラッシュによる相対パス表記 (`.\<WindowsAdminCenterInstallerName>.msi` など) を使用して `msiexec` を起動しないでください。 その表記はサポートされていないため、インストールが失敗します。 `.\`プレフィックスを削除するか、MSI への完全パスを指定してください。

## Windows Admin Center の更新

Microsoft Update を使用するか、手動でインストールすることによって、プレビュー以外のバージョンの Windows Admin Center を更新することができます。 

Windows Admin Center の新しいバージョンにアップグレードする場合、設定は保持されます。 アップグレードの Insider Preview バージョンの Windows Admin Center 公式にサポートされていない - - クリーン インストールを実行することをお勧めと思いますが、ブロックしないでください。