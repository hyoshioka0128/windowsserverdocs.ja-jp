---
title: 高可用性を備えた Windows Admin Center を展開します。
description: 高可用性 (プロジェクト ホノルル) を備えた Windows Admin Center を展開します。
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ad8e2a8eade1ea9d3faaba8f387b1f489854e589
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280632"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>高可用性を備えた Windows Admin Center を展開します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center は、Windows Admin Center ゲートウェイ サービスの高可用性を実現するフェールオーバー クラスターでデプロイできます。 提供されているソリューションとは、Windows Admin Center の 1 つだけのインスタンスがアクティブなときに、アクティブ/パッシブ ソリューションです。 クラスター内のノードのいずれかが失敗した場合は場合、Windows Admin Center 適切にフェールオーバー操作が別のノードに引き続きシームレスに環境内のサーバーを管理することができます。 

[その他の Windows Admin Center 展開オプションについて説明します。](../plan/installation-options.md)

## <a name="prerequisites"></a>前提条件

- Windows Server 2016 または 2019 で 2 つ以上のノードのフェールオーバー クラスター。 [フェールオーバー クラスターのデプロイに関する詳細](../../../failover-clustering/failover-clustering-overview.md)します。
- クラスターの共有ボリューム (CSV)、クラスター内のすべてのノードによってアクセスできる永続的なデータを格納する Windows Admin Center をします。 10 GB は、CSV を十分になります。
- 高可用性デプロイ スクリプトから[Windows Admin Center HA スクリプトの zip ファイル](https://aka.ms/WACHAScript)します。 ローカル コンピューターにスクリプトを含む .zip ファイルをダウンロードし、スクリプトをコピー、必要に応じて、以下のガイダンスに基づく.
- 推奨される、省略可能: 署名証明書の .pfx とパスワード。 既ににクラスター ノードで、証明書をインストールする必要はありません - スクリプトはする処理を実行します。 指定しない場合、インストール スクリプトは、60 日後に有効期限が切れる自己署名証明書を生成します。

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>フェールオーバー クラスターにインストール Windows Admin Center

1. コピー、```Install-WindowsAdminCenterHA.ps1```クラスター内のノードにスクリプト。 ダウンロードするか、Windows Admin Center .msi を同じノードにコピーします。
2. RDP と実行を使用してノードに接続する、```Install-WindowsAdminCenterHA.ps1```は次のパラメーターには、そのノードからスクリプト。
    - `-clusterStorage`: Windows Admin Center のデータを格納するクラスターの共有ボリュームのローカル パス。
    - `-clientAccessPoint`: Windows Admin Center へのアクセスに使用する名前を選択します。 例では、パラメーターを使用して、スクリプトを実行する場合、 `-clientAccessPoint contosoWindowsAdminCenter`、Windows Admin Center サービスにアクセスしてアクセスします。 `https://contosoWindowsAdminCenter.<domain>.com`
    - `-staticAddress` :(省略可能)。 汎用サービスをクラスターの静的アドレスを 1 つまたは複数です。 
    - `-msiPath` :Windows Admin Center の .msi ファイルのパス。
    - `-certPath` :(省略可能)。 証明書の .pfx ファイルのパス。
    - `-certPassword` :(省略可能)。 SecureString で提供される証明書の .pfx のパスワード `-certPath`
    - `-generateSslCert` :(省略可能)。 署名証明書を指定しない場合は、自己署名証明書を生成するには、このパラメーター フラグが含まれます。 自己署名証明書の 60 日間の有効期限が切れることに注意してください。
    - `-portNumber` :(省略可能)。 ポートを指定しない場合は、ポート 443 (HTTPS) でゲートウェイ サービスが配置されます。 使用するには、別のポートは、このパラメーターで指定します。 注こと、カスタム ポート (443) 以外は何を使用する場合がアクセスする、Windows Admin Center https:// に移動して\<clientAccessPoint\>:\<ポート\>します。

> [!NOTE]
> ```Install-WindowsAdminCenterHA.ps1```スクリプト サポート```-WhatIf ```と```-Verbose```パラメーター

### <a name="examples"></a>例

#### <a name="install-with-a-signed-certificate"></a>署名証明書をインストールします。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>自己署名証明書をインストールします。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>既存の高可用性インストールを更新します。

使用して、同じ```Install-WindowsAdminCenterHA.ps1```接続データを失うことがなく、HA デプロイを更新するスクリプト。

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Windows Admin Center の新しいバージョンに更新するには

Windows Admin Center の新しいバージョンがリリースされると、実行、```Install-WindowsAdminCenterHA.ps1```スクリプトのみを使用して、```msiPath```パラメーター。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Windows Admin Center で使用される証明書を更新します。

新しい証明書の .pfx ファイルとパスワードを提供することで、いつでも Windows Admin Center の HA デプロイで使用する証明書を更新することができます。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

新しい .msi ファイルを使用して、Windows Admin Center プラットフォームを更新すると同時に、証明書を更新することもできます。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>Uninstall

フェールオーバー クラスターからアンインストールするには、Windows Admin Center の HA 展開に渡す、```-Uninstall```パラメーターを```Install-WindowsAdminCenterHA.ps1```スクリプト。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>トラブルシューティング

ログは、CSV (たとえば、C:\ClusterStorage\Volume1\temp) の一時フォルダーに保存されます。