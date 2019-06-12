---
title: HGS の証明書を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2dc232eb7aeb8b0807a8e9989ae3dc893f925f66
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447364"
---
# <a name="obtain-certificates-for-hgs"></a>HGS の証明書を取得します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

HGS を展開するときに、シールドされた VM の起動に必要な機密情報を保護するために使用される署名と暗号化の証明書を提供することになります。
これらの証明書をこのことはありませんが、HGS のままにし、実行しているホストが正常な状態を実証されたときに復号化のシールドされた VM のキーにのみ使用されます。
テナント (VM 所有者) を使用して、パブリック証明書の半分、シールドされた Vm を実行するデータ センターの承認します。
このセクションでは、HGS の互換性のある署名と暗号化の証明書を取得するために必要な手順について説明します。

## <a name="request-certificates-from-your-certificate-authority"></a>証明機関から証明書を要求

必須ではありませんは、信頼された証明機関から証明書を入手することを強くお勧めします。
これにより、VM 所有者が、シールドされた Vm を実行する、正しい HGS サーバー (サービス プロバイダーまたはデータ センター) を承認することを確認します。
エンタープライズのシナリオでは、独自のエンタープライズ CA を使用して、これらの証明書を発行することができます。
ホスト側とサービス プロバイダーは、よく知られている、パブリック CA を代わりに使用を検討する必要があります。

(「推奨」マークされている) 場合を除き、プロパティは、次の証明書、署名と暗号化の両方の証明書を発行する必要があります。

証明書テンプレートのプロパティ | 必要な値 
------------------------------|----------------
暗号化プロバイダー               | 任意のキー記憶域プロバイダー (KSP)。 暗号化サービス プロバイダー (Csp) のレガシは**いない**サポートされています。
キー アルゴリズム                 | RSA
最小キー サイズ              | 2048 ビット
署名アルゴリズム           | 推奨:SHA256
キー使用法                     | デジタル署名*と*データの暗号化
拡張キー使用法            | サーバー認証
キーの更新ポリシー            | 同じキーで更新します。 異なるキーを持つ HGS の証明書を更新すると、シールドされた Vm が起動できなくなります。
サブジェクト名                  | お勧めします。 会社の名前または web のアドレス。 この情報は、シールド データ ファイル ウィザードで、VM 所有者に表示されます。

これらの要件には、ハードウェアまたはソフトウェアによって証明書を使用しているかどうかが適用されます。
セキュリティ上の理由は、秘密キーがシステムの電源をコピーすることを防ぐためにハードウェア セキュリティ モジュール (HSM) で、HGS キーを作成することをお勧めします。
上記の属性を持つ証明書を要求する、HSM ベンダーからのガイダンスに従うしをインストールし、HGS のすべてのノードで HSM KSP を承認してください。

HGS のすべてのノードには、同じ署名と暗号化証明書へのアクセスが必要です。
ソフトウェアを基盤と証明書を使用している場合は、パスワードを使用して、PFX ファイルに証明書をエクスポートおよびの証明書を管理するように HGS を許可します。
HGS の各ノードで、ローカル コンピューターの証明書ストアに証明書をインストールし、HGS に拇印を指定することもできます。
両方のオプションについてで、 [HGS クラスターの初期化](guarded-fabric-initialize-hgs.md)トピック。

## <a name="create-self-signed-certificates-for-test-scenarios"></a>テスト シナリオ用の自己署名証明書を作成します。

HGS のラボ環境を作成しがまたはしない証明機関を使用する場合、は、自己署名証明書を作成できます。
シールド データ ファイル ウィザードで証明書の情報をインポートするときに、警告が表示されますが、すべての機能は変わりません。

で自己署名証明書を作成して、PFX ファイルにエクスポートするには、PowerShell で次のコマンドを実行します。

```powershell
$certificatePassword = Read-Host -AsSecureString -Prompt "Enter a password for the PFX file"

$signCert = New-SelfSignedCertificate -Subject "CN=HGS Signing Certificate"
Export-PfxCertificate -FilePath .\signCert.pfx -Password $certificatePassword -Cert $signCert
Remove-Item $signCert.PSPath

$encCert = New-SelfSignedCertificate -Subject "CN=HGS Encryption Certificate"
Export-PfxCertificate -FilePath .\encCert.pfx -Password $certificatePassword -Cert $encCert
Remove-Item $encCert.PSPath
```

## <a name="request-an-ssl-certificate"></a>SSL 証明書を要求します。

HYPER-V ホスト間で転送されるすべてのキーと機密情報と HGS がメッセージ レベルで暗号化された--HGS またはユーザーが、ネットワーク トラフィックをスニッフィングとキーの盗難を防ぐ、HYPER-V のいずれかの既知のキーの情報の暗号化は、vm。
ただし、コンプライアンス reqiurements または Hyper-v ホストと HGS の間のすべての通信を暗号化することを希望するした場合は、トランスポート レベルですべてのデータを暗号化する SSL 証明書で HGS を構成できます。

HYPER-V ホストと HGS ノードの両方が指定すると、SSL 証明書を信頼するため、エンタープライズ証明機関から SSL 証明書を要求することをお勧めする必要があります。 証明書を要求するときに、次を指定することを確認します。

SSL 証明書のプロパティ | 必要な値
-------------------------|---------------
サブジェクト名             | HGS クラスター (分散ネットワーク名) の名前。 これは、HGS に提供されるサービス名を連結したものとなります`Initialize-HgsServer`と HGS ドメイン名。
サブジェクト代替名 | 別の DNS 名を使用して、HGS クラスターに到達するかどうか (例: ロード バランサーの内側にある場合)、証明書の要求の SAN フィールドにこれらの DNS 名を含めるようにしてください。

HGS サーバーを初期化するときに、この証明書を指定するためのオプションは、「 [HGS 最初ノードを構成する](guarded-fabric-initialize-hgs.md)します。
追加または使って後で、SSL 証明書を変更することも、[セット HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver?view=win10-ps)コマンドレット。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [HGS のインストール](guarded-fabric-choose-where-to-install-hgs.md)