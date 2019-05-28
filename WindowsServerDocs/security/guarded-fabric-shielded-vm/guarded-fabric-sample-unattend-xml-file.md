---
title: OS 特殊化応答ファイルの作成
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 299aa38e-28d2-4cbe-af16-5b8c533eba1f
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5717fcc9e1732b6273620e633c140c6df58ec8b7
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624654"
---
# <a name="create-os-specialization-answer-file"></a>OS 特殊化応答ファイルの作成

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

シールドされた Vm をデプロイする準備として、オペレーティング システムの特殊化の応答ファイルを作成する必要があります。 、Windows ではこのよく、"unattend.xml"ファイルと呼ばれます。 **New-shieldingdataanswerfile** Windows PowerShell 関数を使用して、これを実行できます。 作成するときに、応答ファイルを使用して System Center Virtual Machine Manager (またはその他のファブリック コント ローラー) を使用して、テンプレートから Vm をシールドされたできます。

シールドされた Vm の無人セットアップ ファイルの一般的なガイドラインについては、次を参照してください。[応答ファイルを作成](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)です。
 
## <a name="downloading-the-new-shieldingdataanswerfile-function"></a>ダウンロード New-shieldingdataanswerfile 関数

取得することができます、 **New-shieldingdataanswerfile**関数を[PowerShell ギャラリー](https://aka.ms/gftools)します。 お使いのコンピューターにインターネット接続がある場合は、次のコマンドを PowerShell からインストールすることができます。

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

`unattend.xml`テンプレートからシールドされた Vm を作成するために使用できるように追加のアーティファクトと共に、シールド データに出力をパッケージ化できます。

次のセクションでは、関数パラメーターを使用する方法を示します、`unattend.xml`さまざまなオプションを含むファイル。

- [基本的な Windows 応答ファイル](#basic-windows-answer-file)
- [Windows は、ドメイン参加のファイルを回答します。](#windows-answer-file-with-domain-join)
- [静的 IPv4 アドレスでの Windows 応答ファイル](#windows-answer-file-with-static-ipv4-addresses)
- [カスタム ロケールでの Windows 応答ファイル](#windows-answer-file-with-a-custom-locale)
- [基本的な Linux 応答ファイル](#basic-linux-answer-file)

## <a name="basic-windows-answer-file"></a>基本的な Windows 応答ファイル

次のコマンドは、単に、管理者アカウントのパスワードとホスト名を設定する Windows 応答ファイルを作成します。
VM のネットワーク アダプターは DHCP を使用して、IP アドレスを取得して、VM は、Active Directory ドメイン参加していません。
管理者の資格情報の入力を求められたら、目的のユーザー名とパスワードを指定します。
ビルトイン Administrator アカウントを構成する場合は、ユーザー名の「管理者」を使用します。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred
```

## <a name="windows-answer-file-with-domain-join"></a>Windows は、ドメイン参加のファイルを回答します。

次のコマンドは、シールドされた VM を Active Directory ドメインに参加する Windows 応答ファイルを作成します。
VM のネットワーク アダプターでは、DHCP を使用して、IP アドレスを取得します。

最初の資格情報プロンプトには、ローカル管理者アカウントの情報は求められます。
ビルトイン Administrator アカウントを構成する場合は、ユーザー名の「管理者」を使用します。

2 番目の資格情報プロンプトは、マシンを Active Directory ドメインに参加する権限のある資格情報を要求します。

値を変更することを確認する、"-DomainName"パラメーターを Active Directory ドメインの FQDN。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -DomainName 'my.contoso.com' -DomainJoinCredentials $domainCred
```
## <a name="windows-answer-file-with-static-ipv4-addresses"></a>静的 IPv4 アドレスでの Windows 応答ファイル

次のコマンドは、デプロイ時に、System Center Virtual Machine Manager などのファブリック マネージャーによって提供される、静的 IP アドレスを使用する Windows 応答ファイルを作成します。

Virtual Machine Manager は、IP プールを使用して静的 IP アドレスに 3 つのコンポーネントを提供します。IPv4 アドレス、IPv6 アドレス、ゲートウェイ アドレス、および DNS アドレス。 含まれるまたはカスタム ネットワーク構成を必要とする他のフィールドを設定する場合は、スクリプトによって生成された応答ファイルを手動で編集する必要があります。

次のスクリーン ショットでは、Virtual Machine Manager で構成できる IP プールを表示します。 これらのプールは、静的 ip アドレスを使用する場合に必要です。

現時点では、関数は、1 つだけの DNS サーバーをサポートします。 ようになりますが、DNS 設定を次に示します。

![静的 IP プールと DNS サーバーを構成します。](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-dns-settings.png)

ようになりますが、静的 IP アドレス プールを作成するための概要。 つまり、1 つのみのネットワーク ルート、1 つのゲートウェイとの 1 つの DNS サーバーが必要し、IP アドレスを指定する必要があります。

![静的 IP プールの作成の概要](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-summary.png)

仮想マシンのネットワーク アダプターを構成する必要があります。 次のスクリーン ショットでは、その構成を設定する場所と静的 IP を切り替える方法を示します。

![静的 IP を使用するハードウェアを構成します。](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-network-adapter-settings.png)

次に、使用、`-StaticIPPool`パラメーターを応答ファイルで静的 IP の要素が含まれます。 パラメーター `@IPAddr-1@`、 `@NextHop-1-1@`、および`@DNSAddr-1-1@`の回答でファイルは、置き換えられます Virtual Machine Manager でデプロイ時に指定する実際の値。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -StaticIPPool IPv4Address
```

## <a name="windows-answer-file-with-a-custom-locale"></a>カスタム ロケールでの Windows 応答ファイル

次のコマンドは、カスタム ロケールで、Windows 応答ファイルを作成します。

管理者の資格情報の入力を求められたら、目的のユーザー名とパスワードを指定します。
ビルトイン Administrator アカウントを構成する場合は、ユーザー名の「管理者」を使用します。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -Locale es-ES
```

## <a name="basic-linux-answer-file"></a>基本的な Linux 応答ファイル

Windows Server バージョン 1709 以降では、シールドされた Vm で特定の Linux ゲスト Os を実行できます。
System Center Virtual Machine Manager の Linux エージェントは、それらの Vm を特殊化を使用している場合、New-shieldingdataanswerfile コマンドレットは、その互換性のある応答ファイルを作成できます。

Linux 応答ファイルでは、ルート パスワード、ルート SSH キー、および必要に応じて静的 IP プールの情報を通常含まれます。
次のスクリプトを実行する前に、SSH キーのパブリックの半分にパスに置き換えます。

```powershell
$rootPassword = Read-Host -Prompt "Root password" -AsSecureString

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -RootPassword $rootPassword -RootSshKey '~\.ssh\id_rsa.pub'
```

## <a name="see-also"></a>関連項目

- [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
