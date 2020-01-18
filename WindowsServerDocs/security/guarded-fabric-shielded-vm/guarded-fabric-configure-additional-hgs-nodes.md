---
title: 追加の HGS ノードを構成する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 227f723b-acb2-42a7-bbe3-44e82f930e35
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/14/2020
ms.openlocfilehash: ece005617c4a2faac41c2be15967b2f43951517e
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265864"
---
# <a name="configure-additional-hgs-nodes"></a>追加の HGS ノードを構成する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

運用環境では、hgs ノードがダウンした場合でも、シールドされた Vm の電源をオンにできるように、高可用性クラスターで HGS を設定する必要があります。 テスト環境では、セカンダリ HGS ノードは必要ありません。

これらの方法のいずれかを使用して、使用環境に最適な HGS ノードを追加します。

|                |                         |                              | 
|----------------|-------------------------|------------------------------|
|新しい HGS フォレスト  | [PFX ファイルの使用](#dedicated-hgs-forest-with-pfx-certificates) | [証明書の拇印の使用](#dedicated-hgs-forest-with-certificate-thumbprints) |
|既存の要塞フォレスト |  [PFX ファイルの使用](#existing-bastion-forest-with-pfx-certificates) | [証明書の拇印の使用](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>必要条件

次の各ノードが追加されていることを確認してください。 
- プライマリノードと同じハードウェアとソフトウェアの構成 
- 他の HGS サーバーと同じネットワークに接続されている
- 他の HGS サーバーを DNS 名で解決できる

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>PFX 証明書を持つ専用の HGS フォレスト

1. HGS ノードをドメインコントローラーに昇格させる
2. HGS サーバーを初期化する

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>HGS ノードをドメインコントローラーに昇格させる

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化する

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>証明書の拇印を持つ専用の HGS フォレスト
 
1. HGS ノードをドメインコントローラーに昇格させる
2. HGS サーバーを初期化する
3. 証明書の秘密キーをインストールする

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>HGS ノードをドメインコントローラーに昇格させる

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化する

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

### <a name="install-the-private-keys-for-the-certificates"></a>証明書の秘密キーをインストールする

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>PFX 証明書を持つ既存の要塞フォレスト

1. ノードを既存のドメインに参加させる
2. GMSA パスワードを取得するためのコンピューターの権限を付与し、Install-ADServiceAccount を実行します。
3. HGS サーバーを初期化する

### <a name="join-the-node-to-the-existing-domain"></a>ノードを既存のドメインに参加させる

1. 最初の HGS サーバーで DNS サーバーを使用するように、ノードに少なくとも1つの NIC が構成されていることを確認します。
2. 新しい HGS ノードを最初の HGS ノードと同じドメインに参加させます。 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA パスワードを取得するためのコンピューターの権限を付与し、Install-ADServiceAccount を実行します。

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化する

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>証明書の拇印がある既存の要塞フォレスト

1. ノードを既存のドメインに参加させる
2. GMSA パスワードを取得するためのコンピューターの権限を付与し、Install-ADServiceAccount を実行します。
3. HGS サーバーを初期化する
4. 証明書の秘密キーをインストールする

### <a name="join-the-node-to-the-existing-domain"></a>ノードを既存のドメインに参加させる

1. 最初の HGS サーバーで DNS サーバーを使用するように、ノードに少なくとも1つの NIC が構成されていることを確認します。
2. 新しい HGS ノードを最初の HGS ノードと同じドメインに参加させます。 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA パスワードを取得するためのコンピューターの権限を付与し、Install-ADServiceAccount を実行します。

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化する

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

最初の HGS サーバーからの暗号化証明書と署名証明書がこのノードにレプリケートされるまで、最大で10分かかります。

### <a name="install-the-private-keys-for-the-certificates"></a>証明書の秘密キーをインストールする

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>HTTPS 通信用に HGS を構成する

SSL 証明書を使用して HGS エンドポイントをセキュリティで保護する場合は、このノード、および HGS クラスター内の他のすべてのノードで SSL 証明書を構成する必要があります。
SSL 証明書は HGS によってレプリケートさ*れず*、すべてのノードに同じキーを使用する必要はありません (つまり、ノードごとに異なる ssl 証明書を持つことができます)。

SSL 証明書を要求するときは、クラスターの完全修飾ドメイン名 (`Get-HgsServer`の出力に示されているとおり) が、証明書のサブジェクトの共通名であるか、サブジェクト代替 DNS 名として含まれていることを確認します。
証明機関から証明書を取得したら、 [HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/set-hgsserver)で使用するように HGS を構成できます。

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

証明書をローカル証明書ストアに既にインストールして拇印で参照する場合は、代わりに次のコマンドを実行します。

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

HGS は常に通信のために HTTP と HTTPS の両方のポートを公開します。
IIS で HTTP バインドを削除することはサポートされていませんが、Windows ファイアウォールまたは他のネットワークファイアウォールテクノロジを使用して、ポート80での通信をブロックすることができます。

## <a name="decommission-an-hgs-node"></a>HGS ノードの使用を停止する

HGS ノードを使用停止にするには:

1. [HGS の構成をクリア](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration)します。

   これにより、クラスターからノードが削除され、構成証明とキー保護サービスがアンインストールされます。 
   クラスター内の最後のノードの場合は、-Force を使用して、Active Directory で最後のノードを削除してクラスターを破棄する必要があることを示す必要があります。 

   HGS が要塞フォレスト (既定) に展開されている場合、これは唯一の手順です。 
   必要に応じて、ドメインからコンピューターの参加を解除し、Active Directory から gMSA アカウントを削除できます。

2. HGS によって独自のドメインが作成された場合は、 [hgs をアンインストール](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration)してドメインを切断し、ドメインコントローラーを降格する必要もあります。
