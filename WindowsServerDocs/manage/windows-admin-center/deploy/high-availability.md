---
title: 高可用性を備えた Windows 管理センターの展開
description: 高可用性 (プロジェクトホノルル) で Windows 管理センターを展開する
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
# <a name="deploy-windows-admin-center-with-high-availability"></a>高可用性を備えた Windows 管理センターの展開

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターをフェールオーバークラスターに展開して、Windows 管理センターゲートウェイサービスの高可用性を実現することができます。 提供されるソリューションはアクティブ/パッシブソリューションであり、Windows 管理センターの1つのインスタンスのみがアクティブです。 クラスター内のいずれかのノードで障害が発生した場合、Windows 管理センターは正常に別のノードにフェールオーバーします。これにより、環境内のサーバーの管理をシームレスに進めることができます。 

[その他の Windows 管理センターの展開オプションについて説明します。](../plan/installation-options.md)

## <a name="prerequisites"></a>前提条件

- Windows Server 2016 または2019上の2つ以上のノードのフェールオーバークラスター。 [フェールオーバークラスターの展開の詳細については、こちらを参照して](../../../failover-clustering/failover-clustering-overview.md)ください。
- クラスター内のすべてのノードがアクセスできる永続的なデータを格納するための、Windows 管理センター用のクラスター共有ボリューム (CSV)。 CSV の場合、10 GB で十分です。
- [Windows 管理センターの HA スクリプト zip ファイル](https://aka.ms/WACHAScript)からの高可用性展開スクリプト。 スクリプトが含まれている .zip ファイルをローカルコンピューターにダウンロードし、次のガイダンスに基づいて必要に応じてスクリプトをコピーします。
- 推奨されますが、省略可能: 署名入り証明書 .pfx & パスワード。 クラスターノードに証明書を既にインストールしておく必要はありません。スクリプトによって実行されます。 1つも指定しない場合、インストールスクリプトによって自己署名証明書が生成され、60日後に有効期限が切れます。

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>フェールオーバークラスターへの Windows 管理センターのインストール

1. ```Install-WindowsAdminCenterHA.ps1``` スクリプトをクラスター内のノードにコピーします。 Windows 管理センターの .msi をダウンロードするか、同じノードにコピーします。
2. RDP 経由でノードに接続し、次のパラメーターを使用して、そのノードから ```Install-WindowsAdminCenterHA.ps1``` スクリプトを実行します。
    - `-clusterStorage`: Windows 管理センターデータを格納するためのクラスターの共有ボリュームのローカルパス。
    - `-clientAccessPoint`: Windows 管理センターへのアクセスに使用する名前を選択します。 たとえば、`-clientAccessPoint contosoWindowsAdminCenter` というパラメーターを指定してスクリプトを実行した場合、`https://contosoWindowsAdminCenter.<domain>.com` にアクセスして Windows 管理センターサービスにアクセスします。
    - `-staticAddress`:任意。 クラスター汎用サービスの1つまたは複数の静的アドレス。 
    - `-msiPath`:Windows 管理センターの .msi ファイルのパス。
    - `-certPath`:任意。 証明書の .pfx ファイルのパス。
    - `-certPassword`:任意。 `-certPath` で提供されている証明書の SecureString パスワード
    - `-generateSslCert`:任意。 署名入り証明書を提供しない場合は、このパラメーターフラグを指定して自己署名証明書を生成します。 自己署名証明書の有効期限は60日であることに注意してください。
    - `-portNumber`:任意。 ポートを指定しない場合、ゲートウェイサービスはポート 443 (HTTPS) に展開されます。 別のポートを使用するには、このパラメーターにを指定します。 カスタムポート (443 を除く) を使用する場合は、 https://\<clientAccessPoint \>: \<port\> に移動して、Windows 管理センターにアクセスします。

> [!NOTE]
> ```Install-WindowsAdminCenterHA.ps1``` スクリプトでは、```-WhatIf ``` と ```-Verbose``` のパラメーターがサポートされています。

### <a name="examples"></a>使用例

#### <a name="install-with-a-signed-certificate"></a>署名入り証明書を使用してインストールする:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>自己署名証明書を使用してインストールする:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>既存の高可用性インストールを更新する

同じ ```Install-WindowsAdminCenterHA.ps1``` スクリプトを使用して、接続データを失うことなく、HA デプロイを更新します。

### <a name="update-to-a-new-version-of-windows-admin-center"></a>新しいバージョンの Windows 管理センターに更新する

Windows 管理センターの新しいバージョンがリリースされたら、単に ```msiPath``` パラメーターのみを使用して ```Install-WindowsAdminCenterHA.ps1``` スクリプトを再実行します。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Windows 管理センターで使用される証明書を更新する

新しい証明書の .pfx ファイルとパスワードを指定することで、Windows 管理センターの HA 展開で使用される証明書をいつでも更新できます。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

また、Windows 管理センタープラットフォームを新しい .msi ファイルで更新するときにも、証明書を更新することができます。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>アンインストール

フェールオーバークラスターから Windows 管理センターの HA 展開をアンインストールするには、```-Uninstall``` パラメーターを ```Install-WindowsAdminCenterHA.ps1``` スクリプトに渡します。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>トラブルシューティング

ログは CSV の一時フォルダー (たとえば、C:\ClusterStorage\Volume1\temp) に保存されます。