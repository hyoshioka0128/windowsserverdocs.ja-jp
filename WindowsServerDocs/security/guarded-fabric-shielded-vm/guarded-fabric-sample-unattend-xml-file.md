---
title: OS 特殊化応答ファイルの作成
ms.prod: windows-server
ms.topic: article
ms.assetid: 299aa38e-28d2-4cbe-af16-5b8c533eba1f
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 526ded03c877613766b8a0b762f1db1a693d2019
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474999"
---
# <a name="create-os-specialization-answer-file"></a>OS 特殊化応答ファイルの作成

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

シールドされた Vm を展開する準備として、オペレーティングシステムの特殊化応答ファイルを作成する必要がある場合があります。 Windows では、これは "unattend.xml" ファイルと呼ばれることがよくあります。 **ShieldingDataAnswerFile** Windows PowerShell 関数を使用すると、これを行うことができます。 この応答ファイルは、System Center Virtual Machine Manager (またはその他のファブリックコントローラー) を使用してテンプレートからシールドされた Vm を作成するときに使用できます。

シールドされた Vm の無人セットアップファイルに関する一般的なガイドラインについては、「[応答ファイルを作成](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)する」を参照してください。

## <a name="downloading-the-new-shieldingdataanswerfile-function"></a>ShieldingDataAnswerFile 関数のダウンロード

[PowerShell ギャラリー](https://aka.ms/gftools)から**ShieldingDataAnswerFile**関数を取得できます。 コンピューターがインターネットに接続されている場合は、次のコマンドを使用して PowerShell からインストールできます。

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

`unattend.xml`出力を追加のアーティファクトと共にシールドデータにパッケージ化して、テンプレートからシールドされた vm を作成することができます。

次のセクションでは、 `unattend.xml` さまざまなオプションを含むファイルに対して関数パラメーターを使用する方法について説明します。

- [基本的な Windows 応答ファイル](#basic-windows-answer-file)
- [ドメイン参加を含む Windows 応答ファイル](#windows-answer-file-with-domain-join)
- [静的 IPv4 アドレスを持つ Windows 応答ファイル](#windows-answer-file-with-static-ipv4-addresses)
- [カスタムロケールを持つ Windows 応答ファイル](#windows-answer-file-with-a-custom-locale)
- [基本的な Linux 応答ファイル](#basic-linux-answer-file)

## <a name="basic-windows-answer-file"></a>基本的な Windows 応答ファイル

次のコマンドは、管理者アカウントのパスワードとホスト名を設定するだけの Windows 応答ファイルを作成します。
VM ネットワークアダプターは DHCP を使用して IP アドレスを取得し、VM は Active Directory ドメインに参加しません。
管理者の資格情報を入力するように求められたら、目的のユーザー名とパスワードを指定します。
ビルトイン Administrator アカウントを構成する場合は、ユーザー名として "Administrator" を使用します。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred
```

## <a name="windows-answer-file-with-domain-join"></a>ドメイン参加を含む Windows 応答ファイル

次のコマンドは、シールドされた VM を Active Directory ドメインに参加させる Windows 応答ファイルを作成します。
VM ネットワークアダプターは、DHCP を使用して IP アドレスを取得します。

最初の資格情報プロンプトによって、ローカルの管理者アカウント情報が要求されます。
ビルトイン Administrator アカウントを構成する場合は、ユーザー名として "Administrator" を使用します。

2番目の資格情報プロンプトによって、コンピューターを Active Directory ドメインに参加させる権限を持つ資格情報が求められます。

"-DomainName" パラメーターの値は、必ず Active Directory ドメインの FQDN に変更してください。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -DomainName 'my.contoso.com' -DomainJoinCredentials $domainCred
```
## <a name="windows-answer-file-with-static-ipv4-addresses"></a>静的 IPv4 アドレスを持つ Windows 応答ファイル

次のコマンドは、System Center Virtual Machine Manager などのファブリックマネージャーによって展開時に提供される静的 IP アドレスを使用する Windows 応答ファイルを作成します。

Virtual Machine Manager は、IP プール (IPv4 アドレス、IPv6 アドレス、ゲートウェイアドレス、DNS アドレス) を使用して、静的 IP アドレスに3つのコンポーネントを提供します。 追加のフィールドを含める場合、またはカスタムネットワーク構成が必要な場合は、スクリプトによって生成される応答ファイルを手動で編集する必要があります。

次のスクリーンショットは、Virtual Machine Manager で構成できる IP プールを示しています。 静的 IP を使用する場合は、これらのプールが必要です。

現在、この関数は1つの DNS サーバーのみをサポートしています。 DNS 設定は次のようになります。

![静的 IP プールを使用した DNS サーバーの構成](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-dns-settings.png)

静的 IP アドレスプールの作成の概要は次のようになります。 つまり、ネットワークルートは1つ、ゲートウェイ、および DNS サーバーは1つだけである必要があり、IP アドレスを指定する必要があります。

![静的 IP プールの作成の概要](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-summary.png)

仮想マシン用にネットワークアダプターを構成する必要があります。 次のスクリーンショットは、その構成を設定する場所と、その構成を静的 IP に切り替える方法を示しています。

![静的 IP を使用するようにハードウェアを構成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-network-adapter-settings.png)

次に、パラメーターを使用して、 `-StaticIPPool` 静的 IP 要素を応答ファイルに含めることができます。 `@IPAddr-1@`応答ファイルのパラメーター、 `@NextHop-1-1@` 、およびは、 `@DNSAddr-1-1@` デプロイ時に Virtual Machine Manager で指定した実際の値に置き換えられます。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -StaticIPPool IPv4Address
```

## <a name="windows-answer-file-with-a-custom-locale"></a>カスタムロケールを持つ Windows 応答ファイル

次のコマンドは、カスタムロケールで Windows 応答ファイルを作成します。

管理者の資格情報を入力するように求められたら、目的のユーザー名とパスワードを指定します。
ビルトイン Administrator アカウントを構成する場合は、ユーザー名として "Administrator" を使用します。

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -Locale es-ES
```

## <a name="basic-linux-answer-file"></a>基本的な Linux 応答ファイル

Windows Server バージョン1709以降では、シールドされた Vm で特定の Linux ゲスト Os を実行できます。
System Center Virtual Machine Manager Linux エージェントを使用してこれらの Vm を特殊化する場合は、ShieldingDataAnswerFile コマンドレットを使用して、互換性のある応答ファイルを作成できます。

Linux の応答ファイルには、通常、ルートパスワード、ルート SSH キー、および必要に応じて静的 IP プール情報が含まれます。
次のスクリプトを実行する前に、SSH キーのパブリック半分にパスを置き換えます。

```powershell
$rootPassword = Read-Host -Prompt "Root password" -AsSecureString

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -RootPassword $rootPassword -RootSshKey '~\.ssh\id_rsa.pub'
```

## <a name="additional-references"></a>その他のリファレンス

- [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
