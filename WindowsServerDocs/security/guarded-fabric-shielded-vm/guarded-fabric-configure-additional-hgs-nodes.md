---
title: 追加の HGS ノードを構成する
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 227f723b-acb2-42a7-bbe3-44e82f930e35
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/22/2018
ms.openlocfilehash: a89337457cc71ffee78e3f73fecc2262f1fb38e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855203"
---
# <a name="configure-additional-hgs-nodes"></a>追加の HGS ノードを構成する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

運用環境で HGS する必要があるように設定、高可用性クラスターで、HGS ノードがダウンした場合でも、シールドされた Vm を電源できることを確認します。 テスト環境での HGS のセカンダリ ノードは必要ありません。

環境に最適な HGS ノードを追加するのにには、これらのメソッドのいずれかを使用します。

|                |                         |                              | 
|----------------|-------------------------|------------------------------|
|HGS の新しいフォレスト  | [PFX ファイルを使用します。](#dedicated-hgs-forest-with-pfx-certificates) | [証明書の拇印を使用します。](#dedicated-hgs-forest-with-certificate-thumbprints) |
|既存の要塞フォレスト |  [PFX ファイルを使用します。](#existing-bastion-forest-with-pfx-certificates) | [証明書の拇印を使用します。](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>前提条件

必ず各追加ノード。 
- プライマリ ノードと同じハードウェアおよびソフトウェア構成を持つ 
- 他の HGS サーバーと同じネットワークに接続されています。
- HGS の他のサーバーを DNS 名で解決できます。

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>PFX 証明書を持つ専用の HGS フォレスト

1. ドメイン コント ローラーに HGS ノードに昇格します。
2. HGS サーバーを初期化します。

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>ドメイン コント ローラーに HGS ノードに昇格します。

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化します。

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>証明書の拇印を持つ専用の HGS フォレスト
 
1. ドメイン コント ローラーに HGS ノードに昇格します。
2. HGS サーバーを初期化します。
3. 証明書の秘密キーをインストールします。

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>ドメイン コント ローラーに HGS ノードに昇格します。

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化します。

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

### <a name="install-the-private-keys-for-the-certificates"></a>証明書の秘密キーをインストールします。

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>PFX 証明書を既存の要塞フォレスト

1. ノードを既存のドメインに参加させる
2. GMSA パスワードを取得し、Install-adserviceaccount を実行するマシンの権限を付与します。
3. HGS サーバーを初期化します。

### <a name="join-the-node-to-the-existing-domain"></a>ノードを既存のドメインに参加させる

1. 最初の HGS サーバーで DNS サーバーを使用するノード上の少なくとも 1 つの NIC が構成されていることを確認します。
2. 新しい HGS ノードを最初の HGS ノードと同じドメインに参加します。 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA パスワードを取得し、Install-adserviceaccount を実行するマシンの権限を付与します。

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化します。

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>既存の要塞フォレストの証明書の拇印を使用

1. ノードを既存のドメインに参加させる
2. GMSA パスワードを取得し、Install-adserviceaccount を実行するマシンの権限を付与します。
3. HGS サーバーを初期化します。
4. 証明書の秘密キーをインストールします。

### <a name="join-the-node-to-the-existing-domain"></a>ノードを既存のドメインに参加させる

1. 最初の HGS サーバーで DNS サーバーを使用するノード上の少なくとも 1 つの NIC が構成されていることを確認します。
2. 新しい HGS ノードを最初の HGS ノードと同じドメインに参加します。 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA パスワードを取得し、Install-adserviceaccount を実行するマシンの権限を付与します。

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS サーバーを初期化します。

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

このノードにレプリケートする最初の HGS サーバーからの暗号化と署名証明書は最大で 10 分かかります。

### <a name="install-the-private-keys-for-the-certificates"></a>証明書の秘密キーをインストールします。

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>HTTPS 通信の HGS を構成します。

SSL 証明書が HGS エンドポイントをセキュリティで保護する場合は、HGS クラスター内のすべてのノードと同様に、このノードで SSL 証明書を構成する必要があります。
SSL 証明書*ない*HGS でレプリケートされ (つまり各ノード用の別の SSL 証明書を保持できます) のすべてのノードに同じキーを使用する必要はありません。

SSL 証明書を要求するときに、クラスターの完全修飾ドメイン名を確認します (の出力に示すように`Get-HgsServer`) か、サブジェクト共通名、証明書のサブジェクト代替の DNS 名として含まれているか。
と共に使用するように HGS を構成するには、証明機関から証明書を取得したときに[セット HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/set-hgsserver)します。

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

既にローカル証明書ストアに証明書をインストールし、拇印で参照できるようにの場合は、代わりに、次のコマンドを実行します。

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

HGS は常に通信に HTTP と HTTPS の両方のポートを公開します。
ポート 80 経由で通信をブロックする Windows ファイアウォールまたは他のネットワークのファイアウォール テクノロジを使用することができますが、IIS では、HTTP バインドを削除するサポートされていません。

## <a name="decommission-an-hgs-node"></a>HGS のノードを使用停止します。

HGS のノードを使用停止。

1. [HGS の構成をクリア](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration)します。

   これにより、クラスターからノードを削除し、構成証明およびキー保護サービスをアンインストールします。 
   場合、クラスター内の最後のノードは、- Force が最後のノードを削除し、Active Directory でクラスターを破棄することを示すために必要な。 
   
   HGS が要塞フォレスト (既定値) に展開する場合は、のみを行います。 
   必要に応じて、ドメインからコンピューターの参加を解除し、Active Directory から gMSA アカウントを削除できます。

1. 場合は、HGS が独自のドメインを作成する必要がありますも[HGS をアンインストール](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration)をドメインに参加を解除し、ドメイン コント ローラーを降格します。



## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[HGS の構成を検証します。](guarded-fabric-verify-hgs-configuration.md)

