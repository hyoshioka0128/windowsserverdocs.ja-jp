---
title: Windows Admin Center の高可用性展開
description: Windows Admin Center の高可用性展開 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6ae7bd9ed7aee5835ac1f53b9e10879ad8824f52
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406941"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>Windows Admin Center の高可用性展開

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows Admin Center をフェールオーバー クラスターに展開して、Windows Admin Center ゲートウェイ サービスの高可用性を実現することができます。 提供されるソリューションはアクティブ/パッシブ ソリューションであり、Windows Admin Center の 1 つのインスタンスのみがアクティブです。 クラスター内のいずれかのノードで障害が発生した場合、Windows Admin Center では別のノードに速やかにフェールオーバーされます。これにより、環境内のサーバーの管理をシームレスに進めることができます。 

[その他の Windows Admin Center の展開オプションについてはこちら。](../plan/installation-options.md)

## <a name="prerequisites"></a>前提条件

- Windows Server 2016 または 2019 上に 2 つ以上のノードを持つフェールオーバー クラスターがあること。 [フェールオーバー クラスターの展開の詳細についてはこちら。](../../../failover-clustering/failover-clustering-overview.md)
- クラスター内のすべてのノードがアクセスできる永続的なデータを格納するための、Windows Admin Center 用のクラスター共有ボリューム (CSV)。 CSV の場合、10 GB で十分です。
- [Windows Admin Center の HA スクリプト zip ファイル](https://aka.ms/WACHAScript)からの高可用性展開スクリプト。 スクリプトが入っている .zip ファイルをローカル コンピューターにダウンロードし、次のガイダンスに基づいて必要に応じてスクリプトをコピーします。
- 推奨 (省略可能): 署名入り証明書の .pfx と パスワード。 事前にクラスター ノードに証明書をインストールしておく必要はありません。スクリプトによって自動的に実行されます。 1 つも用意していない場合は、60 日後に有効期限が切れる自己署名証明書がインストール スクリプトによって生成されます。

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>Windows Admin Center のフェールオーバー クラスターへのインストール

1. ```Install-WindowsAdminCenterHA.ps1``` スクリプトをクラスター内のノードにコピーします。 Windows Admin Center の .msi を同じノードにダウンロードまたはコピーします。
2. RDP 経由でノードに接続し、次のパラメーターを使用して、そのノードから ```Install-WindowsAdminCenterHA.ps1``` スクリプトを実行します。
    - `-clusterStorage`: Windows Admin Center のデータを格納するクラスター共有ボリュームのローカル パス。
    - `-clientAccessPoint`: Windows Admin Center へのアクセスに使用する名前を選択します。 たとえば、パラメーター `-clientAccessPoint contosoWindowsAdminCenter` を指定してスクリプトを実行した場合、`https://contosoWindowsAdminCenter.<domain>.com` にアクセスして Windows Admin Center サービスにアクセスします。
    - `-staticAddress`:任意。 クラスター汎用サービス用の 1 つまたは複数の静的アドレス。 
    - `-msiPath`:Windows Admin Center の .msi ファイルのパス。
    - `-certPath`:任意。 証明書の .pfx ファイルのパス。
    - `-certPassword`:任意。 `-certPath` で提供されている証明書の SecureString パスワード
    - `-generateSslCert`:任意。 署名入り証明書を提供しない場合は、このパラメーター フラグを指定して自己署名証明書を生成します。 自己署名証明書の有効期限は 60 日で切れるので注意してください。
    - `-portNumber`:任意。 ポートを指定しない場合、ゲートウェイ サービスはポート 443 (HTTPS) に展開されます。 別のポートを使用するには、このパラメーターで指定します。 カスタム ポート (443 を除く) を使用する場合は、 https://\<clientAccessPoint\>:\<port\> に移動して、Windows Admin Center にアクセスします。

> [!NOTE]
> ```Install-WindowsAdminCenterHA.ps1``` スクリプトでは、```-WhatIf ``` パラメーターと ```-Verbose``` パラメーターがサポートされています。

### <a name="examples"></a>例

#### <a name="install-with-a-signed-certificate"></a>署名入り証明書を使用してインストールする:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>自己署名証明書を使用してインストールする:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>既存の高可用性インストールの更新

同じ ```Install-WindowsAdminCenterHA.ps1``` スクリプトを使用して、接続データを失うことなく、HA 展開を更新します。

### <a name="update-to-a-new-version-of-windows-admin-center"></a>新しいバージョンの Windows Admin Center への更新

Windows Admin Center の新しいバージョンがリリースされたら、```msiPath``` パラメーターのみを指定して ```Install-WindowsAdminCenterHA.ps1``` スクリプトを実行します。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Windows Admin Center で使用される証明書の更新

新しい証明書の .pfx ファイルとパスワードを指定することで、Windows Admin Center の HA 展開で使用される証明書をいつでも更新できます。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

また、Windows Admin Center プラットフォームを新しい .msi ファイルで更新するときにも、証明書を更新できます。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>アンインストール

Windows Admin Center の HA 展開をフェールオーバー クラスターからアンインストールするには、```-Uninstall``` パラメーターを ```Install-WindowsAdminCenterHA.ps1``` スクリプトに渡します。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>トラブルシューティング

ログは CSV の一時フォルダー (例: C:\ClusterStorage\Volume1\temp) に保存されます。