---
title: 高可用性を備えた Windows Admin Center を展開します。
description: 高可用性 (Project Honolulu) で Windows Admin Center を展開します。
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a0062230dd3d9e9c52aa317f87e06b0e84507dc4
ms.sourcegitcommit: 802a7bd537cab22893abb7e6657c4be90346ef88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "9025034"
---
# 高可用性を備えた Windows Admin Center を展開します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center ゲートウェイ サービスの高可用性を実現するには、フェールオーバー クラスターで Windows Admin Center を展開することができます。 提供されるソリューションとは、Windows Admin Center の 1 つだけのインスタンスがアクティブになっているときに、アクティブ パッシブ ソリューションです。 クラスター内のノードのいずれかが失敗した場合は、Windows Admin Center 適切フェールオーバー別のノードに引き続きシームレスに環境内のサーバーを管理すること。 

[その他の Windows Admin Center の展開オプションについて説明します。](../plan/installation-options.md)

## 前提条件

- Windows Server 2016 または 2019 に 2 つ以上のノードのフェールオーバー クラスターします。 [フェールオーバー クラスターの展開について詳しく説明します](../../../failover-clustering/failover-clustering-overview.md)。
- クラスター共有ボリューム (CSV)、クラスター内のすべてのノードからアクセスできる永続的なデータを格納する Windows Admin Center のされます。 10 GB は、CSV を十分になります。
- [Windows Admin Center 高可用性スクリプト zip ファイル](https://aka.ms/WACHAScript)から高可用性の展開スクリプトです。 ローカル コンピューターにスクリプトを含む .zip ファイルをダウンロードし、し、スクリプトをコピー、必要に応じて、次のガイダンスに基づきます。
- 推奨されるが省略可能: 署名証明書の .pfx & パスワード。 既にに、クラスター ノード上で証明書をインストールする必要はありません - するが、スクリプトによって実行されます。 いずれかを指定しない場合、インストール スクリプトには、60 日後に期限が自己署名証明書が生成されます。

## フェールオーバー クラスター上で Windows Admin Center のインストール

1. コピー、```Install-WindowsAdminCenterHA.ps1```スクリプト、クラスター内のノードにします。 ダウンロードまたは同一のノードに Windows Admin Center .msi をコピーします。
2. 実行して、RDP 経由でのノードに接続、```Install-WindowsAdminCenterHA.ps1```ノードには、次のパラメーターからスクリプト。
    - `-clusterStorage`: Windows Admin Center のデータを格納するクラスターの共有ボリュームのローカル パス。
    - `-clientAccessPoint`: Windows Admin Center のアクセスに使用する名前を選択します。 たとえば、次のパラメーターを使用してスクリプトを実行する`-clientAccessPoint contosoWindowsAdminCenter`は訪問で Windows Admin Center サービスにアクセスします。 `https://contosoWindowsAdminCenter.<domain>.com`
    - `-staticAddress`: 省略可能です。 クラスターの汎用的なサービスの 1 つ以上の静的のアドレス。 
    - `-msiPath`: Windows Admin Center .msi ファイルのパス。
    - `-certPath`: 省略可能です。 証明書の .pfx ファイルのパス。
    - `-certPassword`: 省略可能です。 提供されている証明書の .pfx の SecureString パスワード `-certPath`
    - `-generateSslCert`: 省略可能です。 署名証明書を提供しない場合は、[自己署名証明書を生成するには、このパラメーター フラグが含まれます。 自己署名証明書は 60 日以内に期限切れことに注意してください。
    - `-portNumber`: 省略可能です。 ポートを指定しない場合は、ポート 443 (HTTPS) でゲートウェイ サービスが配置されます。 使用するには、別のポートは、このパラメーターで指定します。 カスタムのポート (443 以外に何も) を使用する場合がありますアクセスすること、Windows Admin Center https://\<clientAccessPoint\>:\<port\> に移動してに注意してください。

> [!NOTE]
> ```Install-WindowsAdminCenterHA.ps1```スクリプトをサポートしている```-WhatIf ```と```-Verbose```パラメーター

### 例

#### 署名証明書をインストールします。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### 自己署名証明書をインストールします。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## 既存の高可用性のインストールを更新します。

同じを使用して```Install-WindowsAdminCenterHA.ps1```、接続のデータを失うことがなく、あって展開を更新するスクリプト。

### Windows Admin Center の新しいバージョンに更新します。

Windows Admin Center の新しいバージョンが離されたときだけ実行、```Install-WindowsAdminCenterHA.ps1```だけで、再度スクリプト、```msiPath```パラメーター。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### Windows Admin Center を使用する証明書を更新します。

新しい証明書の .pfx ファイルを提供することでいつでもでも Windows Admin Center のあって展開で使用される証明書を更新しておよびパスワード。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

新しい .msi ファイルで、Windows Admin Center プラットフォームを更新すると同時に証明書を更新することがあります。

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## Uninstall

フェールオーバー クラスターから Windows Admin Center のあって展開をアンインストールするに渡す、```-Uninstall```パラメーターを```Install-WindowsAdminCenterHA.ps1```スクリプト。

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## トラブルシューティング

ログは、CSV (たとえば、C:\ClusterStorage\Volume1\temp) の一時フォルダーに保存されます。