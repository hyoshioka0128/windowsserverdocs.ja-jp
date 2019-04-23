---
title: Windows Admin Center のインストール
description: Windows Admin Center のインストール
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 94ac1281ca94a49ae54ce28d86dd4d95ff1d5574
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866923"
---
# <a name="install-windows-admin-center"></a>Windows Admin Center のインストール

>適用先:Windows Admin Center、Windows Admin Center プレビュー

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="determine-your-installation-type"></a>インストールの種類を決定します。

レビュー、[インストール オプション](..\plan\installation-options.md)が含まれています、[サポートされるオペレーティング システム](..\plan\installation-options.md#supported-operating-systems-installation)します。

## <a name="install-on-windows-10"></a>Windows 10 へのインストール

Windows 10 に Windows Admin Center をインストールする場合、既定でポート 6515 が使用されますが、別のポートを指定することもできます。 また、デスクトップ ショートカットを作成したり、Windows Admin Center を使用して TrustedHosts を管理したりすることもできます。

> [!NOTE]
> ワークグループ環境の場合、またはドメイン内でローカル管理者の資格情報を使用する場合は、TrustedHosts を変更する必要があります。 この設定を行わなかった場合は、[TrustedHosts を手動で構成する](../use/troubleshooting.md#configure-trustedhosts)必要があります。

**[スタート]** メニューから Windows Admin Center を起動すると、既定のブラウザーで開きます。

初めて Windows Admin Center を起動したときに、デスクトップの通知領域にアイコンが表示されます。 このアイコンを右クリックし、**[開く]** を選択して既定のブラウザーでツールを開くか、**[終了]** を選択してバックグラウンド プロセスを終了します。

## <a name="install-on-windows-server-with-desktop-experience"></a>Windows Server (デスクトップ エクスペリエンスあり) へのインストール

Windows Server では、Windows Admin Center がネットワーク サービスとしてインストールされます。 サービスがリッスンするポートを指定する必要があり、それには HTTPS 用の証明書が必要です。 インストーラーは、テスト用の自己署名証明書を作成するか、コンピューターに既にインストールされている証明書のサムプリントを提供することができます。 生成された証明書を使用する場合は、証明書がサーバーの DNS 名と一致する必要があります。 独自の証明書を使用することを確認します証明書に指定された名前と一致する場合、コンピューター名 (ワイルドカード証明書はサポートされていません。)また、Windows Admin Center が、TrustedHosts を管理できるようにする選択も付与されます。

> [!NOTE]
> ワークグループ環境の場合、またはドメイン内でローカル管理者の資格情報を使用する場合は、TrustedHosts を変更する必要があります。 この設定を行わなかった場合は、[TrustedHosts を手動で構成する](../use/troubleshooting.md#configure-trustedhosts)必要があります。

インストールが完了すると、リモート コンピューターからブラウザーを開き、インストーラーの最後の手順で示されている URL に移動します。

> [!WARNING]
> 自動的に生成された証明書は、インストール後 60 日で期限が切れます。

## <a name="install-on-server-core"></a>Server Core のインストール

Windows Server の Server Core インストールがある場合は、(管理者として実行されている) コマンド プロンプトから Windows Admin Center をインストールできます。 ポートと SSL 証明書を、それぞれ `SME_PORT` および `SSL_CERTIFICATE_OPTION` 引数を使用して指定します。 既存の証明書を使用する場合は、`SME_THUMBPRINT` を使用してその拇印を指定します。

> [!WARNING]
> Windows Admin Center をインストールすると、すべてのリモート PowerShells セッションはサーバーを WinRM サービスを再起動します。 ローカルの Cmd または PowerShell からインストールすることをお勧めします。 パラメーターを追加するには、WinRM サービスを再起動して分類は、automation ソリューションをインストールする場合```RESTART_WINRM=0```インストールに、引数が WinRM 再起動する必要がある Windows Admin Center を関数にします。

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

## <a name="updating-windows-admin-center"></a>Windows Admin Center を更新しています

設定は、Windows Admin Center の新しいバージョンにアップグレードするときに保持されます。 Windows Admin Center のアップグレードの Insider Preview バージョンは正式にサポートされていません - - クリーン インストールを行う方が優れていると思いますが、それをブロックしません。